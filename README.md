# Grafana Tempo and Elasticsearch performance comparison

This repository compares resource utilization of Tempo and Elasticsearch.

## Methodology

TBD

## Deploy

### Prepare environment

```bash
make start-minikube
make deploy-monitoring
make deploy-jaeger-operator
make deploy-test-opensearch
```

### Deploy load generator
```bash
kubectl apply -f load-generator.yaml  
```

## Check Kubernetes resources
```bash
kubectl describe nodes kind-control-plane
```

```bash
kubectl top pod -n test-opensearch   
```

## Results

### OpenSearch

Max ingestion rate for a single jaeger-collector? / When ES will start dropping data?

no drop (some here and there) 4500 spans/s
```
      # default is 50
      collector.num-workers: 20
      # default is 2000
      # for 400k memory is ~1463Mi
      collector.queue-size: 4000
      es.num-shards: 3
      es.num-replicas: 1
      # default 1
      es.bulk.workers: 3000
      # default 5000000
      es.bulk.size: 5000000
      # default 1000
      es.bulk.actions: 1000
      # default 200ms
```


## Related links
* Grafana Tempo capacity planning https://github.com/grafana/tempo/issues/1540
* Grafana Mimir capacity planning https://github.com/grafana/mimir/issues/1988
