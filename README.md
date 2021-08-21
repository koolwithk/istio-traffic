# istio-traffic


### Deploy apps

```
kubectl create ns istio-test
kubectl annotate ns istio-test linkerd.io/inject=enabled

#install flagger
https://docs.flagger.app/tutorials/istio-progressive-delivery
kubectl apply -k github.com/fluxcd/flagger//kustomize/istio

#deploy
kubectl apply -f appv1.yml -n istio-test
kubectl apply -f canary-flagger.yml -n istio-test

```

## How to see the canary status?
```
#update the image name to see the new rollout status
kubectl -n istio-test set image deployment/appv1 appv1=httpd  #or nginx

#status
kubectl -n istio-test get ev --watch

watch kubectl -n istio-test get canary


## Reference :

1. https://docs.flagger.app/tutorials/istio-progressive-delivery