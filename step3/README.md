# prometheus-adapter 关系图
![image](https://user-images.githubusercontent.com/39818267/122394690-d92d1d80-cfa8-11eb-8eb4-a11d32e70d00.png)

# 因为prometheus-adapter是从prometheus里获取到的数据，所以首先是要安装一个prometheus
# 这里选择安装prometheus-operator(这个里面自带了grafana)
# https://github.com/prometheus-operator/kube-prometheus
# 这里选择的是0.5版本 (可以自己按照自己集群的版本来选择operator的版本)
# git clone https://github.com/prometheus-operator/kube-prometheus.git
# git checkout release-0.5
# cd manifests 
# kubectl apply -f setup
# kubectl apply -f .
# 执行完yaml文件以后,kubectl get pods -n monitoring 来查看pod是否running
# 此处需要修改prometheus和grafana的 svc暴露方式为nodeport ,prometheus-service.yaml grafana-service.yaml
![image](https://user-images.githubusercontent.com/39818267/123056718-c186e680-d439-11eb-9296-c5d9b8dbfcae.png)
# 下面就继续安装prometheus-adapter 让他去获取prometheus内的数据
# prometheus-adapter 使用helm安装 如果你的机器没有helm是需要安装一下
# wget https://get.helm.sh/helm-v3.0.0-linux-amd64.tar.gz
# tar zxvf helm-v3.0.0-linux-amd64.tar.gz 
# mv linux-amd64/helm /usr/bin/
# helm repo add stable http://mirror.azure.cn/kubernetes/charts
# helm repo update
# helm repo list
# helm install prometheus-adapter stable/prometheus-adapter --namespace kube-system --set prometheus.url=http://prometheus.kube-system,prometheus.port=9090
# 注意此处需要修改prometheus-adapter的deploy 因为此处他获取的是同namespcace的prometheus,但是咱们的prometheus安装在monitoring这个namespace,所以此处需要修改一下
![image](https://user-images.githubusercontent.com/39818267/123087865-9f03c600-d457-11eb-9ff3-4b5d727f9ec3.png)

# 修改完成以后查看一下adapter的日志，应该是正常的没有任何问题的
# helm list -n kube-system 查看到adapter 正常启动即可
# kubectl get apiservices   此时应该看到两个,一个是metrics-server 一个是prometheus-adapter
# kubectl get --raw "/apis/custom.metrics.k8s.io/v1beta1"
![image](https://user-images.githubusercontent.com/39818267/123087913-ae830f00-d457-11eb-9378-5f1339e5d152.png)

