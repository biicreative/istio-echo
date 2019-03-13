## Setup

`kubectl apply -f <(istioctl kube-inject -f echo.yaml)`

`kubectl apply -f echo-gateway.yaml`

`kubectl apply -f echo-virtualservice.yaml`

`curl http://$INGRESSGATEWAY:31380/echo -s -o /dev/null -w "%{http_code}\n"`

## Add JWT Authentication

`kubectl apply -f echo-policy.yaml`

```
TOKEN=$(curl https://raw.githubusercontent.com/istio/istio/release-1.0/security/tools/jwt/samples/demo.jwt -s)

curl --header "Authorization: Bearer $TOKEN" http://$INGRESSGATEWAY:31380/echo -s -o /dev/null -w "%{http_code}\n"
```
