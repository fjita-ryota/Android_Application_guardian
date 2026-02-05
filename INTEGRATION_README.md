# MyApplication + AppGuardian 統合プロジェクト

## 統合の概要

MyApplicationプロジェクトにAppGuardian(アプリガーディアン)の機能を統合しました。

## 実施した変更

### 1. ビルド設定の更新

#### ルートレベル [build.gradle.kts](build.gradle.kts)
- Hilt プラグイン追加 (v2.48)
- KSP プラグイン追加 (v2.0.21-1.0.28)
- Compose Compiler プラグイン追加 (v2.0.21)

#### アプリレベル [app/build.gradle.kts](app/build.gradle.kts)
- Jetpack Compose依存関係追加
- Hilt (Dependency Injection)
- Room (ローカルデータベース)
- DataStore (設定保存)
- WorkManager (バックグラウンドタスク)
- Navigation Compose
- Coil (画像読み込み)
- その他必要な依存関係

#### [gradle.properties](gradle.properties)
- Jetifier有効化
- Gradle最適化設定
- Compose実験的機能有効化

### 2. ソースコード統合

#### AppGuardianソースコード
以下のパスにAppGuardianのコードがコピーされています:
- `app/src/main/java/com/appguardian/`

#### 主なコンポーネント:
- **data層**: リポジトリ実装、データソース、Room Database
- **domain層**: ユースケース、ビジネスロジック
- **presentation層**: Compose UI、ViewModel
- **service層**: AccessibilityService、監視サービス

### 3. AndroidManifest統合

[app/src/main/AndroidManifest.xml](app/src/main/AndroidManifest.xml)に以下を追加:

#### 権限
- `PACKAGE_USAGE_STATS` - アプリ使用統計
- `SYSTEM_ALERT_WINDOW` - オーバーレイ表示
- `FOREGROUND_SERVICE` - バックグラウンド監視
- `POST_NOTIFICATIONS` - 通知

#### コンポーネント
- AppGuardianのMainActivity
- BlockActivity (ブロック画面)
- AppBlockService (AccessibilityService)
- UsageMonitoringService (監視サービス)

### 4. リソース統合

以下のリソースが統合されています:
- `res/values/strings.xml` - AppGuardianの文字列リソース
- `res/values/themes.xml` - AppGuardianとMyApplicationのテーマ
- `res/xml/` - XMLリソース(AccessibilityService設定など)
- `res/drawable/` - アイコンなどの画像リソース

### 5. メインアクティビティ

[MainActivity.kt](app/src/main/java/com/example/myapplication/MainActivity.kt)を更新:
- Jetpack Composeに変換
- AppGuardianを起動するボタンを追加

## 起動方法

### Android Studioで開く

1. Android Studioを起動
2. `File` → `Open` を選択
3. `c:\Users\dev\Desktop\AI-dev\MyApplication` を選択
4. Gradle Syncを待つ

### アプリの起動

1. エミュレーターまたは実機を接続
2. `Run` ボタンをクリック
3. メイン画面から「アプリガーディアンを起動」ボタンをタップ

## ✅ ビルド成功!

**プロジェクトは正常にビルドされ、APKが生成されました!**

### 修正した主なエラー

以下のコンパイルエラーをすべて修正しました:

1. **✅ UnlockRequest モデルの不一致** - 修正完了
   - `UnlockRequestMapper.kt`: プロパティ名を統一 (`createdAt` → `requestedAt`, `requestedMinutes` → `unlockDurationMinutes`)
   - `UnlockRequestRepositoryImpl.kt`: コンストラクタに`reason`と`requestedMinutes`を追加
   - `UnlockRequestDao.kt`: 不足していたメソッド(`getAllRequests()`, `updateStatus()`, `getRequest()`)を追加

2. **✅ Material Icons Extended** - 追加完了
   - `build.gradle.kts`に`material-icons-extended`依存関係を追加
   - `Backspace`, `Cancel`, `ChevronRight`, `Security`などのアイコンが利用可能に

3. **✅ Result型の variance 問題** - 修正完了
   - `Result.kt`: `getOrElse`メソッドを関数パラメータに変更し、`@UnsafeVariance`を使用
   - `onSuccess()`と`onError()`メソッドを追加

4. **✅ NotificationHelper の R 参照エラー** - 修正完了
   - `NotificationHelper.kt`: インポートを`com.appguardian.R`から`com.example.myapplication.R`に変更

5. **✅ Repository の型推論エラー** - 修正完了
   - `UnlockRequestRepositoryImpl.kt`: Flow.mapに明示的な型パラメータを追加
   - `UsageStatsRepositoryImpl.kt`: 同様に修正

6. **✅ その他の修正**
   - `AppNavigation.kt`: `dp`のインポート追加
   - `PinManager.kt`: `bytesToHex()`をpublicに変更

## AppGuardianの機能

### 主要機能
1. **アプリ使用時間の計測** - UsageStats APIを使用
2. **アプリ利用制限** - 1日の使用上限を設定
3. **アプリブロック** - AccessibilityServiceで自動ブロック
4. **ホーム画面ダッシュボード** - 使用統計の表示
5. **アプリ一覧・管理** - 制限時間の設定UI
6. **親モード** - PIN認証による管理機能

### アーキテクチャ
- **MVVM + Clean Architecture**
- **Jetpack Compose** - UI
- **Hilt** - Dependency Injection
- **Room** - ローカルデータベース
- **Coroutines + Flow** - 非同期処理

## 次のステップ

1. Android StudioでMyApplicationプロジェクトを開く
2. 上記のコンパイルエラーを修正
3. ビルドを実行
4. エミュレーターまたは実機でテスト
5. 必要な権限を手動で許可:
   - 設定 → アプリ → MyApplication → 権限
   - UsageStats権限を有効化
   - AccessibilityServiceを有効化

## トラブルシューティング

### Gradle Syncエラー
- `./gradlew clean` を実行
- Android Studioを再起動
- キャッシュをクリア: `File` → `Invalidate Caches / Restart`

### ビルドエラー
- JDK 17を使用していることを確認
- Gradle versionが8.13以上であることを確認
- Kotlin versionが2.0.21であることを確認

## 参考リンク

- [Jetpack Compose ドキュメント](https://developer.android.com/jetpack/compose)
- [Hilt ドキュメント](https://dagger.dev/hilt/)
- [Room ドキュメント](https://developer.android.com/training/data-storage/room)
- [AccessibilityService ガイド](https://developer.android.com/guide/topics/ui/accessibility/service)
