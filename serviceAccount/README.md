# ServiceAccount
**serviceaccount** konusuyla ilgili dosyalara buradan erişebilirsiniz.

## servisleri görmek için

kubectl get svc 


kubectl exec -it testpod -bash
cd /var/run/secrets/kubernetes.io/serviceaccount/
bash-5.0# curl --insecure https://kubernetes
{
  "kind": "Status",
  "apiVersion": "v1",
  "metadata": {},
  "status": "Failure",
  "message": "forbidden: User \"system:anonymous\" cannot get path \"/\"",
  "reason": "Forbidden",
  "details": {},
  "code": 403
}bash-5.0# 

### yetkisi ollmadığı için göremedi

TOKEN=$(cat /var/run/secrets/kubernetes.io/serviceaccount/token)
echo TOKEN
curl --insecure https://kubernetes --header "Authorization:Bearer $TOKEN"

curl --insecure https://kubernetes/api/v1/namespaces/default/pods --header "Authorization:Bearer $TOKEN"

## bu urlye giderbilir çünkü yetkisi bunun için verildi .

curl --insecure https://kubernetes/api/v1/namespaces/default/pods --header "Authorization:Bearer $TOKEN" | jq '.items[].metadata.name'
