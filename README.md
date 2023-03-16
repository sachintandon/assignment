* This code base contains 2 services
  * redis -  which can be used to store data and act as dataStorage , this is created as statefulset deployment thus has a perisistent volume.
  * redisinsight - this is a standalone GUI which can be accessed to view the metrics of redis and connect to redis to get insight


* The Folder structure

  * `Charts` -  contains the charts for both redis & redisinsight
  * `Values/env/` - this contains the specific value file for each service
* Deployment :

  * update the values based on the need in `Values/env/` files.
  * argocd :  application code base prenset in `argocd` folder
  * manual :

    * `helm repo add bitnami https://charts.bitnami.com/bitnami`
    * ` helm repo update`
    * `helm dependency build Charts/redis-cluster`
    * `helm install Charts/redis-cluster -f Values/env/redis-cluster.yaml -n <namespace>` - this install redis
    * `helm template Charts/redisinsight -f Values/env/redisinsight.yaml` -n `<namespace>` -  this install redisinsight
