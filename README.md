# k8s-hpa 基于k8s 1.18.0
# 全篇文章介绍如何基于k8s的hpa来进行pod的自动扩缩容
# 第一步安装 metrics-server (kubectl top pods/node)
# 第二步v1版本基于cpu来进行扩缩容
# 第三步prometheus-adapter 
# 第四步v2版本的多选择属性来进行扩缩容
