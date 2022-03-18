# 개요
* 같은 노드에 있는 파드간 통신

# 파드 배포
```sh
kubectl apply -f same_node.yaml
```

# 패킷 덤프
* **k8s-m노드**에서 각 파드에 연결된 calice 인터페이스 확인
```sh
# calice 
calicoctl get workloadendpoints
```

* **k8s-w1노드**에서 tcpdump
> tmux 사용 추천
```sh
# calice 인터페이스 tcpdump
tcpdump -i <client pod에 연결된 calice> -nn
tcpdump -i <server pod에 연결된 calice> -nn

# iptables tcpdump
watch iptables -v --numeric --table filter --list FORWARD | egrep '(cali-FORWARD|pkts)'
```
