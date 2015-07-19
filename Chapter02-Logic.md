#Logic in jade
##If / else
Jade 可以編譯到 JS 也允許直接使用 JS 到 template 中。所以我們可以使用任何 JS 所提供的邏輯運算子來建立。其中最為常見的就是`if`

	- name = "Bob"	- if (name == "Bob") {	h1 Hello Bob	- } else {	h1 My name is #{name}	- }
-->  `<h1>Hello Bob</h1>`  

也可以使用縮寫版

	- name = 'Bob'	- greeting = (name == 'Bob' ?	'Hello' : 'My name is')	h1 #{greeting} #{name}
-->  `<h1>Hello Bob</h1>`  
##Unless
Jade 也提供了`unless`，相當於 `if(!(expr))`

	- name = "Bob"	unless name == "Bob"		h1 My name is #{name}	else		h1 Hello Bob
-->  `<h1>Hello Bob</h1>`  
##Case
The case statement is a shorthand for JavaScript's switch statement.

	- var friends = 10
	case friends
		when 0
   			p you have no friends
		when 1
    		p you have a friend
		default
    		p you have #{friends} friends
-->  `<p>you have 10 friends</p>`

You can use fall through just like in a select statement in JavaScript.  

	- var friends = 0
	case friends
  		when 0
		when 1
    		p you have very few friends
		default
    		p you have #{friends} friends
-->  `<p>you have very few friend</p>`

Block expansion may also be used.  

	- var friends = 1
	case friends
		when 0: p you have no friends
		when 1: p you have a friend
		default: p you have #{friends} friends
--> `<p>you have a friend</p>`
##For
Loops can be used to iterate over lists or repeat elements a certain number of times.

	- list = ['one', 'two', 'three'];	ul		- for (var i = 0; i < list.length; i++){			li=list[i]		- }
-->

	<ul>		<li>one</li>		<li>two</li>		<li>three</li>	</ul>
##Each
	ul
		each val in [1, 2, 3, 4, 5]
			li= val
-->  

	<ul>
  		<li>1</li>
		<li>2</li>
		<li>3</li>
		<li>4</li>
		<li>5</li>
	</ul>
You can also get the index as you iterate. Jade also lets you iterate over the keys in an object  

	ul
  		each val, index in ['zero', 'one', 'two']
  						   {1:'one',2:'two',3:'three'}
    		li= index + ': ' + val
-->

	<ul>
  		<li>0: zero</li>
  		<li>1: one</li>
  		<li>2: two</li>
	</ul>
   	---
	<ul>
  		<li>1: one</li>
  		<li>2: two</li>
  		<li>3: three</li>
	</ul>
The object or array to iterate over is just plain JavaScript so it can be a variable or the result of a function call or almost anything else. e.g.

	- var values = [];
	ul
		each val in values.length ? values : ['There are no values']
			li= val	
-->

	<ul>
		<li>There are no values</li>
	</ul>
##While
	- list = ["one","two", 'three']	- i = 0	ul		while i < list.length			li=list[i]			- i++;
-->

	<ul>		<li>one</li>		<li>two</li>		<li>three</li>	</ul>
