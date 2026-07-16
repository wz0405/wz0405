# 한현희 · Backend Engineer

결제 시스템 백엔드 — PG 승인 · 선불 · CDC 파이프라인.
**정합성과 대용량 트래픽이 충돌하는 지점을 설계로 푸는 일**을 해왔습니다.

## 해온 일

**PG 결제 승인** — 신용카드부터 오픈뱅킹까지 7개 결제수단의 승인 흐름을 설계·개발하고 운영까지 담당했습니다. 동기 승인되는 카드, 입금 통지를 기다리는 가상계좌, 빌키 기반 정기결제처럼 수단마다 승인·취소·대사 구조가 달라 각 특성에 맞춰 흐름을 설계했고, 2차 PG·VAN·금결원과 카카오·네이버·위챗 등 국내외 제휴사 연동을 두루 경험했습니다.

**선불 시스템** — 레거시 모듈을 인수받으며 시작했습니다. 그대로 쓰기 어렵다고 판단해 머니·포인트형·상품권형 세 가지 모델을 전면 재설계했고, 초기 아키텍처와 핵심 구현을 직접 만든 뒤 구현 태스크를 팀원에게 분배·리드하며 운영까지 책임졌습니다. 잔액이 걸린 시스템인 만큼 다층 정책 검증, 거래 원자성, 오류 시 롤백을 설계의 중심에 뒀고, 선불업 보안심사 대응까지 마쳤습니다.

**CDC 데이터 동기화** — 5분 주기 배치 동기화를 실시간 CDC로 전환했습니다. 같은 망은 Kafka+Debezium 파이프라인으로, Debezium을 둘 수 없는 망분리 구간은 BinLog 수신부터 송수신 커넥터까지 자체 구현해 1년 이상 무중단 운영했습니다. RDS 업데이트로 binlog 오프셋이 유실되는 장애를 겪은 뒤 GTID 기반 추적으로 바꿔 같은 장애가 재발할 수 없는 구조로 만들었습니다.

**자사 서비스** — 메시지 발송 플랫폼과 B2C 주문 시스템 백엔드를 처음부터 설계해 수년간 직접 운영하고 있습니다. 현재는 레거시 PG 솔루션 전체를 일관된 설계 원칙으로 재구성하는 프로젝트를 리딩하고 있습니다. 공통 설계 가이드를 정립해 팀이 같은 원칙으로 이관하게 하고, 승인 중심이던 담당 영역을 기본정보·매입·입금·정산 도메인까지 넓혀가는 중입니다. AS-IS/TO-BE 대조 하네스와 다중 에이전트 병렬 검수 등 AI 워크플로우를 검증 중심으로 설계해, 사람이 검수 병목이 되지 않는 이관 프로세스를 정착시켰습니다.

## 저장소

실무에서 다룬 구조를 학습·시연용으로 재작성한 샘플과 개인 프로젝트입니다. 사내 코드·식별 데이터는 포함하지 않습니다.

| 레포 | 내용 |
|---|---|
| [messageTransServer](https://github.com/wz0405/messageTransServer) | Virtual Thread + Semaphore 격리 스케줄러 기반 대량 메시지 발송 (JDK 21) |
| [debeziumCdcPipeline](https://github.com/wz0405/debeziumCdcPipeline) | Kafka + Debezium CDC — binlog→GTID 전환, 운영·트러블슈팅 문서 포함 |
| [mysqlBinLogCdc](https://github.com/wz0405/mysqlBinLogCdc) | Debezium 없이 BinaryLogClient로 직접 구현한 애플리케이션 레벨 CDC |
| [nettyMigrationAPI](https://github.com/wz0405/nettyMigrationAPI) | Servlet → Netty 이벤트 루프 전환, 처리량·운영 트레이드오프 검증 |
| [dynamicQueryDSL](https://github.com/wz0405/dynamicQueryDSL) | MyBatis 동적 쿼리를 대체하는 타입세이프 빌더 + EXPLAIN 자동 검증 |
| [ticketingFlow](https://github.com/wz0405/ticketingFlow) | 대기열 기반 티켓 예매 — Redis ZSET·Lua 원자 처리·Streams write-behind, k6 오버셀 불변식 검증 (개인 프로젝트, 운영 중) |

## 일하는 방식

- 성능 문제는 계측에서 시작합니다 — EXPLAIN 기반 쿼리 개선, 부하테스트, 불변식 검증
- 장애를 겪으면 같은 장애가 다시 올 수 없는 구조로 바꿔둡니다
- 새 기술의 도입과 보류를 모두 근거로 결정합니다

<sub>Java 21 · Spring Boot · MyBatis · Redis · Kafka · Debezium · MySQL · Netty · AWS</sub>
