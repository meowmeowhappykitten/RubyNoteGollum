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

