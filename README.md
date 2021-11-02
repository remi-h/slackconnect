# slack connect

``` javascript
function myFunction() {
  var activeSpreadsheet = SpreadsheetApp.getActiveSpreadsheet(); // スプレッドシート
  var activeSheet = activeSpreadsheet.getActiveSheet(); // アクティブシート
  if(activeSheet.getName() != "シートの名前"){
    return;
  }
  var activeCell = activeSheet.getActiveCell(); // アクティブセル
 
  if(activeCell.getColumn() == 32 && activeCell.getValues() == "済"){ //32列目が済になったら
    var newInputRow = activeCell.getRow();
    // var taskNo = activeSheet.getRange(activeCell.getRow(), 0).getValues();
    var taskName = activeSheet.getRange(activeCell.getRow(), 1).getValues();
    // 送信するSlackのテキスト
    var slackText = "👀 <@U024N5E737C>" + newInputRow + "列目の「" + taskName + "」が完成しました\n\n" ;
    sendSlack(slackText);
  }
}

function sendSlack(slackText){
  // Step1で取得したWebhook URLを設定
  var webHookUrl = "webhookURL";
  
  var jsonData =
      {
        "channel": "#制作管理通知チャンネル",   // 通知したいチャンネル 
        'icon_url' : "https://image/01.png",
        "text" : slackText,
        "link_names" : 1,
        "username" : "botName"
      };
  
  var payload = JSON.stringify(jsonData);
  
  var options =
      {
        "method" : "post",
        "contentType" : "application/json",
        "payload" : payload,
      };
  
  // リクエスト
  UrlFetchApp.fetch(webHookUrl, options);
}
```
