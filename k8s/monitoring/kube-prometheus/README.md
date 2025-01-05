helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo updata
helm install cflb-kps-1 -f values.yaml prometheus-community/kube-prometheus-stack
