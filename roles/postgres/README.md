# Роль postgres

Ставит PostgreSQL 16 из репозиториев убунты, кластер в своем каталоге, своя systemd служба `postgres`, плюс postgres_exporter (служба `postgres-exporter`).

## Переменные

| переменная | по умолчанию | что это |
|---|---|---|
| `postgres__data_dir` | `/data/postgres/data` | каталог данных (PGDATA) |
| `postgres__opts` | listen_addresses, port, max_connections | словарь параметров для postgresql.conf, строки в одинарных кавычках |
| `postgres__hba` | local peer + host scram на localhost | список правил pg_hba.conf (type, database, user, address, method) |
| `postgres__users` | `[]` | список пользователей (name, password) |
| `postgres__databases` | `[]` | список баз (name, owner) |
| `postgres__exporter_version` | `0.16.0` | версия postgres_exporter |
| `postgres__exporter_user` | `postgres_exporter` | пользователь для экспортера (в ОС и в бд, роль pg_monitor) |
| `postgres__exporter_password` | `""` | пароль экспортера, лучше через vault |
| `postgres__exporter_port` | `9187` | порт метрик |

## Пример

```yaml
- hosts: vm1
  become: true
  vars:
    postgres__users:
      - name: app_user
        password: "{{ vault_app_password }}"
    postgres__databases:
      - name: app_db
        owner: app_user
    postgres__exporter_password: "{{ vault_exporter_password }}"
  roles:
    - postgres
```

Нужна коллекция community.postgresql (`ansible-galaxy collection install -r requirements.yml`).
