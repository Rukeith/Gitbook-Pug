#Advanced Use
##Filters
　　Filters let you use other languages within a jade template. They take a block of plain text as an input.  
　　All JSTransformers can be used as jade filters. Popular filters include `:coffee-script`, `:babel`, `:uglify-js`, `:less`, and `:markdown-it`.
###Template engines
* atpl: Compatible with twig templates
* ejs: Embedded JavaScript templates

###Stylesheet languages
* less: This extends CSS with dynamic behaviors such as variables, mixins, operations, and functions

###Minifiers
• uglify-js: No need to install anything, just minifies/beautifies JavaScript
　　You need to install the individual language
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