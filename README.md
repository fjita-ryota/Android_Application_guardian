# MyApplication + AppGuardian

**統合Androidアプリ - スマホ依存防止・利用制限アプリ**

[![Build Status](https://img.shields.io/badge/build-passing-brightgreen)](https://github.com/yourusername/myapplication-appguardian)
[![Kotlin](https://img.shields.io/badge/Kotlin-2.0.21-blue.svg)](https://kotlinlang.org)
[![Jetpack Compose](https://img.shields.io/badge/Jetpack%20Compose-2023.10.01-blue)](https://developer.android.com/jetpack/compose)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)

## 📱 概要

MyApplicationは、AppGuardian（アプリガーディアン）のスマホ依存防止機能を統合したAndroidアプリケーションです。親子で使える利用制限機能により、健全なスマートフォン利用習慣の形成をサポートします。

### ✨ 主な機能

- 📊 **アプリ使用時間の計測** - UsageStats APIを使用した正確な計測
- ⏱️ **アプリ利用制限** - 1日の使用上限時間を設定
- 🚫 **自動ブロック** - AccessibilityServiceによる制限時間到達時の自動ブロック
- 📈 **ダッシュボード** - 使用統計の可視化
- 🔐 **親モード** - PIN認証による管理機能
- 📝 **解除申請** - 子どもから親への延長申請機能

## 🏗️ アーキテクチャ

**MVVM + Clean Architecture**

```
presentation/  (UI層 - Jetpack Compose)
    ├── ui/
    ├── viewmodel/
    └── navigation/

domain/       (ビジネスロジック層)
    ├── model/
    ├── usecase/
    └── repository/

data/         (データ層)
    ├── local/     (Room Database)
    ├── repository/
    └── mapper/

service/      (サービス層)
    ├── accessibility/  (AccessibilityService)
    ├── monitoring/     (UsageMonitoringService)
    └── notification/   (NotificationHelper)
```

## 🚀 技術スタック

### コア
- **言語**: Kotlin 2.0.21
- **UI**: Jetpack Compose + Material Design 3
- **DI**: Hilt 2.48
- **非同期処理**: Coroutines + Flow

### データ
- **データベース**: Room 2.6.0
- **設定保存**: DataStore 1.0.0
- **バックグラウンド**: WorkManager 2.9.0

### その他
- **ナビゲーション**: Navigation Compose 2.7.5
- **画像読み込み**: Coil 2.5.0
- **ビルドツール**: Gradle 8.13 + KSP

## 📋 必要要件

- **Android Studio**: Arctic Fox以降
- **最小SDK**: API 26 (Android 8.0)
- **ターゲットSDK**: API 34 (Android 14)
- **JDK**: 17以上

## 🛠️ セットアップ

### 1. リポジトリのクローン

```bash
git clone https://github.com/yourusername/myapplication-appguardian.git
cd myapplication-appguardian
```

### 2. Android Studioで開く

1. Android Studioを起動
2. `File` → `Open`
3. クローンしたディレクトリを選択
4. Gradle Syncを待つ

### 3. ビルド

```bash
# デバッグビルド
./gradlew assembleDebug

# リリースビルド
./gradlew assembleRelease
```

### 4. 実行

1. エミュレーターまたは実機を接続
2. `Run` → `Run 'app'` (Shift+F10)

## 🔑 必要な権限

アプリを使用するには、以下の権限を手動で許可する必要があります:

### 1. UsageStats権限
```
設定 → アプリ → My Application → 特殊なアプリアクセス → 使用状況へのアクセス
```

### 2. AccessibilityService
```
設定 → ユーザー補助 → My Application
```

### 3. オーバーレイ表示
```
設定 → アプリ → My Application → 他のアプリの上に重ねて表示
```

### 4. 通知権限 (Android 13+)
```
設定 → アプリ → My Application → 通知
```

## 📖 使い方

### 初回起動

1. アプリを起動すると「My Application」画面が表示されます
2. 「アプリガーディアンを起動」ボタンをタップ
3. 権限設定画面で必要な権限を許可

### アプリ利用制限の設定

1. アプリ一覧画面を開く
2. 制限したいアプリをタップ
3. 1日の使用上限時間を設定

### 親モードの設定

1. 設定画面から「親モード」を開く
2. PINコードを設定
3. 親モードでのみ制限設定の変更が可能になります

## 📸 スクリーンショット

<details>
<summary>スクリーンショットを表示</summary>

### メイン画面
![Main Screen](docs/screenshots/main.png)

### ダッシュボード
![Dashboard](docs/screenshots/dashboard.png)

### アプリ一覧
![App List](docs/screenshots/app-list.png)

### ブロック画面
![Block Screen](docs/screenshots/block.png)

</details>

## 🧪 テスト

```bash
# ユニットテスト
./gradlew test

# インストゥルメンテッションテスト
./gradlew connectedAndroidTest

# カバレッジレポート
./gradlew jacocoTestReport
```

## 🔧 ビルド成功

プロジェクトは正常にビルドされます:

- ✅ ビルドステータス: 成功
- ✅ APKサイズ: 19MB (デバッグビルド)
- ✅ ビルド時間: 約26秒
- ✅ エラー: なし

詳細は [BUILD_SUCCESS.md](BUILD_SUCCESS.md) を参照してください。

## 📚 ドキュメント

- [BUILD_SUCCESS.md](BUILD_SUCCESS.md) - ビルド成功の詳細と修正内容
- [INTEGRATION_README.md](INTEGRATION_README.md) - 統合の詳細説明
- [API Documentation](docs/api/README.md) - APIドキュメント

## 🤝 貢献

プルリクエストを歓迎します! 大きな変更の場合は、まずissueを開いて変更内容を議論してください。

### 開発の流れ

1. このリポジトリをフォーク
2. フィーチャーブランチを作成 (`git checkout -b feature/AmazingFeature`)
3. 変更をコミット (`git commit -m 'Add some AmazingFeature'`)
4. ブランチにプッシュ (`git push origin feature/AmazingFeature`)
5. プルリクエストを作成

## 📄 ライセンス

このプロジェクトは MIT ライセンスの下で公開されています - 詳細は [LICENSE](LICENSE) ファイルを参照してください。

## 👥 作者

- **開発**: Claude Code + User
- **統合日**: 2026-01-11

## 🙏 謝辞

- [Jetpack Compose](https://developer.android.com/jetpack/compose) - UI開発
- [Hilt](https://dagger.dev/hilt/) - Dependency Injection
- [Room](https://developer.android.com/training/data-storage/room) - ローカルデータベース
- Material Design 3

## 📞 サポート

問題が発生した場合は、[Issues](https://github.com/yourusername/myapplication-appguardian/issues) を作成してください。

## 🗺️ ロードマップ

- [ ] 週次/月次レポート機能
- [ ] 複数の子どもアカウント管理
- [ ] クラウド同期機能
- [ ] ウィジェット対応
- [ ] 生体認証サポート

---

**Note**: このアプリは教育目的で開発されています。実際の使用は自己責任でお願いします。
