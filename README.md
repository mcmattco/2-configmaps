# 2-configmaps

objectives:

1. take previous project, split nginx into seperate pods
  * use configmaps to do something, maybe to mount files instead of importing files into container
  * end up using base nginx container instead
2. something using secrets
  * webpage that shows select query from a mysql db?
3. use cronjobs to do something
  * backup of database?

lessons learned:

1. initContainers, can use to run a load before the other pods start
2. Can mount a volume to the initContainer, output to the volume, then mount that into the pod
  * getting elb info wth aws-cli in this case into 'workdir' volume
  * can use grep/awk/sed/cut to get only the DNS name (elbcmd.txt)
  * but this caused initContainer to crash, not sure why yet
3. using secrets with aws-cli to authenticate
4. using configmap to mount files into a pod, default.conf in this case
  * default.conf has some variables available to use, but these are not env vars
  * can't set env vars using a configmap then use that in default.conf
4. jq and yq can be used to parse json and yaml
5. running commands on pod start, syntax very finicky
  * depends on containers entrypoints
  * https://kubernetes.io/docs/tasks/inject-data-application/define-command-argument-container/
