# API Features

## Full-Height Captures

By default, screenshots are rendered based on the height of the selected (or default) viewport. Alternatively, you can request the full height of the target website to be captured, simply by setting the API's `fullpage` parameter to `1`.

### Example Query:

```url
http://api.screenshotlayer.com/api/capture
    ? access_key = YOUR_ACCESS_KEY
    & url = http://www.cnn.com
    & fullpage = 1
```

## Thumbnails

By default, the screenshotlayer API returns your target website's snapshot in original size (1:1). If you'd like to request a thumbnail, append the API's width parameter containing your preferred thumbnail width in pixels.

### Example Query:

```url
http://api.screenshotlayer.com/api/capture
    ? access_key = YOUR_ACCESS_KEY
    & url = http://www.facebook.com
    & width = 350
```

## Viewport Control

The screenshotlayer API's default viewport setting is `1440x900`. You can specify a custom viewport by setting the `viewport` parameter to your desired dimensions. (format: `width x height`, in pixels)

#### Example Query:

```url
http://api.screenshotlayer.com/api/capture
    ? access_key = YOUR_ACCESS_KEY
    & url = http://www.tumblr.com
    & user_agent = Mozilla/5.0 (iPhone; CPU iPhone OS 8_0_2 like Mac OS X) AppleWebKit/600.1.4 (KHTML, like Gecko) Version/8.0 Mobile/12A366 Safari/600.1.4&viewport=375x667   
    & viewport = 375x667
```

**Important**: When requesting mobile-sized viewports (example above), it is highly recommended to also specify a `user_agent` parameter, as some websites (e.g. google.com) tend to ignore mobile viewports that come without specified HTTP User-Agent headers (See User-Agent parameter).

You can find a comprehensive [list of mobile viewport sizes here](http://viewportsizes.com/).



## Output Formats

Your snapshots can be requested in three different formats: **PNG**, **JPG** and **GIF**. You can change the default format (PNG) simply by appending the API's `format` parameter containing your preferred format.

### Example Query:

```url
http://api.screenshotlayer.com/api/capture
    ? access_key = YOUR_ACCESS_KEY
    & url = http://www.cnn.com
    & format = JPG
```

**Please note**: Output formats are not case sensitive, and appending "JPEG" is just as valid "JPG".


## URL Encryption

For those of you who have to display API request URLs on their website (e.g. inside an `<img src="...">` tag, it is crucial to make use of the screenshotlayer API's **URL Encryption** method, which lets you generate a unique **Secret Key** for every API request and simply append it to the respective query URL.

### Step 1: Define your target website's URL

First of all, define the URL of the website you want to take a snapshot of. In our example we will use the following URL:

```url
http://www.apple.com
```

### Step 2: Define your secret keyword

A secret keyword can be any secret word or phrase of your choice. As the next step, make sure you have defined it in your [account dashboard](https://screenshotlayer.com/dashboard).

```url
mysecretkeyword
```

### Step 3: Combine

Now you will need to combine these two parts (URL & secret keyword) into one, resulting in:

```url
http://www.apple.commysecretkeyword
```

### Step 4: Generate your md5 Secret Key

Finally, create an `md5 hash` of the combined parts. (this will be your `secret_key`)

```url
a9d09c5b1cda7e5ef51fed4526e9cff3
```

Now that you have your Secret Key, you can simply append to your query URL using the API's `secret_key` parameter and rest assured that your API access is - as long as you'll keep your secret keyword secret - safe from abuse.

### Syntax:

```url
http://api.screenshotlayer.com/api/capture
    ? access_key = YOUR_ACCESS_KEY
    & url = http://www.apple.com
    & secret_key = a9d09c5b1cda7e5ef51fed4526e9cff3
```

## CSS Injection

The screenshotlayer API enables you to inject a custom CSS stylesheet into the target website by appending an existing CSS file URL to the API's `css_url` parameter.

For our example we have prepared a file called **css_inject.css**, containing the following CSS declaration:

```css
body {
background: #00ff00 !important;
}
```

### Example Query:

```url
http://api.screenshotlayer.com/api/capture
    ? access_key = YOUR_ACCESS_KEY
    & url = http://www.youtube.com
    & css_url = https://screenshotlayer.com/downloads/css_inject.css
```

**Please note**: Attached CSS files must not exceed a file size of 100kB (around 100,000 characters)

## Capturing Delay

The API's `delay` parameter enables you to specify a custom delay time (in seconds) before the snapshot is captured. This feature may especially useful if certain contents of your target website appear after the initial page load. (e.g. CSS animations, JavaScript effects)

### Example Query:

The following query sets a delay time of 3 seconds in order to capture any delayed/animated contents on the target website. (http://tumblr.com)

```url
http://api.screenshotlayer.com/api/capture
    ? access_key = YOUR_ACCESS_KEY
    & url = http://www.tumblr.com
    & delay = 3
```

**Please note**: The maximum supported delay time is 20 seconds.

## TTL (Caching Time)

By default, website screenshots are cashed for 30 days (2,592,000 seconds). Using the API's ttl parameter, you can specify a custom caching time (time-to-live) lower than the default setting.

### Example Query:

The following query requests the snapshot's ttl to be set to 259,200 seconds (3 days).

```url
http://api.screenshotlayer.com/api/capture
    ? access_key = YOUR_ACCESS_KEY
    & url = http://www.tumblr.com
    & ttl = 259200
```

**Please note**:  The default ttl (30 days, or 2,592,000 seconds) is the maximum supported caching time.

## Force Refresh

You can easily force the API to capture a fresh screenshot of the requested target URL by appending the `force` parameter to the request URL and setting it to `1`.

### Example Query:

```url
http://api.screenshotlayer.com/api/capture
    ? access_key = YOUR_ACCESS_KEY
    & url = http://www.tumblr.com
    & force = 1
```

**Please note**: "Force Refresh" screenshots override all other existing snapshots of the respective target website.

## Placeholder image

For the very few seconds a freshly captured screenshot loads, there are two options for requesting a placeholder image:

### Option 1: Using the default placeholder

By appending the API's `placeholder` parameter and setting it to `1`, you can request the default screenshotlayer placeholder image.

### Option 2: Setting a custom placeholder image URL

f you prefer setting your own custom placeholder image, simply append it to the API's `placeholder` parameter as an image URL.

Supported file formats: PNG, JPEG, GIF

### Example query: (using option 1)

```url
http://api.screenshotlayer.com/api/capture
    ? access_key = YOUR_ACCESS_KEY
    & url = http://www.twitter.com
    & placeholder = 1
```

**Please note**: If activated, placeholder images are returned immediately after the API request and remain visible until the respective page is refreshed.

## HTTP User-Agent Headers

By default, the screenshotlayer API does not send any HTTP User-Agent headers with your request. You can specify a custom user-agent string by appending it to the API's `user_agent` parameter.

### Example Query

The following query requests a screenshot of http://facebook.com on mobile Safari (iOS 8.0.2, iPhone):

```url
http://api.screenshotlayer.com/api/capture
    ? access_key = YOUR_ACCESS_KEY
    & url = http://www.facebook.com
    & viewport = 375x667
    & user_agent = Mozilla/5.0 (iPhone; CPU iPhone OS 8_0_2 like Mac OS X) AppleWebKit/600.1.4 (KHTML, like Gecko) Version/8.0 Mobile/12A366 Safari/600.1.4   
```

You can find a comprehensive [list of user-agent strings here](http://www.useragentstring.com/pages/useragentstring.php).

## HTTP Accept-Language Headers

The default HTTP Accept-Language header is `en-US`, en (US English, or English in general). You can specify a custom Accept-Language header by appending it to the API's `accept_lang` parameter.

### Example Query

The following query requests a screenshot of http://facebook.com in Spanish:

```url
http://api.screenshotlayer.com/api/capture
    ? access_key = YOUR_ACCESS_KEY
    & url = http://www.facebook.com
    & accept_lang = es
```

You may also specify several different languages at once. Each additional language is separated by a comma. The order in which the values appear in the header determine the hierarchy of importance.

In the following example `es-MX` (Spanish, Mexico) is the hightest priority, followed by general Spanish and general English:

```url
es-MX,es,en
```

You can find a comprehensive [list of Accept-language strings here](http://www.metamodpro.com/browser-language-codes).

## Export to AWS S3

If you are subscribed to the Professional or Enterprise Plan, you may request the API to directly export your snapshot to your **AWS S3 Bucket**. This can be done simply by appending your S3 Bucket path (format: `s3://API_KEY:API_SECRET@bucket`) to the API's export parameter.

### Example Query

Find below an example query requesting the API to export a screenshot of http://tumblr.com directly to a specified AWS S3 Bucket.

```url
http://api.screenshotlayer.com/api/capture
    ? access_key = YOUR_ACCESS_KEY
    & url = http://www.tumblr.com
    & export = s3://DHSJ2HDGALIIDHSJDGAH:7SH6s7Sw9DKSH7h8Zs9Bw9DKSSH7h86s7Sw9Bw9D@mybucket.test/path/to  
```

**Important**: Uploading your snapshot to the given S3 path may take up to 1 minute to complete. Please be aware that our system can only attempt accessing the specified export path and cannot notify you in case your upload fails.

## Export to FTP

Professional and Enterprise Customers may also specify a custom `ftp` path to directly export captured snapshots to. This can be achieved simply by appending your desired FTP path (format: `ftp://user:password@server`) to the API's `export` parameter.

### Example Query

Find below an example query requesting the API to export a screenshot of http://tumblr.com directly to a specified FTP path.

```url
http://api.screenshotlayer.com/api/capture
    ? access_key = YOUR_ACCESS_KEY
    & url = http://www.tumblr.com
    & export = ftp://myusername:mypassword@123.12.12.1/path/to    
```

**Important**: Uploading your snapshot to the given S3 path may take up to 1 minute to complete. Please be aware that our system can only attempt accessing the specified export path and cannot notify you in case your upload fails.




