# MonacaUserDemoApp

* ID/PW 認証、Email/PW 認証、匿名認証の３種類を試すことができる、ニフティクラウド mobile backend のサンプルアプリです。

## 動作確認までの手順
1. ニフティクラウド mobile backend（以下 mBaaS）の[会員登録](http://mb.cloud.nifty.com/signup.htm)（無料）
1. mBaaS にアプリを新規作成し、APIキーを発行する
1. Monaca の[会員登録](https://ja.monaca.io/)（無料）
1. Monaca プロジェクトをインポート
   * https://github.com/natsumo/MonacaUserDemoApp/archive/master.zip
1. mBaaS SDK を Monaca に設定
   * 設定 ＞ JS/CSSコンポーネントの追加と削除 ＞ 「ncmb」を追加
1. Monaca プロジェクト `www/app.js` にAPIキーの設定
```js
// [NCMB] APIキー設定
var appKey    = "YOUR_NCMB_APPKEY";
var clientKey = "YOUR_NCMB_CLIENTKEY";
```

## コード
### SDK の初期化
```js
// [NCMB] SDKの初期化
var ncmb = new NCMB(appKey, clientKey);
```

### ID/PW 認証
#### 新規登録 + ログイン
```js
// [NCMB] user インスタンスの生成
var user = new ncmb.User();
// [NCMB] ID / PW で新規登録
user.set("userName", username)
    .set("password", password)
    .signUpByAccount()
    .then(function(user) {
        /* 処理成功 */
        // [NCMB] ID / PW でログイン
        ncmb.User.login(user)
                 .then(function(user) {
                     /* 処理成功 */
                 })
                 .catch(function(error) {
                     /* 処理失敗 */
                 });
    })
    .catch(function(error) {
        /* 処理失敗 */
    });
```

#### ログイン
```js
// [NCMB] ID / PW でログイン
ncmb.User.login(username, password)
         .then(function(user) {
             /* 処理成功 */
         })
         .catch(function(error) {
             /* 処理失敗 */
         });
```

### Email/PW 認証
#### 新規登録
```js
// [NCMB] Email に会員登録を行うためのメールを送信
ncmb.User.requestSignUpEmail(mailAddress)
         .then(function(user){
             /* 処理成功 */
         })
         .catch(function(error){
             /* 処理失敗 */
         });
```

#### ログイン
```js
// [NCMB] Email / PW でログイン
ncmb.User.loginWithMailAddress(mailAddress, password)
         .then(function(user) {
             /* 処理成功 */
         })
         .catch(function(error) {
             /* 処理失敗 */
         });
```

### 匿名認証
#### ログイン
```js
// [NCMB] 匿名 でログイン
ncmb.User.loginAsAnonymous()
         .then(function(user){
             /* 処理成功 */
         })
         .catch(function(error){
             /* 処理失敗 */
         });
```

### ログアウト（共通）
```js
// [NCMB] ログアウト
ncmb.User.logout();
```

### ログイン中のユーザー情報の取得
```js
// [NCMB] ログイン中のユーザー情報の取得
currentLoginUser = ncmb.User.getCurrentUser();
```
