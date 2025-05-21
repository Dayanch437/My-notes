~~~javascript
function doGet(e) {
  var url = e.parameter.url;

  if (!url) {
    return ContentService.createTextOutput("Missing 'url' parameter");
  }

  try {
    var response = UrlFetchApp.fetch(url);
    var contentType = response.getHeaders()['Content-Type'] || 'text/plain';
    var content = response.getContentText();

    return ContentService
      .createTextOutput(content)
      .setMimeType(getMimeType(contentType));
  } catch (err) {
    return ContentService.createTextOutput("Error: " + err)
      .setMimeType(ContentService.MimeType.TEXT);
  }
}

function getMimeType(contentType) {
  if (contentType.includes("html")) return ContentService.MimeType.HTML;
  if (contentType.includes("json")) return ContentService.MimeType.JSON;
  if (contentType.includes("xml")) return ContentService.MimeType.XML;
  return ContentService.MimeType.TEXT;
}
~~~
	
~~~bash
docker cp marzban-marzban-1:/code/app/telegram/utils/shared.py ./shared.py
~~~

~~~bash
nano shared.py
~~~

~~~bash
./shared.py docker cp marzban-marzban-1:/code/app/telegram/utils/shared.py 
~~~

~~~bash
docker restart marzban-marzban-1
~~~
Telegram user info boot
~~~bash
@userinfobot
~~~

~~~python
sudo bash -c "$(curl -sL https://github.com/Gozargah/Marzban-scripts/raw/master/marzban-node.sh)" @ install
~~~
