# zap_report_round5

ZAP by [Checkmarx](https://checkmarx.com/).


## Summary of Alerts

| Risk Level | Number of Alerts |
| --- | --- |
| High | 0 |
| Medium | 1 |
| Low | 0 |
| Informational | 11 |




## Insights

| Level | Reason | Site | Description | Statistic |
| --- | --- | --- | --- | --- |
| High | Exceeded High |  | Percentage of memory used | 95    |
| Low | Warning |  | ZAP errors logged - see the zap.log file for details | 495    |
| Low | Warning |  | ZAP warnings logged - see the zap.log file for details | 98    |
| Info | Informational |  | Percentage of network failures | 1 % |
| Info | Informational | http://localhost:8006 | Percentage of responses with status code 2xx | 74 % |
| Info | Informational | http://localhost:8006 | Percentage of responses with status code 3xx | 15 % |
| Info | Informational | http://localhost:8006 | Percentage of responses with status code 4xx | 10 % |
| Info | Informational | http://localhost:8006 | Percentage of endpoints with content type application/json | 25 % |
| Info | Informational | http://localhost:8006 | Percentage of endpoints with content type image/png | 12 % |
| Info | Informational | http://localhost:8006 | Percentage of endpoints with content type text/html | 50 % |
| Info | Informational | http://localhost:8006 | Percentage of endpoints with method GET | 100 % |
| Info | Informational | http://localhost:8006 | Count of total endpoints | 8    |
| Info | Informational | http://localhost:8006 | Percentage of slow responses | 5 % |
| Info | Informational | https://archive.mozilla.org | Percentage of endpoints with content type application/x-xpinstall | 100 % |
| Info | Informational | https://archive.mozilla.org | Percentage of endpoints with method GET | 100 % |
| Info | Informational | https://archive.mozilla.org | Count of total endpoints | 1    |
| Info | Informational | https://firefox-settings-attachments.cdn.mozilla.net | Percentage of endpoints with content type text/plain | 100 % |
| Info | Informational | https://firefox-settings-attachments.cdn.mozilla.net | Percentage of endpoints with method GET | 100 % |
| Info | Informational | https://firefox-settings-attachments.cdn.mozilla.net | Count of total endpoints | 5    |
| Info | Informational | https://firefox.settings.services.mozilla.com | Percentage of responses with status code 2xx | 100 % |
| Info | Informational | https://firefox.settings.services.mozilla.com | Percentage of endpoints with content type application/json | 100 % |
| Info | Informational | https://firefox.settings.services.mozilla.com | Percentage of endpoints with method GET | 100 % |
| Info | Informational | https://firefox.settings.services.mozilla.com | Count of total endpoints | 1    |




## Alerts

| Name | Risk Level | Number of Instances |
| --- | --- | --- |
| Cross-Domain Misconfiguration | Medium | 1 |
| Authentication Request Identified | Informational | 1 |
| Information Disclosure - Suspicious Comments | Informational | 2 |
| Modern Web Application | Informational | 3 |
| Re-examine Cache-control Directives | Informational | 1 |
| Retrieved from Cache | Informational | 1 |
| Session Management Response Identified | Informational | 4 |
| Tech Detected - HSTS | Informational | 1 |
| Tech Detected - Nginx | Informational | 1 |
| Tech Detected - Tailwind CSS | Informational | 1 |
| Tech Detected - Varnish | Informational | 1 |
| User Agent Fuzzer | Informational | Systemic |




## Alert Detail



### [ Cross-Domain Misconfiguration ](https://www.zaproxy.org/docs/alerts/10098/)



##### Medium (Medium)

### Description

Web browser data loading may be possible, due to a Cross Origin Resource Sharing (CORS) misconfiguration on the web server.

* URL: https://firefox.settings.services.mozilla.com/v1/buckets/main/collections/mfcdm-origins-list/changeset%3F_expected=1750871406038
  * Node Name: `https://firefox.settings.services.mozilla.com/v1/buckets/main/collections/mfcdm-origins-list/changeset (_expected)`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `access-control-allow-origin: *`
  * Other Info: `The CORS misconfiguration on the web server permits cross-domain read requests from arbitrary third party domains, using unauthenticated APIs on this domain. Web browser implementations do not permit arbitrary third parties to read the response from authenticated APIs, however. This reduces the risk somewhat. This misconfiguration could be used by an attacker to access data that is available in an unauthenticated manner, but which uses some other form of security, such as IP address white-listing.`


Instances: 1

### Solution

Ensure that sensitive data is not available in an unauthenticated manner (using IP address white-listing, for instance).
Configure the "Access-Control-Allow-Origin" HTTP header to a more restrictive set of domains, or remove all CORS headers entirely, to allow the web browser to enforce the Same Origin Policy (SOP) in a more restrictive manner.

### Reference


* [ https://vulncat.fortify.com/en/detail?category=HTML5&subcategory=Overly%20Permissive%20CORS%20Policy ](https://vulncat.fortify.com/en/detail?category=HTML5&subcategory=Overly%20Permissive%20CORS%20Policy)


#### CWE Id: [ 264 ](https://cwe.mitre.org/data/definitions/264.html)


#### WASC Id: 14

#### Source ID: 3

### [ Authentication Request Identified ](https://www.zaproxy.org/docs/alerts/10111/)



##### Informational (High)

### Description

The given request has been identified as an authentication request. The 'Other Info' field contains a set of key=value lines which identify any relevant fields. If the request is in a context which has an Authentication Method set to "Auto-Detect" then this rule will change the authentication to match the request identified.

* URL: http://localhost:8006/login
  * Node Name: `http://localhost:8006/login ()(csrf_token,password,username)`
  * Method: `POST`
  * Parameter: `username`
  * Attack: ``
  * Evidence: `password`
  * Other Info: `userParam=username
userValue=foo-bar@example.com
passwordParam=password
referer=http://localhost:8006/login
csrfToken=csrf_token`


Instances: 1

### Solution

This is an informational alert rather than a vulnerability and so there is nothing to fix.

### Reference


* [ https://www.zaproxy.org/docs/desktop/addons/authentication-helper/auth-req-id/ ](https://www.zaproxy.org/docs/desktop/addons/authentication-helper/auth-req-id/)



#### Source ID: 3

### [ Information Disclosure - Suspicious Comments ](https://www.zaproxy.org/docs/alerts/10027/)



##### Informational (Medium)

### Description

The response appears to contain suspicious comments which may help an attacker.

* URL: http://localhost:8006/static/index.js
  * Node Name: `http://localhost:8006/static/index.js`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `= session.role === 'administrator' || session.usernam`
  * Other Info: `The following pattern was used: \bADMINISTRATOR\b and was detected in likely comment: "//const canEdit = session.role === 'administrator' || session.username === r.reserver_username;", see evidence field for the suspicious comment/snippet.`
* URL: http://localhost:8006/static/index.js
  * Node Name: `http://localhost:8006/static/index.js`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `trieve reservations from the API and update `
  * Other Info: `The following pattern was used: \bFROM\b and was detected in likely comment: "// Retrieve reservations from the API and update the table", see evidence field for the suspicious comment/snippet.`


Instances: 2

### Solution

Remove all comments that return information that may help an attacker and fix any underlying problems they refer to.

### Reference



#### CWE Id: [ 615 ](https://cwe.mitre.org/data/definitions/615.html)


#### WASC Id: 13

#### Source ID: 3

### [ Modern Web Application ](https://www.zaproxy.org/docs/alerts/10109/)



##### Informational (Medium)

### Description

The application appears to be a modern web application. If you need to explore it automatically then the Ajax Spider may well be more effective than the standard one.

* URL: http://localhost:8006/cookiepolicy
  * Node Name: `http://localhost:8006/cookiepolicy`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `<script src="/static/footer.js"></script>`
  * Other Info: `No links have been found while there are scripts, which is an indication that this is a modern web application.`
* URL: http://localhost:8006/privacypolicy
  * Node Name: `http://localhost:8006/privacypolicy`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `<script src="/static/footer.js"></script>`
  * Other Info: `No links have been found while there are scripts, which is an indication that this is a modern web application.`
* URL: http://localhost:8006/terms
  * Node Name: `http://localhost:8006/terms`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `<script src="/static/footer.js"></script>`
  * Other Info: `No links have been found while there are scripts, which is an indication that this is a modern web application.`


Instances: 3

### Solution

This is an informational alert and so no changes are required.

### Reference




#### Source ID: 3

### [ Re-examine Cache-control Directives ](https://www.zaproxy.org/docs/alerts/10015/)



##### Informational (Low)

### Description

The cache-control header has not been set properly or is missing, allowing the browser and proxies to cache content. For static assets like css, js, or image files this might be intended, however, the resources should be reviewed to ensure that no sensitive content will be cached.

* URL: https://firefox.settings.services.mozilla.com/v1/buckets/main/collections/mfcdm-origins-list/changeset%3F_expected=1750871406038
  * Node Name: `https://firefox.settings.services.mozilla.com/v1/buckets/main/collections/mfcdm-origins-list/changeset (_expected)`
  * Method: `GET`
  * Parameter: `cache-control`
  * Attack: ``
  * Evidence: `max-age=3600`
  * Other Info: ``


Instances: 1

### Solution

For secure content, ensure the cache-control HTTP header is set with "no-cache, no-store, must-revalidate". If an asset should be cached consider setting the directives "public, max-age, immutable".

### Reference


* [ https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html#web-content-caching ](https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html#web-content-caching)
* [ https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Cache-Control ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Cache-Control)
* [ https://grayduck.mn/2021/09/13/cache-control-recommendations/ ](https://grayduck.mn/2021/09/13/cache-control-recommendations/)


#### CWE Id: [ 525 ](https://cwe.mitre.org/data/definitions/525.html)


#### WASC Id: 13

#### Source ID: 3

### [ Retrieved from Cache ](https://www.zaproxy.org/docs/alerts/10050/)



##### Informational (Medium)

### Description

The content was retrieved from a shared cache. If the response data is sensitive, personal or user-specific, this may result in sensitive information being leaked. In some cases, this may even result in a user gaining complete control of the session of another user, depending on the configuration of the caching components in use in their environment. This is primarily an issue where caching servers such as "proxy" caches are configured on the local network. This configuration is typically found in corporate or educational environments, for instance.

* URL: https://firefox.settings.services.mozilla.com/v1/buckets/main/collections/mfcdm-origins-list/changeset%3F_expected=1750871406038
  * Node Name: `https://firefox.settings.services.mozilla.com/v1/buckets/main/collections/mfcdm-origins-list/changeset (_expected)`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `HIT`
  * Other Info: ``


Instances: 1

### Solution

Validate that the response does not contain sensitive, personal or user-specific information. If it does, consider the use of the following HTTP response headers, to limit, or prevent the content being stored and retrieved from the cache by another user:
Cache-Control: no-cache, no-store, must-revalidate, private
Pragma: no-cache
Expires: 0
This configuration directs both HTTP 1.0 and HTTP 1.1 compliant caching servers to not store the response, and to not retrieve the response (without validation) from the cache, in response to a similar request.

### Reference


* [ https://datatracker.ietf.org/doc/html/rfc7234 ](https://datatracker.ietf.org/doc/html/rfc7234)
* [ https://datatracker.ietf.org/doc/html/rfc7231 ](https://datatracker.ietf.org/doc/html/rfc7231)
* [ https://www.rfc-editor.org/rfc/rfc9110.html ](https://www.rfc-editor.org/rfc/rfc9110.html)


#### CWE Id: [ 525 ](https://cwe.mitre.org/data/definitions/525.html)


#### Source ID: 3

### [ Session Management Response Identified ](https://www.zaproxy.org/docs/alerts/10112/)



##### Informational (High)

### Description

The given response has been identified as containing a session management token. The 'Other Info' field contains a set of header tokens that can be used in the Header Based Session Management Method. If the request is in a context which has a Session Management Method set to "Auto-Detect" then this rule will change the session management to use the tokens identified.

* URL: http://localhost:8006/login
  * Node Name: `http://localhost:8006/login`
  * Method: `GET`
  * Parameter: `csrf_token`
  * Attack: ``
  * Evidence: `csrf_token`
  * Other Info: `cookie:csrf_token`
* URL: http://localhost:8006/register
  * Node Name: `http://localhost:8006/register`
  * Method: `GET`
  * Parameter: `csrf_token`
  * Attack: ``
  * Evidence: `csrf_token`
  * Other Info: `cookie:csrf_token`
* URL: http://localhost:8006/login
  * Node Name: `http://localhost:8006/login`
  * Method: `GET`
  * Parameter: `csrf_token`
  * Attack: ``
  * Evidence: `csrf_token`
  * Other Info: `cookie:csrf_token`
* URL: http://localhost:8006/register
  * Node Name: `http://localhost:8006/register`
  * Method: `GET`
  * Parameter: `csrf_token`
  * Attack: ``
  * Evidence: `csrf_token`
  * Other Info: `cookie:csrf_token`


Instances: 4

### Solution

This is an informational alert rather than a vulnerability and so there is nothing to fix.

### Reference


* [ https://www.zaproxy.org/docs/desktop/addons/authentication-helper/session-mgmt-id/ ](https://www.zaproxy.org/docs/desktop/addons/authentication-helper/session-mgmt-id/)



#### Source ID: 3

### [ Tech Detected - HSTS ](https://www.zaproxy.org/docs/alerts/10004/)



##### Informational (Medium)

### Description

The following "Security" technology was identified: HSTS.
Described as:
HTTP Strict Transport Security (HSTS) informs browsers that the site should only be accessed using HTTPS.

* URL: https://firefox.settings.services.mozilla.com/v1/buckets/main/collections/mfcdm-origins-list/changeset%3F_expected=1750871406038
  * Node Name: `https://firefox.settings.services.mozilla.com/v1/buckets/main/collections/mfcdm-origins-list/changeset (_expected)`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `Strict-Transport-Security`
  * Other Info: ``


Instances: 1

### Solution



### Reference


* [ https://www.rfc-editor.org/rfc/rfc6797#section-6.1 ](https://www.rfc-editor.org/rfc/rfc6797#section-6.1)



#### WASC Id: 13

#### Source ID: 4

### [ Tech Detected - Nginx ](https://www.zaproxy.org/docs/alerts/10004/)



##### Informational (Medium)

### Description

The following "Web servers, Reverse proxies" technology was identified: Nginx.
Described as:
Nginx is a web server that can also be used as a reverse proxy, load balancer, mail proxy and HTTP cache.

* URL: https://firefox.settings.services.mozilla.com/v1/buckets/main/collections/mfcdm-origins-list/changeset%3F_expected=1750871406038
  * Node Name: `https://firefox.settings.services.mozilla.com/v1/buckets/main/collections/mfcdm-origins-list/changeset (_expected)`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `nginx`
  * Other Info: `The following CPE is associated with the identified tech: cpe:2.3:a:f5:nginx:*:*:*:*:*:*:*:*
`


Instances: 1

### Solution



### Reference


* [ https://nginx.org/en ](https://nginx.org/en)



#### WASC Id: 13

#### Source ID: 4

### [ Tech Detected - Tailwind CSS ](https://www.zaproxy.org/docs/alerts/10004/)



##### Informational (Medium)

### Description

The following "UI frameworks" technology was identified: Tailwind CSS.
Described as:
Tailwind is a utility-first CSS framework for rapidly building custom user interfaces.

* URL: http://localhost:8006/static/tailwind.css
  * Node Name: `http://localhost:8006/static/tailwind.css`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `--tw-border-opacity`
  * Other Info: ``


Instances: 1

### Solution



### Reference


* [ https://tailwindcss.com/ ](https://tailwindcss.com/)



#### WASC Id: 13

#### Source ID: 4

### [ Tech Detected - Varnish ](https://www.zaproxy.org/docs/alerts/10004/)



##### Informational (Medium)

### Description

The following "Caching" technology was identified: Varnish.
Described as:
Varnish is a reverse caching proxy.

* URL: https://firefox.settings.services.mozilla.com/v1/buckets/main/collections/mfcdm-origins-list/changeset%3F_expected=1750871406038
  * Node Name: `https://firefox.settings.services.mozilla.com/v1/buckets/main/collections/mfcdm-origins-list/changeset (_expected)`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `varnish`
  * Other Info: `The following CPE is associated with the identified tech: cpe:2.3:a:varnish-software:varnish_cache:*:*:*:*:*:*:*:*
`


Instances: 1

### Solution



### Reference


* [ https://www.varnish-cache.org ](https://www.varnish-cache.org)



#### WASC Id: 13

#### Source ID: 4

### [ User Agent Fuzzer ](https://www.zaproxy.org/docs/alerts/10104/)



##### Informational (Medium)

### Description

Check for differences in response based on fuzzed User Agent (eg. mobile sites, access as a Search Engine Crawler). Compares the response statuscode and the hashcode of the response body with the original response.

* URL: http://localhost:8006/api
  * Node Name: `http://localhost:8006/api`
  * Method: `GET`
  * Parameter: `Header User-Agent`
  * Attack: `Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)`
  * Evidence: ``
  * Other Info: ``
* URL: http://localhost:8006/favicon.ico
  * Node Name: `http://localhost:8006/favicon.ico`
  * Method: `GET`
  * Parameter: `Header User-Agent`
  * Attack: `Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)`
  * Evidence: ``
  * Other Info: ``
* URL: http://localhost:8006/login
  * Node Name: `http://localhost:8006/login`
  * Method: `GET`
  * Parameter: `Header User-Agent`
  * Attack: `Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)`
  * Evidence: ``
  * Other Info: ``
* URL: http://localhost:8006/login
  * Node Name: `http://localhost:8006/login ()(csrf_token,password,username)`
  * Method: `POST`
  * Parameter: `Header User-Agent`
  * Attack: `Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)`
  * Evidence: ``
  * Other Info: ``
* URL: http://localhost:8006/register
  * Node Name: `http://localhost:8006/register ()(accept_terms,birthdate,csrf_token,password,role,username)`
  * Method: `POST`
  * Parameter: `Header User-Agent`
  * Attack: `Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)`
  * Evidence: ``
  * Other Info: ``

Instances: Systemic


### Solution



### Reference


* [ https://owasp.org/wstg ](https://owasp.org/wstg)



#### Source ID: 1


