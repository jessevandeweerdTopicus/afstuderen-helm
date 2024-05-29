# Start spreekuur-uitnodigingen


#### Downloads:

- Docker
    - https://docs.docker.com/engine/install/
- Minikube
    - MacOs: brew install minikube
    - Windows: https://github.com/kubernetes/minikube/releases
- Helm
    - MacOs: brew install helm
    - Windows: choco install kubernetes-helm
- Kubectl
    - https://kubernetes.io/docs/tasks/tools/

#### Optional (but definitely recommended):
- K9s
    - MacOs: brew install derailed/k9s/k9s
    - Windows: https://github.com/derailed/k9s/releases

### Prerequisites:
- Docker needs to be up and running.
- You need to have the following secrets set up to connect to Cloudsmith;
  - cloudsmith-secret
    - `kubectl create secret generic cloudsmith-secret \` <br>
    `--from-literal=username= <insert your cloudsmith username> \` <br>
    `--from-literal=password= <insert your cloudsmith token>`
  - cloudsmith-pull-secret
    - `kubectl create secret docker-registry cloudsmith-pull-secret \` <br>
      `--docker-server=docker.cloudsmith.io \` <br>
      `--docker-username=<insert your cloudsmith username> \` <br>
      `--docker-password=<insert your cloudsmith token> \` <br>
      `--docker-email=<insert your cloudsmith email address>`

## Step 1: Start minikube

Open a terminal and run `minikube start`. This will start a local kubernetes cluster.

## Step 2: Install the chart

Open a terminal and navigate to the root of the chart, where Chart.yaml is located. Run `helm install spreekuur-uitnodigingen .` to install the chart.

## Step 3: Check if the chart is running

Run `k9s` to open the k9s dashboard. You should see a pod called `spreekuur-uitnodigingen-webservice`. 

The pods `activemq`, `postgresql`, `service` and `webservice` should all be running soon after installing the chart.
`migrations` and `filler` will only start running when `postgresql` is up and running and should both have the status `Completed` soon after.

## Step 4: Port forwarding

If you're using k9s you can easily port forward the webservice by selecting the pod and pressing `shift + f`. The pod will be accessible on the selected port.

If you're not using k9s you can run `kubectl port-forward <pod-name> <local-port>:<pod-port>` to port forward the service.

## Step 5: Uninstall the chart and stop minikube

Run `helm uninstall spreekuur-uitnodigingen` to uninstall the chart.

Run `minikube stop` to stop the local kubernetes cluster.

