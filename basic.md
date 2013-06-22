# Laravel 4 Cheat Sheet

This is a quick reference for Laravel 4. 

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

## Views (Blade Templates)
Path: app/*.blade.php

	$view = View::make('users', array('name'=>'John') );

**layout.blade.php**

	<html><h1>Title</h1>
	@yield('content') - create a content section
	</html>

**view.blade.php**

	@extends('layout')
	@section('content')
	Any content that goes here will be use the layout.blade.php template.
	@stop

**Control Flow**

	// conditional
	@if (count($records) === 1)
	I have one record!
	@elseif (count($records) > 1)
	I have multiple records!
	@else
	I don't have any records!
	@endif

	// loops
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
Path: app/controllers/*.php

	class UserController extends BaseController {
		public function showProfile($id) {
		$user = User::find($id);
		return View::make('user.profile', array('user' => $user));
		}
	}
	$action = Route::currentRouteAction(); // get current controller action
	$url = URL::action('FooController@method'); // generate a url to a controller

## Models (Eloquent ORM)
Path: app/models/*.php

	class User extends Eloquent {
	    	protected $table = 'my_users'; // override default behavior (class = table)
		protected $hidden = array('password');   // hide attributes
	}
