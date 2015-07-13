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

｜Jade 提供｜原文｜
｜---｜---｜
｜doctype ｜<!DOCTYPE html>｜
｜doctype default｜｜
｜doctype html｜｜
｜doctype xml｜<?xml version="1.0" encoding="utf-8" ?>｜
｜doctype transitional｜<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">｜
｜doctype strict｜<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://
www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">｜
｜doctype frameset｜<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Frameset//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd">｜
｜doctype 1.1｜<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.
w3.org/TR/xhtml11/DTD/xhtml11.dtd">｜
｜doctype basic｜<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML Basic 1.1//EN" "http://
www.w3.org/TR/xhtml-basic/xhtml-basic11.dtd">｜
｜doctype mobile｜<!DOCTYPE html PUBLIC "-//WAPFORUM//DTD XHTML Mobile 1.2//EN"
"http://www.openmobilealliance.org/tech/DTD/xhtml-mobile12.dtd">｜

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
  <html lang="en" class="lt-ie9">
  <![endif]-->
  <!--[if gt IE 8]><!-->
  <html lang="en">
  <!--<![endif]-->
