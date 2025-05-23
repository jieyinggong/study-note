---
tags:
  - lec-note
  - temp
  - language
---
![[2. Interactive frontends with JavaScript.pdf]]

###  Practice: 
[[lab 3 - JavaScript]]


**First class functions (functions itself are variables! thus itself can be passed)**

-use es6

mutable v.s. immutable: whether we can point the address. immutable can be only overwrite

array manipulation ← useful

for now either use `const` and `let` : `const` never changed, `let` can be changed:

```jsx

const a = 0 // -> immutable

a = 1 // error

let b = 0 // use for mutable

b = 1 // ok!

```

  
## functions as variables
-what `map` do: for every input in a array and then return a new array (a new instance)

## Tricks  

1. use changing optional operater

2. use triple equals(`===`) always rather than double equals (`==`)


# JavaScript in the browser
- trigger events
- dom : document object model

javascript is limited to what we are viewing (cannot access OS and other tabs)
new API to filesystem (filesystem API)
 
### use separate file: at the end of the body

```jsx

<script src = "js file path">

```

  ---
## DOM

- Tree representation

- within the elements

- use CSS selector
  

### Dom Node selector: selecting elements

Different between `querySelector` and `querySelectorAll` : first only give the first element

  
### DOM method: updating
- Tree based methods
- all the stuffs have to do in the css


## web events
select + add listener: every time some one do the event and then execute the function
event triggered and then sth happened

  

## Observer Design Pattern
#design 

we have something observed → and we have observer to do with it

  

# Good browser JS practices

## Strict mode: “use strict”
```jsx

"use strict";

```

  

## Scoping problem

Closure: encapsulate
When run in the scope (the round bracket `()`),the function become local

```jsx

  

(function() {
  
function getChirps() {} // this one be a local var rather than global var

})();

  
```

  

the global variable will be overwritten

**question**: module and private functions used in the closure

  

## DOM

Difference between the `onload` and `addEventListener`: one event and multiple events trigger
if not use `preventDefault()` : it will use default behavior: reload the page!
when create a new element, it’s a node itself but hasn’t attached to the tree  

- Imperative programming


## Model-View-View model (MVVM)
#design 

  refactor the logic to create and view
use chirpService to do the operation for chirp

  

### Debug

-`console.log`

-`debugger;`

  
**bug reason:** don’t update chirp services and we try to delete the one we have already delete it (because DOM hasn't updated before)

  

Controller never stores data.
js can change everything when changing the DOM

  

**Component**
the edit button that is not the id, we gonna close the edit forms for other chirp
make own event and then make own event listener

  

## meact.js

```jsx

useEffectListeners(key).foreach

```

- setChrips: just auto do everything
- `setActiveChrip` : set the active chirp, whenever the active chirp change, `meact.useEffect()` happen for only active chirp

**use variables rather than use for all DOM**



## dev tool
- console
- debugger

  

# JSON