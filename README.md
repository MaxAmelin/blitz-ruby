## ![blitz.io](http://blitz.io/images/logo2.png)

Make load and performance a fun sport.

* Run a sprint from around the world
* Rush your API and website to scale it out
* Condition your site around the clock

## Getting started

Login to [blitz.io](http://blitz.io) and open blitz keys tab:
https://blitz.io/to#/settings/blitz_keys/api_key

Now
    gem install blitz
    
and run a sprint like this:
    blitz curl --region california http://blitz.io
    
and you can rush like this:
    blitz curl --region california --pattern 1-100:60 http://blitz.io
    
## Using the couch:fuzz command
Simply point this blitz gem to your CouchDB URL and we'll auto generate
full parameterized tests that you can use to measure view performance.

    blitz http://localhost:5984 my_database
    
will generate tests like this:

    -v:l number[1,10] -v:gl number[1,5] http://dell-5:5984/my_database/_design/pcaps/_view/by_service?group=true&limit=#{l}&group_level=#{gl}
    -v:sk alpha[4,12] -v:ek alpha[4,12] -v:l number[1,10] -v:id [true,false] http://dell-5:5984/my_database/_design/pcaps/_view/indexed?startkey=%22am#{sk}%22&endkey=%22ykz#{ek}%22&include_docs=#{id}&limit=#{l}
    
which you can simply copy/paste to the [blitz.io](http://blitz.io). Your
CouchDB must be on the public cloud though.

## Using blitz gem on your application

You can integrate blitz gem to your application and run tests whenever you want.

### Sprint

```ruby
require 'blitz'

...

result = Blitz::Curl.parse('-r california www.example.com').execute
```

### Rush

```ruby
require 'blitz'

...

result = Blitz::Curl.parse('-r california -p 10-50:30 www.example.com').execute do |partial|
    pp [ partial.region, partial.timeline.last.hits ]
end
```

Copyright (c) 2011 Mu Dynamics. See LICENSE.txt for further details.
