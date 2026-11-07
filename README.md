# メトロノーム・ジャンプ・トレーニング（GitHub Pages版）

## ファイル
- `index.html`：元アプリをベースに、メール/パスワード認証とFirestore同期を組み込んだ版
- `assets/IMG_3589.PNG`：キャラクター初期画像
- `assets/IMG_3591.PNG`：背景初期画像
- `firestore.rules`：UIDごとのアクセス制御

## 今回の構成（Sparkプランを維持）
Firebase Storageは使用しません。2026年2月3日以降、Cloud Storage for FirebaseはBlazeプランが必要です。画像は最適化してFirestoreの画像専用ドキュメントに1枚ずつ保存します。Firestoreの1ドキュメント上限を超えないよう、画像データのサイズを制限しています。

## Firebase側で必要な設定
1. Authentication > ログイン方法で「メール/パスワード」を有効化（設定済み）
2. Cloud Firestoreを作成（大阪 `asia-northeast2`、作成済み）
3. Firestore > ルール に `firestore.rules` の内容を貼り付けて「公開」
4. Authentication > Settings > 承認済みドメインに、公開後の `ユーザー名.github.io` を追加

## GitHub Pages
1. GitHubで新しいリポジトリを作成
2. このフォルダ内の `index.html`、`firestore.rules`、`assets` フォルダをリポジトリ直下へアップロード
3. Settings > Pages > Deploy from a branch > `main` / `/(root)` を選択
4. 公開URLを開き、アカウントを新規作成してログイン

## 注意
- Firebase Web APIキーはWebアプリ用の公開設定値です。Google Cloud ConsoleでHTTPリファラー制限とAPI制限を設定してください。
- Gemini APIキーはブラウザ側で入力する方式です。公開利用する場合はAPIキーをHTTPリファラー制限し、利用量を監視してください。機密性が必要ならサーバー側プロキシが必要です。
- カメラはHTTPSで動作します。GitHub PagesはHTTPSです。ブラウザのカメラ利用許可が必要です。
- Firestoreには無料枠・利用上限があります。多数の画像や大量の利用があると制限・課金条件に影響する可能性があるため、Firebaseの利用状況を確認してください。
- Firestoreルールは本人のUID配下だけを許可します。全員許可やテストモードのルールは使わないでください。
- 実際のFirebaseプロジェクトで、登録・ログイン・画像保存・別端末同期を必ず確認してください。
