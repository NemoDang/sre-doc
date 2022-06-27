# HashicropVaultTokenExpiring

## Meaning

Hashicrop Vault token will expiring on the specific date time mentioned in the description.

## Impact

Expired Hashicrop Vault token will block the sync of Argocd app that further block the gitops updates. Need to rotate the token in time.  

## Diagnosis

1. Reference the doc [here](https://docs.google.com/document/d/1E5n62ed9-ls3rIIPqd8SoTM2W9OzC6xQTq6jQc11fsA/edit#) to identify the token which about to expire.
2. Rotate the token with Vault UI console or CLI.
3. Update the new token in Vault. Then bump the Vault version in `openshift-gitops/overlay/*/argocd.yaml`. eg:
```yaml
apiVersion: argoproj.io/v1alpha1
kind: ArgoCD
metadata:
  name: openshift-gitops
  namespace: openshift-gitops
  annotations:
    avp.kubernetes.io/path: "/sre-dev/data/vault"
    avp.kubernetes.io/secret-version: "2"
```

## Mitigation

N/A
