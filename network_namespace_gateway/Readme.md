# 개요
* 네트워크 네임스페이스와 외부통신 예제입니다.
> 유투브 링크: https://www.youtube.com/watch?v=_gZyN3tOggo

# 준비
* 네트워크 네임스페이스와 브릿지 연결이 구축이 완료되어 있어야 합니다.
> [구축 링크](../network_namespace_bridge/Readme.md)

# 네트워크 네임스페이스에서 구글서버로 통신시도
```sh
ip netns exec RED ping 8.8.8.8
ip netns exec BLUE ping 8.8.8.8
```

# 네트워크 네임스페이스 디폴트 게이트웨이 추가
```sh
ip netns exec RED ip route add default via 11.11.11.1
ip netns exec BLUE ip route add default via 11.11.11.1
```

# iptables 마스커레이드 설정
```sh
iptables -t nat -A POSTROUTING -s 11.11.11.0/24 -j MASQUERADE
```

# 네임스페이스에서 다시 구글서버로 ping통신
```sh
ip netns exec RED ping 8.8.8.8
ip netns exec BLUE ping 8.8.8.8
```

# 삭제
```sh
ip netns delete RED
ip netns delete BLUE
ip link delete br0
iptables -t nat -D POSTROUTING -s 11.11.11.0/24 -j MASQUERADE
```