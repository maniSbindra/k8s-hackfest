# KUBERNETES-HACK


## Sample services for php and mysql
* mysql.yaml, php.yaml, secrets.yaml and data-loader-job.yaml  files were used. Please refer [https://github.com/heptio/example-lamp](https://github.com/heptio/example-lamp) for more details on these yamls

## External DNS
* External-dns.yaml file was deployed

## Nginx ingress
* nginx-ingress Helm chart was locally downloaded, the controller-service yaml file was modified to the controller-service.yaml file in this repo. Command executed

    ```sh
    helm install --name ingress-controller11 ./nginx-ingress/

    # replica count was later changed
    # helm  upgrade ingress-controller11 ./nginx-ingress/ --set controller.replicaCount=3
    ```

## Ingress rule for PHP Web application : 
* File is phpingress.yaml
* sample secret was created using the command below

    ```sh
    openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /tmp/tls.key -out /tmp/tls.crt -subj "/CN=*.manitestdomain.com"

    kubectl create secret tls manitestdomain-secret --key /tmp/tls.key --cert /tmp/tls.crt
    ```

## EFK installation
* For elastic search following command was executed

    ```sh
    helm install --name esearch5 incubator/elasticsearch --namespace kube-system --set client.replicas=1 --set master.replicas=2 --set data.replicas=1 --set master.persistence.storageClass=default
    ```

* for fluentd and kibana yamls refer [https://github.com/maniSbindra/OSS-Meetup](https://github.com/maniSbindra/OSS-Meetup)
