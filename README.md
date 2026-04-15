# react-sbom-github-actions

React + TypeScript + Vite のサンプルアプリに対して、GitHub Actions で 2 種類の SBOM を生成するリポジトリです。

- SPDX SBOM（`sbom-tool`）
- CycloneDX SBOM（`cyclonedx-npm`）

## 前提

- Node.js `22.x`（Vite 8 の要件を満たすため）
- npm

## ローカル実行

```bash
npm ci
npm run dev
```

### 利用可能なスクリプト

- `npm run dev`: 開発サーバー起動
- `npm run build`: TypeScript ビルド + Vite ビルド
- `npm run lint`: ESLint 実行
- `npm run preview`: ビルド成果物のプレビュー

## GitHub Actions

ワークフロー: `.github/workflows/build-and-sbom.yml`

### トリガー

- `push`（全ブランチ）
- `workflow_dispatch`（手動実行）

### 実行内容

1. アプリをビルド（`npm ci` / `npm run build`）
2. ビルド成果物 `dist/` を Artifact としてアップロード
3. SPDX SBOM を生成・zip 化して Artifact としてアップロード
4. CycloneDX SBOM を生成・zip 化して Artifact としてアップロード

### 生成される主な Artifact 名

- `react-app-build`
- `react-sbom-github-actions-spdx-sbom`
- `react-sbom-github-actions-cyclonedx-sbom`

## 脆弱性バージョン検証用ブランチ

`axios` の脆弱性バージョン指定を含む検証用ブランチとして、以下を用意しています。

- `security/axios-vulnerable-version`
