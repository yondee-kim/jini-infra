## 인프라 실행 (Database)

두 서비스는 각자 독립된 PostgreSQL을 사용합니다 (Database per Service).
`docker-compose.yml`로 두 DB 컨테이너를 함께 띄웁니다.

| 서비스 | 컨테이너 | DB | 호스트 포트 |
|--------|----------|-----|------------|
| jini-auth | jini-postgres-auth | auth_db | 5432 |
| jini-chat | jini-postgres-chat | chat_db | 5433 |

### 실행

```bash
docker compose up -d      # 두 DB 컨테이너 백그라운드 실행
docker compose ps         # 상태 확인 (둘 다 healthy 여야 함)
```

### 종료

```bash
docker compose down       # 컨테이너 중지 및 제거 (데이터는 볼륨에 유지)
docker compose down -v    # 볼륨까지 삭제 (DB 데이터 완전 초기화)
```

> 두 DB는 볼륨(`pgdata-auth`, `pgdata-chat`)이 분리되어 있어
> 데이터가 섞이지 않습니다.