# API Access & Specification

See the API's [Full Documentation](https://screenshotlayer.com/documentation).

The **currencylayer API** provides real-time (updates ranging from 60 seconds to 1 hour, depending on your Subscription Plan) Currency Exchange Rates, by default relative to US Dollars (USD) in `JSON` format.

It is - and will always be - free for personal use (up to 100 monthly snapshots) and affordable for business. You can [sign up to get Free API Access here](https://screenshotlayer.com/product).

## 3-Step Quickstart Guide

### Step 1: Base URL
Capturing a snapshot using the screenshotlayer API is simple. Each API request is based at the following URL:

```url
http://api.screenshotlayer.com/api/capture
```

### Step 2: Required parameters
In order to make any API request, two required parameters - your personal access_key and the target website's `url` - have to be specified:

| Parameter | Description |
| --------------|-------------- |
| `access_key` | your personal password used to authenticate with the API - located in your [Account Dashboard](https://screenshotlayer.com/dashboard). |
| `url` | the full URL of the website you want to request a snapshot from, e.g. `http://abc.com` |

**Please note**: A URL can only be processed if it contains its respective **HTTP Protocol**.

### Step 3: Optional parameters
Based on how you you wish to configure your screenshot, you can choose from a number of optional parameters:

| Parameter | Description | Default |
|--------------|-------------- |-----------|
| `fullpage` | set to "1" if you want to capture the full height of the target website ||
| `width` | specify your preferred thumbnail width in pixels | 1:1 |
| `viewport` | specify your preferred viewport dimensions in pixels | 1440x900 |
| `format` | set your preferred image output format | PNG |
| `secret_key` | your secret key, an md5 hash of the target URL and your secret word. ||
| `css_url` | attach a URL containing a custom CSS stylesheet ||
| `delay` | specify a delay before screenshot is captured (in seconds) ||
| `ttl` | define the time (in seconds) your snapshot should be cached | 2592000 (30 days) |
| `force` | set to "1" if you want to force the API to capture a fresh screenshot ||
| `placeholder` | attach a URL containing a custom placeholder image or set to "1" to use default placeholder ||
| `user_agent` | specify a custom User-Agent HTTP header to send with your request ||
| `accept_lang` | specify a custom Accept-Language HTTP header to send with your request ||
| `export` | export snapshot via custom ftp path or using your AWS S3 user details ||

### Example Query:
The following query requests a full-height screenshot of apple.com

```url
http://api.screenshotlayer.com/api/capture
    ? access_key = YOUR_ACCESS_KEY
    & url = http://www.apple.com
    & viewport = 1440x900
    & fullpage = 1
```

## Access Key

After signing up, every user is assigned a personal API Access Key - a unique "password" used to authenticate with the API.

To call the screenshotlayer API, simply append your `access_key` as a parameter to the base URL:

```url
http://api.screenshotlayer.com/api/capture?access_key=YOUR_ACCESS_KEY 
```

You can [sign up for a free Access Key here](https://screenshotlayer.com/product). Our Free Plan offers up to 100 monthly snapshots. Paid plans provide larger request volumes and a full stack of advanced features.

## HTTPS - Secure Datastreams

Paid Customers may establish a secure connection via 256-bit HTTPS (industry-standard SSL) to the screenshotlayer API, ensuring encrypted datastreams between server and client.

To connect securely, simply append an `s` to the HTTP Protocol:

```url
https://api.screenshotlayer.com/api/capture?access_key=YOUR_ACCESS_KEY 
```

## API Error Codes

If your query fails, the screenshotlayer API will return a 3-digit error-code, an internal error type and a plain text "info" object containing suggestions for the user.

Find below an example error - triggered when the user did not provide a valid API Access Key:

```json
{
  "success": false,
  "error": {
    "code": 104,
    "type": "invalid_access_key",
    "info": "You have not supplied a valid API Access Key. [Technical Support: support@apilayer.net]"    
  }
}
```

### Common API errors:

| Type | Message  | Description |
|------------ |---------------| -----|
| 404 | "404_not_found" | User requested a resource which does not exist. |
| 101 | "missing_access_key" | User did not supply an Access Key. |
| 101 | "invalid_access_key" | User entered an invalid Access Key. |
| 103 | "invalid_api_function" | User requested a non-existend API Function. |
| 104 | "usage_limit_reached" | User has reached or exceeded his Subscription Plan's monthly API Request Allowance. |
| 210 | "invalid_url" | User provided an invalid website URL. |

[See all Error Types](https://screenshotlayer.com/documentation#error_codes)
