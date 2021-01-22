# tips_GoogleAppsScript
Google SpreadsheetでURLからタイトルに変換(オリジナルの関数を作成)

URLからタイトルを取得するのはURLFetchAppを使うことで簡単に実現できる。  
Spreadsheetでハイパーリンクとしたい場合も標準関数と組み合わせることで簡単に実現できる。  

## GoogleAppsScriptの関数
```java:title
function URLtoTitle(url) {
  var response = UrlFetchApp.fetch(url);

  var myRegexp = /<title>([\s\S]*?)<\/title>/i;
  var match = myRegexp.exec(response.getContentText());
  var title = match[1];

  title = title.replace(/(^\s+)|(\s+$)/g, "");
  return(title);
}
```
