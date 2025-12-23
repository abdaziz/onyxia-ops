https://docs.onyxia.sh/admin-doc/offline-airgap-considerations#mounting-certificates-recommended
Certificates
If you are using non-public (internal) certificates, you need to either mount them (recommended) or skip tls validation (not recommended).  

Mounting certificates (recommended) 
Certificates can be mounted on the API pod :


Copy
api:
  extraVolumeMounts:
    - mountPath: "/usr/local/share/ca-certificates"
      name: ca-bundle
  extraVolumes:
    - name: ca-bundle
      secret:
        secretName: ca-bundle
Disabling tls validation (not recommended)
To disable tls validation for the API ⇒ OIDC provider : oidc.skip-tls-verify
To disable tls validation for Helm (catalogs retrieval) : skipTlsVerify

Images
Currently, Onyxia's images and images used by our opensource catalogs are hosted on Dockerhub.  
Make sure your cluster nodes are configured to pull from a mirror or prepull the corresponding images.  
If needed, you can override the images Onyxia uses in the values.yaml and the images of your services in your catalogs values.yaml / values.schema.json

# Issue:
WARN  [org.keycloak.events] (executor-thread-10) type="LOGIN_ERROR", realmId=" │ycloak", authSessionParentId="b63cdc09-34fa-4f06-aadb-1352e42ea248", authSessionTabId="c-4mgamEmUY"                    │
│ b3a40b95-2b5e-498d-aca0-cf420d2e629a", realmName="datalab", clientId="onyxia", userId="null", ipAddress="10.42. │c8a09fd-aab3-441d-b92c-d2b7fbe4f627", realmName="master", clientId="security-admin-console", userId="ed630eb7-0121-456 │
│ 0.0", error="invalid_redirect_uri", redirect_uri="https://datalab.databrin.com/"                                │14711a9-bf07-ac29-7759-627811f101d8", grant_type="authorization_code", refresh_token_type="Refresh", scope="openid ema │

# Solution: 
make sure the valide redirection match:
https://datalab.databrin.com/
\!/ Do not forget the / at the end


