# jQuery

## Basics  
Used for: finding elements in an HTML document, changing HTML content, listening to what a user does and reacting accordingly, animating contents on a page, and talking over the network to fetch new content.  

### Document Object Model (DOM)  
-A tree-like structure created by browsers so we can quickly find HTML Elements using JavaScript  
1.) Browser loads HTML into the DOM 1 by 1  
2.) Inside DOM, HTML elements become nodes, which have relationships with eachother;  
3.)Javascript is language used to interact with DOM, but each browser has a slightly different DOM, so JQuery is needed to work on most modern web browsers
4.) To access the DOM using jQuery use JQuery function jQuery(document);  
5.) To search through DOM, need to use CSS selectors ex. jQuery("h1");  can also use $("h1");  to return text, use $("h1").text();  to modify element's text use $("h1").text("Where to?");  which would change text to "Where to?"  
Note:  when running jQuery that interacts with DOM, must submit code AFTER DOM is finished loading.  When DOM is finished loading, DOM triggers event, "I'm ready!"  jQuery(document).ready(function(){}); will only run after DOM is ready.  

###How to get jQuery on your page:  
1.) Download jQuery from [web page](http://jquery.com)  
2.) load it into your HTML document using <script src="jquery.min.js"></script>  
3.)make application.js document and start using it with <script src="application.js"></script>  

##Searching the DOM  
-descendant selector: $("#destination li"); calls list items underneath parent destination id  
-child selector:  $("#destinations > li");  calls direct descendants of li destinations  
-select multiple items with a comma  
-can also select by class example: $(".articles");  or by style element/id $("#container");  
-pseudo-selector:  $("destination li:first"); selects first item in unordered list, can also use :last, or :odd to select odd list items(by index, so starts at 0) ...  

###Traversing  
-example:  $("#destinations").find("li");
-when finding elements by traversing it has 2 parts: selection and traversal.  It usually takes more code, but is faster.
- more examples:  $("li").first();  
-Walking the DOM:  $("li").first().next();  is basically method chaining to select the element that you want.  ex.  $("li).first().parent();  or  $("destinations").children("li");  children, unlike find, only specifies direct descendants 
-Traversal methods: .prev(); .last(); .first(); .next(); .children(); .find();  
-Example:  
$(document).ready() {  


###Appending the DOM
$(document).ready(function() {  
  var price = $('< p>From $399.99< /p>');  
  $('.vacation').before(price);  
});  
puts the price node before.vacation  
-can also append with .append(<element>), .prepend(<element>), .after(<element>), .remove(), appendTO(<element>), .prependTo(<element>), .insertAfter(<element>), .insertBefore(<element>)  

###Acting on Interaction:  
$document.ready(function() {  
  $('button').on('click', function()  {  
    var price = $('< p>From $399.99< /p>);  
    $('.vacation').append(price);
    $('button').remove();  
  });  
});  
This will add the words "From $399.99" while removing the "Get price" button after it is clicked.  Happens after the DOM is finish loading.  
The .ready method takes an event handler function as an argument  
.on(<event>, <event handler>)  
-Must refactor so that ALL buttons do not disappear/show up as price, just the one that is clicked on:  
￼￼$document.ready(function() {  
  $('button').on('click', function()  {  
    var price = $('< p>From $399.99< /p>);  
    $(this).closest('.vacation').append(price);
    $(this).remove();  
  });  
}); 