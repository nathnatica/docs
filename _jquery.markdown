jQuery(document).ready(function(){});
or
$(function(){}); // shorthand

#####Filter and Find
<a></a>
<a class="external"></a>
<a></a>
jQuery('a').filter('.external').length;


<p><em>text</em></p>
jQuery('p').find('em').length;

 
#####Returning to the prior selection before a destructive change(like filter() ,find(), next() ,prev(), etc.)
end()

#####Operate on the prior set as well as the current set
<div>
<p>paragraph</p>
<p>paragraph</p>
</div>
jQuery('div').find('p').andSelf().css('border', '1px solid #993300')

#####Traversing
jQuery('li:eq(1)') // second element
jQuery('li:last') // last element
next(), prev(), parent(), parent().children(), nextAll(), prevAll()

#####Create, Operate and Insert DOM Elements
jQuery('<p><a>jQuery</a></p>').find('a').attr('href','http://www.jquery.com').end().appendTo('body');
append(), prepend(), prependTo(), after(), before(), insertAfter(), insertBefore(), warp(), wrapAll(), wrapInner()

#####Remove (not removed from the jQuery wrapper set, so can continue operation), also removes all event handlers and internally cached data
jQuery('a').remove();
jQuery('a').remove('.remove');

#####Replace DOM Element
jQuery('li.remove').replaceWith('<li>removed</li>');
jQuery('<li>removed</li>').replaceAll('li.remove'); // inverse to prev method

#####Cloning DOM Element
clone()
clone(true) // clone the elements and all its children, including events


#####Getting and Setting Text Contents 
jQuery('p').text('Hello World'); // set
jQuery('p').text(); // get

#####Using the $Alias without Global Conflicts
(function($){
	// private scope and using $ without conflict
})(jQuery); // invoke nameless function and pass it the jQuery object



###Selectors

#####Direct descendant(child) combinator(>)

#####Select adjacent siblings(+)
jQuery('h1 + h2') // selects H2 elements that are adjacenet siblings of H1 elements

#####Select siblings adjacent or not 
jQuery('h1').siblings('h2,h3,p') // select H2,H3,p elements that are siblings of H1 elements

#####General sibling combinator(~)
jQuery('li.selected').nextAll(li)
jQuery('li.selected ~ li') // same

#####Selecting Elements by Index Order
:first
:last
:even
:odd
:eq(n)
:lt(n)
:gt(n)


#####Elements That Are Currently Animating
jQuery('div:animated')

if(jQuery('#ele')is(':animated')) {
	//do something
}


#####Selecting Elements Based on What They Contain
jQuery('span:contains("Bob")') 
jQuery('div:has(p a)')
jQuery('p').filter(function(){
	return /(^|\s)(apple|orange|lemon)(\s|$)/.test(jQuery(this).text);
};


#####Selecting Elements by What They Don't Match
jQuery('div:not(#content)')
jQuery('a:not(div.important a, a.nav)') // select anchors that do not reside within 'div.important' or have the class 'nav'

var $anchors = jQuery('a');
$anchors.click(function){
	$anchors.not(this).addClass('not-clicked');
});

$('#nav a').not('a.active');



#####Selecting Elements Based on Their Visibility
if (jQuery('#ele').is(':hidden')) {
	// do something
}
jQuery('p:visible').hide();



#####Select Elements Based on Attributes
jQuery('a[href="http://www.google.com"]');
[attr]
[attr=value]
[attr!=value]
[attr^=value]
[attr$=value]
[attr~=value] // contain the specified value with spaces, on either side



#####Selecting Form Elements by Type
:input
:text
:password
:radio
:checkbox
:submit
:image
:reset
:button
:file
:hidden

jQuery(':text, textarea'); // all text and textarea input elements


jQuery('\*').filter(function {
	return !!jQuery(this).css('backgroundImg'); 
	// !! converting any type in JS to its boolean expression
	// empty string, 0, undefined, null, false > return false
});



#####Context Parameter
jQuery('p','#context');
jQuery('#context p'); // same but fast

#####Creating a Custom Filter Selector
jQuery.expr[':'].newFilter = function(ele, index, match) {
	return true; // return true/false like you would on the filter() method
}

Parameters
ele : the element in question
index : the index of this element among the entire collection
match : a match array returned from a regular expression

jQuery.expr[':'].inline = function(elem) {
	return jQuery(elem).css('display') === 'inline';
}
jQuery('div a:inline').css('color','red'); // example


// when want to use more than one new selector, use jQuery's extend() method:
jQuery.extend(jQuery.expr[':'], {
	newFilter1 : function(ele, index, match) {
		// return true or false
	},
	newFilter2 : function(ele, index, match) {
		// return true or false
	},
	newFilter3 : function(ele, index, match) {
		// return true or false
	}
});



#####Each
var urls[];
$("div#post a[href]").each(function(i){
	urls[i] = $(this).attr(href); // wrap DOM element
});


#####eq()
.eq() method is similar to using the $(":eq()");


#####Convert jQuery Object to Raw DOM Object
.get() // converts into an array of DOM objects
$.get(index) or $("div")[index]
// best way is using []notation

Example)
var lis = $("ol li").get().reverse();
$("ol").empty();
$.each(lis, function(i){
	$("ol").append("<li>" + lis[i].innerHTML + "</li>");
});


#####Index
$("div").click(function(){
	alert($("div").index(this));
});

or

var test = $("div.test");
$("div").each(function(i){
	if ($(this).index(test) >= 0) {
		// do something
	}
});


#####$.map()
take an existing array and "map" it into another array
var arr = $.map($("li"), function(item, index){
	while (index <3) {
		$(item).html();
	}
});


#####Subset of the Selected Set
$("p").slice(startIndex, endIndex).wrap("<i></i>");


#####No Conflict
1. jQuery.noConflict(); // and use jQuery via jQuery 
2. var j = jQuery.noConflict(); // and use jQuery via j
3. using closure
(function($){
	$("div").css("something");
})(jQuery);



#####$.each
loop over each element in an array or attribute of an object

var months = ['one','two','three'];
$.each(months, function(index, value){
	$('month').append('<li>' + value + '</li>');
});

var days = { sunday:0, monday:1 };
$.each(days, function(key, value){
	$('day').append('<li>' + key + '(' + value + ')' + '</li>');
});

// when the callback function is executed, the `this` variable is set to the value of the element
// so could be rewritten as follows

$.each(months, function(){
	$('month').append('<li>' + this + '</li>');
});

$.each(days, function(key){
	$('day').append('<li>' + key + '(' + this + ')' + '</li>');
});


#####$.grep
filter and remove elements in an array

$.grep(array, function(value, index){
	return ( value.indexOf('J') == 0);	
});


#####$.merge
combine two arrays

$.merge(array1, array2);

#####$.unique
remove duplicate DOM elements from an array or collection

var temp = $.merge(array1, array2);
temp = $.unique(temp);


#####$.isFunction
check whether param is a function
but
$.isFunction(document.getElementById) 
returns false in versions of IE

#####$.trim
remove whitespace

$('input.cleanup').blur(function(){
	var value = $.trim($(this).val());
	$(this).val(value);
});



#####$.data
because of falwed garbage collection implementations of some web browsers, this code can cause memory leaks

var node = document.getElementById('myId');
node.myObject = {
	label: document.getElementById('myLabel');
};

// avoid memory leak issues

$('#myId').data('myObject', {
	label: $('#myLabel')[0]
});

var myObject = $('#myId').data('myObject');
myObject.myLabel;


#####$.extend
return a reference to the first object passed in with the latter objects overwriting any properties they define

var obj1 = { foo: {bar: '123', baz: '456'}, hello: 'world'};
var obj2 = { foo: {car: '789'}};

var obj3 = $.extend(obj1, obj2);
// obj3 = { foo: {car: '789'}, hello: 'world'};

var obj4 = $.extend(true, obj1, obj2); // deep(recursive) copy
// var obj4 = { foo: {bar: '123', baz: '456', car: '789'}, hello: 'world'};


#####this
1. `this` is used in an object's methods to refer to that object
2. in the code for a traditional `onevent` attributes, `this` refers to the element receiving the event
<a href="#" id="test" onclick="clicked(this);" >Test</a>
function clicked(it) {
	alert(it); // 'test'
	alert(this); // undefined
	alert(this === window); // true 
}
3. `window` is the 'default' meaning of `this` when a function is called directly (i.e. not called as a method of an object)
4. in a jQuery event handler, `this` is the DOM element handling the event


$(document).ready( function(){
	$('.clicky').click( function() {
		$(this).addClass('clicked');
		setTimeout( function(){
			$(this).removeClass('clicked'); // not working
		})
	});
});


$(document).ready( function(){
	$('.clicky').click( function() {
		var $element = $(this);
		$element.addClass('clicked');
		setTimeout( function(){
			$element.removeClass('clicked'); // working
		})
	});
});


#####trigger
fire the event immediately after attaching it, along with the `.bind()`

$(document).ready( function() {
	$('#country')
	.bind( 'change keyup', function() {
		var value = $(this).val();
		$('#state').toggle( value == 'US' );
		$('#province').toggle( value == 'CA' );
	})
	.trigger('change');
});


p99
