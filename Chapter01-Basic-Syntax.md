#Basic Syntax
Jade  使用了縮排的方式取代了 HTML 的 tag 寫法  
雖然在習慣上會讓人不太適應，但是卻也可以強迫自己在編寫時記得一定要保持住好的縮排習慣  
每一階層之間都要相隔一個縮排  

##Doctype  
對於 HTML 的開頭宣告`doctype`，通常都會非常的冗長  
但是 Jade 提供了縮寫讓編寫更方便，除了 Jade 提供的`doctype`  
也可以自己設定客制的`doctype`  
`doctype html PUBLIC "-//W3C//DTD XHTML Basic 1.1//EN"`  
--> `<!DOCTYPE html public "-//w3c//dtd xhtml basic 1.1//en">`  

|Jade 提供|原文|
|---|---|
|doctype|<!DOCTYPE html>|
|doctype default||
|doctype html||
|doctype xml|<?xml version="1.0" encoding="utf-8" ?>|
|doctype transitional|<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">|
|doctype strict|<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">|
|doctype frameset|<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Frameset//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd">|
|doctype 1.1|<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">|
|doctype basic|<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML Basic 1.1//EN" "http://www.w3.org/TR/xhtml-basic/xhtml-basic11.dtd">|
|doctype mobile|<!DOCTYPE html PUBLIC "-//WAPFORUM//DTD XHTML Mobile 1.2//EN" "http://www.openmobilealliance.org/tech/DTD/xhtml-mobile12.dtd">|

##Comments  
###Single Line Comments  
單行註解類似於 JavaScript 的單行註解  
`// just some paragraphs` --> `<!-- just some paragraphs-->`  

如果不希望在編譯過後顯示在 HTML 中的話，可以加上連字符號  
`//- will not output within markup`  

###Block Comments  
如果在單行註解後縮排一個區塊，則此區塊自動加入到註解中  

	//  
		As much text as you want  
		can go here.  
    
-->

  	<!--  
  		As much text as you want  
  		can go here.  
  	-->  
  
當然也可以使用`//-`，來避免編譯後顯示  

###Conditional Comments  
Jade 並沒有提供特殊的語法來處理 Conditional comments.  
如果是使用 `<` 開頭，會被當作文字，所以就直接使用一般的 HTML 的Conditional comments 即可  

	  <!--[if IE 8]>  
	  `<html lang="en" class="lt-ie9">`  
	  <![endif]-->  
	  <!--[if gt IE 8]><!-->  
	  `<html lang="en">`  
	  <!--<![endif]-->  

##Tags  
Jade 是以縮排為基準的方式來編排，所以沒有 close tag 也沒有 `< >`  

	p			-->		<p>
	  spam 				<spam></spam>
	 					</p>

	p         -->    <p></p>
	spam             <spam></spam>

###Block Expansion
為了解省空間，Jade 也提供同行的方式來呈現巢狀標籤結構  

	a: img   --> <a><img/></a>
	
	ul
		li.first: a(href='#') foo
		li: a(href='#') bar
		li.last: a(href='#') baz
	
The `:` (colon) after the tag name and attributes indicates that there is another tag following that one. We can even make really long chains of tags.

`ul: li.first: b: a(href='#') foo`  
-->
  
	<ul>
		<li class="first">
			<b>
				<a href="#">foo</a>
			</b>
		</li>
	</ul>
>But that is really hard to read, so please, never do that unless you have a very good reason.


###Self Closing Tags
Tags such as `img`, `meta`, `link` and so on are automatically self-closing (unless you use the xml doctype). You can also explicitly self close a tag by simply appending the`/`character. Only do this if you know what you're doing  

	img --> <img/>

##Plain Text  
Jade 提供了三種方式來幫助書寫文本

###Piped Text
The simplest way of adding plain text to templates is to prefix the line with a `|` character (pronounced "pipe"). These text blocks can be mixed with regular tags as follows.

	| Plain text can include <strong>html</strong>
	p
	  | It must always be on its own line
-->

	Plain text can include <strong>html</strong>
	<p>It must always be on its own line</p>

###Inline in a Tag
You can put the text directly after the tag name (separated by a space) as follows.

	p Plain text can include <strong>html</strong>
-->

	<p>Plain text can include <strong>html</strong></p>

###Block in a Tag
Jade provides a shorthand method for indicating that all of the nested code in an element are text blocks. This is represented by a `.` after the tag as follows.

	p.
		This is a demonstration
		of Jade's text blocks,
		using the "." shorthand
-->

	<p>
		This is a demonstration
		of Jade's text blocks,
		using the "." shorthand
	</p>

###Inline HTML
It's also perfectly fine to put inline HTML in any of those text blocks.

	p.
		This is a <i>
		demonstration</i>
		of Jade's <b>text
		blocks</b>
-->

	<p>
		This is a <i>
		demonstration</i>
		of Jade's <b>text
		blocks</b>
	</p>
	
##Attributes
Tag attributes look similar to html, however their values are just regular JavaScript.

	a(href='google.com') Google
	a(class='button', href='google.com') Google
-->

	<a href="google.com">Google</a>
	<a href="google.com" class="button">Google</a>
	
All the normal JavaScript expressions work fine too

	- var authenticated = true
	body(class=authenticated ? 'authed' : 'anon')
-->`<body class="authed"></body>`

If you have many attributes, you can also spread them across many lines.

	input(
	  type='checkbox'
	  name='agreement'
  	  checked
	)
-->`<input type="checkbox" name="agreement" checked="checked"/>`

###Unescaped Attributes
By default, all attributes are escaped (**replacing special characters with escape sequences**) to prevent attacks such as cross site scripting. If you need to use special characters you can use `!=` instead of `=`.

	div(escaped="<code>")
	div(unescaped!="<code>")
-->

	<div escaped="&lt;code&gt;"></div>
	<div unescaped="<code>"></div>

###Boolean Attributes
Boolean attributes are mirrored by Jade, and accept bools, aka `true` or `false`. When no value is specified true is assumed.

	input(type='checkbox', checked)
	input(type='checkbox', checked=true)
	input(type='checkbox', checked=false)
	input(type='checkbox', checked=true.toString())
-->

	<input type="checkbox" checked="checked"/>
	<input type="checkbox" checked="checked"/>
	<input type="checkbox"/>
	<input type="checkbox" checked="true"/>

>If the doctype is `html` jade knows not to mirror the attribute and uses the terse style (understood by all browsers).

	doctype html
	input(type='checkbox', checked)
	input(type='checkbox', checked=true)
	input(type='checkbox', checked=false)
	input(type='checkbox', checked=true && 'checked')
-->

	<!DOCTYPE html>
	<input type="checkbox" checked>
	<input type="checkbox" checked>
	<input type="checkbox">
	<input type="checkbox" checked="checked">

###Style Attributes
The `style` attribute can be a string (like any normal attribute) but it can also be an object, which is handy when parts of the style are generated by JavaScript.
`a(style={color: 'red', background: 'green'})`  
-->  
`<a style="color:red;background:green"></a>`

###ID and Class
IDs and classes are both pretty common attributes, so Jade gives us a shorthand method for writing them. This is similar to the way CSS selectors are written. An example of this is as follows:  
`p#hello.world`  
-->   `<p id="hello" class="world"></p>`  

也因為 ID 和 Class 相當頻繁地被使用，所以當沒有被指定 tag 時會自動的貼加生成 div
`.content`  --> `<div class="content"></div>`  
`#content`  --> `<div id="content"></div>`  

###Passing objects as attributes
In Jade, you can easily pass strings as attributes, but if you pass objects, they will be turned into the most useful representation for that particular attribute. For example, passing an array to the class attribute will be interpreted as a list of classes:  

`p(class=['first-class', 'another-class', 'last-class'])`  
--> `<p class="first-class anotherclass last-class"></p>`

Another example is when you pass any type of object to a `data-*` attribute, it will be encoded as JSON, as shown:  
`p(data-myattr={numbers: [2, 4, 8], string: 'this is a string'})`  
--> `<p data-myattr='{"numbers":[2,4,8], "string":"this is a string"}'></p>`

However, for most attributes, it just outputs the standard string representation of the object, as shown:  
`p(value=['one', 'two', 'three'])`  
-->  `<p value="one,two,three"></p>`  

The class attribute may also be repeated to merge arrays  
`a.bing(class=classes class=['bing'])`  
--> `<a class="bing foo bar baz bing"></a>`

###&attributes
The `&attributes` syntax can be used to explode an object into attributes of an element.  
`div#foo(data-bar="foo")&attributes({'data-foo': 'bar'})`  
-->  `<div id="foo" data-bar="foo" data-foo="bar"></div>`

The object does not have to be an object literal. It can also just be a variable that has an object as its value.  

	- var attributes = {'data-foo': 'bar'};
	div#foo(data-bar="foo")&attributes(attributes)
-->  `<div id="foo" data-bar="foo" data-foo="bar"></div>`
>Attributes applied using `&attributes` are not automatically escaped. You must be sure to sanitize any user inputs to avoid cross-site scripting. This is done for you if you are passing in attributes from a mixin call.

##Interpolation
Jade provides operators for a variety of your different interpolative needs.
