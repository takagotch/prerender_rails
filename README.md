### prerender_rails
---
https://github.com/prerender/prerender_rails

```
export PRERENDER_SEVICE_URL=<new url>
heroku config:add PRERENDER_SERVICE_URL=<new url>


```


```ruby
gem 'prerender_rails'

config.middlewre.use Rack::Prerender
config.middleware.use Rack::Prerender, prerender_token: 'YOUR_TOKEN'

config.middleware.use Rack::Prerender, whitelist; '^/search'
config.middleware.use Rack::Prerender, whitelist: ['/serch', '/users/.*/profile']

config.middleware.use Rack::Prerender, blacklist: '^/search'
config.middleware.use Rack::Prerender, blacklist: ['/search', '/users/.*/profile']

config.middleware.use Rack::Prerender,
        before_render: (Proc.new do |env|
        end)
   
config.middleware.use Rack::Prerender,
        after_render: (Proc.new do |env, response|
        end)

config.middleware.use Rack::Prerender,
        build_rack_response_from_prerender: (Proc.new do |response, prerender_response|
        end)
        
config.middleware.use Rack::Prerender, protocol: 'https'

require 'redis'
@redis = Redis.new
config.middleware.use Rack::Prerender,
  before_render: (Proc.new do |env|
    @redis.get(Rack::Request.new(env).url)
  end)
  after_render: (Proc.new do |env, response|
    @redis.set(Rack::Request.new(env).url, response.body)
  end)
config.middleware.use Rack::Prerender, prerender_service_url: '&lt;new url>'
```

```
```
