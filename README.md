# Налаштування локального MCP-сервера bitbucket

1. Зклонувати даний репозиторій собі на девайс.
2. В руті проекту додати файл `.mcp.json`, якщо його ще не існує, з наступним контентом, замінивши `PATH_TO_MCP_REPO` на реальне розташування зклонованого репозиторію:
```json
{
  "mcpServers": {
    "bitbucket": {
      "command": "node",
      "args": [
        "PATH_TO_MCP_REPO"
      ],
      "env": {
        "BITBUCKET_URL": "https://api.bitbucket.org/2.0",
        "BITBUCKET_WORKSPACE": "funplace",
        "BITBUCKET_USERNAME": "${BITBUCKET_USERNAME}",
        "BITBUCKET_PASSWORD": "${BITBUCKET_PASSWORD}"
      }
    }
  }
}
```
1. У зклонованій директорії `bitbucket-mcp` виконати команду `npm install`.
2. Далі за посиланням https://id.atlassian.com/manage-profile/security/api-tokens сформувати власний API token з наступними скоупами: `read:user:bitbucket`, `read:repository:bitbucket`, `read:pullrequest:bitbucket`, `write:pullrequest:bitbucket`, `read:pipeline:bitbucket`.
3. Після цього даний токен необхідно додати у власний MacOS-кічейн, за допомогою наступної команди в терміналі: `security add-generic-password -a "$USER" -s "bitbucket-mcp" -w "YOUR_API_TOKEN"`, замінивши `YOUR_API_TOKEN` на згенерований токен.
5. Потім рекомендую повністю перезапустити додаток терміналу або iTerm.
6. Далі при запуску `claude` всередині директорії проекту, перевірити статус mcp-сервера командою `/mcp`, у списку має бути `bitbucket` зі статусом `connected`.
