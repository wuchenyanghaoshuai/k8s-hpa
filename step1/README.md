# 首先找到官方github地址
# https://github.com/kubernetes-sigs/metrics-server
# 往下翻找到自己相对应的版本(我这边选择是0.5)
# 找到右侧的release版本 复制想对应的版本的yaml即可
# 复制到自己服务器的地址进行稍微的修改一下
# - --kubelet-preferred-address-types=InternalIP,ExternalIP,Hostname
# - --kubelet-insecure-tls
# - hostNetwork: true
# 如果yaml内镜像下载失败,可以换另外一个 willdockerhub/metrics-server 具体的镜像版本自己手动查看
# 此处说明我加serviceaccount是因为我要从我自己的私有harbor里拉取镜像
# 注意: kubeadm 方式部署的话，在/etc/kubernetes/manifests/kube-apiserver.yaml修改
#   增加这一句话     - --enable-aggregator-routing=true 开启路由
# 二进制部署的话
# vi /opt/kubernetes/cfg/kube-apiserver.conf
...
--requestheader-client-ca-file=/opt/kubernetes/ssl/ca.pem \
--proxy-client-cert-file=/opt/kubernetes/ssl/server.pem \
--proxy-client-key-file=/opt/kubernetes/ssl/server-key.pem \
--requestheader-allowed-names=kubernetes \
--requestheader-extra-headers-prefix=X-Remote-Extra- \
--requestheader-group-headers=X-Remote-Group \
--requestheader-username-headers=X-Remote-User \
--enable-aggregator-routing=true \
...

#
