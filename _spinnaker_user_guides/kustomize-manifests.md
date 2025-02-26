---
layout: post
title: Using Kustomize for Manifests
order: 100
---
Note that Kustomize is currently in [Beta](https://kb.armory.io/releases/early-release-beta-GA/). The feature is working and installable but is not meant for production use.


* This is a placeholder for an unordered list that will be replaced with ToC. To exclude a header, add {:.no_toc} after it.
{:toc}


Kustomize is a tool that lets you create customized Kubernetes deployments without modifying underlying YAML configuration files. Since the files remain unchanged, others are able to reuse the same files to build their own customizations. Your customizations are stored in a file called `kustomization.yaml`. If configuration changes are needed, the underlying YAML files and `kustomization.yaml` can be updated independently of each other.

To learn more about Kustomize and how to define a `kustomization.yaml` file, see the following links:

* [Kubernetes SIG for Kustomize](https://github.com/kubernetes-sigs/kustomize)
* [Documentation for Kustomize](https://github.com/kubernetes-sigs/kustomize/tree/master/docs)
* [Example Kustomization](https://github.com/kubernetes-sigs/kustomize/tree/master/examples/wordpress)

In the context of Spinnaker, Kustomize lets you generate a custom manifest, which can be deployed in a downstream `Deploy (Manifest)` stage. This manifest is tailored to your requirements and built on existing configurations.

Spinnaker uses the latest non-kubectl version of Kustomize. 

## Enabling Kustomize in 2.16 (Beta)

Kustomize can be enabled by a feature flag in 2.16.

For Halyard, add the following line to `~/.hal/{DEPLOYMENT_NAME}/profiles/settings-local.js`:

```javascript
window.spinnakerSettings.feature.kustomizeEnabled = true;
```

## Using Kustomize

Kustomize works by running `kustomize build` against a `kustomization.yaml` file located in a Git repository. This file defines all of the other files needed by Kustomize to render a fully hydrated manifest.

Select `Kustomize` as the Render Engine and define the artifact for your `kustomization.yaml`:

![](/images/kustomize-render-engine.png)


With the Kustomize file defined, configure a Produced Artifact to use the result in a stage downstream.
Add an artifact:

![](/images/kustomize-add-artifact.png)

Define the artifact:

![](/images/kustomize-define-artifact.png)

You can now run your pipeline and get a Kustomize rendered manifest!
