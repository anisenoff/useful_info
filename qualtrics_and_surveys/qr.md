# QR Code

`<div id="qrcode"></div>` goes in the html for the question

`./resources/qr.js` needs to be hosted on a website and the following needs to go into the js for the question.

```JavaScript
Qualtrics.SurveyEngine.addOnReady(function()
{
    jQuery.getScript( "<DOMAIN WHERE FILE IS HOSTED>/qr.js",function(){

        try{
        new QRCode(document.getElementById("qrcode"), "<WHAT YOU WANT THE QR CODE TO REPRESENT>");
        } catch(e){
        
            document.getElementById('qrcode').innerText = "<ERROR TEXT>";
        }
        
    });

});
```