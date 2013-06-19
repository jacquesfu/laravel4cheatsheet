# Laravel Cheat Sheet

This is a guide on how to setup and use laravel. 

** Installing Composer**

Run this in your terminal to get the latest Composer version and install it globally:

  $ curl -sS https://getcomposer.org/installer | php
	$ mv composer.phar /usr/local/bin/composer

**Installing Composer on Mac**

	$ su
	$ curl -s getcomposer.org`/installer `| php -d detect_unicode=Off
	$ mv composer.phar /usr/local/bin/composer

## Quick Install

** Installing Laravel with Composer on Mac**
This will create a subfolder called your-project-name.
Update the `php.ini` to enable mcrypt and reboot.
$ composer create-project laravel/laravel your-project-name
> Added `composer create-project laravel/laravel your-project-name --prefer-source` to get the above to work.


** Installing Laravel with GIT**
Or, you may also download a copy of the repository from Github. Next, afterinstalling Composer, run the `composer install` command in the root of your project directory. This command will download and install the framework's dependencies.
> Added `composer install --prefer-source` to get the above to work.

## Configuration
> This setup assumes your web server is **Apache** and is setup and running.

* Ensure `/storage` is writeable
* Update url in `application/config/application.php`
* Add `.htaccess` file in `/public`
* If using git, add the following to .gitignore
* php artisan key:generate

**MySQL Setup**

	GRANT ALL PRIVILEGES
	ON database_name.*
	TO user_name@'%'
	IDENTIFIED BY 'password';

	iptables -I INPUT -p tcp --dport 3306 -j ACCEPT // open port 80
	service iptables save // save firewall rules


## Simple Database
Path: app/config/database.php

	$results = DB::select('select * from users where id = ?', array(1));
	DB::insert('insert into users (id, name) values (?, ?)', array(1, 'Dayle'));
	DB::update('update users set votes = 100 where name = ?', array('John'));
	DB::delete('delete from users');

## Routes
Path: app/routes.php
	
**Static Views**

	// route with callback to anonymous function
	Route::get('users', function() {
		return View::make('users');
	});

**Controller Route**

	// route to controller
	Route::get('user/{id}', 'UserController@showProfile'); 

## Views (Blade)
Path: app/*.blade.php

**layout.blade.php**

	<html>
	@yield('content') - create a content section
	</html>

**view.blade.php**

	@extends('layout')
	@section('content')
	Any HTML goes here
	@stop

**Conditional**

	@if (count($records) === 1)
	I have one record!
	@elseif (count($records) > 1)
	I have multiple records!
	@else
	I don't have any records!
	@endif

**Loops**

	@for ($i = 0; $i < 10; $i++)
	The current value is {{ $i }}
	@endfor
	
	@foreach ($users as $user)
	<p>This is user {{ $user->id }}</p>
	@endforeach
	
	@while (true)
	<p>I'm looping forever.</p>
	@endwhile

## Controllers

	class UserController extends BaseController {
		public function showProfile($id) {
		$user = User::find($id);
		return View::make('user.profile', array('user' => $user));
		}
	}
	$action = Route::currentRouteAction(); // get current controller action
	$url = URL::action('FooController@method'); // generate a url to a controller

## Models (Eloquent ORM)

TBD
