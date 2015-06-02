# Ruby

## Capture Snapshots via Ruby:

Find below a Ruby function that lets you capture a screenshot and define all required and optional parameters:

```php
require 'cgi' unless defined?(CGI)
require 'digest' unless defined?(Digest)
 
def screenshotlayer(url, options={})
    
  # set access key
  access_key = 'YOUR_ACCESS_KEY'
  
  # set secret keyword (defined in account dashboard)
  secret_keyword = 'YOUR_SECRET_KEYWORD'
 
  # define parameters
  parameters = {
    :url       => url,
    :fullpage  => options[:fullpage],
    :width  => options[:width],
    :viewport  => options[:viewport],
    :format  => options[:format],
    :css_url  => options[:css_url],
    :delay  => options[:delay],
    :ttl  => options[:ttl],
    :force  => options[:force],
    :placeholder  => options[:placeholder],
    :user_agent  => options[:user_agent],
    :accept_lang  => options[:accept_lang],
    :export  => options[:export],
  }
   
  query = parameters.
    sort_by {|s| s[0].to_s }. 
    select {|s| s[1] }.       
    map {|s| s.map {|v| CGI::escape(v.to_s) }.join('=') }.
    join('&')
  
  # generate md5 secret key
  secret_key = Digest::MD5.hexdigest(url + secret_keyword)
 
  "https://api.screenshotlayer.com/api/capture?access_key=#{access_key}&secret_key=#{secret_key}&#{query}"
end
 
# set url (required), optional parameters (leave blank if unused) & call function
puts screenshotlayer("www.cnn.com",{ 
    fullpage: "", 
    width: "", 
    viewport: "", 
    format: "", 
    css_url: "", 
    delay: "", 
    ttl: "", 
    force: "", 
    placeholder: "", 
    user_agent: "", 
    accept_lang: "", 
    export: "" })                   
```

**Please note**: Optional parameters may be left blank if they are not being used.
