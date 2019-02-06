---
layout: post
title: Isolated self-managed environments in the same OpenStack cloud
date: 2019-02-06 17:07:10.000000000 +01:00
tags:
- OpenStack
- Domain Admin
- Project Admin
status: publish
type: post
published: true
meta:
  _edit_last: '1'
author:
  login: palvarez89
  email: palvarez89@gmail.com
  display_name: palvarez89
  first_name: 'Pedro'
  last_name: 'Alvarez Piedehierro'
---

{:toc}

## State of the art in OpenStack

### Using domains

The usage of OpenStack domains is the main approach to implement this.

We have been testing it and found out that the following things are working using the default policy files provided by different OpenStack projects:

- Cloud Admin (CA) can create Domains and Domain Admins (DA) on them
- DA can create and manage projects under that domain
- DA can create and manage users on that domain


- Project Admin (PA) can change quotas of project
- PA can create flavours
- PA can create availability zones
- PA can manage members of the project


- Project Member (PMem) can create networks in the project
- PMem can create instances in the project
- PMem can use volumes, etc


This all looks good, but we are seeing problems with the PAs and DAs, given that they can see and manage all the networks on the cloud:

<!--more-->

- DA can delete any network, even outside of its domain
- PA can delete any network, even outside of its domain

We haven't tried ourselves, but apparently DAs and PAs will also be able to see all the volumes of the cloud and modify/delete them.


Another problem we have seen is that if an user is a DA and a PMem, he will stop seeing the domain admin interface in horizon. A possible workaround for this is to only use DA accounts to only administrate domains, and have PMem accounts for everything else.



### Using Project as domains, creating a project hierarchy

After reading around it looks like it's possible to create a project that would behave as a domain, and then add child projects to it[1]. The steps to do do are:

    openstack project create  --property is_domain=True project-domain
    openstack project create  --parent $(openstack domain show project-domain -c id -f value) --domain project-domain project-openstack
    openstack project create  --parent project-openstack --domain project-domain project-keystone

> Note that "is_domain=True" doesn't work at the moment, the openstack client needs a fix for this to work correctly, as the property is being passed as String and not as Boolean.

For this approach to work we need to define a new role that lets the project-as-domain admin do things. If we assign the admin role on that project to an user then we are in the same situation as before using domains: the Project Admin will be able to do way too much in the cloud.

For now, the only difference that this solution gives compared to using domains, is that the Cloud Admin will be able to decide the full quota of the root project (project-as-domain), and child projects will not be able to go over that quota.

## Possible solution to above limitations

A workaround, that was suggested to us in #openstack, is to implement any of the above approaches without giving to anybody the "admin" role and hitting this bug[2]. To do this we would have to create a new role called "domain-manager", and grant that role very specific permissions like:

- Creating users on the domain
- Creating projects on the domain


We are currently testing this approach. It's possible that if we allow "domain-manager"s to create/modify users, then they will be able to create an admin user (of a project maybe).


## Implementing the workaround (the SOLUTION)

### Creating a domain-admin role to avoid using the admin one

Given that assigning the admin role to users in different domains wasn't working for some services (keystone seemed to behave well, but e.g. not neutron). We decided to create a new role for domain admins called domain-admin.

To create the role:

    openstack role create domain-admin
    openstack role add --domain $DOMAIN_ID --user $DOMAIN_ADMIN_USER domain-admin

Policy change:

    "admin_required": "role:admin or role:domain-admin",

Using this approach, these users will not have extra privileges in other services, and they won't be able to see/delete other domain networks.

The only remaining problem is that the domain-admin can assign the admin role to an user, to solve that situation we can do some policy changes to constrain the roles that a domain-admin can assign:

    "domains_grant_rule": "rule:domain_admin_for_grants and ('_member_':%(target.role.name)s or 'domain-admin':%(target.role.name)s",
    "identity:create_grant": "rule:cloud_admin or rule:domains_grant_rule",

A domain-admin will be able, given the policy above, to delegate its role:

    openstack role add --domain $DOMAIN_ID --user-domain $DOMAIN_ID --user $USER domain-admin



### Creating a project-admin role to avoid using the admin one (policy changes combined with domain-admin changes)

For the same reasons as with domain admins, don't want to use the `admin` role to create project admins.

To create the role:

    openstack role create domain-admin
    openstack role add --domain $DOMAIN_ID --user $PROJECT_ADMIN_USER project-admin

Policy change:
    "admin_required": "role:admin or role:domain-admin or role:project-admin"

Now, to let project admins assign roles, but limiting the choices:

    "domains_grant_rule": "rule:domain_admin_for_grants and ('_member_':%(target.role.name)s or 'domain-admin':%(target.role.name)s or 'project-admin':%(target.role.name)s)",
    "projects_grant_rule": "rule:project_admin_for_grants and ('_member_':%(target.role.name)s or 'project-admin':%(target.role.name)s)",
    "identity:create_grant": "rule:cloud_admin or rule:domains_grant_rule or rule:projects_grant_rule",


And then, further changes in the policy file were needed to let project-admins assign users to projects through horizon:

    "admin_and_token_matching_project_domain_id": "rule:admin_required and token.user.domain.id:%(project.domain_id)s",
    "identity:list_projects": "rule:cloud_admin or rule:admin_and_matching_domain_id or rule:admin_and_token_matching_domain_id",
    "identity:update_project": "rule:cloud_admin or rule:admin_and_matching_target_project_domain_id or rule:admin_and_token_matching_project_domain_id",
    "admin_and_token_matching_domain_id": "rule:admin_required and token.user.domain.id:%(domain_id)s",
    "identity:list_users": "rule:cloud_admin or rule:admin_and_matching_domain_id or rule:admin_and_token_matching_domain_id",
    "identity:list_groups": "rule:cloud_admin or rule:admin_and_matching_domain_id or rule:admin_and_token_matching_domain_id",
    "identity:list_role_assignments_for_tree": "rule:cloud_admin or rule:admin_on_domain_of_project_filter or (rule:admin_required and token.user.domain.id:%(target.project.domain_id)s)",






## More alternatives researched (previous failures)

### Admin role per domain

We are now creating a drole called `admin-$DOMAIN_ID` for each domain created. With this approach and modifying the keystone policy file to give the user access to all the domain admin operations, see

Policy:

    "admin_required": "role:admin or role:admin-%(domain_id)s"


### admin role within domain, not in default domain

To create the role

    openstack role create admin --domain test-domain
    openstack role add --domain test-domain --role-domain test-domain --user test-admin admin

The result doesn't give the domain admin user any extra permissions


### domain-admin role for the domain admins

To create the role

    openstack role create domain-admin
    openstack role add --domain foo-domain --user foo-admin domain-admin

Policy:

    "admin_required": "role:admin or role:domain-admin",

This is the closest result to what we want, the only problem is that the "domain-admin" is allowed to assign the "admin" role to any user.


### domain-admin role, and redefining grant rules

To create the role

    openstack role create domain-admin
    openstack role add --domain foo-domain --user foo-admin domain-admin


Policy:

    "admin_required": "role:admin or role:domain-admin",
    "old_grant_rule": "rule:cloud_admin or rule:domain_admin_for_grants or rule:project_admin_for_grants",
    "identity:create_grant": "rule:old_grant_rule and '_member_':%(target.role.name)s",


### Continuing previous example, letting domain-admins assign that role, and project-admins also its role

For domain-admin to delegate role

    openstack role add --domain deb0caeada4a49c6a297ac23868e2fa4 --user-domain deb0caeada4a49c6a297ac23868e2fa4 --user test-user domain-admin

And to verify it's there

    openstack role assignment list --domain deb0caeada4a49c6a297ac23868e2fa4 --user-domain deb0caeada4a49c6a297ac23868e2fa4 --user test-user  --name 

To create project-admin role

    openstack role create project-admin
    openstack role add --domain foo-domain --user foo-user domain-admin

As a project admin now you can

    openstack role add --user 5574b8438509463e9baa3ee1dd364c1a _member_ --user-domain 7fcecb8762a44381b382c74ce5de0f13 --project 5328e4a9f5914635bfaa4117cdec4dc4
    openstack role add --user 5574b8438509463e9baa3ee1dd364c1a project-admin --user-domain 7fcecb8762a44381b382c74ce5de0f13 --project 5328e4a9f5914635bfaa4117cdec4dc4
    openstack role add --user 5574b8438509463e9baa3ee1dd364c1a domain-admin --user-domain 7fcecb8762a44381b382c74ce5de0f13 --project 5328e4a9f5914635bfaa4117cdec4dc4
        You are not authorized to perform the requested action: identity:create_grant. (HTTP 403) (Request-ID: req-487cf08a-83bd-41f3-a218-da79e607f21b)

You can't list the users of the domain though, which would be important to know who to asign to what role



Seems to do what we want. Users and projects can be created by "domain-admin", and they can add members in projects. The problem is that in horizon creating users and projects is not exposed.

[1]: https://www.openstack.org/assets/presentation-media/Flat-no-more-Hierarchical-multitenancy-and-projects-acting-as-domains-in-OpenStack.pdf
[2]: https://bugs.launchpad.net/keystone/+bug/968696
