# Release Process

The release process of a new version of KEDA involves the following:

## 0. Prerequisites

Look at the last released version in the releases page: https://github.com/kedacore/keda/releases
For example: currently it is 2.3.0
The next version will thus be 2.4.0

## 1. Changelog

Provide a new section in `CHANGELOG.md` for the new version that is being released along with the new features, patches and deprecations it introduces.

It should not include every single change but solely what matters to our customers, for example issue template that has changed is not important.

## 2. Add the new version to GitHub Bug report template
Add the new released version to the list in `KEDA Version` dropdown in [3_bug_report.yml](https://github.com/kedacore/keda/blob/main/.github/ISSUE_TEMPLATE/3_bug_report.yml).

## 3. Publish documentation for new version

Publish documentation for new version on https://keda.sh.

See [docs](https://github.com/kedacore/keda-docs#publishing-a-new-version).

## 4. Create KEDA release on GitHub

Creating a new release in the releases page (https://github.com/kedacore/keda/releases) will trigger a GitHub workflow which will create a new image with the latest code and tagged with the next version (in this example 2.4.0).

KEDA Deployment YAML file (eg. keda-2.4.0.yaml) is also automatically created and attached to the Release as part of the workflow.

> Note: The Docker Hub repo with all the different images can be seen here: https://hub.docker.com/r/kedacore/keda/tags

### Release template

Every release should use the following template to create the GitHub release.

> 💡 Don't forget to update the version in the template

Here's the template:

```markdown
We are happy to release KEDA <INSERT-CORRECT-VERSION> 🎉

Here are some highlights:

- <list highlights>

Learn how to deploy KEDA by reading [our documentation](https://keda.sh/docs/INSERT-CORRECT-VERSION/deploy/).

### New

- <list items>

### Improvements

- <list items>

### Breaking Changes

- <list items>

### Other

- <list items>
```

## 5. Prepare our Helm Chart

Before we can release our new Helm chart version, we need to prepare it:

- Update the `version` and `appVersion` in our [chart definition](https://github.com/kedacore/charts/blob/master/keda/Chart.yaml).
- Update the CRDs & Kubernetes resources based on the release artifact (YAML)

## 6. Ship new Helm chart

Guidance on how to release it can be found in our [contribution guide](https://github.com/kedacore/charts/blob/master/CONTRIBUTING.md#shipping-a-new-version).

### Deploy KEDA through Azure Functions Core Tools (optional)

Update the following file:
https://github.com/Azure/azure-functions-core-tools/blob/v3.x/src/Azure.Functions.Cli/StaticResources/keda-v2.yaml
[Search for 1.1.0 etc. and replace it]

## 7. Prepare next release

Prepare next release by creating a [new GitHub milestone](https://github.com/kedacore/keda/milestones/new) called `v{upcoming-semver-version}` with a target date in 3 months as per our [release governance](https://github.com/kedacore/governance/blob/main/RELEASES.md).
