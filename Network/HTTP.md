# HTTP

## HTTP 1.0
- RTT 증가 : 각 요청마다 새로운 TCP 연결을 맺어야 하므로 왕복 지연(Round Trip Time)이 증가
- 비효율적 자원 사용 : 단일 요청/응답 후 연결 종료.
## HTTP 1.1
- HOL Blocking : 한 연결 내에서 요청이 직렬로 처리되어, 앞선 요청이 느리면 뒤 요청이 대기(Head-of-Line Blocking)
- 무거운 헤더구조 : HTTP 헤더가 반복적으로 전송되어 오버헤드 발생

## HTTP /2
- 멀티 플렉싱 : 한 연결에서 여러 요청/응답을 병렬로 처리하여 HOL Blocking 문제 해소
- 헤더 압축 : HPACK을 이용해 헤더 크기 감소
- 서버 푸시 : 클라이언트 요청 전에 서버가 리소스 미리 전송

## HTTPS
- SSL/TLS 암호화: HTTP에 SSL/TLS 보안 계층을 추가해 데이터 암호화 및 인증 제공
-  보안 강화: 데이터 변조 방지, 신원 인증, 피싱 방지 등

## HTTPS /3
- UDP 기반(QUIC): TCP 대신 UDP 사용으로 연결 지연 감소 및 패킷 손실에 강함
- HOL Blocking 해소: TCP의 HOL Blocking 문제를 해결해 더 빠른 전송
- 0-RTT Resumption: 이전 연결 정보를 활용해 빠른 재연결 가능
- 강화된 보안: 더 많은 연결 정보를 암호화
