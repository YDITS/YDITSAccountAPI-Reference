# YDITSアカウント 登録用REST API 仕様書
URL:[/ydits-api/ydits-account/regist.php](https://api.schnetworks.net/ydits-api/ydits-account/regist.php)
** **
<br>

## **URL引数**
引数
|要素名|内容|形式|備考|
|-|-|-|-|
|g|GUIの有無|String(「true」or「false」のみ)|true：GUIあり(対人専用)<br>false:GUIなし(ソフトからの操作専用)|
** **
<br>

## **POSTデータ形式**
```json
{
    "name":"example",
    "mail":"example@example.com", 
    "pass":"example_a"
}
```
### **キー**

|要素名|内容|形式|備考|
|-----|---|----|---|
|name|ユーザ名|String 50文字上限|
|mail|メールアドレス|String 50文字上限|存在しないアドレスの指定不可|
|pass|パスワード|String 20文字上限||
** **
<br>

## **レスポンスデータ形式**
```json
{
    "result":"ユーザ登録に成功しました",
    "resultcode":200
}
```
### **キー**
|要素名|内容|形式|備考|
|-|-|-|-|
|result|実行結果|String|成功時：ユーザー登録が完了しました<br>使用不可メールアドレス指定時：指定されたメールアドレスは使用できません。<br>メールアドレス重複時：同じメールアドレスが存在します。|
|resultcode|実行結果|int|HTMLステータスコード準拠<br>成功時：200<br>使用不可メールアドレス指定時：406<br>メールアドレス重複時：409|