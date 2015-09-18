###This tutorial is not complete yet


# asmallorange.com Sinatra
This is a list of steps or reminder :) to create a Sinatra app on asmallorange shared hosting server. These steps are adapted from https://kb.asmallorange.com/customer/portal/articles/1603613-get-ruby-on-rails-up-and-running?b_id=4859


# Steps

1.	Login to ssh
	*	`ssh your_user_name@your_website_ip` like `ssh jonhdoe@12.345.67.890`
	* type `pwd` and make sure that you are on `home/your_user_name`
2.  Setup the LANG environment variable so there's proper UTF-8 support:
	* If you had already done this current step when you had created a previous Ruby on Rails app on the server, then skip this step
	*	`echo "export LANG=en_US.UTF-8" >> ~/.bashrc`
	*	`source ~/.bashrc`
3.  Retrieve your shared hosting server ruby version
	*	`ruby --version`
4. 	Create a dir for the project
	*	`mkdir sinatra-blog && cd sinatra-blog`
5.  Create a Gemfile
```ruby
# Gemfile

source 'https://rubygems.org'

gem "sinatra"
gem 'sinatra-flash'
gem 'sinatra-redirect-with-flash'
gem 'bcrypt', '~> 3.1.10'

#for db
# I'm installing 2 ORM I don't know yet which one is better
gem "activerecord"
gem "sinatra-activerecord"
gem 'datamapper', '~> 1.2.0'
gem 'dm-sqlite-adapter', '~> 1.2.0'

group :development do
 gem 'sqlite3'
 gem "tux"
end

group :production do
 #gem 'pg' #not available on asmallorange.com
 gem 'sqlite3'
 #or
 gem 'dm-mysql-adapter', '~> 1.2.0'
end
```
1. 	Create a public folder
	*	`mkdir public`
2. 	Create a file named `app.rb`
```ruby
require 'sinatra'
set :root, File.dirname(__FILE__)
set :public_folder, Proc.new { File.join(root, "public") }


get "/" do
  "hello world"
end

get "/hello/:name" do
  "Hello #{params['name']}"
end
```
3. 	Inside the folder `public` create an .htaccess file
```ruby
PassengerRuby /usr/local/bin/ruby
PassengerAppRoot /home/wadiyabi/sinatra-blog
RailsBaseURI /sinatra-blog
```




## Contributing

1. Fork it ( https://github.com:guinslym/aso_up_and_running.git )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request

