# Authentication
**Authentication** konusuyla ilgili dosyalara buradan erişebilirsiniz.



**Key ve CSR oluşturma**
```
$ openssl genrsa -out rumeysayuk.key 2048 

$ openssl req -new -key rumeysayuk.key -out rumeysayuk.csr -subj "/CN=rumeysa@rumeysayuk.net/O=DevTeam"
```
### sertifika oluşturup kullanıcı grupları -o ile verilir


**CertificateSigningRequest oluşturma**

```
$ cat <<EOF | kubectl apply -f -
apiVersion: certificates.k8s.io/v1
kind: CertificateSigningRequest
metadata:
  name: rumeysayuk
spec:
  groups:
  - system:authenticated
  request: $(cat rumeysayuk.csr | base64 | tr -d "\n")
  signerName: kubernetes.io/kube-apiserver-client
  usages:
  - client auth
EOF
```

**CSR onaylama ve crt'yi alma**

```
$ kubectl get csr

$ kubectl certificate approve rumeysayuk
** statusta nulunan sertificate alanını alamk için: **
$ kubectl get csr rumeysayuk -o jsonpath='{.status.certificate}' | base64 -d >> rumeysayuk.crt 
```


**kubectl config ayarları**

```
$ kubectl config set-credentials rumeysa@rumeysayuk.net --client-certificate=rumeysayuk.crt --client-key=rumeysayuk.key

$ kubectl config set-context rumeysayuk-context --cluster=minikube --user=rumeysa@rumeysayuk.net

$ kubectl config use-context rumeysayuk-context
```

# Kullanıcı ıluşturup 0 yetki ile içeri aldık bu aşamaya kadar kullanıcıyı(0 yetki varsayılan)

## authentication ve authorization aynı şey değil k8s için.


##