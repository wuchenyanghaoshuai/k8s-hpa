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
![image](https://user-images.githubusercontent.com/39818267/123056718-c186e680-d439-11eb-9296-c5d9b8dbfcae.png)

