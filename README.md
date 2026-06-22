# OpenCode
- https://zenn.dev/merume/articles/39240f2432eb49
- https://note.com/safe_shark6918/n/n6545700ac685
- https://zenn.dev/yanasan/articles/9e3c5473206a27
## インストール
- WSL
- Ollama
- OpenCode
### OpenCode起動
- OpenCodeインストール
```
curl -fsSL https://opencode.ai/install | bash
```
### サーバー起動
- サーバー
```
ollama serve
```
- モデル取得
```
ollama pull gemma4:e2b
```
- IP確認
```
WINDOWS_IP=$(ip route show | grep -i default | awk '{ print $3}')
echo "Windows IP: ${WINDOWS_IP}"
```

### opencode.json作成
```
{
  "$schema": "https://opencode.ai/config.json",

  "provider": {
    "ollama": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "Ollama (Windows)",

      "options": {
        "baseURL": "http://<WINDOWS_IP>:11434/v1"
      },

      "models": {
        "qwen2.5-coder:7b": {
          "name": "Qwen2.5 Coder 7B",
          "limit": {
            "context": 32768,
            "output": 4096
          }
        }
      }
    }
  },

  "model": "ollama/qwen2.5-coder:7b",
  "small_model": "ollama/qwen2.5-coder:7b"
}
```
### Ollama APIにアクセス確認
```
curl http://${WINDOWS_IP}:11434/v1/models
```
### OpenCode起動
```
opencode
```
- 起動後に"/models"コマンドでモデル選択
