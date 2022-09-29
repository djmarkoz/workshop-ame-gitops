# 4. Install FluxCD

We will now be installing fluxcd and integrating it with your Kubernetes cluster.

**If you are doing this with a team: these steps should only be done once per cluster**

## Tasks

- [Install fluxcd](https://fluxcd.io/flux/installation/) locally (`brew install fluxcd/tap/flux`)
- [Fork this repository](https://github.com/avisi-cloud/workshop-ame-gitops/fork) to your own Github profile or organisation. (Only one person per team should do this. You should give your other team members access to the forked repository.)
- [Create a GITHUB_TOKEN](https://github.com/settings/tokens/new) with `Full control of private repositories` which Fluxcd should use to access the git repository.
- Bootstrap fluxcd in your cluster (See below).
- Observe Kubernetes deployments being installed in your cluster (`kubectl get deploy -A`).

## References

- [fluxcd installation](https://fluxcd.io/flux/installation/)
- [Github Fork a Repo](https://docs.github.com/en/get-started/quickstart/fork-a-repo)
- [Install flux into your cluster](https://fluxcd.io/flux/get-started/#install-flux-onto-your-cluster)

## Examples

### Bootstrap

[flux bootstrap github](https://fluxcd.io/flux/cmd/flux_bootstrap_github/)

```bash
# Create a GitHub personal access token and export it as an env var
export GITHUB_TOKEN=<my-token>

flux bootstrap github \
  --owner=<your user name> \
  --repository=workshop-ame-gitops \
  --branch=main \
  --path=clusters/workshop \
  --personal
```

The output is similar to:

```bash
► connecting to github.com
✔ repository created
✔ repository cloned
✚ generating manifests
✔ components manifests pushed
► installing components in flux-system namespace
deployment "source-controller" successfully rolled out
deployment "kustomize-controller" successfully rolled out
deployment "helm-controller" successfully rolled out
deployment "notification-controller" successfully rolled out
✔ install completed
► configuring deploy key
✔ deploy key configured
► generating sync manifests
✔ sync manifests pushed
► applying sync manifests
◎ waiting for cluster sync
✔ bootstrap finished
```

## Next assignment

[05. Change node pool](/assignments/05-change-node-pool.md)
