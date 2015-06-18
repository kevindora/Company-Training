# Company-Training
Best Practices


o	https://github.com/sencha/code-guidelines

•	General
o	Create functional project folders under ./src directory to organize your code
o	Define one class per file
o	Custom css goes in ./sass/etc/all.scss
o	Overrides:  Review files in /override.  App-specific overrides should be stored in each App’s ./overrides directory and reviewed with common portal team.
o	Use DeftJS for:
	dependency injection
	Use promises in lieu of nested AJAX calls and callbacks
o	
•	Naming Conventions (from Joe Guarneri)
o	Store field and Variable names use camelCase (first letter lowercase)
 var myNumber = 123;
o	Only use underscores and all caps on statics.  Do not use underscores for variables or Classes.
o	Class names use CamelCase (first letter capitalized)

•	Components
o	Don’t use id’s.  Instead use itemId and reference configs (view controllers)
o	Avoid Ext.getCmp.  Use down() from parent to search for itemId.  Use lookupReference(‘myRef’) for common lookups of cached references.  Can use up(), but better to use either down() or references.
o	Don’t use aliases when instantiating components.  Instead use full class name.
o	When adding multiple sub-components do all at once:  container.add(comp1, comp2, comp3, …)
o	Avoid deeply nested or redundant layouts

•	View Controllers
o	All view methods not being extended should be in View Controller
o	View Controller auto-destroyed with the View.
o	Don’t use global controllers

•	View Models
o	User View Models over Stores.  
o	View Model auto-destroyed with the View

•	Right-click Menus
o	Store initial creation of popup menu with component and re-use (don’t recreate after each right-click)

•	Event listeners
o	Use .mon(…) over .on(…) so that listener is removed upon panel destroy
o	If necessary to remove a listener then use .mun(…)
o	Don’t define functions within a listener handler.  Instead the handler should reference a separate view controller method.

•	JavaScript
o	Consider using "js lint" or "js hint" to check javascript proper coding.
o	Declare variable for "this" at top of every function (i.e. that would use ‘this’)
var me = this;
o	Use === over == as much as possible
o	Make use of  Ext.isEmpty() where possible.
o	Review the many useful methods in API for Ext, Ext.Array, Ext.Object
o	Arrays should be uniform, else use objects
o	Don’t use eval()
o	Variables
	avoid global variables
	declare local variables at top of code and don’t miss any (particular use of “for loop” indexes like i,j,…)
o	Avoid trailing comma after last item when defining object
o	Consistent indentation:
if(! This.isReadable()) {
	this.refactorWith({
		properIndeation		: true,
		optimizedCodeForReadability	: true
	});
}
Else {
	This.beHappy();
}

o	From Joe Guarneri regarding use of Try/Catch
A good article on JS Error Handling and the importance of try/catch: http://www.techrepublic.com/blog/australian-technology/error-handling-in-javascript-rarely-done-often-needed/

I updated the jsperf to include one other important test that was missed:
http://jsperf.com/try-catch-cost-in-a-loop

The rule really shouldn't be to not use try-catch, but to not use a try-catch and functional code within the same scope.  By wrapping the code in a function the js compiler is able to optimize the subroutine lessening the penalty of using a try-catch.  I've added this as a forth test.  For the most part, this should benchmark a little bit faster than the other two way in the code.  Microbenchmarks aren't the best thing in the world, but I do know this is a best practice.  This gets aggravated the more lines of code you have within the try catch block so the difference could be better shown by having large routines done in the jsperf test.

Also, just like in Java, the rule should be: if a try-catch is not needed and can be replaced with a if-else:

if(foo) {
  foo.bar();
}

rather than:

try {
  foo.bar();
} catch(e) {
  // foo doesn't exist
}

The performance of if-else is exponentially better and it is also easier to read the code as well.

o	
•	CSS
o	Pre-fix all selector names with unique application code
o	Trend is to use icons over images

•	Performance
o	use store.suspendEvents(false) when modifying a store, followed by store.resumeEvents()
o	Animations
	Minimize use and do coarse-grained animations if needed
	Order:  Server Calls -> Animations -> rest goes into setTimeout
o	Do batch record updates when necessary:  record.set({field1: ‘xxx’, field2: ‘yyy’, …})
o	When instantiating, use xclass over xtype for lazy loading
o	Don’t define functions within loops

•	Local cache
o	Clean or use aging mechanism to minimize storage use

•	Documentation
o	Comment top-level structures
o	Use meaningful names (self-documenting code)
o	Add notes where logic is not obvious
o	Future use of JSDuck for searchability?
o	Other documentation standards – Future topic
•	Style Guidelines and Standards
o	Future topic
