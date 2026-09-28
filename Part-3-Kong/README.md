# 1. Add the official Kong Helm repository
helm repo add kong https://charts.konghq.com
helm repo update

# 2. Install Kong using the recommended ingress chart layout
# This sets up an opinionated, high-performance DB-less gateway ecosystem
# Execute the installation using the unified core container chart topology
helm install my-kong kong/kong --namespace kong --create-namespace -f values.yaml



# 3. Make values.yaml file to fix the error "Data cannot be displayed due to an error"
helm upgrade my-kong kong/kong \
  --namespace kong \
  -f values.yaml
