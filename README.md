# Docker Practice — Практикалық жұмыс

## Жұмыстың мақсаты

Docker платформасымен жұмыс істеуді үйрену, контейнерлерді іске қосу, Dockerfile көмегімен жеке Docker образын құру және дайын образдарды Docker Hub платформасына жүктеу.

## 1-тапсырма. Nginx веб-серверін іске қосу

Бірінші тапсырмада Docker көмегімен Nginx веб-сервері іске қосылды.

Nginx — веб-сайттарды орналастыруға және пайдаланушыларға веб-беттерді көрсетуге арналған веб-сервер.

**Docker контейнерін іске қосу командасы:**

```bash
docker run -d --name my-nginx -p 8080:80 nginx:alpine
```

**Команданың түсіндірмесі:**

- `docker run` — жаңа контейнерді іске қосады.
- `-d` — контейнерді фондық режимде іске қосады.
- `--name my-nginx` — контейнердің атауын белгілейді.
- `-p 8080:80` — компьютердің 8080 портын контейнердің 80 портымен байланыстырады.
- `nginx:alpine` — қолданылатын Docker образы.

**Нәтиже:**

Nginx веб-сервері сәтті іске қосылды. Браузерде `http://localhost:8080` мекенжайы арқылы стандартты Nginx беті ашылды.

## 2-тапсырма. Redis деректер қорын іске қосу

Екінші тапсырмада Redis деректер қоры Docker контейнерінде іске қосылды.

Redis — ақпаратты кілт пен мән түрінде сақтауға арналған жылдам деректер қоры.

**Контейнерді іске қосу:**

```bash
docker run -d --name my-redis -p 6379:6379 redis:alpine
```

**Redis жүйесіне қосылу:**

```bash
docker exec -it my-redis redis-cli
```

**Деректерді сақтау:**

```text
SET student "Docker Student"
```

Нәтижесі:

```text
OK
```

**Сақталған деректерді тексеру:**

```text
GET student
```

Нәтижесі:

```text
"Docker Student"
```

**Қорытынды нәтиже:**

Redis контейнері сәтті іске қосылды. Деректерді сақтау және қайта оқу командалары дұрыс жұмыс істеді.

## 3-тапсырма. Жеке веб-сайт құру

Үшінші тапсырмада HTML және CSS технологиялары арқылы жеке веб-сайт жасалды.

Веб-сайтты Docker контейнерінде іске қосу үшін арнайы Dockerfile файлы құрылды.

**Жобаның файлдары:**

```text
custom-site/
├── Dockerfile
└── index.html
```

**Dockerfile мазмұны:**

```dockerfile
FROM nginx:alpine

COPY index.html /usr/share/nginx/html/index.html

EXPOSE 80
```

**Docker образын құрастыру:**

```bash
docker build -t my-custom-site:v1 ./custom-site
```

**Контейнерді іске қосу:**

```bash
docker run -d --name custom-site -p 8081:80 my-custom-site:v1
```

**Нәтиже:**

Жеке веб-сайт сәтті құрылды және Docker контейнерінде іске қосылды.

Сайт `http://localhost:8081` мекенжайы арқылы ашылады.

Веб-бетте «My Docker Project» тақырыбы және контейнердің жұмыс істеп тұрғанын көрсететін «Container Running» жазуы орналасқан.

## 4-тапсырма. Docker образдарын Docker Hub платформасына жүктеу

Төртінші тапсырмада Docker Hub платформасында жеке аккаунт құрылды.

Жасалған үш Docker образы Docker Hub репозиторийлеріне жүктелді.

**Docker Hub жүйесіне кіру:**

```bash
docker login
```

**Образдарға тег беру:**

```bash
docker tag nginx:alpine aldanazar/my-nginx:v1
docker tag redis:alpine aldanazar/my-redis:v1
docker tag my-custom-site:v1 aldanazar/my-custom-site:v1
```

**Образдарды Docker Hub жүйесіне жүктеу:**

```bash
docker push aldanazar/my-nginx:v1
docker push aldanazar/my-redis:v1
docker push aldanazar/my-custom-site:v1
```

**Docker Hub репозиторийлері:**

- [Nginx образы](https://hub.docker.com/r/aldanazar/my-nginx)
- [Redis образы](https://hub.docker.com/r/aldanazar/my-redis)
- [Жеке веб-сайт образы](https://hub.docker.com/r/aldanazar/my-custom-site)

Барлық образдар `v1` тегімен жарияланды.

## 5. Docker контейнерлерін тексеру

Жұмыс істеп тұрған контейнерлерді тексеру үшін келесі команда қолданылды:

```bash
docker ps
```

**Іске қосылған контейнерлер:**

| Контейнер атауы | Порт | Қызметі |
|---|---|---|
| my-nginx | 8080 | Nginx веб-сервері |
| my-redis | 6379 | Redis деректер қоры |
| custom-site | 8081 | Жеке веб-сайт |

## 6. Орындалған жұмыстың скриншоттары

### 6.1. Nginx веб-серверінің нәтижесі

![Nginx веб-сервері](screenshots/nginx.png)

### 6.2. Redis деректер қорының нәтижесі

![Redis деректер қоры](screenshots/redis.png)

### 6.3. Жеке веб-сайттың нәтижесі

![Жеке веб-сайт](screenshots/custom-site.png)

### 6.4. Docker Hub репозиторийлері

![Docker Hub](screenshots/docker-hub.png)

## Қорытынды

Практикалық жұмыс барысында Docker платформасының негізгі мүмкіндіктері зерттелді.

Жұмыс нәтижесінде:

1. Nginx веб-сервері Docker контейнерінде іске қосылды.
2. Redis деректер қоры орнатылып, оның жұмысы тексерілді.
3. HTML және CSS көмегімен жеке веб-сайт жасалып, Dockerfile арқылы Docker образы құрылды.
4. Үш Docker образы Docker Hub платформасына жүктелді.
5. Жобаның бастапқы кодтары мен Dockerfile файлдары GitHub репозиторийіне орналастырылды.

**Жалпы қорытынды:** Docker көмегімен қосымшаларды контейнерлерде іске қосу, жеке образдар құрастыру және оларды Docker Hub арқылы жариялау дағдылары меңгерілді.
