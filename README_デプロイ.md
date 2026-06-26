# プロトタイプを外部公開する手順

このプロトタイプは**クライアント側だけで動く静的HTML**です。バックエンド（サーバ）は不要で、
静的ホスティングに `index.html` を置くだけで、外部から開いて操作できます。
※ 実患者データを扱う本番サーバは Track D（コンプラ承認）後の別物。これは合成データのレビュー用。

## 同梱ファイル
- `index.html` … プロトタイプ本体（検索除け `noindex` 付き）
- `robots.txt` … クローラ拒否

---

## 方法A：すぐ・単発（アカウント不要）
1. **Netlify Drop**（https://app.netlify.com/drop）を開く
2. `index.html` を含むフォルダをドラッグ&ドロップ
3. 発行されたURLを大上に共有

→ 数十秒で公開。手早く見せたいとき向き。

## 方法B：反復前提（おすすめ・dev向け）
GitリポジトリにこのフォルダをコミットしてPages系に連携 → push で自動更新。
- **Cloudflare Pages** / **Vercel** / **GitHub Pages** のいずれか
- 例（Vercel CLI）：`npm i -g vercel` → フォルダで `vercel`
- 例（GitHub Pages）：リポジトリ Settings → Pages → ブランチ公開

→ 更新のたびにURLが最新化。Claude Code での反復と相性が良い。

## 方法C：PCから一時的に見せる（その場限り）
PCを起動している間だけ公開：
```
npx serve .                 # ローカルで配信（例: http://localhost:3000）
npx cloudflared tunnel --url http://localhost:3000   # 一時公開URLを発行
```
→ デモのときだけ。PCを閉じると消える。

---

## 社外秘・アクセス制限（重要）
- 合成データのみだが、本プロジェクトは**社外秘**。**仕様書（要件定義書）等は公開URLに置かない**。
- 公開する場合は **推測されないURL** ＋ **noindex（同梱済み）**。可能なら**パスワード保護**：
  - Cloudflare Pages＋**Cloudflare Access**（無料枠あり）
  - Vercel の Password Protection（Proプラン）
  - Netlify の Password protection（有料プラン）
- 大上（社内）には**ファイル直送**でも十分。リンクが要るときだけ上記で。
