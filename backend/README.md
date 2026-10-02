# DOCKER Commands

```
FROM eclipse-temurin:21-jdk-alpine AS build
WORKDIR /usr/src
COPY Main.java .
RUN javac Main.java


FROM eclipse-temurin:21-jre-alpine
WORKDIR /usr/src
COPY --from=build /usr/src/Main.class .
CMD ["java", "Main"]

```

```cmd
docker build -t eugene/tp1-backend .
```

```cmd
docker run --name tp1backend eugene/tp1-backend
```

```cmd
docker start -a tp1backend
```

<br>
<br>

## API

```cmd
docker build -t eugene/tp1-backend-api .
```

```cmd
docker run --name tp1-backend-api --network tp1network -p"8080:8080" eugene/tp1-backend-api
```
