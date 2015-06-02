
# PHP

## Capture Snapshots via PHP:

Find below a simple PHP function that lets you capture a screenshot and define all required and optional parameters:

```php
function screenshotlayer($url, $args) {

  // set access key
  $access_key = "YOUR_ACCESS_KEY";
  
  // set secret keyword (defined in account dashboard)
  $secret_keyword = "YOUR_SECRET_KEYWORD";

  // encode target URL
  $params['url'] = urlencode($url);

  $params += $args;

  // create the query string based on the options
  foreach($params as $key => $value) { $parts[] = "$key=$value"; }

  // compile query string
  $query = implode("&", $parts);

  // generate secret key from target URL and secret keyword
  $secret_key = md5($url . $secret_keyword);

  return "https://api.screenshotlayer.com/api/capture?access_key=$access_key&secret_key=$secret_key&$query";

}

// set optional parameters (leave blank if unused)
$params['fullpage']  = '';    
$params['width'] = '';      
$params['viewport']  = '';  
$params['format'] = '';      
$params['css_url'] = '';      
$params['delay'] = '';      
$params['ttl'] = '';  
$params['force']     = '';     
$params['placeholder'] = '';      
$params['user_agent'] = '';      
$params['accept_lang'] = '';      
$params['export'] = '';      

// capture
$call = screenshotlayer("google.com", $params);    
```

**Please note**: Optional parameters may be left blank if they are not being used.
