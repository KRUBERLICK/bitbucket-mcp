# Налаштування локального MCP-сервера bitbucket

В корені проекту Tvorra тепер закомічена директорія `bitbucket-mcp`, що містить вихідні файли mcp-сервера. Для налаштування роботи даного сервера у claude code, необхідно виконати наступне:
1. У директорії `bitbucket-mcp` виконати команду `npm install`.
2. Далі за посиланням https://id.atlassian.com/manage-profile/security/api-tokens сформувати власний API token з наступними скоупами: `read:user:bitbucket`, `read:repository:bitbucket`, `read:pullrequest:bitbucket`, `write:pullrequest:bitbucket`, `read:pipeline:bitbucket`.
3. Після цього даний токен необхідно додати у власний MacOS-кічейн, за допомогою наступної команди в терміналі: `security add-generic-password -a "$USER" -s "bitbucket-mcp" -w "YOUR_API_TOKEN"`, замінивши `YOUR_API_TOKEN` на згенерований токен.
4. Далі необхідно створити або відредагувати вже існуючий файл `~/.zshrc`, додавши наступний код, замінивши `your.email@gen.tech` на ваш актуальний, який ви використовуєте для логіну в бітбакет:
```bash
export BITBUCKET_USERNAME="your.email@gen.tech"
export BITBUCKET_PASSWORD=$(security find-generic-password -a "$USER" -s "bitbucket-mcp" -w 2>/dev/null)
```
5. Після цього рекомендую повністю перезапустити додаток терміналу або iTerm.
6. Далі при запуску `claude` всередині директорії проекту, перевірити статус mcp-сервера командою `/mcp`, у списку має бути `bitbucket` зі статусом `connected`.
