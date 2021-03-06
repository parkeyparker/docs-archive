---
layout: default
title: "Alternate Workflow to Replace Cloning Tool"
canonical: "/pe/latest/cloning_alt.html"
---


We are continuing to improve resource inspection and interactive orchestration commands in the console.

In general, we recommend managing resources with Puppet manifests instead of one-off commands. This page describes an alternate workflow which can provide the same funtionality as the cloning tool did.

##### Alternate Workflow in Brief
Use `puppet resource` or [the puppetral plugin's `find` action](./orchestration_actions.html#find) to learn the details of resources on individual host. Then, use that information to write or append to a manifest.

* * *
