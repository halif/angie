# Angie mTLS – Ansible role

Устанавливает веб‑сервер **Angie** на Ubuntu 22.04, настраивает репозиторий,
конфигурирует взаимную аутентификацию TLS (mTLS) для сколь угодно
публикаций 1С и опционально разворачивает обычные HTTP‑прокси‑хосты.

## Возможности
* Добавляет APT‑репозиторий `download.angie.software` и ключ
* Устанавливает пакет `angie`, включает и перезапускает сервис
* Разворачивает корневой CA для проверки клиентских сертификатов
* Генерирует по переменной **`angie_mtls_sites`** любое кол‑во `server {}` на 443
* Поддерживает ACME (Let’s Encrypt) с авто‑продлением
* Создаёт файл `extra_servers_acme.conf` с HTTP‑проксями для acme из **`angie_extra_servers_acme`**

## Быстрый пример
```yaml
- hosts: proxy
  become: true
  roles:
    - role: angie_mtls
      vars:
        angie_mtls_sites:
          - domain: erp.example.com
            backend: "http://10.10.0.11:8080/erp/"
          - domain: crm.example.com
            locations:
              - path: /sales/
                proxy_pass: "http://10.10.0.12:8080/sales/"
              - path: /support/
                proxy_pass: "http://10.10.0.13:8080/support/"

        angie_extra_servers_acme:
          - listen: 80
            server_name: mail.example.com
            proxy_pass: "http://10.229.32.20/"
