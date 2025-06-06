# PSUP-CONFIG-SERVER

**PSUP-CONFIG-SERVER** — это сервер, который позволяет получить настройки для всех сервисов, отвечающих за бизнес логику,
входящих в кластер универсальной платформы по дистрибуции товаров. Конфигурационный сервер получает настойки из репозитория
который хранит конфигурации для каждого сервиса.

---

## 🛠️ Используемые технологии

| Технология                     | Назначение                                     |
|--------------------------------|------------------------------------------------|
| **Spring Cloud Config Server** | Запуск конфигурационного сервера               |
| **Spring Security**            | Защита конфигурационного сервера               |
| **Docker Mvn Plugin**          | Для создания образа в docker                   |

---

## 🧪 Профили конфигурации

| Профиль                 | Назначение                                         | База данных |
|-------------------------|----------------------------------------------------|-------------|
| `application.yaml`      | Локальный запуск без Docker                        | -           |
| `application-test.yaml` | Локальный запуск в Docker (`docker-compose-test`). | -           |

---

## 🗄️ Доступ к серверу (тестовая среда)

- **Пользователь**: `myUsername`
- **Пароль**: `mySecretPassword`

---

## 🚀 Запуск

### 🔹 Локально (без Docker)

```bash
./mvnw spring-boot:run
```

### 🔹 Локально (Docker) с профилем test
Для создания единой сети в docker
```bash
docker network create psup-test-net
```
Для очистки старых образов в docker:
```bash
docker image prune -f
```
Для сборки образа
```bash
mvn clean package -DskipTests docker:build
```
Для запуска контейнера
```bash
docker-compose -f docker-compose-test.yaml up --build
```

## 🔐 Шифрование и дешифрование конфигураций

### Шифрование
- Uri: http://localhost:8888/encrypt
- Method: Post 
- Content-Type: text/plain
- Body: mySecretText
- Authorization: Basic

### Дешифрование
- Uri: http://localhost:8888/decrypt
- Method: Post
- Content-Type: text/plain
- Body: 68ab666b42e5063082c7611c3f82c755d4991559df080d74facb52f7dc89d10c
- Authorization: Basic

---

## 🔄 Получение конфигурации
- Uri: http://localhost:8888/PRODUCT_SERVICE/test
- Method: GET
- Authorization: Basic

---

## 📝 Список сервисов c настройками
- EUREKA_SERVER
- PRODUCT_SERVICE

---

## 🛠️ Поддерживаемые профили
- test


