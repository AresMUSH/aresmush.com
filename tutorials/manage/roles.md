---
title: Using Roles and Permissions
description:
layout: page
---

Ares has a robust and flexible roles/permissions system.  This article describes how you can utilize roles on your game.

<div id="inline_toc" markdown="1">
**Table of Contents**

* TOC
{:toc}
</div>

## Roles vs Permissions

There are two levels to the Roles system:  roles and permissions.

Roles are assigned to characters.  You could have a 'builder' role or a 'pilot' role.  Some things - like channels or forums - can be locked so that only people with certain roles can use them.

Permissions are assigned to roles, and allow you to further refine what people with a given role can do.  

## Default Roles

The default Ares database comes with several roles:

* **Admin** gives access to all game commands except tinkering.  This means they can use the existing commands but can't alter the database directly.
* **Coder** gives access to the [tinker command](/tutorials/code/tinker.html) (which lets them execute arbitrary code) and commands to reload the game code.
* **Builder** gives access to building commands, the ability to describe rooms, and the ability to teleport around.
* **Guest** doesn't give any permissions, but the role is used to identify guest characters so the game can choose one when someone tries to log in as a guest.
* **Approved** grants some basic permissions that are available to approved characters, such as the ability to use the 'home' command.
* **Everyone** is a default role granted to all characters, approved or not.

Additionally, there is a special character - the master admin (default name Headwiz).  The master admin has both the admin and coder roles, and is the only one that can assign those roles.

{% include note.html content="Coders essentially have the keys to the kingdom.  They can do anything to the database, including changing the master admin password.  Make sure you trust your coders!" %}

## Permissions

Roles contain **permissions**, which control access to most commands.  For example, the 'home' command is limited to people with the "go_home" permission.  The ability to create and delete channels is limited to people with the "manage_channels" permission.   

You cannot assign individual permissions to characters.  Permissions may only be assigned to *roles*, which are in turn assigned to characters.

Characters with the Admin role automatically have access to **all** permissions.

{% include tip.html content="A list of the default permissions can be found below." %}

## Creating a New Role - App Staff

Let's say you wanted to create a more limited admin role for apps staff.  You want them to have access to review and approve characters, access to read jobs in the APP category, and access to an Apps forum.

1. Create the role using `role/create app_staff`.
2. Assign permissions using `role/addpermission app_staff=<permission>`.   You probably want to give them things like `manage_apps`, `view_sheets` and `access_jobs`.
3. Update the jobs config to add the `app_staff` role to the APP category.  See the [jobs configuration tutorial](/tutorials/config/jobs.html) for details.
4. Set permissions on the Apps forum using `forum/readroles <roles>` and `forum/writeroles <roles>`.

{% include note.html content="Numerous commands are locked to characters with the 'approved' role as a defense against trolls. Full-fledged admins automatically count as approved, but you'll need to assign the 'approved' role to your other staff manually using <code>role/add &lt;name&gt;=approved</code>.  You should also mark them as player bits with the <code>playerbit</code> command so they don’t show up on the character gallery." %}
  
## Using Permissions in Code

In your code, permissions can restrict who can use commands.  For example, if you wanted to lock the 'home' command to only people who have the 'go_home' permission, you would add the following error checker in the home command handler.

      def check_can_go_home
        return "You are not allowed to do that." if !enactor.has_permission?("go_home")
        return nil
      end

Many plugins have helper methods to check for the necessary permission.  For example:

    Rooms.can_go_home?(enactor)
    Chargen.can_approve?(enactor)

{% include tip.html content="It's preferable to use the helper methods instead of the permission names so you only have to update one place if the permission ever changes." %}

{% include tip.html content="Remember that characters with the 'admin' role automatically have all permissions." %}

## Default Permissions

{% include tip.html content="If you want to know exactly which commands are accessible with these permissions, use the 'search' feature of help files to look for help files referencing these permissions.  You'll see a statement like  \"These commands require the Admin role or the permission: whatever_permission\"." %}

| Role | Notes |
| ---- |
| access_jobs | Characters with the admin role have access to all job categories, but you have to edit the [jobs configuration](/tutorials/config/jobs.html) to give access to other roles. |
| announce | By default this is given to all approved characters so storytellers can announce the start of events. |
| boot | By default this is given to all approved characters as part of the tools for [managing trolls](/tutorials/manage/trolls.html). |
| build | |
| desc_anything | |
| desc_places | | 
| go_home | |
| login | |
| manage_achievements | |
| manage_abilities | |
| manage_apps | |
| manage_channels | |
| manage_combat | |
| manage_demographics | |
| manage_events | |
| manage_forum | |
| manage_idle | |
| manage_login | |
| manage_notes | |
| manage_ranks | |
| manage_roster | |
| manage_scenes | |
| manage_weather | |
| set_duty | |
| teleport | |
| view_bgs | |
| view_sheets | |
