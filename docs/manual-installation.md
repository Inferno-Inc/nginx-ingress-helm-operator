# Manual installation

This will deploy the operator in the `nginx-ingress-operator-system` namespace.


1. Deploy the Operator and associated resources:
   1. Clone the `nginx-ingress-operator` repo and checkout the latest stable tag:
    ```
    git clone https://github.com/nginxinc/nginx-ingress-helm-operator/
    cd nginx-ingress-helm-operator/
    git checkout v1.2.0
    ```

   2. `OpenShift` To deploy the Operator and associated resources to an OpenShift environment, run:
    ```
    make deploy IMG=nginx/nginx-ingress-operator:1.2.0
    ```

   3. Alternatively, to deploy the Operator and associated resources to all other environments:
    ```
    make deploy IMG=nginx/nginx-ingress-operator:1.2.0
    ```

2. Check that the Operator is running:
    ```
    kubectl get deployments -n nginx-ingress-operator-system

    NAME                                        READY   UP-TO-DATE   AVAILABLE   AGE
    nginx-ingress-operator-controller-manager   1/1     1            1           15s
    ```

3. `OpenShift` Additional steps:

In order to deploy NGINX Ingress Controller instances into OpenShift environments, a new SCC is required to be created on the cluster which will be used to bind the specific required capabilities to the NGINX Ingress service account(s). To do so, please run the following command (assuming you are logged in with administrator access to the cluster):

`kubectl -f https://raw.githubusercontent.com/nginxinc/nginx-ingress-helm-operator/v1.2.0/resources/scc.yaml`
