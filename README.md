# zmk-config-nickey

分割40%ワイヤレス自作キーボード **「Nickey44」** のZMK Firmware設定リポジトリです。

---

## 🛒 販売 & 関連記事

* 🛍️ **BOOTH (購入ページ):** [Nickey44 - BOOTH](https://booth.pm/ja/items/8178906)
* 🛠️ **ビルドガイド:** [Nickey44 ビルドガイド](https://nixdesire.com/nickey-buildguide-2/)
* 📝 **開発記 (なぜ44キーなのか):** [「Nickey44」を設計した理由。理想の44キーと40%レイアウトの最適解を求めた開発記](https://nixdesire.com/nickey44-review/)
* 📖 **紹介記事 (詳細解説):** [デスクの上を、最も美しく。パームレスト不要の極薄設計と完全ワイヤレスが融合した分割40%自作キーボード『Nickey44』](https://nixdesire.com/nickey44-introduction/)

---

## 現在のキーマップ

![Nickey44 Keymap](keymap-drawer/nickey.svg)

---

## ⌨️ キーマップの変更方法 (Keymap Editor)

Web GUIツール **[Keymap Editor](https://nickcoutsos.github.io/keymap-editor/)** を使うと、コードを直接編集せずにブラウザ上で直感的にキーマップを変更できます。

### 1. 事前準備 (リポジトリのForkと権限設定)

1. 本リポジトリを自身のGitHubアカウントに **Fork** します。
2. Forkしたご自身のリポジトリの **Actions** タブを開き、**「I understand my workflows, go ahead and enable them」** ボタンを押してGitHub Actionsを有効化しておきます。（※初回のみ必要）
3. ブラウザで [Keymap Editor](https://nickcoutsos.github.io/keymap-editor/) にアクセスし、GitHubアカウントでログイン（連携）します。
4. 初回はリポジトリが表示されないため、画面左上の **Repository** プルダウンから **「add/remove repositories...」** を選択します。
5. **Repository access** 欄で **Select repositories** を選択し、Forkした `zmk-config-nickey` を指定して **Save** を押します。
6. Keymap Editorのページを更新（リロード）すると、**Repository** のプルダウンから `zmk-config-nickey` が選択できるようになります。

---

### 2. キーマップの編集と保存

1. **Repository** から `zmk-config-nickey` を選択します。
2. 画面上でキー配置やレイヤーをお好みに合わせて変更します。
3. 編集が完了したら、右上の **Save** ボタンを押します。
4. コミットメッセージ（変更内容のメモ）を入力し、**Commit** ボタンを押します。
   - これによりGitHub上のリポジトリへ自動で反映され、GitHub Actionsによるファームウェアの自動ビルドが開始されます。

> 💡 **コードを直接編集する場合:**  
> リポジトリ内の `config/nickey.keymap` を直接編集して Commit / Push することでも変更可能です。

---

## 🛠️ ファームウェアのビルドと書き込み方法 (Flashing)

### 1. ビルド済みファイルの入手

Keymap Editor での変更を Commit（または `main` ブランチへ Push）すると、**GitHub Actions** によって自動的にファームウェアがビルドされます。

1. リポジトリの **Actions** タブを開きます。
2. 一番上の最新のワークフロー（緑のチェックマークがついたもの）をクリックします。
3. ページ下部の **Artifacts** から `firmware`（または `firmware.zip`）をダウンロードして解凍します。

解凍すると、以下の `.uf2` ファイルが入っています。
* `nickey_l.uf2` （左手用）
* `nickey_r.uf2` （右手用）
* `settings_reset.uf2` （設定リセット用）

> 💡 **出荷時（デフォルト）ファームウェアについて:**  
> BOOTH等で販売している完成品向けの書き込み済みファームウェアは、本リポジトリの [`firmware`](firmware/) フォルダにバージョン別で格納しています。新規セットアップや通常の更新には、ZMK v0.4.0（Zephyr 4.1.0ベース）の最新版 [`v2.0.0`](firmware/v2.0.0/) を使用してください。左右には必ず同じバージョンのファームウェアを書き込んでください。

---

### 2. キーボードへの書き込み手順

1. **MCUをPCに接続:**
   - 書き込みを行う側のMCU（Seeed Studio XIAO BLE等）をUSBケーブルでPCに接続します。
2. **ブートローダーモードに入る:**
   - MCU上のリセットボタンを **2回素早く押す（ダブルタップ）** か、キーマップ上の `&bootloader` キーを押します。
   - PC上にストレージドライブ（`NICKEY44` または `XIAO-BOOT` 等）として認識されます。
3. **UF2ファイルの転送:**
   - **左手側**のマイコンには `nickey_l.uf2` をドラッグ＆ドロップします。
   - **右手側**のマイコンには `nickey_r.uf2` をドラッグ＆ドロップします。
   - 転送が完了すると**ドライブが自動的にアンマウント（消失）し**、マイコンが再起動して書き込み完了となります。

> 💡 **左右の接続やペアリングがおかしい場合:**  
> 接続トラブル時は `settings_reset.uf2` を左右両方のマイコンに一度書き込んで設定を完全にクリアしたあと、**改めて上記の手順で左右それぞれのファームウェア（`nickey_l.uf2` / `nickey_r.uf2`）を焼き直してください。**

---

## 📄 ライセンス

This repository is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
