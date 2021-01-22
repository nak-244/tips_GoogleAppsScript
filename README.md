# GAS オリジナルの関数を作成

URLからタイトルを取得するのはURLFetchAppを使うことで簡単に実現できる。  
Spreadsheetでハイパーリンクとしたい場合も標準関数と組み合わせることで簡単に実現できる。  

## URLからタイトルに変換
### GAS
```java:URLからタイトルに変換
function URLtoTitle(url) {
  var response = UrlFetchApp.fetch(url);

  var myRegexp = /<title>([\s\S]*?)<\/title>/i;
  var match = myRegexp.exec(response.getContentText());
  var title = match[1];

  title = title.replace(/(^\s+)|(\s+$)/g, "");
  return(title);
}
```
### Google Spreadsheet内の利用
`=URLtoTitle(セル)`

上記　var myRegexp = /<title>([\s\S]*?)<\/title>/i;　を変更すれば、簡易的なスクレイピングも可能。

## URLからページ内の一部を抜き出す
### GAS
```java:URLからページ内の一部を抜き出す
function URLtoTitle(url) {
  var response = UrlFetchApp.fetch(url);

  var myRegexp = /<img src=\"https:\/\/olp.hibarai.com\/img_sys_link\/1\/job\/olp\/([\s\S]*?)\/35.jpg/gi;
  var match = myRegexp.exec(response.getContentText());
  var title = match[1];

  title = title.replace(/(^\s+)|(\s+$)/g, "");
  return(title);
}
```
上記は、しごとらの詳細ページで、`<img src="https://olp.hibarai.com/img_sys_link/1/job/olp/198929/35.jpg" alt="コールセンター・テレオペ(短期のコールセンター/シフト相談可能！)" />`　から `198929` を抜き出す方法。
