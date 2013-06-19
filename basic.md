# Laravel Cheat Sheet

This is a guide on how to setup and use laravel. 

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
