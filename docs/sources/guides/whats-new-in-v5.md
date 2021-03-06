+++
title = "What's New in Grafana v5.0"
description = "Feature & improvement highlights for Grafana v5.0"
keywords = ["grafana", "new", "documentation", "5.0"]
type = "docs"
[menu.docs]
name = "Version 5.0"
identifier = "v5.0"
parent = "whatsnew"
weight = -6
+++

# What's New in Grafana v5.0

This is the most substantial update that Grafana has ever seen. This article will detail the major new features and enhancements.

- [New Dashboard Layout Engine]({{< relref "#new-dashboard-layout-engine" >}}) enables a much easier drag, drop and resize experience and new types of layouts.
- [New UX]({{< relref "#new-ux-layout-engine" >}}). The UI has big improvements in both look and function.
- [New Light Theme]({{< relref "#new-light-theme" >}}) is now looking really nice.
- [Dashboard Folders]({{< relref "#dashboard-folders" >}}) helps you keep your dashboards organized.
- [Permissions]({{< relref "#dashboard-folders" >}}) on folders and dashboards helps manage larger Grafana installations.
- [Group users into teams]({{< relref "#teams" >}}) and use them in the new permission system.
- [Datasource provisioning]({{< relref "#data-sources" >}}) makes it possible to setup datasources via config files.
- [Dashboard provisioning]({{< relref "#dashboards" >}}) makes it possible to setup dashboards via config files.

### Video showing new features

<iframe height="215" src="https://www.youtube.com/embed/BC_YRNpqj5k?rel=0&amp;showinfo=0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
<br />

## New Dashboard Layout Engine

{{< docs-imagebox img="/img/docs/v50/new_grid.png" max-width="1000px" class="docs-image--right">}}

The new dashboard layout engine allows for much easier movement and sizing of panels, as other panels now move out of the way in
a very intuitive way. Panels are sized independently, so rows are no longer necessary to create layouts. This opens
up many new types of layouts where panels of different heights can be aligned easily. Checkout the new grid in the video
above or on the [play site](http://play.grafana.org). All your existing dashboards will automatically migrate to the
new position system and look close to identical. The new panel position makes dashboards saved in v5.0 not compatible
with older versions of Grafana.

<div class="clearfix"></div>

## New UX

{{< docs-imagebox img="/img/docs/v50/new_ux_nav.png" max-width="1000px" class="docs-image--right" >}}

Almost every page has seen significant UX improvements. All pages (except dashboard pages) have a new tab-based layout that improves navigation between pages. The side menu has also changed quite a bit. You can still hide the side menu completely if you click on the Grafana logo.

<div class="clearfix"></div>

### Dashboard Settings

{{< docs-imagebox img="/img/docs/v50/dashboard_settings.png" max-width="1000px" class="docs-image--right" >}}
Dashboard pages have a new header toolbar where buttons and actions are now all moved to the right. All the dashboard
settings views have been combined with a side nav which allows you to easily move between different setting categories.

<div class="clearfix"></div>

## New Light Theme

{{< docs-imagebox img="/img/docs/v50/new_white_theme.png" max-width="1000px" class="docs-image--right" >}}

This theme has not seen a lot of love in recent years and we felt it was time to rework it and give it a major overhaul. We are very happy with the result.

<div class="clearfix"></div>

## Dashboard Folders

{{< docs-imagebox img="/img/docs/v50/new_search.png" max-width="1000px" class="docs-image--right" >}}

The big new feature that comes with Grafana v5.0 is dashboard folders. Now you can organize your dashboards in folders,
which is very useful if you have a lot of dashboards or multiple teams.

- New search design adds expandable sections for each folder, starred and recently viewed dashboards.
- New manage dashboard pages enable batch actions and views for folder settings and permissions.
- Set permissions on folders and have dashboards inherit the permissions.

## Teams

A team is a new concept in Grafana v5. They are simply a group of users that can be then be used in the new permission system for dashboards and folders. Only an admin can create teams.
We hope to do more with teams in future releases like integration with LDAP and a team landing page.

## Permissions

{{< docs-imagebox img="/img/docs/v50/folder_permissions.png" max-width="1000px" class="docs-image--right" >}}

You can assign permissions to folders and dashboards. The default user role-based permissions can be removed and replaced with specific teams or users enabling more control over what a user can see and edit.

<div class="clearfix"></div>

# Provisioning from configuration

In previous versions of Grafana, you could only use the API for provisioning data sources and dashboards.
But that required the service to be running before you started creating dashboards and you also needed to
set up credentials for the HTTP API. In 5.0 we decided to improve this experience by adding a new active
provisioning system that uses config files. This will make GitOps more natural as data sources and dashboards can
be defined via files that can be version controlled. We hope to extend this system to later add support for users, orgs
and alerts as well.

### Data sources

Data sources can now be setup using config files. These data sources are by default not editable from the Grafana GUI.
It's also possible to update and delete data sources from the config file. More info in the [data source provisioning docs](/administration/provisioning/#datasources).

### Dashboards

We also deprecated the [dashboard.json] in favor of our new dashboard provisioner that keeps dashboards on disk
in sync with dashboards in Grafana's database. The dashboard provisioner has multiple advantages over the old
[dashboard.json] feature. Instead of storing the dashboard in memory we now insert the dashboard into the database,
which makes it possible to star them, use one as the home dashboard, set permissions and other features in Grafana that
expects the dashboards to exist in the database. More info in the [dashboard provisioning docs](/administration/provisioning/#dashboards)

# Dashboard model & API

We are introducing a new identifier (`uid`) in the dashboard JSON model. The new identifier will be a 9-12 character long unique id.
We are also changing the route for getting dashboards to use this `uid` instead of the slug that the current route and API are using.
We will keep supporting the old route for backward compatibility. This will make it possible to change the title on dashboards without breaking links.
Sharing dashboards between instances becomes much easier since the uid is unique (unique enough). This might seem like a small change,
but we are incredibly excited about it since it will make it much easier to manage, collaborate and navigate between dashboards.