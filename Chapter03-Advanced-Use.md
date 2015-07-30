#Advanced Use
##Filters
　　Filters let you use other languages within a jade template. They take a block of plain text as an input.  
　　All JSTransformers can be used as jade filters. Popular filters include `:coffee-script`, `:babel`, `:uglify-js`, `:less`, and `:markdown-it`.
###Template engines
* atpl: Compatible with twig templates
* coffeecup: Pure CoffeeScript templates (fork of coffeekup)
* dot: Focused on speed
* dust: Asynchronous templates
* eco: Embedded CoffeeScript templates
* ect: Embedded CoffeeScript templates
* ejs: Embedded JavaScript templates
* haml: Dry indented markup
* haml-coffee: This is haml with embedded CoffeeScript
* handlebars: Extension of mustache templates
* hogan: mustache templates
* jade: Robust, elegant, feature-rich template engine
* jazz
* jqtpl: Extensible logic-less templates
* JUST: EJS style template with some special syntax for layouts/partials among others
* liquor: Extended EJS with significant whitespace
* mustache: Logic-less templates
* QEJS: Promises and EJS for async templating
* swig: Django-like templating engine
* templayed: mustache focused on performance
* toffee: Templating language based on CoffeeScript
* underscore
* walrus: A bolder kind of mustache
* whiskers: Logic-less focused on readability

###Stylesheet languages
* less: This extends CSS with dynamic behaviors such as variables, mixins, operations, and functions
* stylus: Revolutionary CSS generator making braces optional
* sass: Sassy CSS

###Minifiers
* uglify-js: No need to install anything, just minifies/beautifies JavaScript
* uglify-css: No need to install anything, just minifies/beautifies CSS
* uglify-json: No need to install anything, just minifies/beautifies JSON

###Others
* cdata: With cdata we don't need to install anything, it just wraps input as `<![CDATA[${INPUT_STRING]]>` with the standard escape for `]]>(]]]]><![CDATA[>)`
* cdata-js: This is the same as cdata, but with surrounding comments
suitable for inclusion into a HTML/JavaScript `<script>` block:
`//<![CDATA[\n${INPUT_STRING\n//]]>`
* cdata-css: This is the same as cdata, but with surrounding comments
suitable for inclusion into a HTML/CSS `<style>` block: `/*<![CDATA[*/\n${INPUT_STRING\n/*]]>*/`
* verbatim: With verbatim, there's no need to install anything, it acts as a verbatim pass-through `${INPUT_STRING}`
* coffee-script: A little language that compiles into JavaScript
* cson: This is a coffee-script-based JSON format
* markdown: You can use marked, supermarked, markdown-js, or markdown
* component-js: npm install component-builder options: `{development: false}`
* component-css: npm install component-builder options: `{development: false}`
* html2jade: Converts HTML back into Jade: npm install html2jade

　　You need to install the individual language
compilers for most of the transformers, but they're usually pretty easy to install
because they're almost all contained in npm modules like the Jade compiler
>Filters are compile time. This makes them fast but means they cannot support dynamic content.

>Built in filters are not available in the browser as they would not all work. Providing you compile your templates server side, they will still work fine though.

	:markdown
	  # Markdown

	  I often like including markdown documents.
	script
	  :coffee-script
	    console.log 'This is coffee script'
-->

	<h1>Markdown</h1>
	<p>I often like including markdown documents.</p>
	<script>console.log('This is coffee script')</script>

##Blocks
Blocks function like small containers for Jade. Their content can be appended to, prepended to, or replaced entirely. To define a block, simply use the `block` keyword, and then the name of the block, as shown:

	block scripts
		script(src='jquery.js')
-->  `<script src="jquery.js"></script>`

By default, a block will just output the nested content.

	layout.jade:
		doctype
		html
			head
				block scripts
					script(src='jquery.js')
				block styles
			body
				block content
					p there's no content here
-->

	<!DOCTYPE html>
	<html>
		<head>
			<script src="jquery.js"></script>
		</head>
		<body>
			<p>there's no content here</p>
		</body>
	</html>
###Blocks don't provide encapsulation
Variables defined in blocks can be accessed outside of blocks.

	block example
		- variable_from_a_block = 'I was defined inside a block'
	p=variable_from_a_block
--> `<p>I was defined inside a block</p>`

##Inheritance
Jade supports template inheritance via the `block` and `extends` keywords. A block is simply a "block" of Jade that may be replaced within a child template. This process is recursive.

###Append
We could simplify this example by using the `append` keyword. You could decide to write `block append` rather than just `append`.

	layout.jade:
	doctype
	html
		head
			block scripts
				script(src='jquery.js')
			block styles
		body
			block content
				p there's no content here

	page2.jade (in the same directory as layout.jade)
	
	extends layout
	append scripts
		script(src='underscore.js')
	block content
-->

	<!DOCTYPE html>
	<html>
		<head>
			<script src="jquery.js"></script>
			<script src="underscore.js"></script>
		</head>
	<body></body>
	</html>
	
###Prepend
The `prepend` keyword does the exact opposite of the `append` keyword, and also has a longer variant: `block prepend`. It is useful when you want to add something to the beginning of a block.

	page3.jade (in the same directory as layout.jade)
	
	extends layout
	prepend scripts
		script(src='underscore.js')
	block content
-->

	<!DOCTYPE html>
	<html>
		<head>
			<script src="underscore.js"></script>
			<script src="jquery.js"></script>
		</head>
		<body></body>
	</html>

##Extends
The `extends` keyword allows a template to extend a layout or parent template. It can then override certain pre-defined blocks of content.

	//- layout.jade
	doctype html
	html
	  head
	    block title
	      title Default title
	  body
	    block content
	    
	//- index.jade
	extends ./layout.jade

	block title
	  title Article Title

	block content
	  h1 My Article
-->

	<!doctype html>
	<html>
	  <head>
	    <title>Article Title</title>
	  </head>
	  <body>
	    <h1>My Article</h1>
	  </body>
	</html>
>You can have multiple levels of inheritance, allowing you to create powerful hierarchies of templates.

###Incompatibility
It is worth noting that blocks are evaluated during compilation, so they will not work with render-time logic such as `if/else` statements.

	if true
		extends layout1
	else
		extends layout2

##Includes
Includes allow you to insert the contents of one jade file into another.

	//- index.jade
	doctype html
	html
	  include ./includes/head.jade
	  body
	    h1 My Site
	    p Welcome to my super lame site.
	    include ./includes/foot.jade

	//- includes/head.jade
	head
	  title My Site
	  script(src='/javascripts/jquery.js')
	  script(src='/javascripts/app.js')
	  
	//- includes/foot.jade
	#footer
	  p Copyright (c) foobar
-->

	<!doctype html>
	<html>
	  <head>
	    <title>My Site</title>
	    <script src='/javascripts/jquery.js'></script>
	    <script src='/javascripts/app.js'></script>
	  </head>
	  <body>
	    <h1>My Site</h1>
	    <p>Welcome to my super lame site.</p>
	    <div id="footer">
	      <p>Copyright (c) foobar</p>
	    </div>
	  </body>
	</html>
###Including Plain Text
Including files that are not jade just includes the raw text.

	//- index.jade
	doctype html
	html
	  head
	    style
	      include style.css
	  body
	    h1 My Site
	    p Welcome to my super lame site.
	    script
	      include script.js

	/* style.css */
	h1 { color: red; }
	
	// script.js
	console.log('You are awesome');
-->

	<!doctype html>
	<html>
	  <head>
	    <style>
	      /* style.css */
	      h1 { color: red; }
	    </style>
	  </head>
	  <body>
	    <h1>My Site</h1>
	    <p>Welcome to my super lame site.</p>
	    <script>
	      // script.js
	      console.log('You are awesome');
	    </script>
	  </body>
	</html>

###Including Filtered Text
You can combine filters with includes to filter things as you include them.

	//- index.jade
	doctype html
	html
	  head
	    title An Article
	  body
	    include:markdown article.md

	//- article.md
	# article.md
	This is an article written in markdown.
-->

	<!doctype html>
	<html>
	  <head>
	    <title>An Article</title>
	  </head>
	  <body>
	    <h1>article.md</h1>
	    <p>This is an article written in markdown.</p>
	  </body>
	</html>

##Mixins
Mixins are small, encapsulated pieces of code that are reusable throughout the template.  
###Defining mixins
Mixin definitions don't output any HTML and are defined using the following syntax.  

	mixin book(name, price)
		li #{name} for #{price}

In the preceding code snippet, `book` is the name of the mixin, and `name` and `price` are both named arguments. The indented block of Jade gets executed in its own scope, where the variables `name` and `price` are passed. So basically, it works just like you would expect a function to work.

###Calling mixins
The syntax for calling mixins is also similar to that of function calls, except we prefix the function name with a + symbol to say that it isn't a tag (which can look quite similar).

	ul#books
		+book("Book A", 12.99)
		+book("Book B", 5.99)
-->

	<ul id="books">
		<li>Book A for 12.99 €</li>
		<li>Book B for 5.99 €</li>
	</ul>

Simpler mixins don't even need to accept arguments and can even be called without args:

	mixin copyleft
		| (&#596;)
	p
		+copyleft
		| - Sean Lang - 2013
--> `<p>(&#596;) - Sean Lang - 2013</p>`
###Passing blocks
Besides just being able to pass arguments, you can also pass entire blocks to a mixin, as shown in the following code snippet:

	mixin input(name)
		li(id=name.replace(/\s/g, '-'))
			label= name + ':'
			block
			
	form: ul
		+input('favorite color')
			input('type'='text')
		+input('comments')
			textarea Type your comment here.
-->

	<form>
		<ul>
			<li id="favorite-color">
				<label>favorite color:</label>
				<input type="text">
			</li>
			<li id="comments">
				<label>comments:</label>
				<textarea>Type your comment here.</textarea>
			</li>
		</ul>
	</form>
The block that will be passed to the mixin is whatever indented block comes after the mixin call. It is just like the way in which whatever indented block comes after a tag is nested in that tag, except here they are passed to the mixin. In this case, `input('type'='text')` and `textarea Type your comment here.` are the passed blocks. Inside the mixin, the `block` keyword tells Jade where to put the contents of
the block that is passed to it.
>that interpolation doesn't work in the arguments used to call a mixin.

###The arguments object
Just as the `arguments` object is a local variable available in JavaScript objects, it is available in Jade mixins. In fact, it is used frequently in Jade to make mixins that accept a variable number of args.

	mixin list()
		ul
			- var args = Array.prototype.slice.call(arguments);
			for item in args
				li= item
	+list('one', 'two', 'three')
-->

	<ul>
		<li>one</li>
		<li>two</li>
		<li>three</li>
	</ul>
