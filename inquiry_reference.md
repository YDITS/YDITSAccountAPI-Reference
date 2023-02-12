# YDITSアカウント 登録情報照会用REST API 仕様書
URL:[/ydits-api/ydits-account/inquiry.php](https://api.schnetworks.net/ydits-api/ydits-account/inquiry.php)
** **
<br>

## **URL引数**
引数
|要素名|内容|形式|備考|必須|
|-|-|-|-|-|
|g|GUIの有無|String(「true」or「false」のみ)|true：GUIあり(対人専用)<br>false：GUIなし(ソフトからの操作専用)|〇|
** **
<br>

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
    "result":"ユーザ照会に成功しました",
    "resultcode":200,
    "userdata":{
        "uuid":"uuid",
        "mail":"example@example.com",
        "name":"exampleUser"
        }
}
```
### **キー**
|要素名|内容|形式|備考|
|-|-|-|-|
|result|実行結果|String|成功時：ユーザー照会に成功しました<br>未登録時：このメールアドレスは登録されていません。|
|resultcode|実行結果|int|HTMLステータスコード準拠<br>成功時：200<br>未登録時：406|
|userdata.uuid|照会ユーザのuuid|String|システム上で割り振られる一意の値です。|
|userdata.mail|照会ユーザのメールアドレス|String|照会したユーザに登録されているメールアドレスです。|
|userdata.name|照会ユーザのユーザ名|String|照会したユーザのユーザ名です。|