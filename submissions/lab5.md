# Lab 5 — CI/CD & GitOps

## Task 1 — CI Pipeline + ArgoCD Setup

### GitHub Actions run

- Run URL: TODO
- Result: TODO

### GHCR packages

```bash
TODO: paste output of gh api user/packages?package_type=container --jq '.[].name'
```

### ArgoCD application state

```bash
TODO: paste output of argocd app get quickticket
```

### GitOps sync proof

```bash
TODO: paste output proving the Git change reached the cluster
```

### What happens if someone manually runs `kubectl edit` on an ArgoCD-managed resource?

Manual edits create drift between the live Kubernetes object and the desired state stored in Git. ArgoCD detects the resource as `OutOfSync`; with automated sync and self-heal enabled, ArgoCD reverts the manual change back to the Git version. Without self-heal, the drift remains visible until the next sync.

## Task 2 — Rollback via GitOps

### Bad deploy evidence

```bash
TODO: paste argocd app get quickticket after bad image deploy
```

```bash
TODO: paste kubectl get pods showing ImagePullBackOff or ErrImagePull
```

### Git revert evidence

```bash
TODO: paste git log --oneline -3 showing deploy and revert commits
```

### Recovery evidence

```bash
TODO: paste argocd app get quickticket after rollback
```

- Time from `git revert` + push to healthy pods: TODO

## Bonus Task — Automated Image Tag Update

The CI workflow builds all three service images, pushes them to GHCR with the immutable `${{ github.sha }}` tag, updates the image tags in `k8s/*.yaml`, and commits the manifest change with a `ci:` prefix. The build job skips `ci:` commits to avoid an infinite loop.

### Auto-tag evidence

```bash
TODO: paste git log showing code commit followed by ci: update image tags commit
```

```bash
TODO: paste ArgoCD/image output showing the auto-updated SHA tag deployed
```
