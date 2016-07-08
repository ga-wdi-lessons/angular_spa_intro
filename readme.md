# Angular and Single-Page Apps

## Learning Objectives
- Give an example of a single-page app and explain why its single-page-ness is important
- Explain the difference between directives, models, modules, and controllers in Angular
- Use Angular to display a collection of data with sorting and filtering
- Give one reason why two-way data-binding is valuable

## Framing

Today we will be diving into our first front end framework by building a dynamic Single Page App with Angular.

But first, let's talk about why we are doing this.

<details>
<summary> What do we mean by the term Single Page App?</summary>

> While there's no uniform definition, in essence Single Page Applications are Web apps that load a single HTML page
and dynamically update that page as the user interacts with the app. SPAs use AJAX and
HTML5 to create fluid and responsive web apps, without constant page reloads.

</details>

<br>

Important to note, single page does **not** necessarily mean:

> The user sees everything on one page.

It **does** mean:

> The user never *actually* goes to a different page in their browser, but they may *feel* like they do. There's one main `index.html` page, and then other "pages" are really just pieces of HTML that are loaded in and out as necessary.

<details>
<summary>Why do we do this?</summary>

```
In short, to give the user a more "native" experience for web-based applications.
```

</details>

Some examples:

- [Hyrule Potion Shop](http://ga-wdi-exercises.github.io/hyrule_potion_shop/)
- [RepoTagger](http://repotagger.github.io/?name=ga-wdi-lessons), which uses Angular
- [Google Maps](https://www.google.com/maps/@38.9048728,-77.0362223,17z)

Google is one big multi-page app that contains smaller SPAs, like Google Maps. Same for Trello and Pinterest.

#### Why do people like SPAs?

### Angular

Angular markets itself as being "what HTML would have been, had it been designed for building web apps."

It has lots of functionality built in for rendering data, and swapping views in and out to give the impression of having multiple pages.

Angular is considered a *framework*, not a library.

#### What's the difference between a framework and a library?

Angular is all Javascript, just like jQuery is all Javascript, but it's very picky. Angular forces you to organize your code in a very structured way.

Confusingly, it uses a lot of the same words as Rails, but with different definitions. Please refer to [the comparison to Rails](#references) at the end of this lesson plan.

To introduce Angular, we're going to *do* some Angular.

## Setting up a server

Angular uses a lot of AJAX -- Javascript making requests to another server. When you're viewing an Angular app using `file://` on your computer -- that is, without running it on a server -- this can cause problems.

We're going to download a handy little server that lets us run Angular using `http://`.

```bash
$ npm install -g http-server
$ hs
```

You should see something like:

```
Starting up http-server, serving ./
Available on:
  http:127.0.0.1:8080
  http:172.20.8.228:8080
```

### If you run into trouble

#### First, try:

```
$ sudo npm install -g http-server
$ hs
```

#### If that doesn't work:

```
$ brew uninstall node
$ brew install node
# wait...
$ sudo chown -R "$(whoami)" /usr/local
# wait...
$ brew link --overwrite node
$ sudo npm install -g http-server
$ hs
```

> Where will you go in your browser? For comparison, Rails says this `Listening on localhost:3000, CTRL+C to stop`

From now on, we'll be accessing Angular this way.

## [We Do: Inventory Tracker Walkthrough](walkthrough.md)

## References

### Comparison to Rails

|An Angular [this]... |is like a Rails [that].|
|------------|---------------------|
| module     | gem                 |
| controller | controller's action |
| resource   | model               |
| model      | model's field       |
| directive  | helper              |
| service    | ActiveRecord::Base  |
| view       | view                |

### Screencasts
- WDI8
  - [Part 1](https://youtu.be/e05pA3VSM6I)
  - [Part 2](https://youtu.be/MP2RD5d9RfA)
