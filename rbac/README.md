# RBAC
**rbac** konusuyla ilgili dosyalara buradan erişebilirsiniz.
## bulunulan contexti görmek için (cluster)
kubectl config current-context

## bulunulan contexti değiştirmek için
kubectl config use-context minikube

## bulunulan klasördeki tüm yamlları kaldırmak için 
kubectl apply -f .

get rolebindings.rbac.authorization.k8s.io
kubectl get clusterrole
kubectl get rolebindings.rbac.authorization.k8s.io