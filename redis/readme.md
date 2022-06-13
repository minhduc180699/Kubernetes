helm install my-release -n redis bitnami/redis-cluster -f redis-values.yaml --timeout 10m30s

IMPORTANT NOTE:
    REMOVE PVCs BEFORE DEPLOYING REDIS