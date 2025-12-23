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
