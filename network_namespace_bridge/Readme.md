# 개요
* 네트워크 네임스페이스를 가상 브릿지에 연결하는 예제입니다.
> 유투브 링크: https://youtu.be/iWVSZa8RnZc

# 가상 브릿지 생성
```sh
# 생성
ip link add br0 type bridge
ip addr add 11.11.11.1/24 dev br0

# 확인
brctl show
```

# 네트워크 네임스페이스 생성
```sh
# 네트워크 네임스페이스 생성
ip netns add RED
ip netns add BLUE

# 확인
ip netns ls
```

# 인터페이스 생성과 브릿지 연결
```sh
ip link add veth1 type veth peer name veth2
ip link add veth3 type veth peer name veth4
ip link set veth1 netns RED
ip link set veth3 netns BLUE
ip link set veth2 master br0
ip link set veth4 master br0

# IP할당
ip netns exec RED ip addr add 11.11.11.2/24 dev veth1
ip netns exec BLUE ip addr add 11.11.11.3/24 dev veth3

# 인터페이스 활성화
ip link set br0 up
ip link set veth2 up
ip link set veth4 up
ip netns exec RED ip link set dev veth1 up
ip netns exec BLUE ip link set dev veth3 up
```

# 네임스페이스간 ping통신
* iptables forward설정이 되지 않아서 실패합니다.
```sh
ip netns exec RED ping 11.11.11.3 -c 2
ip netns exec BLUE ping 11.11.11.2 -c 2
```

# iptables forward설정
```sh
iptables --policy FORWARD ACCEPT
echo 1 > /proc/sys/net/ipv4/ip_forward
```

# 네임스페이스간 다시 ping통신
```sh
ip netns exec RED ping 11.11.11.3 -c 2
ip netns exec BLUE ping 11.11.11.2 -c 2
```

# 삭제
```sh
ip netns delete RED
ip netns delete BLUE
ip link delete br0
```