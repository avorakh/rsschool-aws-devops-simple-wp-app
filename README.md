# rsschool-aws-devops-simple-wp-app

## Tools

- [WordPress](https://wordpress.com/)
- [Kubernetes](https://kubernetes.io/)
- [helm](https://helm.sh/)
- [K3s](https://k3s.io/)
- [MariaDB](https://mariadb.org/)

## Create K8s Cluster
Please see the steps on the page.
- [Link](https://github.com/avorakh/rsschool-devops-course-tasks/blob/task-04/README.md)
- [Change, including helm installation on a bastion host](https://github.com/avorakh/rsschool-devops-course-tasks/pull/10)

## Prerequisites
1. **Clone the Repository**: Clone the project repository to your local machine using the following command:

   ```bash
   git clone hhttps://github.com/avorakh/rsschool-aws-devops-simple-wp-app.git
   ```

2. **Navigate to the Project Directory**: Change a working directory to the project folder:

   ```bash
   cd rsschool-aws-devops-simple-wp-app
   ```

## Prepare the Cluster
### 1. Installation and Configuration MariaDB
1. **Create Namespace:**

    ```bash
    kubectl create namespace wordpress-namespace
    ```

2. **Install MariaDB using Helm:**

    ```bash
    helm install mariadb-wp ./mariadb --namespace wordpress-namespace
    ```

3. **Verify MariaDB installation:**

    ```bash
    kubectl get pods -n wordpress-namespace
    kubectl get deployments -n wordpress-namespace
    kubectl get services -n wordpress-namespace
    ```

    Ensure all pods are running.

### 2. WordPress Installation and Configuration
1. **Install WordPress using Helm**

    ```bash
    helm install wordpress ./wordpress --namespace wordpress-namespace
    ```

2. **Verify WordPress installation:**

    ```bash
    kubectl get pods -n wordpress-namespace
    kubectl get deployments -n wordpress-namespace
    kubectl get services -n wordpress-namespace
    ```

    Ensure all pods are running. Check a jenkins-ci pod log.

3. **Visit WordPress in the browser**

- Login with the password and the username.

    ```
    # for HTTP
    http://<PUT_PUBLIC_IP_OF_WORKER_NODE>:8080
    http://<PUT_PUBLIC_IP_OF_WORKER_NODE>:8080/admin
    # for HTTPS
    https://<PUT_PUBLIC_IP_OF_WORKER_NODE>:8443
    https://<PUT_PUBLIC_IP_OF_WORKER_NODE>:8443/admin
    ```

## Clean Up

- **Run the following command to delete the Helm deployments**
    ```bash
    helm delete wordpress -n wordpress-namespace
    helm delete mariadb-wp -n wordpress-namespace
    ```