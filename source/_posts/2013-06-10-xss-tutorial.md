---
layout: post
title: XSS Tutorial
date: 2013-06-10 08:25
comments: true
---

### Introduction

An XSS attack allows an attacker to run client-side scripts on webpages viewed by other users. In this article, you'll learn about the different types of XSS attacks, apply these attacks in your own demo page, and learn how to prevent them. I'd recommend you set these test pages up on your own servers to understand them better. A quick Google search will get you started with that.

<!--more-->

## Basic XSS Example 

Imagine I'm adding search functionality to my site. My search page looks something like the following,

		<html>
		   <body>
    	      <form>
      	         <input type="text" name="query">
      	         <input type="submit">
    	      </form>
  		   </body>
		</html>

Now when the user types in a search query and clicks submit, the form is posted to the page and a PHP script processes the query,

	<html>
	  <body>
	    <form>
	      <?php
	        if (array_key_exists('query', $_GET)) {
	          $query = $_GET['query'];
	          echo 'Displaying search results for query: ' . $query . '<br>';
	        }
	      ?>
	      <input type="text" name="query">
	      <input type="submit">
	    </form>
	  </body>
	</html>
	
Try this out on a test page and see what happens. When you search for something like "Gulshan Singh", you get a webpage that says, "Displaying search results for query: Gulshan Singh". Now enter the query "`<b>Gulshan Singh</b>`" instead. You should still see the same text displayed on the page, but now the text "Gulshan Singh" should be in bold. What happened? Take a look at the HTML source of the resulting page. The exact text we enter into the search box gets written to the page, meaning that we can write our own HTML, and consequently our own JavaScript, to the page.

So what malicious JavaScript could we execute on this page? One common XSS attack is cookie theft. Go back to the test page and search for `<script>document.cookie="username=gsingh";alert(document.cookie);</script>`. If you're using a browser that doesn't protect against XSS attacks at the time of this writing (Firefox, IE, but not Chrome), then you should see an alert box popup with the text `"username=gsingh"`. By using XSS, you were able to access and display your cookies. In theory, the script could do much more. It could send the cookies in an email to any email account, or instead of messing with cookies, it could run a script that could DDOS attack any site you wanted it to. Note that Chrome prevents XSS attacks, so in order to get the test page to work with Chrome you need to put the following code at the top of the page,

	<?php
		header('X-XSS-Protection: 0');
	?>
	
This sends an HTTP Header to the server to disable XSS filtering. In real world scenarios we obviously can't do this, and we're left to look for other security holes.

You may be wondering how any of this will help if you can only insert the malicious XSS vector into your own browser. Search something on our test page and look at the URL. Our query is in the page URL since we're using an HTTP GET request, and so we can send this URL to anyone and have the JavaScript execute on their page.