# Docker Compose - Rails new template

Simple change my_app_name to well your app name!

```bash
git clone https://github.com/thinkidea/docker-compose-rails-template my_app_name && cd my_app_name && rm -rf .git && rm README.md
docker-compose run --no-deps --rm app bundle exec rails new . --force --skip-bundle --skip-active-record
```

### Change the app name in

- config/application.rb

### Add Mongoid

Add the following to **Gemfile**

```ruby
gem 'mongoid'
```

```bash
docker-compose run --no-deps --rm app bundle install && bundle exec rails g mongoid:config
```

then run `docker-compose up` (and new gems will automatically be installed)

### Also

#### Whitelist your IP for the web console

To avoid warnings about blocked ip's in your server log and get the Rails web console working again, In your config/environments/development.rb, add the following line:

```ruby
def whitelisted_ip
  addrinfo = Socket.ip_address_list.detect(&:ipv4_private?)
  addrinfo.try(:ip_address).sub(/\.(\d{1,3})$/, '.0/16')
end

config.web_console.whitelisted_ips = whitelisted_ip
```

## LICENSE

The MIT License (MIT)

Copyright (c) 2020 Thinkidea Ltd

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
