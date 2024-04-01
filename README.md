# aws-demos-running-containers-on-eks-website

A sample website for demonstration with the AWS course Running Containers on EKS

First, install Helm 3

```bash
curl -sSL https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
helm version --short
```

This presumes you already deployed the Bitnami nginx Helm chart to Kubernetes. The [docs are here](https://artifacthub.io/packages/helm/bitnami/nginx)

```bash
helm pull my-nginx oci://registry-1.docker.io/bitnamicharts/nginx
tar zxvf nginx*.tgz
cd nginx
helm install my-nginx .
```

At this point it should be spinning up a generic NginX container. Navigate to the `EC2 Load Balancer` and look for the Load Balancer for this ingress. Copy the DNS name and put that into a browser - it will take about 1 minute to be ready.

If you go down to the `Deploying your custom web application` section, you will see the three values you need to edit in the values.yaml file:

```yaml
cloneStaticSiteFromGit.enabled: true
cloneStaticSiteFromGit.repository: "https://github.com/CloudNutter/aws-demos-running-containers-on-eks-website.git"
cloneStaticSiteFromGit.branch: "main"
```

Then just update the helm chart and see the new webpage:

`helm update my-nginx .`

Wait 30 seconds or so, then refresh the page nad see the new website.
