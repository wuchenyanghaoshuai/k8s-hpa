# 在kube-system这个namespace下查看prometheus-adapter是否正常运行
# kubectl get pods -n kube-system|grep prometheus-adapter
# 上面正常再执行下面的命令,看是否注册到apiserver
```
# kubectl get apiservices |grep custom 
# kubectl get --raw "/apis/custom.metrics.k8s.io/v1beta1"
```
# 两个都正常的话,就部署下面的yaml,开始使用自定义指标来扩缩容
# kubectl apply -f deployment-v2.yaml 
# kubectl apply -f hpa-v2.yaml
# 查看是否正常 kubectl get hpa
# 此时hpa应该是不正常的因为没有更新prometheus-adapter,下面就添加一下这个语句即可,添加完以后pod不会自动重启，需要手动的删除这个pod,然后再次get hpa就不会显示unknow了
# 接着使用ab 来进行测试，然后就会触发pod的基于自定义指标的自动扩缩容


```
# kubectl edit cm prometheus-adapter -n kube-system
apiVersion: v1
kind: ConfigMap
metadata:
  labels:
    app: prometheus-adapter
    chart: prometheus-adapter-v0.1.2
    heritage: Tiller
    release: prometheus-adapter
  name: prometheus-adapter
data:
  config.yaml: |
    rules:
    - seriesQuery: 'http_requests_total{kubernetes_namespace!="",kubernetes_pod_name!=""}'
      resources:
        overrides:
          kubernetes_namespace: {resource: "namespace"}
          kubernetes_pod_name: {resource: "pod"}
      name:
        matches: "^(.*)_total"
        as: "${1}_per_second"
      metricsQuery: 'sum(rate(<<.Series>>{<<.LabelMatchers>>}[2m])) by (<<.GroupBy>>)'
...
```
