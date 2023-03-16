# Redis-cluster helm chart

## Increasing storage

1. Change `redis-cluster.persistence.size` to the higher value, for example 210Gi
2. Manually change size of all PVCs:

```
kubectl edit pvc redis-data-beta2-redis-redis-cluster-0
...
```

3. Delete statefulset for Redis:

```
kubectl delete sts --cascade=orphan beta2-redis-redis-cluster
```

4. Rollout new sts:

```
kubectl rollout restart sts beta2-redis-redis-cluster
```

5. Ensure that all PVCs were scaled:

```
kg pvc redis-data-beta2-redis-redis-cluster-0
...

k exec -ti beta2-redis-redis-cluster-0 -c beta2-redis-redis-cluster -- df -h /bitnami/redis/data
Filesystem      Size  Used Avail Use% Mounted on
/dev/nvme1n1    207G   48K  207G   1% /bitnami/redis/data
```
