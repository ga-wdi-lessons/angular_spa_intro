# Inventory Tracker

## App demo

We're going to create an inventory tracker for 100 imaginary products.

## Logistics

Please clone the [Inventory Tracker repo](https://github.com/ga-wdi-exercises/inventory_tracker).

Then, in your browser, open [this page](https://github.com/ga-wdi-exercises/inventory_tracker/commits/angular-solution). This is the commit history for the solution. We're going to be working toward this solution.

This walkthrough goes commit-by-commit through that commit history.

Note that in your starter code all the files you'll be using have already been created. Note that Angular and Bootstrap are included as well.

> These could (and probably should) be loaded from a CDN; they're included here just in case the WiFi gives out.

The `angular.js` and `bootstrap.css` files are unminified, and therefore **ENORMOUS**. You should never have to open them, let alone modify them.

# Commit-by-Commit

Each of the headers below corresponds to one of the commits in the `angular-solution` branch of `inventory_tracker`.

## Commit: Added module and controller

This is going to be the most "explain-y" step.

### app.js

The layout of this file looks pretty strange. Two things may be new to you. They have nothing to do with Angular, but are considered "good form" for Angular developers:

- `"use strict"` basically puts Javascript in "expert mode". Things you could normally get away with -- like declaring a variable without using `var` -- will now throw an error. This forces you to write better code.
- `(function(){ ... })()` is an *immediately-invoked function expression*, or IIFE (pronounced "iffy"). Don't worry about it too much -- this app would work fine without it. It's here simply because it's Angular convention to use these. The IIFE's job is to keep your app from having lots of global variables.

#### Components

Building an Angular app is a lot like  playing with Legos, in that we will mostly just be putting together a bunch of special pieces to construct a complex structure.

An Angular app is made of modules. A module is made of components. This Angular app has just one module, and that model has one component: a controller.

These components are always declared in a chain that begins with `angular`. Here we have `angular.module().controller()`. It's written on separate lines only for readability.

#### .module

The first argument is the "name" of this app.

The second argument, `[]`, is necessary for something called "dependency injection", which is Angular's way of loading other modules and libraries. We won't be exploring it in this class.

#### .controller

The first argument is the "name" of this controller. (Notice a pattern?)

The second argument is the function that encloses all the functionality of the controller. This function can be called anything -- `.controller("apple", Orange)` would work fine.

The controller is an interface between your data and your view, as in Rails. In Rails, to make data show up in a view, we'd make it an instance variable, as in `@variable = "Some data"`. To do the same in Angular, we attach it to `this`, as in `this.variable = "Some data"`.

#### VM

In order to not "lose" `this`, I've saved it to a variable called `vm`. This variable can be named anything, but `vm` is convention.

"VM" stands for "view model". Basically, it means "an object that contains the data you want to show up in your view, and also contains methods for people using the view to interact with the data."

Here I've attached a property called `hello` to `vm`. In the `index.html`, we can reference `vm.hello` and get its data.

### index.html

#### data-ng-something

This is a **directive**. Directives are the bread-and-butter of Angular. They're *custom HTML attributes*. Each has special abilities.

Starting them with `data-` is optional: `ng-app` works the same as `data-ng-app`. The only difference is custom, non-standard HTML attributes that begin with `data-` are ignored by the HTML validator.

#### data-ng-app

In Angular, an app is an instance of a module. This directive tells Angular that the "inventory" module we defined should run inside this `body` element.

`ng-app` is necessary so that you can run multiple apps on one page. If you didn't tell Angular which elements belong to which app, you might have code collisions.

If you have only one app on a page, you can put `ng-app` in your `body` tag.

`<body class="container" data-ng-app="inventory">`

#### data-ng-controller

A page can have multiple apps, and an app can have multiple controllers.

> Unlike Rails, a controller in Angular does *not* necessary correspond to just one webpage.

`inventory_controller as vm` says we want to create a new instance of this controller and save it to a variable called `vm`. This variable could be named anything; I've chosen `vm` so it matches the `vm` inside the controller's function.

`<main data-ng-controller="inventory_controller as vm">`

#### {{handlebars}}

ERBs use clownhats (`<%= %>`); most Javascript libraries use "handlebars" syntax (or moustache syntax).

It serves the same purpose: text inside handlebars is treated as executable Javascript. However, `{{}}` can only **return** data -- there's no `{{ vm.array.each do }}`!

`{{vm.hello}}` lets us access the `hello` property attached to `vm` inside the controller function.

`<h2>{{vm.hello}}</h2>`

### Review

- What's a directive?
- What's a controller?
- What's the purpose of putting `data-` at the beginning of a directive?
- What is the Javascript equivalent of ERB's "clown hats"?

## Commit: Added ng repeat and a row for each product

### app.js

#### vm.data

The `data.js` file contains the information for 100 products, and saves it to a global variable called `data`: an array. You would never do this in the real world. Later we'll be learning how to interact with APIs.

### index.html

#### ng-repeat

This is Angular's version of `each..do`. It repeats HTML for each item in an array, and lets you access each item in a variable -- in this case `product`.

`vm.data` is an array of 100 objects. Each object is being saved to a variable called `product`. This lets us access each object's properties.

#### ng-href

The reason we use this instead of `href` is HTML validators will throw an error if you put something like `{{product.url}}` in an `href`.

#### ng-src

Your browser tries to load `<img>` tags before it runs Javascript. If we used the usual `src` attribute your console would be full of errors caused by your browser trying to load `product.image_url` before it's run the Javascript necessary to figure out what `product.image_url` is.

-----

## Commit: Added index and number formatting

#### $index

Inside any `ng-repeat`, you automatically have access to a variable called `$index`. This represents the index of the current item in the array you're looping through.

#### toFixed(2)

By default, Javascript displays numbers without trailing zeroes. So if your bank account balance is $1.00, it would display `$1`. `toFixed(2)` tells Javascript to include the trailing zeroes, up to 2 places.

This is native Javascript -- not Angular.

Here's our updated index.html:

## Commit: Added filter

#### data-ng-model

This creates **two-way data binding** between the `value` of an `input` or `textarea` and a variable in the controller. Next to directives, it's one of Angular's most important concepts and selling points.

This is a fancy way of saying: "If the data for `vm.filter_on` changes in the back-end, I want that change to show up automatically in this `<input>` element. If the data for `vm.filter_on` changes in this `<input>` element, I want that change to be saved automatically in the back-end." There's no need to "refresh" -- it all happens under the hood without you having to worry.

Note: Typically, your data will be coming from the backend but in this example, you are working with static data in the frontend.

#### filter: vm.filter_on

Try typing something in the "Filter on..." text field!

`filter` is unique to `ng-repeat`. Angular will check each item being repeated to see if it contains the value of `vm.filter_on`. If it doesn't, that item is not displayed in the `ng-repeat`.

Note the pipe `|`!


### Review

- What is two-way data binding?

## Commit: Added total value calculator

You can attach functions as well as properties to the controller instance, and reference them in the view. Any time there's a change to any of the data in the controller, the function will be re-evaluated.

-----

## Commit: Added sorting

#### ng-click

This is Angular's version of `onclick`. In this case, it changes the value of a property `vm.sort_on` whenever the element is clicked on.

#### orderBy

Like filter, this is another awesome functionality built into Angular's `ng-repeat`.

If each item in the `ng-repeat` array is an object, Angular checks each object for a property matching whatever was passed into `orderBy`, and then sorts them by that property.

So in this case, if `vm.sort_on` is `"name"`, Angular checks each `product` for `product.name`, and then sorts them by `product.name`.

Note the pipe `|`!

## Commit: Added ordering

#### something = !(something)

This is a short way of writing:

```js
if(something !== false){
  something = false;
}else{
  something = true;
}
```


#### ng-if

The data inside the `ng-if` attribute is evaluated. If it's truthy, the element is shown. If it's falsy, the element is not shown.

#### orderBy

`orderBy` can take a second argument. If this second argument is truthy, the items in `ng-repeat` are ordered in ascending order. Otherwise, they're ordered in descending order.


## Commit: Combined ordering and sorting

Before, `ng-click` simply set a property equal to a value. Now it calls a function.

### Review

- How are we seeing two-way data binding in this step?

-----

## Commit: Added delete button

`.indexOf` finds the position of the product that was clicked in the `vm.data` array. `.splice` removes that product from the array. So in this example, we could have used `<td data-ng-click="vm.destroy(vm.indexOf())">&cross;</td>` instead of `<td data-ng-click="vm.destroy($index)">&cross;</td>`.


## Commit: Added create method

#### angular.copy

This duplicates an object. It's useful when you want to save a value at a certain point when the variable could later be modified.

Example:

```js
var x = {name: ‘john’};
var y = x;
x.name = “bob”;
y.name   //this is 'bob'
```
```js
var x = {name: ‘john’};
y= angular.copy(x)
x.name = “bob”;
y.name   //this is ‘john’
```
