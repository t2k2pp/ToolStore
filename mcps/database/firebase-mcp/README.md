# Firebase MCP

## 概要

Firebase サービス連携を提供するModel Context Protocol。

## ステータス

🚧 **プレースホルダー** - 実装予定

## 予定機能

- Firestore CRUD操作
- Authentication連携
- Cloud Functions呼び出し
- Cloud Storage操作

## 設定例（予定）

```json
{
  "name": "firebase",
  "type": "mcp",
  "config": {
    "project_id": "${FIREBASE_PROJECT_ID}",
    "credentials": "${FIREBASE_CREDENTIALS_PATH}"
  }
}
```

## 参考

- [Firebase公式](https://firebase.google.com/)
