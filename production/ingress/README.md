# This folder contains the ingress for mapping service exposed by the deployments step.

## Root Ingress

This contains the root domain mapping of all apps and subdomains to its corresponding services of deployments.

**Note :**

1. SSL for root domains (domains related to the platform) will be auto provisioned by the cert-manager internally,

2. But custom domain for tenants can't be auto provisioned with SSL, for that we need to programatically add corresponding ingress with the domain name of the particular tenant to the corresponding service.
   In the ingress itself we use http01 cert issuer resolution to provision ssl to that particular tenant.

3. If a Tenant uses Custom domain feature, while on deletion of the pariticaular tenant account, the ingress resource created for that particular domain also need to delted, programatically. hence we don't need to auto renew the SSL (after 90 days) for the revoked tenant.

4. Programattic kubernetes api access source is available on the separate repo, that needs to consumed while performing such programatic operations.

5. **Important :** Don't forget to mention namespace in the ingress file, this will cause serious issue in service mapping via ingress resource if applied ingress applied on different namespace, so make sure to have control over that.
   ```yaml
   kind: Ingress
   metadata:
     name: <ingress-name>
     namespace: <namespace-name>
   ```
