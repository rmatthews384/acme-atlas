# acme-atlas (demo)

Demo Atlas repo showing the **v2 layout** from
[`_template-v2`](https://github.com/cfacorp/kube-projects-argo/tree/master/akuity-appteam-projects/_template-v2):

```text
<region>/<full-namespace-name>/<app>/
```

Environment is selected by **git branch**, not by a folder:

| Branch | Environment |
|--------|-------------|
| `dev`  | development |
| `test` | test        |
| `prod` | production  |

## Layout in this repo

```text
use1-01/
  acme-web/
    portal/          # Deployment + Service
    admin/
  acme-batch/
    nightly-job/
usw2-01/
  acme-web/
    portal/
  acme-batch/
    nightly-job/
```

This matches the fictional `acme` atlas in the AppProject / ApplicationSet
examples (`acme-web`, `acme-batch`).

## How Argo would name Applications

With the v2 ApplicationSet template, each app dir becomes:

```text
<env>-<region>-<namespace>-<app>
```

Examples on the `dev` branch:

- `dev-use1-01-acme-web-portal`
- `dev-use1-01-acme-web-admin`
- `dev-use1-01-acme-batch-nightly-job`
- `dev-usw2-01-acme-web-portal`
- `dev-usw2-01-acme-batch-nightly-job`

## Notes

- This is a **walkthrough / shape demo** only. Manifests are minimal placeholders.
- Namespace dirs use the **full** Kubernetes namespace name.
- Files sitting directly in a namespace dir (for example a README) are ignored by
  the git generator; only app subdirectories create Applications.
- A team adding `use1-01/rogue-ns/app/` without KSS provisioning that namespace
  would create **no** Application, because AppSets only scan allowlisted
  namespaces.