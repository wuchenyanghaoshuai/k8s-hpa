# 首先确保kubectl top node/pods 出现数据
# kubectl apply -f deployment.yaml
# kubectl apply -f auto-scale-v1.yaml
# kubectl expose deployment nginx-deployment --name=nginx-svc --port=80 --target-port=80 --typr=NodePort
# yum -y install httpd-tools
#  ab -n 100000000 -c 100  10.244.4.2/index.html (此ip为svc的地址)
<<<<<<< HEAD
# 过了大概30s-60s 再去查看kubectl top pods or kubectl get hpa 就可以发现 阈值明显高于设定的值,随后pod的数量会增加
=======
![image](https://user-images.githubusercontent.com/39818267/122325046-73b33f80-cf5c-11eb-8d5b-2243c88cbda7.png)
![image](https://user-images.githubusercontent.com/39818267/122325186-b37a2700-cf5c-11eb-96da-aed1f2180bf8.png)

>>>>>>> b884a7252d5d63390ad76a6e4587b77cf871e977
