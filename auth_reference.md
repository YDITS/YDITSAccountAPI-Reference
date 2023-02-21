# YDITSアカウント ソフト使用登録・認証用REST API 仕様書
URL:[/ydits-api/ydits-account/auth.php](https://api.schnetworks.net/ydits-api/ydits-account/auth.php)
** **
<br>

## **URL引数**
引数
|要素名|内容|形式|備考|必須|
|-|-|-|-|-|
|step|操作タイプ|int(1～3の数値)|1：ランダム認証キーの生成<br>2：使用ソフトウェアの登録<br>3：ソフトウェア使用時の利用権認証|〇|
** **
<br>

# step=1の場合
## **POSTデータ形式**
```json
{
    "mail":"example@example.com", 
    "pass":"example_a"
}
```
### **キー**

|要素名|内容|形式|備考|必須|
|-|-|-|-|-|
|mail|メールアドレス|String 50文字上限|存在しないアドレスの指定不可|〇|
|pass|パスワード|String 20文字上限||〇|
** **
<br>

## **レスポンスデータ形式**
```json
{
    "result":"ソフト利用登録を受け付けました",
    "resultcode":200,
    "uuid":"uuid",
    "key":"soft_key"
}
```
### **キー**
|要素名|内容|形式|備考|
|-|-|-|-|
|result|実行結果|String|成功時：ユーザー照会に成功しました<br>未登録時：このメールアドレスは登録されていません。|
|resultcode|実行結果|int|HTMLステータスコード準拠<br>成功時：200<br>未登録時：406|
|uuid|UUID|String|指定したユーザにシステム上で割り振られる一意の値|
|key|ソフト利用キー|String|ソフトウェアの利用権登録に必要なキーです|

** **
<br>

# step=2の場合
## **POSTデータ形式**
```json
{
    "uuid":"uuid", 
    "softname":"SoftName",
    "key":"softkey"
}
```
### **キー**

|要素名|内容|形式|備考|必須|
|-|-|-|-|-|
|uuid|UUID|String 50文字上限|Step1のレスポンスデータ(uuid要素)で返却されるものと同一。<br/>独自キー利用時は登録情報照会APIを用いて取得してください。|〇|
|softname|ソフト名|String 20文字上限|登録するソフトの名前|〇|
|key|利用権登録キー|String 50文字上限|Step1のレスポンスデータ(key)要素で返却されるものと同一。<br/>独自キー利用時は独自で登録するキーを送信してください。|〇|
** **
<br>

## **レスポンスデータ形式**
```json
{
    "result":"ソフト利用登録を受け付けました",
    "resultcode":200,
    "uuid":"uuid",
    "key":"soft_key"
}
```
### **キー**
|要素名|内容|形式|備考|
|-|-|-|-|
|result|実行結果|String|成功時：ソフトの登録を行いました。<br>未登録時：このソフトはすでに登録されています|
|resultcode|実行結果|int|HTMLステータスコード準拠<br>成功時：200<br>未登録時：406|
|uuid|UUID|String|指定したユーザにシステム上で割り振られる一意の値|
|key|ソフト利用キー|String|ソフトウェアの利用権登録を実行したキーです。<br/>ソフト内に保存するなどして、次回実行時にStep3で認証できるようにしておく必要があります。|

** **
<br>

# step=3の場合
## **POSTデータ形式**
```json
{
    "uuid":"uuid", 
    "key":"softkey"
}
```
### **キー**

|要素名|内容|形式|備考|必須|
|-|-|-|-|-|
|uuid|UUID|String 50文字上限|Step2で送信したものと同じ内容(uuidはユーザ情報照会APIで取得可能)|〇|
|key|ソフト利用キー|String 50文字上限|Step2で送信したものと同じ内容|〇|
** **
<br>

## **レスポンスデータ形式**
```json
{
    "result":"認証に成功しました",
    "resultcode":200
}
```
### **キー**
|要素名|内容|形式|備考|
|-|-|-|-|
|result|実行結果|String|成功時：認証に成功しました<br>未登録時：このソフトは利用登録されていません|
|resultcode|実行結果|int|HTMLステータスコード準拠<br>成功時：200<br>未登録時：406|

** **