# Налаштування локального MCP-сервера bitbucket

1. Зклонувати даний репозиторій.
2. В руті проекту додати файл `.mcp.json`, якщо його ще не існує, з наступним контентом, замінивши `PATH_TO_MCP_ROOT` на АБСОЛЮТНИЙ ШЛЯХ зклонованого репозиторію (приклад `/Users/username/Documents/work/bitbucket-mcp/dist/index.js`):
```json
{
  "mcpServers": {
    "bitbucket": {
      "command": "node",
      "args": [
        "/Users/kruberlick/Documents/work/bitbucket-mcp/dist/index.js"
      ],
      "env": {
        "BITBUCKET_URL": "https://api.bitbucket.org/2.0",
        "BITBUCKET_WORKSPACE": "funplace",
        "BITBUCKET_ENABLE_DANGEROUS": "true"
      }
    }
  }
}
```
1. У зклонованій директорії `bitbucket-mcp` виконати команду `npm install && npm run build`.
2. Далі за посиланням https://id.atlassian.com/manage-profile/security/api-tokens сформувати власний API token з наступними скоупами: `read:user:bitbucket`, `read:repository:bitbucket`, `read:pullrequest:bitbucket`, `write:pullrequest:bitbucket`, `read:pipeline:bitbucket`.
3. Після цього даний токен разом з вашим юзернеймом необхідно додати у власний MacOS-кічейн, за допомогою наступних команд в терміналі, замінивши `YOUR_EMAIL` та `API_TOKEN` на ваші значення:
```bash
security add-generic-password -a "$USER" -s "bitbucket-mcp-username" -w "YOUR_EMAIL"
security add-generic-password -a "$USER" -s "bitbucket-mcp-password" -w "API_TOKEN"
```
5. Потім рекомендую повністю перезапустити додаток терміналу або iTerm.
6. Далі при запуску `claude` всередині директорії проекту, перевірити статус mcp-сервера командою `/mcp`, у списку має бути `bitbucket` зі статусом `connected`.

Для підключення mcp-сервера до інших проектів - просто скопіюйте файл `.mcp.json` у рут відповідного проекту та перезапустіть `claude`.

## Приклади запитів

Запит на виконання код-ревʼю вказаного PR:
```
Perform a comprehensive code review for PR #666, following the guidelines and style guides of the project, adding necesary comments in the corresponding places, highlighting possible issues or suggestions. Use real code suggestions in the comments when applicable. Then request changes if there are any issues or possible improvements that need to be addressed by the author.
```

Запит на аналіз коментарів до вказаного PR та виконання запропонованих змін:
```
Check the added comments to PR #666 and analyse their proposals. Identify the ones that make good point, indicating real issues or improvements that can be done. Plan the corresponding updates in the project.
```

Запит на закриття усіх відкритих до вказаного PR коментарів та апрув PR:
```
Resolve all my comments to PR #666 and approve the PR.
```
