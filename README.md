# Angular 1.* Tables with paging as easy as:

    <table ev-table="vmDemo.tableData">
		<thead>
			<tr>
				<th ev-sort="Name">Name</th> <!-- ev-sort is optional -->
				<th ev-sort="Age">Age</th>
			</tr>
		</thead>  
		<tr ng-repeat="item in collection">
			<td>{{ item.Name }}</td>
			<td>{{ item.Age }}</td>
		</tr>
	</table>
	
> SORTING is as easy as adding ev-sort on a your Header & providing the server-side column name 

> LOOPING DATA : "collection" is required - data is passed to it. Do whatever you like with it!

Designed to be extremely uninvasive, `ev-table` let's you sculpt tables exactly the way you want!
Created with server-side paging in mind, since it's always the most hassle (but of course works with static client-side paging as well) - Extremely easy to use and lightweight Angular table/grid (ngTable) directive.

# Easy to use

### Include the directive: (Or add it within your own file)

`<script src="ev-table.directive.js"></script>`

### Add evTable to your App module dependencies: (or rename the module to your own to omit this)

`var APP = angular.module('app', ['evTable']);`


# Directive in action:

In your View, make your `<table>` like usual! Simply add the `ev-table="{TableDataFromController"` attribute directive!
Sorting is as easy as adding ev-sort on a your Header & providing the server-side column name. You can ng-repeat through `collection` for the remaining rows, that is what's passed up to your View to loop through.


    


### In the Controller

All we need is to pass that tableData. Which is a factory object called evTableParams.


    APP.controller('DemoController', function (evTableParams) {

		var vm = this;
		
		// Server-side Paging:
		//////////////////////////////////

		vm.tableData = new evTableParams({ 
			serverPaging : true,
			ajaxUrl      : '/api/pagingdemo'
		});

		// Client-side Paging:
		//////////////////////////////////
		
		vm.tableData = new evTableParams({ 
			data         : [] // <-- your static Array of Objects
		});

	});
		
There are some other options you can utilize on Start-up such as Ordering or starting at a specific page.

    vm.tableData = new evTableParams({ 

		serverPaging : true,
		ajaxUrl      : '/api/pagingdemo',

		// OPTIONAL PARAMETERS BELOW ::
		//////////////////////////////////////

		// [Optional] Incase you want to do something else everytime it finishes running AJAX or static paging
		callback     : function (data) { 
			// data === the current pages data or "collection"
		},

		pageSize 	    : 10,  	      // [Optional] Defaults to 10
		pageSizeOptions : [5,10,20],  // [Optional] Defaults to [10,20,50]
		pageNumber	    : 1,   	      // [Optional] Defaults to 1 : If you want to start on a different page
		orderBy         : 'Name'      // [Optional] Sort on page start
		orderDirection  : 'desc'      // [Optional] Sort direction on page start
	});
		

			
# That's it!

> NOTE: For server-side paging, I'm passing an Object with these properties for you to handle your Take/Skips/Orders etc. They are found within the factory in the JS file if you want them to match your back-end.

	PageSize 
	PageNumber 
	OrderBy 
	OrderDirection


# TO-DO List:

* Show example implementing bootstraps styles?
* Test for multiple evTable useage
* Retrieve correct totalCount coming from server
* Add more styles
* Add ability to disable pageSizeOptions
* ~~Add Dropdown to handle changing the PageSize~~
* ~~Add Previous/Next arrow buttons~~
