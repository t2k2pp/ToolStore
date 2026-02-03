# OpenAI MCP

## 概要

OpenAI API連携を提供するModel Context Protocol。

## ステータス

🚧 **プレースホルダー** - 実装予定

## 予定機能

- Chat Completions
- Embeddings生成
- 画像生成（DALL-E）
- Audio Transcription（Whisper）

## 設定例（予定）

```json
{
  "name": "openai",
  "type": "mcp",
  "config": {
    "api_key": "${OPENAI_API_KEY}",
    "organization": "${OPENAI_ORG_ID}",
    "default_model": "gpt-4-turbo"
  }
}
```

## 参考

- [OpenAI公式](https://openai.com/)
- [OpenAI API Docs](https://platform.openai.com/docs/)
