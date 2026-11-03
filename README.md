# Google OAuth2 login demo

Минимальное учебное Spring Boot приложение демонстрирует OAuth2
Authorization Code flow через Google. Главная страница открыта, а
`/profile` доступен только после входа.

## Настройка Google

В Google Cloud Console нужно создать OAuth Client ID типа **Web application**
и добавить redirect URI:

```text
http://localhost:8080/login/oauth2/code/google
```

Затем передать credentials через окружение:

```bash
export GOOGLE_CLIENT_ID='your-client-id'
export GOOGLE_CLIENT_SECRET='your-client-secret'
mvn spring-boot:run
```

Без обеих переменных приложение не запустится. Client secret нельзя
хранить в Git, `application.yml` или скачанном Google JSON внутри
проекта.

## Сценарий

1. Открыть <http://localhost:8080>.
2. Нажать **Login with Google**.
3. Spring Security создаёт authorization request и перенаправляет браузер в Google.
4. Google возвращает одноразовый authorization code на callback URI.
5. Spring Security обменивает code на access token по server-to-server каналу.
6. После успешного входа открывается `/profile` с именем и email.
