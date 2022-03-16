# 개요
* 네트워크 네임스페이스 예제입니다.

# 네트워크 네임스페이스 생성
```sh
# 네트워크 네임스페이스 생성
ip netns add RED
ip netns add BLUE

# veth를 네트워크네임스페이스에 연결
ip link add veth1 type veth peer name veth2
ip link set veth1 netns RED
ip link set veth2 netns BLUE

# ip할당
ip netns exec RED ip addr add 11.11.11.2/24 dev veth1
ip netns exec BLUE ip addr add 11.11.11.3/24 dev veth2

# 인터페이스 활성화
ip netns exec RED ip link set dev veth1 up
ip netns exec BLUE ip link set dev veth2 up

# 인터페이스 확인
ip netns exec RED ip -c -br addr show
ip netns exec BLUE ip -c -br addr show
```

# 네임스페이스간 ping통신
```sh
ip netns exec RED ping 11.11.11.3 -c 2
ip netns exec BLUE ping 11.11.11.2 -c 2
```

# 예제 삭제
```sh
ip netns del RED
ip netns del BLUE
```
