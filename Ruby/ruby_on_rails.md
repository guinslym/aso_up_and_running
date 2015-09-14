# asmallorange.com Ruby on Rails
This is a list of steps or reminder :) to create a Ruby on Rails app on asmallorange shared hosting server. These steps are adapted from https://kb.asmallorange.com/customer/portal/articles/1603613-get-ruby-on-rails-up-and-running?b_id=4859


# Steps

1.	Login to ssh
	*	`ssh your_user_name@your_website_ip` like `ssh jonhdoe@12.345.67.890`
	* type `pwd` and make sure that you are on `home/your_user_name`
2.  Setup the LANG environment variable so there's proper UTF-8 support:
	* If you had already done this current step when you had created a previous Ruby on Rails app on the server, then skip this step
	*	`echo "export LANG=en_US.UTF-8" >> ~/.bashrc`
	*	`source ~/.bashrc`
4. 	Create a new Ruby on Rails application
	*	`rails new newapp`
	*	`cd newapp`
	*	`rails g controller welcome index`
	*	Open `config/routes.rb` and uncomment the line `#root "welcome#index"` so that it will look `root "welcome#index"`
5.  Link your Rails application into your web directory so that you may access the Rails application on your website:
	*	`cd ~/public_html`
	*	`ln -s ../newapp/public newapp`
6. 	Go back to your app and create a `.htaccess` file with this content
	*	`cd -`
	* `vim public/.htaccess`
```php
PassengerRuby /usr/local/bin/ruby
PassengerAppRoot /home/username/newapp
RailsBaseURI /newapp
```
7. 	Create models on your app
	*	`rails g scaffold student name age:integer`
	*	Open up `db/seed.rb` and add this content
	* `vim db/seed.rb`
```ruby
names = ['Sandra', 'Chris', 'Matt', 'Stephanie', 'Judy']
30.times do 
	Student.create(
		name: names.sample,
		age: Random.rand(17) + 18
	)
end
```
8.	type in your command line (terminal) 
	*	`rake db:create db:migrate db:seed`
9. 	Refresh your application 
	*	`touch tmp/restart.txt`
10. Go to  `http://www.example.com/newapp` or `http://www.example.com/students` 

##Notes
1.  You cannot necessarly add gems on your Gemfile and `bundle install` them. To do so 
	*	Add your gems (i.e : `gem 'bereshit', '~> 0.0.6'`)
	* Contact the tech support so that they will do a `bundle install`
	* If you create other Ruby on Rails applications using the same gems, there is no need to contact the tech support because the gems are already install globally on the server. You can `bundle install` install it yourself
2. 	To view the lists of all the gems that are installed on the server don't type `gem query --local` or `ruby -S gem list --local`. It will only show a partial list of gems
	* you can list this directory to view the gems installed on your server
	* `ls /usr/local/rubies/ruby-1.9.3/lib/ruby/gems/1.9.1/gems/`


## Todo
1. Add step for deploying on the root as `http://www.example.com/` instead of `http://www.example.com/newapp`
2. Add step for `capistrano` or `mina` or `puma`
3. Create a wiki instead

## Contributing

1. Fork it ( https://github.com:guinslym/aso_up_and_running.git )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request

