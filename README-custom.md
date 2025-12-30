

Note: To update a large file on s3, you have to add in the ingress annotation of ther console and api:
     
 annotations:
   nginx.ingress.kubernetes.io/proxy-body-size: "0"
