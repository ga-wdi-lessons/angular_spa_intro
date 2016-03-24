# Angular and Single-Page Apps

<!-- AM: More LOs? Maybe something about SPAs or important higher-level features of directives/models/controllers. -->
## Learning Objectives
- Explain the difference between directives, models, and controllers in Angular

<!-- NHO: Define how Angular utilizes modules -->

## Framing

Single page apps (SPAs) are so hot right now. Single page does **not** necessarily mean:

> The user sees everything on one page.

It **does** mean:

> The user never *actually* goes to a different page in their browser, but they may *feel* like they do. There's one main `index.html` page, and then other "pages" are really just pieces of HTML that are loaded in and out as necessary.

There's no single definition of a SPA.

Some examples:

- [Hyrule Potion Shop](http://ga-wdi-exercises.github.io/hyrule_potion_shop/)
- [RepoTagger](http://repotagger.github.io/?name=ga-wdi-lessons), which uses Angular
- [Google Maps](https://www.google.com/maps/@38.9048728,-77.0362223,17z)

Google is one big multi-page app that contains smaller SPAs, like Google Maps. Same for Trello and Pinterest.
<!-- AM: Could use this as an opportunity to preview/tie back to the AJAX class. -->

#### Why do people like SPAs?

<!-- NHO: is this a question to pose to the class? Or are you planning on having more follow up to answer?  -->
<!-- Could do a similar compare / contrast as was built into the previous spa lesson  -->
<!--
https://github.com/ga-dc/wdi6-formerly-curriculum/tree/7935ec8271d1d0372dd978be43fd75a015ef90a6/08-single-page-web-apps/single-page-applications  -->


### Angular

Angular markets itself as being "what HTML would have been, had it been designed for building web apps."
<!-- NHO: how does this tie into why people like SPA's?  -->

Angular is considered a *framework*, not a library.,
<!-- AM: ^ Extra comma at end of sentence ^ -->

#### What's the difference between a framework and a library?

Angular is all Javascript, just like jQuery is all Javascript, but it's very picky. Angular forces you to organize your code in a very structured way.

Confusingly, it uses a lot of the same words as Rails, but with different definitions. Please refer to [the comparison to Rails](#references) at the end of this lesson plan.

To introduce Angular, we're going to *do* some Angular.

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

<!-- AM: ^ I love these. ^ -->
