# S3 MCP

## 概要

AWS S3ストレージ連携を提供するModel Context Protocol。

## ステータス

🚧 **プレースホルダー** - 実装予定

## 予定機能

- オブジェクトアップロード/ダウンロード
- バケット操作
- 署名付きURL生成

## 設定例（予定）

```json
{
  "name": "s3",
  "type": "mcp",
  "config": {
    "region": "${AWS_REGION}",
    "bucket": "${S3_BUCKET}",
    "access_key_id": "${AWS_ACCESS_KEY_ID}",
    "secret_access_key": "${AWS_SECRET_ACCESS_KEY}"
  }
}
```
