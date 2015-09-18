# asmallorange.com Ruby on Rails
This is a list of steps or reminder :) to create a Sinatra app on asmallorange shared hosting server. These steps are adapted from https://kb.asmallorange.com/customer/portal/articles/1603613-get-ruby-on-rails-up-and-running?b_id=4859


# Steps

A.	Login to ssh
	*	`ssh your_user_name@your_website_ip` like `ssh jonhdoe@12.345.67.890`
	* type `pwd` and make sure that you are on `home/your_user_name`
B.  Setup the LANG environment variable so there's proper UTF-8 support:
	* If you had already done this current step when you had created a previous Ruby on Rails app on the server, then skip this step
	*	`echo "export LANG=en_US.UTF-8" >> ~/.bashrc`
	*	`source ~/.bashrc`
C.  Retrieve your shared hosting server ruby version
	*	`ruby --version`
D. 	Create a dir for the project
	*	`mkdir sinatra-blog && cd sinatra-blog`
E.  Create a Gemfile
```ruby
 Gemfile

source 'https://rubygems.org'
ruby "1.9.3" #or whatever your ruby version

gem "sinatra"
gem "activerecord"
gem "sinatra-activerecord"
gem 'sinatra-flash'
gem 'sinatra-redirect-with-flash'
gem 'dm-sqlite-adapter', '~> 1.2.0'

gem 'datamapper', '~> 1.2.0'

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


## Contributing

1. Fork it ( https://github.com:guinslym/aso_up_and_running.git )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request

