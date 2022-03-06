* 같은 노드 pod간통신
```sh
# calice-server pod ip확인
kubectl get po -o wide
# client -> server ping
kubectl exec -it calice-client -- ping -c <calice-server ip>
```
