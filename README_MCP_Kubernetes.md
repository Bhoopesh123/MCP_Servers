# Grafana LLM Plugin

    Reference Documentation:
    https://grafana.com/docs/grafana-cloud/machine-learning/llm/

# 1. Install Ingress

helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update

helm upgrade --install ingress-nginx ingress-nginx/ingress-nginx \
  --namespace ingress-nginx --create-namespace



helm repo add aws-ebs-csi-driver https://kubernetes-sigs.github.io/aws-ebs-csi-driver
helm repo update


helm upgrade --install aws-ebs-csi-driver aws-ebs-csi-driver/aws-ebs-csi-driver \
  --namespace kube-system \
  --set controller.serviceAccount.create=false \
  --set controller.serviceAccount.name=ebs-csi-controller-sa



# 2. Install Grafana

helm  upgrade  --install grafana prometheus-community/kube-prometheus-stack


helm repo add grafana https://grafana.github.io/helm-charts
helm repo update

helm upgrade --install grafana grafana/grafana \
  --namespace monitoring --create-namespace \
  --set persistence.enabled=true \
  --set adminPassword='admin123' \
  --set service.type=ClusterIP

helm upgrade --install grafana grafana/grafana \
  --namespace monitoring --create-namespace \
  --set persistence.enabled=true \
  --set persistence.storageClassName="gp2" \
  --set persistence.size=10Gi \
  --set adminPassword='admin123' \
  --set service.type=ClusterIP


# 2. Install MCP-Grafana

helm repo add grafana https://grafana.github.io/helm-charts
helm upgrade --install --set grafana.apiKey=xxxxx --set grafana.url=fgfddf mcp grafana/grafana-mcp

# 4. Validate the metrics on Grafana
To Search all of the time series data points grouping by job  in query  

    count({__name__=~".+"}) by (job)