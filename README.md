# AppGuardian - スマホ依存防止・利用制限アプリ

スマートフォンの利用時間を管理し、使いすぎを防止するAndroidアプリです。  
親モードによる制限機能を備え、健全なスマホ利用習慣の形成をサポートします。

---

## 📱 概要
AppGuardianは、アプリの使用時間を可視化し、設定した時間を超えると自動で制限を行うアプリです。  
「使いすぎてしまう」という課題に対して、ユーザー自身や保護者がコントロールできる仕組みを提供します。

---

## ✨ 主な機能

- 📊 **アプリ使用時間の計測**  
  UsageStats APIを使用し、アプリごとの利用時間を取得

- ⏱️ **利用時間制限**  
  アプリごとに1日の使用上限を設定

- 🚫 **自動ブロック機能**  
  制限時間到達時にAccessibilityServiceでアプリをブロック

- 📈 **ダッシュボード表示**  
  使用時間の可視化

- 🔐 **親モード**  
  PINコードによる設定ロック

- 📝 **解除申請機能**  
  制限解除のリクエストを送信可能

---

## 🚀 技術スタック

### コア
- Kotlin
- Jetpack Compose（Material3）

### アーキテクチャ
- MVVM
- Clean Architecture

### 非同期処理
- Coroutines / Flow

### データ
- Room
- DataStore

### その他
- Hilt（DI）
- WorkManager
- Navigation Compose
- Coil

---

## 🛠️ 開発で工夫した点

- ユーザーが直感的に使えるUI/UX設計を意識
- 使用時間の取得・制御など、Android特有の権限を活用した実装
- Clean Architectureを採用し、保守性を意識した構成に設計

---

## 📋 必要要件
- Android Studio
- API 26以上
- JDK 17

---

## 🔑 必要な権限

- 使用状況アクセス（UsageStats）
- アクセシビリティサービス
- オーバーレイ表示
- 通知権限

---

## 📖 使い方

1. アプリ起動
2. 必要な権限を許可
3. 制限したいアプリを選択
4. 使用時間を設定

## 🧪 テスト

```bash
./gradlew test
./gradlew connectedAndroidTest
