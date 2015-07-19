#Advanced Use
##Filters
　　Filters let you use other languages within a jade template. They take a block of plain text as an input.  
　　All JSTransformers can be used as jade filters. Popular filters include `:coffee-script`, `:babel`, `:uglify-js`, `:less`, and `:markdown-it`.
###Template engines
* atpl: Compatible with twig templates* coffeecup: Pure CoffeeScript templates (fork of coffeekup)* dot: Focused on speed* dust: Asynchronous templates* eco: Embedded CoffeeScript templates* ect: Embedded CoffeeScript templates
* ejs: Embedded JavaScript templates* haml: Dry indented markup* haml-coffee: This is haml with embedded CoffeeScript* handlebars: Extension of mustache templates* hogan: mustache templates* jade: Robust, elegant, feature-rich template engine* jazz* jqtpl: Extensible logic-less templates* JUST: EJS style template with some special syntax for layouts/partials among others* liquor: Extended EJS with significant whitespace* mustache: Logic-less templates* QEJS: Promises and EJS for async templating* swig: Django-like templating engine* templayed: mustache focused on performance* toffee: Templating language based on CoffeeScript* underscore* walrus: A bolder kind of mustache* whiskers: Logic-less focused on readability

###Stylesheet languages
* less: This extends CSS with dynamic behaviors such as variables, mixins, operations, and functions* stylus: Revolutionary CSS generator making braces optional* sass: Sassy CSS

###Minifiers
• uglify-js: No need to install anything, just minifies/beautifies JavaScript• uglify-css: No need to install anything, just minifies/beautifies CSS• uglify-json: No need to install anything, just minifies/beautifies JSON
　　You need to install the individual languagecompilers for most of the transformers, but they're usually pretty easy to installbecause they're almost all contained in npm modules like the Jade compiler
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


##Extends
##Includes
##Inheritance
##Mixins