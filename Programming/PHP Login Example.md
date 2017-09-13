<!-- permalink: b58b4dd09982f702a245236d12ed90d0 DO NOT DELETE OR EDIT THIS LINE -->
# PHP Login

* login.php:

		<?php
		   ob_start();
		   session_start();
		?>

		<?
		   // error_reporting(E_ALL);
		   // ini_set("display_errors", 1);
		?>

		<?php
		   $msg = '';

		$loggedIn = false;

		   if (isset($_POST['login']) && !empty($_POST['username']) && !empty($_POST['password'])) {

			  if ($_POST['username'] == 'tutorialspoint' && $_POST['password'] == '1234') {
				 $_SESSION['valid'] = true;
				 $_SESSION['timeout'] = time();
				 $_SESSION['username'] = 'tutorialspoint';
				 $loggedIn = true;

				 $msg = 'You have entered valid use name and password';
			  } else {
				 $msg = 'Wrong username or password';
			  }
		   }
		?>

		<html lang = "en">

		   <head>
			  <title>Tutorialspoint.com</title>
		   </head>

		   <body>

			  <h2>Enter Username and Password</h2>

			  <div class = "container">

		<?php

		if ($loggedIn == true) {
			print 'Click here to clean <a href = "logout.php" tite = "Logout">Session.</a>';
		} else {
			$serverSelf = htmlspecialchars($_SERVER['PHP_SELF']);
			print '<form class = "form-signin" role = "form" action="' . "$serverSelf" . '" method = "post">
				<h4 class = "form-signin-heading">' . "$msg" . '</h4>
				<input type = "text" class = "form-control" name = "username" placeholder = "username = tutorialspoint" required autofocus></br>
				<input type = "password" class = "form-control" name = "password" placeholder = "password = 1234" required></br>
				<button class = "btn btn-lg btn-primary btn-block" type = "submit" name = "login">Login</button>
			</form>';
		}

		?>
			  </div>

		   </body>
		</html>


* logout.php


		<?php
		   session_start();
		   unset($_SESSION["username"]);
		   unset($_SESSION["password"]);

		   echo 'You have cleaned session';
		   header('Refresh: 2; URL = login.php');
		?>


* [reference](http://www.tutorialspoint.com/php/php_login_example.htm) - note that it was pretty much ripped from this link, just edited for clarity
