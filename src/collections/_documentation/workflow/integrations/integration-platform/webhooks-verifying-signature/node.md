```javascript
const crypto = require('crypto');

function verifySignature(request, secret='') {
  const hmac = crypto.createHmac('sha256', secret);
  hmac.update(JSON.stringify(request.body), 'utf8');
  const digest = hmac.digest('hex');
  return digest === request.headers['Sentry-Hook-Signature'];
}
```
