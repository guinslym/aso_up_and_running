# asmallorange.com Ruby on Rails
This is a list of steps or reminder :) to create a Ruby on Rails app on asmallorange shared hosting server. These steps are adapted from https://kb.asmallorange.com/customer/portal/articles/1603613-get-ruby-on-rails-up-and-running?b_id=4859


# Steps

1.	Login to ssh
	*	I'm using Unix or a Unix-like computer
	*	`ssh your_user_name@your_website_ip` like `ssh jonhdoe@12.345.67.890`
	* type `pwd` and make sure that you are on `home/your_user_name`
2.  Setup the LANG environment variable so there's proper UTF-8 support:
	*	echo "export LANG=en_US.UTF-8" >> ~/.bashrc
	*	source ~/.bashrc
4. 	Create a new Ruby on Rails application
	*	`rails new newapp`
	*	`cd newapp`
	*	`rails g controller welcome index`
	*	Open `config/routes.rb` and uncomment the line `#root "welcome#index"` so that it will look `root "welcome#index"`
5.  Link your Rails application into your web directory so that you may access the Rails application on your website:
	*	`cd ~/public_html`
​	*	`ln -s ../newapp/public newapp`
6. 	Go back to your app and create a `.htaccess` file with this content
	*	`cd -`
	* vim public/.htaccess
```php
PassengerRuby /usr/local/bin/ruby
PassengerAppRoot /home/username/newapp
RailsBaseURI /newapp
```
7. 	Create models on your app
	*	`rails g scaffold student name age:integer`
	*	Open up `db/seed.rb` and add this content
```ruby
names = ['Sandra', 'Chris', 'Matt', 'Stephanie', 'Judy']
30.times do 
	Student.create(
		name: names.sample,
		age: Random.rand(17) + 18
	)
end
```
8.	type on your command line (terminal) 
	*	`rake db:create db:migrate db:seed`
9. 	Refresh your application 
	*	`touch tmp/restart.txt`
10. Go to  `http://www.example.com/newapp` or `http://www.example.com/students` 


## Todo
1. Create a wiki instead

## Contributing

1. Fork it ( https://github.com:guinslym/asmallorange_app_up_and_running.git )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request

