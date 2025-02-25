## Runtime
Приложение отвечает по 3 эндпоинтам:  
* /health - 200 ok
* /metrics - в формате метрик для prometheus, включая счётчик запросов в основной эндпоинт `my-container_http_requests_total`
* / - основной эндпоинт, возвращающий часть запроса и генерирующий строчку лога.

## Как работать с приложением без docker:  
1. Установить golang 1.16
2. Установить зависимости:

   ```shell
   go mod download
   ```

3. Запустить тесты:
   ```shell
   go test -v ./...
   ```
4. Собрать приложение:
   ```
   GO111MODULE=on go build -o app cmd/server/app.go
   ```
5. Запустить его:
   ```shell
   ./app
   ```

## Как работать с приложением в docker:  
1. Установить docker
2. Запустить тесты
   ```shell
   ./run-tests.sh
   ```
3. Собрать:
   ```shell
   docker-compose build
   ```
   or
   ```shell
   docker build . -t my-container/app
   ```
4. Запустить:
   ```shell
   docker-compose up
   ```
   or
   ```shell
   docker run -p8080:8080 my-container/app
   ```
