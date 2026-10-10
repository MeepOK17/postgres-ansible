# ДЗ: ansible роль для PostgreSQL

- роль: `roles/postgres`
- плейбук: `postgres.play.yml`
- инвентарь: `inventories/main`
- пароли лежат в `inventories/main/group_vars/all/vault.yml` (ansible-vault)

Запуск:

```bash
ansible-galaxy collection install -r requirements.yml
ansible-playbook postgres.play.yml
```

Пароль от vault кладется в файл `vault-pass` (он в .gitignore).
