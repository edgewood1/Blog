
# Web Components Documentation

This file is a consolidation of all the documentation and notes related to Web Components from the `JS-UI libs/Web-components` directory.

---

## Overview.md

# Overview — Web Components

Web Components are a set of standardized browser APIs for building encapsulated, reusable UI elements that work with any framework or no framework at all.

Core building blocks:
- Custom Elements — define new HTML tags with lifecycle callbacks.
- Shadow DOM — encapsulated DOM and scoped styles.
- HTML Templates & Slots — declarative markup for content distribution and reuse.

Why use them:
- Interoperability across frameworks and plain JS.
- Encapsulation of markup, style, and behavior.
- Future-proof: based on web standards rather than a single library.

This repository's `archive/6.web-components/` contained several demos and longer examples (AppDrawer, slot/template demos, lifecycle experiments). Those examples have been consolidated into `APIs.md`, `Examples.md`, and `Best-practices.md`. The original demos remain in `archive/` if you want to restore any interactive samples.


---

## README.md

# Web Components — Guide & TOC

This folder contains consolidated, up-to-date notes and examples for Web Components.

- Overview: Overview.md
- Core APIs: APIs.md
- Examples & Patterns: Examples.md
- Best Practices: Best-practices.md

Legacy/raw notes and example files are left untouched in `6.web-components/` for reference.

If you'd like, I can move older files into an `archive/` subfolder after you review these consolidated pages.

---

## APIs.md

# Core APIs — Custom Elements, Shadow DOM, Templates & Slots

Custom Elements (basic):

```js
class MyElement extends HTMLElement {
  static get observedAttributes() { return ['open']; }
  constructor() {
    super();
    this.attachShadow({ mode: 'open' });
  }
  connectedCallback() { /* called when added to DOM */ }
  disconnectedCallback() { /* cleanup */ }
  attributeChangedCallback(name, oldVal, newVal) { /* react to attr changes */ }
}
customElements.define('my-element', MyElement);
```

Shadow DOM:
- Use `attachShadow({mode: 'open'})` to create an encapsulated root.
- Add styles inside the shadow root so they don't leak out and global styles don't leak in.

Templates & Slots:
- `<template>` holds inert markup you can clone via `document.importNode(template.content, true)`.
- `<slot>` inside a shadow root marks insertion points for light DOM children. Named slots allow multiple insertion points.

Interoperability notes:
- React: React uses its own event system and passes data via attributes; use refs or wrapper components to pass objects or listen to custom events.
- Frameworks: Consider tiny wrappers for idiomatic integration or use libraries like Lit for authoring.

Lifecycle & attributes:
- Use `static get observedAttributes()` to list attributes to watch and implement `attributeChangedCallback(name, oldVal, newVal)` to reflect attribute changes to properties.
- Prefer initializing DOM/template cloning in the constructor but attach event listeners in `connectedCallback` and clean up in `disconnectedCallback`.

Styling and selectors:
- Use `:host` to style the custom element itself from inside the shadow root.
- Use `::slotted()` to style light-DOM children that are projected into slots.
- Use `::part()` when exposing internal elements for styling via the `part` attribute.

Template techniques:
- Keep a `<template>` element in the document (or create one programmatically) and use `document.importNode(template.content, true)` or `tpl.content.cloneNode(true)` to instantiate.
- Insert the cloned template into the shadow root via `this.attachShadow({mode:'open'}).appendChild(clone)`.

Eventing:
- Use `this.dispatchEvent(new CustomEvent('my-event', { detail, bubbles: true, composed: true }))` so events can cross shadow boundaries and be observed by parent components or frameworks.

---

## Best-practices.md

# Best Practices

- Prefer `attachShadow({mode:'open'})` and clone templates into the shadow root.
- Use custom events to communicate upward (`this.dispatchEvent(new CustomEvent('change', { detail }))`).
- Keep APIs attribute-based (strings/primitives) and use properties for richer data when needed.
- Avoid global stylesheet assumptions; scope styles inside the shadow root.
- For production, consider using Lit or Stencil for ergonomics and small runtimes.
- Polyfills are rarely needed for modern browsers; only add them if you must support legacy environments.

- Lifecycle hygiene: avoid heavy DOM work after `connectedCallback` completes; attach event listeners in `connectedCallback` and remove them in `disconnectedCallback`.
- Attribute/property reflection: keep primitive data on attributes and richer objects on properties; reflect attributes to properties in `attributeChangedCallback` when needed.
- Event composition: dispatch `CustomEvent` with `{ bubbles: true, composed: true }` so events cross shadow boundaries and frameworks can observe them.
- Templates: clone template content with `tpl.content.cloneNode(true)` and append to shadow root; prefer pre-declared `<template>` nodes over string `innerHTML` for performance and safety.


---

## Examples.md

# Examples & Patterns

Minimal shadow-root component using a template and slot:

```html
<template id="my-tpl">
  <style> :host { display:block; border:1px solid #ccc; padding:8px } </style>
  <header><slot name="title"></slot></header>
  <div><slot></slot></div>
</template>

<script>
class MyCard extends HTMLElement {
  constructor(){
    super();
    const tpl = document.getElementById('my-tpl');
    this.attachShadow({mode:'open'}).appendChild(tpl.content.cloneNode(true));
  }
}
customElements.define('my-card', MyCard);
</script>

<!-- usage -->
<my-card>
  <span slot="title">Hello</span>
  <p>Content goes here.</p>
</my-card>
```

Vue / build notes:
- To produce a web component from a framework, follow the framework's official build pipeline (for example Vue supports `--target wc`). Prefer using framework docs and current CLI versions rather than ad-hoc commands.

Additional example — AppDrawer (from archived examples):

```html
<template id="app-drawer-tpl">
  <style>
    :host { display:block; border:1px solid #ddd; padding:8px }
    header { font-weight:600 }
  </style>
  <header><slot name="title">Default title</slot></header>
  <section><slot></slot></section>
</template>

<script>
class AppDrawer extends HTMLElement {
  static get observedAttributes(){ return ['open']; }
  constructor(){
    super();
    const tpl = document.getElementById('app-drawer-tpl');
    this.attachShadow({mode:'open'}).appendChild(tpl.content.cloneNode(true));
  }
  attributeChangedCallback(name, oldV, newV){ this[name] = this.hasAttribute(name); }
}
customElements.define('app-drawer', AppDrawer);
</script>

<!-- usage -->
<app-drawer open>
  <span slot="title">Menu</span>
  <p>Drawer content</p>
</app-drawer>

Notes: the archived `6.web-components/index.html` contains a larger AppDrawer demo with multiple subcomponents and examples of `document.importNode` and light-DOM vs shadow-DOM usage; that material has been integrated into the APIs and Best-practices files.

---

## web-components2.raw.md

```markdown
what are web componets? 

1. they are build on existing Web apis
   - CustomElements API (lets you create / register comopnents as new HTML elements that have their own lifecycle.
   - Shadow Dom ~ provides encapsulation of styles so comonet has its own mini-dom such that global styles can't affect it.
   - uses template/slot HTML elements
   - components compatible with nearly every ui framework / library and vanilla JS

what are benefits

2. web standards are more future proof than any given JS library
3. 


react + webomponents

This is both true and false. Web Components themselves work fine, but by default React passes all data to Custom Elements in the form of attributes, meaning you can’t pass objects or arrays without workarounds. Additionally, because React has its own synthetic event system, it cannot listen for DOM events coming from Custom Elements without the use of refs.

Both of these issues can be fixed, but for some they might be showstoppers. For our team the benefits of Web Components far surpassed these and we decided to work our way around these issues by automatically wrapping our Web Components with React based wrappers.


two modes of single page apps

react 
- builds UI components
- state-management files
- uses React classes

lit
- builds web components
- uses JS classes so all properties function as kind of state > no special 'hooks' for these
- props / children passed between components via events(upwards) or passing attributes to children tags (downwards)
- a web component has containerized styling (css-html)

```

---

## index.html

```html
<!DOCTYPE html>
<body>
<h1>I'm outside the CE</h1>
<!-- light dom -->
<template id='hi'> 
  <div>
    shit</div></template>
<app-drawer class ='a' open> 
  <!-- children - only appear if we define slots -->
  <!-- <p> I'm passed into the slot </p>
  <app-drawer2 slot="a"> </app-drawer2>
  <app-drawer3 slot="b"></app-drawer3> -->
</app-drawer>
<!-- if appdrawer doesn't render its children render normally -->

<!-- javascript -->

<script>

// this is shadowDOM because it uses slots
class AppDrawer extends HTMLElement {
  static get observedAttributes() {
    return ['open'];
  }
  
  attributeChangedCallback(attrName, oldValue, newValue) {
    // if (newValue !== oldValue) {
      this[attrName] = this.hasAttribute(attrName);
 
    // }
  }

  // descendant selector (space)
// child selector (>)
// adjacent sibling selector (+)
// general sibling selector (~)
  
  constructor() {
    // set up the basics here
    super()
    // this.innerHTML = `<style>h1{background:green}</style><slot name="b"></slot><h1 class = a>I'm in main CE</h1><slot name="a"></slot>`
    this.template = document.createElement('template');
    // :host() refers to shadowRoot.  h1, h2, and slots are children of shadowRoot; hence >
    // slot won't work because slot is an empty div that contains what's being passed up in light dom. 
    // to access this - i go up
    //   this.template.innerHTML = `
    //   <style>
    //     :host([open])> h1{background:green}
    //     :host([open])> slot{background:red}
    //   </style>

    //   <slot id="b" name="b"></slot><h1>I'm in main CE</h1><h2> I"m second pt CE </h2><slot name="a"></slot> `
    //   this.attachShadow({mode:'open'})
    // this.shadowRoot.appendChild(this.template.content.cloneNode(true))
    const template=document.getElementById('hi');
    console.dir(template)
    const node = document.importNode(template.content, true); // doc fragment
    console.dir(node)
  this.appendChild(template.content);
  this.appendChild(node)
  
    // this.insertAdjacentHTML('beforeend',node)
 

  }
 
  connectedCallback() {
    const template=document.getElementById('hi');
    this.appendChild(template.content)
    this.setAttribute('open1∂', '')
  } 
}

window.customElements.define('app-drawer', AppDrawer);


// so this will work, but not passing it in as an attribute. 
const c = document.querySelector('app-drawer')
// c.open = 'fart'



// OTHER CLASSES


class AppDrawer2 extends HTMLElement {
 
constructor() {
super()
  const template = document.createElement('template');
  template.innerHTML = `<h1> I am app drawer 2 </h1>`
  const node = document.importNode(template.content, true);
  this.appendChild(node);
}
  }
window.customElements.define('app-drawer2', AppDrawer2);

class AppDrawer3 extends HTMLElement {
constructor() {
super()
  const template = document.createElement('template');
  template.innerHTML = `<h1>I'm the third part</h1>`
  const node = document.importNode(template.content, true);
  this.appendChild(node);
}
  }
window.customElements.define('app-drawer3', AppDrawer3);


</script>
</body>
```

---

## 1.intro/

### 1.intro/console.md

$('cs-app').shadowRoot.querySelector('#udiDialog').querySelector(.... )

custom Elements spec is part of Web Components

customElementRegistry interface is a class? 

You can get an instance of it via window.customElements (this is the object)

To register a custom element on the page, you use the CustomElementRegistry.define() method.
However, the example shows the object - 

customElements.define('word-count', WordCount, { extends: 'p' });

life cycles

1. when created
2. when added
3. when removed


https://goo.gl/Ykp35L

we can extend a custom element that extends a native element

### 1.intro/customElements.md

__What are custom elements?__ 

- self-made elements that contain their own semantics, behaviors, markup and can be shared across frameworks and browsers. They exist without third-party frameworks

__how to create one?__

- tech 1 - add innerHTML to the CE (stopped at the end of this).
- tech 2 - create template in HTML and not JS
- tech 3 - create template using JS - add via .innerHTML.
- tech 4 - append node as a shadowroot. 

object life cycles
- constructor > code inserted at moment of creation // happens at moment of 'new'
  - memory allocation (declaration of a variable) - reserving space fo robject
  initialization - assigning values to object fields, runnin g other code (definition of variable / assigning values)
- destructor > code inserted at moment of destruction
    - finalization / removing value
    - memory deallocation // removing from memory


__tech 1__

1. begin with a class that extends a built-in element (would a function work?)? 

- register class in the browser using `customElements.define`

```js
class AppDrawer extends HTMLElement {
  }
window.customElements.define('app-drawer', AppDrawer);
```

2. populate this class with a lifecycle method.  

- 3 such methods include:  

- **constructor** - runs when object (node) is created: `createElement`
  - create shadow DOM here.
  - can't add or set an attribute. ???  

- **connectedCallback** - runs when object / node / component is attached to the DOM via  `appendChild`  

- **attributeChangedCallback** = runs when user changes object's attributes / properties.  
    - we can use a static `get observedAttribute` to notice attribute changes 

How to add node? 

- use innerHTML to add DOM element 

```js
    constructor() {
      super()
        this.innerHTML = `<h1>Hello, World!</h1>`;
    }
  ```
- Place custom element in an html file:

html
```html
    <app-drawer></app-drawer>
```
 

Questions: 
1. what does innerHTML do? It gets or sets the HTML of an element.  T insert the HTML rather than replace contents, use `insertAdjacentHTML()`
2. is that a template strings? string literals that allow for multi=line strings and string interpolation.  Used via backticks. https://hacks.mozilla.org/2015/05/es6-in-depth-template-strings-2/

3. what does "this" refer to?  it refers to the custom-element itself as the object instantiated by the class.  The class is the 'constructor' for the new object/element.  Does this happen in define()?  

##### TECH 2: create template in HTML and not JS

or you might use a template in the html.  a template holds hidden content.  We will copy its contents and add to customelement: 
```html
    <template id="hi"> shit </template>
    <app-drawer></app-drawer>
```
In this case: 
1. get template
2. copy the template notde to document ***
3. append it to the custom element.  
4. append the previous hellow world

```js
    const template = document.getElementById('hi');  // 1
    const node = document.importNode(template.content, true); // 22
    this.appendChild(node); //3
    this.insertAdjacentHTML('beforeend','<p>hello</p>') //4
```

*** use document.importNode() to create a copy of the template’s content and prepare it to be inserted into another document (or document fragment). It takes two argumnts: 
  1. grab the template
  2. use `document.importNode` in order to create a deep copy (gets all the children) of the node/documentfragment held in `template.content`, which holds the fragment that is in the template. 
  3. append this copied node to the customElement.
  4. as a special add, preserve our previous this.innerHTML.  We can't use innerHTML here because it would wipe out the node appended to the child.  WHY?

this could be done inside the constructor or outside the class.

Note: We could have used the template.content directly, as in: `this.appendChild(template.content)`.  This would remove the content from the element and added to the DOM.  But if we wanted to use it later, we'd be unable to.  (it's got a one-time use - any DOM node can only connect to one location).  But if we merely copy it, we can re-use in multiple locations.

Because this is a template, slots will show.

DOM:
```html
<!-- this is still invisble -->
<template id="hi"> 
  #document-fragment
</template>
<!-- this is visible -->
<app-drawer>
  <!-- 'shit' is the fragment from the template -->
  "shit"  
  <h1> Hellow world</h1>
</app-drawer>
```

##### TECH 3: create template using JS - add via .innerHTML.

- this can be done in the constructor or the connected callback - especially if you use `this.template` instead of `const template`

 ```js 
  const template = document.createElement('template'); // 1
  template.innerHTML = `<h1>Hello, World!</h1>` // 2
```
We would copy and append as before.   

### tech 4
or we could append it as a SHADOW DOM element: 
but this would overwrite any other inner HTML defined in the connected Callback - why 

```js
  this.attachShadow({mode:'open'}) // 1
  this.shadowRoot.appendChild(template.content.cloneNode(true)) //2
```
1. create a shadowRoot and attach it to the customElement. `mode:open` elements of shadow root are accessbile from JS outside the roo.  so we can use `element.shdadowRoot`  `mode:closed` denies access ot the nodes of a closed sr from js outside. it. 
2. use `cloneNode` instead of `importNode`.  `cloneNode` returns a duplicate of node on which method was called: `newClone = node.cloneNode([true])`  - true if we clone whole subtree or only node.  `this.shadowRoot` refers to the shadowRoot created and attached - to this we will apend our copied template. 

This creates an encapsulated DOM element (app-drawer) so any style inside it doesn't affect anything else:

```html
<h1>hi</h1>
<app-drawer>
  #shadow-root
    <h1> Hellow world</h1>
</app-drawer>
```

### 1.intro/intro.md

Vanilla.js - webcomponents



Lit-element - library that makes web-components easier

- styling - css module
- templating - html module
- extended lifecycle - litElement module
- property binding
- events
- Decorators -t o use decorators, you need to use a compiler such as Babel or the TypeScript compiler.

---

## 2.Slots-templates/

### 2.Slots-templates/0.customElements.md

# Register custom element with window 

This is an instance of the CustomElementRegistery object? it allows you to regist a custom element on the page, get a list of all custom-elements, etc. 

`window.customElements.define('starter-app', starter)`

* The customElements read-only property of the Window interface returns a reference to the CustomElementRegistry object, which can be used to register new custom elements and get information about previously registered custom elements.

`customElements.define('my-main', MyMain);`
 
- A DOMString representing the name you are giving to the element. Note that custom element names require a dash to be used in them (kebab-case); they can't be single words.
- A class object that defines the behavior of the element.
- Optionally, an options object containing an extends property, which specifies the built-in element your element inherits from, if any (only relevant to customized built-in elements; see the definition below).

So for example, we can define a custom word-count element like this:

`customElements.define('word-count', WordCount, { extends: 'p' });`

The element is called word-count, its class object is WordCount, and it extends the <p> element.

# write the class

A custom element's class object is written using standard ES 2015 class syntax. For example, WordCount is structured like so:

```js
class WordCount extends HTMLParagraphElement {
  constructor() {
    // Always call super first in constructor
    super();

    // Element functionality written in here

    ...
  }
}
```
STOP
This is just a simple example, but there is more you can do here. It is possible to define specific lifecycle callbacks inside the class, which run at specific points in the element's lifecycle. For example, connectedCallback is invoked each time the custom element is appended into a document-connected element, while attributeChangedCallback is invoked when one of the custom element's attributes is added, removed, or changed.

You'll learn more about these in the Using the lifecycle callbacks section below.

There are two types of custom elements:

Autonomous custom elements are standalone — they don't inherit from standard HTML elements. You use these on a page by literally writing them out as an HTML element. For example <popup-info>, or document.createElement("popup-info").
Customized built-in elements inherit from basic HTML elements. To create one of these, you have to specify which element they extend (as implied in the examples above), and they are used by writing out the basic element but specifying the name of the custom element in the is attribute (or property). For example <p is="word-count">, or document.createElement("p", { is: "word-count" }).
Working through some simple examples
At this point, let's go through some more simple examples to show you how custom elements are created in more detail.

Autonomous custom elements
Let's have a look at an example of an autonomous custom element — <popup-info-box> (see a live example). This takes an image icon and a text string, and embeds the icon into the page. When the icon is focused, it displays the text in a pop up information box to provide further in-context information.

To begin with, the JavaScript file defines a class called PopUpInfo, which extends the generic HTMLElement class.

class PopUpInfo extends HTMLElement {
  constructor() {
    // Always call super first in constructor
    super();

    // write element functionality in here

    ...
  }
}
The preceding code snippet contains the constructor() definition for the class, which always starts by calling super() so that the correct prototype chain is established.

Inside the constructor, we define all the functionality the element will have when an instance of it is instantiated. In this case we attach a shadow root to the custom element, use some DOM manipulation to create the element's internal shadow DOM structure — which is then attached to the shadow root — and finally attach some CSS to the shadow root to style it.

// Create a shadow root
this.attachShadow({mode: 'open'}); // sets and returns 'this.shadowRoot'

// Create (nested) span elements
const wrapper = document.createElement('span');
wrapper.setAttribute('class','wrapper');
const icon = wrapper.appendChild(document.createElement('span'));
icon.setAttribute('class','icon');
icon.setAttribute('tabindex', 0);
// Insert icon from defined attribute or default icon
const img = icon.appendChild(document.createElement('img'));
img.src = this.hasAttribute('img') ? this.getAttribute('img') : 'img/default.png';

const info = wrapper.appendChild(document.createElement('span'));
info.setAttribute('class','info');
// Take attribute content and put it inside the info span
info.textContent = this.getAttribute('data-text');

// Create some CSS to apply to the shadow dom
const style = document.createElement('style');
style.textContent = '.wrapper {' +
// CSS truncated for brevity

// attach the created elements to the shadow DOM
this.shadowRoot.append(style,wrapper);

Finally, we register our custom element on the CustomElementRegistry using the define() method we mentioned earlier — in the parameters we specify the element name, and then the class name that defines its functionality:

customElements.define('popup-info', PopUpInfo);
It is now available to use on our page. Over in our HTML, we use it like so:

<popup-info img="img/alt.png" data-text="Your card validation code (CVC)
  is an extra security feature — it is the last 3 or 4 numbers on the
  back of your card."></popup-info>
Note: You can see the full JavaScript source code here.

Internal vs. external styles
In the above example we apply style to the Shadow DOM using a <style> element, but it is perfectly possible to do it by referencing an external stylesheet from a <link> element instead.

For example, take a look at this code from our popup-info-box-external-stylesheet example (see the source code):

// Apply external styles to the shadow dom
const linkElem = document.createElement('link');
linkElem.setAttribute('rel', 'stylesheet');
linkElem.setAttribute('href', 'style.css');

// Attach the created element to the shadow dom
shadow.appendChild(linkElem);
Note that <link> elements do not block paint of the shadow root, so there may be a flash of unstyled content (FOUC) while the stylesheet loads.

Many modern browsers implement an optimization for <style> tags either cloned from a common node or that have identical text, to allow them to share a single backing stylesheet. With this optimization the performance of external and internal styles should be similar.

Customized built-in elements
Now let's have a look at another customized built in element example — expanding-list (see it live also). This turns any unordered list into an expanding/collapsing menu.

First of all, we define our element's class, in the same manner as before:

class ExpandingList extends HTMLUListElement {
  constructor() {
    // Always call super first in constructor
    super();

    // write element functionality in here

    ...
  }
}
We will not explain the element functionality in any detail here, but you can discover how it works by checking out the source code. The only real difference here is that our element is extending the HTMLUListElement interface, and not HTMLElement. So it has all the characteristics of a <ul> element with the functionality we define built on top, rather than being a standalone element. This is what makes it a customized built-in, rather than an autonomous element.

Next, we register the element using the define() method as before, except that this time it also includes an options object that details what element our custom element inherits from:

customElements.define('expanding-list', ExpandingList, { extends: "ul" });
Using the built-in element in a web document also looks somewhat different:

<ul is="expanding-list">

  ...

</ul>
You use a <ul> element as normal, but specify the name of the custom element inside the is attribute.

Note: Again, you can see the full JavaScript source code here.


# 5. export class and add the custom tag to the imported file 

 

### 2.Slots-templates/litHTML.md

lit-html = html imported from @polymer/lit-element

static elements: 
html`<div>hi</div>`

expression: 

html`<div>${disabled?'off':'on'}</div>`

attribute 

html`<div class$="${color} special"></div>`

event: 

html`<button on-click="${(e)=>this.clickHandler(e)}"></button>`

use custom libraries - 

import 
npm install --save
@polymer/paper-checkbox@3.0.0-pre.21

----------

shadow dom - a dom feature
- a scoped sub-tree inside your element
- shadow host > <my-element> 
- shadow root > #shadow-root
- shadow tree > elements within the root

part of a components implementation that outside elements don't need to know about
polymer attaches a shadow root for each instance of the element an dcopies the html comment into the shadow tree - this may include style

slot elements

added to shadow tree
shows where child nodes would render
instance: <my-header>hi</my-header>
class: <header><h1><slot></slot></h1></header>
slot holds "hi"... i could also move hi by changing slot

named slots - used for multiple slots? no name becomes default
accept top level children

<my-header><span slot="title">A head</span></my-header>

<header><h2><slot name="title></slot></h2></header>

styles

### 2.Slots-templates/mixins.md

a mixin provides methods that implement a certain behavior, but we do not use it alone, we use it to add the behavior to other classes.

https://www.webcomponents.org/element/@polymer/app-layout/behaviors/AppScrollEffectsBehavior

what does a mixin look like? 

how do you add one? 

### 2.Slots-templates/slots copy.md

flattening - virtual Dom present for the purpose of rendering and event handling.  

not flatteneed - the way the code is actually written - this is how js sees it.  span elements with slot attributes to be inserted are still outside their slots. slot elements are empty.  


An HTMLSlotElement instance, or null if the element is not assigned to a slot, or if the associated shadow root was attached with its mode set to closed (see Element.attachShadow for further details).

Examples
In our simple-template example (see it live), we create a trivial custom element example called <my-paragraph> in which a shadow root is attached and then populated using the contents of a template that contains a slot named my-text.

When <my-paragraph> is used in the document, the slot is populated by a slotable element by including it inside the element with a slot attribute with the value my-text. Here is one such example:

<my-paragraph>
  <span slot="my-text">Let's have some different text!</span>
</my-paragraph>
In our JavaScript file we get a reference to the <span> shown above, then log a reference to the original <slot> element the <span> was inserted in.

let slottedSpan = document.querySelector('my-paragraph span')
console.log(slottedSpan.assignedSlot); // logs '<slot name="my-text">'

only works on slotted elements: 

HTMLSlotElement
The HTMLSlotElement interface of the Shadow DOM API enables access to the name and assigned nodes of an HTML <slot> element.

Properties
HTMLSlotElement.name
DOMString: Can be used to get and set the slot's name.
Methods
HTMLSlotElement.assignedNodes()
Returns the sequence of elements assigned to this slot, or alternatively the slot's fallback content.
Examples
The following snippet is taken from our slotchange example (see it live also).

let slots = this.shadowRoot.querySelectorAll('slot');
slots[1].addEventListener('slotchange', function(e) {
  let nodes = slots[1].assignedNodes();
  console.log('Element in Slot "' + slots[1].name + '" changed to "' + nodes[0].outerHTML + '".');
});

### 2.Slots-templates/slots.md

ways to pass things into a component

1. attributes - this passes in the variable 5
<header start='my name'></header>

2. slots

<header>my name</header>


header component {

static get properties(){
  return {
    start: string
  }
}
  

static get template() {
  return html`
  <slot></slot>                     // equiv. of <div> my name </div>
  <button></button>
  `
}

OR 

static get template() {
  return html`
  <div> {{${start}}}                  // equiv. of <div> my name </div>
  <button></button>
  `
}

 
  

}

divs with slot attributes passed into child div name in the parent

<header>
        <div slot='a'>insert </div>
        <div slot='b'>insert</div>
</header>

header cmponent {
  static get template() {
    return html`
      <slot name="a"></slot>
      <div> fourth </div>
      <slot name="b"></slot>
  }
}

PASSING A STRING: doesn't require divs w/slot attributes in the parent OR name attributes in the child

<header> whatever </header>

header cmponent {
  static get template() {
    return html`
      <slot></slot>
      <div> fourth </div>
      <slot></slot>
  }
}

Light DOM are inserted through slot elements

### 2.Slots-templates/templating.md

JavaScript templating refers to the client side data binding method implemented with the JavaScript language. 

Templating and JSX are considered Domain Specific Languages (DSL). A DSL is an abstraction to a particular part of your application. In our cases, both templating and JSX are DSLs for interacting with the user interface.

https://medium.com/modern-user-interfaces/dear-templating-sincerely-jsx-part-1-1df99c599001

google: is jsx a templating language
what is a js template

template tag

---

## 3.styling/

### 3.styling/2.style.md

Templates and Slot - 

slot tag only works in shadowDOM elements!!!

We can nest elements inside our light-DOM element and they will be rendered.
The browser represents these elements as NODES (which are objects) on the DOM (document object)
HTML becomes bytes, which the browser translates to DOM tree. 

<app-drawer>
  <p> whatever </p>
<app-drawer>

How, if we try to next elements inside a shadowDOM element, nothing will happen - they will be invisble. 
UNLESS, we make space for them in app-drawer's shadowDOM.  We do this using a <slot> element: 

  template.innerHTML = `<h1>Hello, World!</h1>
  <slot> </slot>`

  Above, we show where the child element passed to app-drawer will go. 

  We could also have multiple elements passed in, and they will appear in order. 

  Or we can designate using the name attribute.

<app-drawer>
  <p slot="a"> whatever </p>
    <p slot="c"> whatever </p>
      <p slot="b"> whatever </p>
<app-drawer>

Consider: 

  template.innerHTML = `<h1>Hello, World!</h1>
  <slot name ="c"> </slot>
  <p> next </p>
  <slot name="a"></slot>`
 
 GETTERS AND SETTERS

 a property getter and setter that will keep the property and attributes in sync by setting the element’s attribute when the element’s property gets updated. The attributeChangedCallback does the inverse: updates the property when the attribute changes.



 How to set up to accept attributes? 

  // A getter/setter for an open property.
  get open() {
    return this.hasAttribute('open');
  }

  set open(val) {
    // Reflect the value of the open property as an HTML attribute.
    if (val) {
      this.setAttribute('open', '');
    } else {
      this.removeAttribute('open');
    }
    this.toggleDrawer();
  }


Sources

https://css-tricks.com/creating-a-custom-element-from-scratch/

### 3.styling/classList.md

using classes in css dev

cslx


observer / 

  /** The current value:  */
  @property({ type: String, notify: true, observer:'addLabelFloat' })
  value: string = '';

  @property({ type: Boolean, notify: true, observer:'addWidth' })
  width: boolean = false;

  addWidth(newValue) {
    if (newValue) {
      const input = this.shadowRoot.querySelector('input')
      input.style.width = '256px'
    }
  }
  addLabelFloat() {
    const label = this.shadowRoot.querySelector('label')
    label.classList.add('mdc-floating-label--float-above');
  }
=======
  /** The current value */
  @property({ type: String, notify: true, observer: MdcTextFieldComponent.prototype._valueChanged })
  value: string = '';

  private _valueChanged(value, oldValue) {
    if (!oldValue && value) {
      this.shadowRoot.querySelector('label').classList.add('mdc-floating-label--float-above');
    } else if (!value) {
      this.shadowRoot.querySelector('label').classList.remove('mdc-floating-label--float-above');
    }
  }

### 3.styling/decorators.md

__query__

import { customElement, property, query } from '@polymer/decorators';

 @query('#appNotification')
  appNotification: PaperToastElement;

  @query('#editStatementDialog')
  editStatementDialog: PaperDialogElement;

__properties__

  /** Name of the currently selected page. */
  @property({ type: String, reflectToAttribute: true, observer: '_pageChanged' })
  page: string;

  /** Currently selected study ID */
  @property({ type: Number })
  studyId: number;

  __JS docs__

  

var car = {
  @readonly
  name: "jack"
}


function readonly(target, key, descriptor) {
  descriptor.value = "mel"
  return descriptor
}

### 3.styling/hostContext.md

https://polymer-library.polymer-project.org/3.0/docs/devguide/style-shadow-dom


https://github.com/vaadin/vaadin-date-picker/issues/604

<!DOCTYPE html>
<html>
<head>
  <script src="bower_components/webcomponentsjs/webcomponents-lite.js"></script>
  <link rel="import" href="bower_components/vaadin-date-picker/vaadin-date-picker.html">
</head>  

<body style="height: 100vh">
  <dom-module id="my-custom-stuff" theme-for="vaadin-text-field">
    <template>
      <style>
        :host([theme="my-theme"]) [part~="label"] {
          color: red;
        }
      </style>
    </template>
  </dom-module> 
  
  <vaadin-date-picker label="My label" theme="my-theme"></vaadin-date-picker>
  
</body>

</html>

https://meowni.ca/posts/polymer-2-cheatsheet/

https://www.w3schools.com/jsref/met_node_appendchild.asp

https://meowni.ca/posts/part-theme-explainer/

https://www.bennadel.com/blog/3484-using-css-host-context-to-theme-components-in-angular-6-1-3.htm

### 3.styling/style.md

CSS

1. class = getClass()
2. class = variable
3. property > reflectToAttribute / :host([attr])
4. event > listen then varible = x
5. pass an attribute (create an attribute)
6. clsx - https://www.npmjs.com/package/clsx
7. javascript
8. host(context)
9. custom props


10. getClass()

  getClass() {
    return this._prevStudyVisible ? null : 'bottom'  
  }

 <mdc-fab class$="[[getClass()]]" id="saveFAB" icon="cs:save" on-tap="save" disabled="[[_shouldDisplayLoading]]"></mdc-fab>

5. 

 one element

         <mdc-textfield
          .label="${this.label}"
          @focus="${this.handleFocus}"
          ?opened="${this.open}"
          trailing-icon="paper-dropdown-menu:arrow-drop-down"
          slot="anchor"
          .value="${label}"
          ?clear="${this.clear}"
          ?disabled ="${this.disabled}"
          ?width="${this.width}"
        ></mdc-textfield>

 import clsx from 'clsx';

     <div class$="[[_generateClassNames(trailingIcon)]]">
      <dom-if if="[[trailingIcon]]">
        <template>
          <iron-icon
            class="material-icons mdc-text-field__icon"
            icon="[[trailingIcon]]"
          ></iron-icon>
        </template>
      </dom-if>


       _generateClassNames(trailingIcon) {
    return clsx('mdc-text-field', {
      'mdc-text-field--with-trailing-icon': trailingIcon !== null,
    });
  }

  ## Css

# attribute selector 

```css
a[target] {
  background-color: yellow;
}
```

above will select any tag that has a target attribute <a target="hello">

# polymer root

This.classList.add(‘something) // 

- you can create a property, like `population` with a value of `500` and assign it `Reflect to attribute`
- if you're doing this in `<app-name>` then this will appear as `<app-name population="500">`
- or if you add a class, like this.classList.add('something'), which adds a class="something" to the attribute (`this`)
- if study page has a class of something, ou could say: 
:host(.something)  {}   *** see Line 396 convention

https://www.html5rocks.com/en/tutorials/webcomponents/shadowdom-201/

host context


mdc-textfield
input {
width: var(--mdc-textfield-input-wide, 256px)
}
define in study page

give css dropdown an id 

#cs-dropdown {
     --mdc-textfield-input-width: 56px
}



custom variables

1. declare custom property in the :root psuedo-class
:root {
  --main-bg-color: brown;
}

2. use the var() function, and pass in the custom property - in this case, red is teh fall back if 

.one {
  color: white;
  background-color: var(--main-bg-color, red);

3. use values in js


element.style.getPropertyValue("--my-var");

dynamic classeless


.top-margin-2 {
    margin-top: 2em;
}
.top-margin-5 {
    margin-top: 5em;
}
Then you can generate your HTML with class="top-margin-#{margin}"


use less or sass



override previous classes

There are different ways in which properties can be overridden. Assuming you have

.left { background: blue }
e.g. any of the following would override it:

a.background-none { background: none; }
body .background-none { background: none; }
.background-none { background: none !important; }
The first two “win” by selector specificity; the third one wins by !important, a blunt instrument.

You could also organize your style sheets so that e.g. the rule

.background-none { background: none; }
wins simply by order, i.e. by being after an otherwise equally “powerful” rule. But this imposes restrictions and requires you to be careful in any reorganization of style sheets.

These are all examples of the CSS Cascade, a crucial but widely misunderstood concept. It defines the exact rules for resolving conflicts between style sheet rules.

P.S. I used left and background-none as they were used in the question. They are examples of class names that should not be used, since they reflect specific rendering and not structural or semantic roles.

setting  custom properties

https://vanseodesign.com/css/custom-properties-and-javascript/

How to style node-modules? 

see styles folder

 
https://stackoverflow.com/questions/49722415/vaadin-component-styling-confusion

---

## 4.properties/

### 4.properties/data_binding.md

__nomenclature__

parent / host class containst a host-proprty

it contains a child-element, which is represented by a child class, which contains a child-property (the target property).

we bind the host-property (5) to the child-property. 


hostProperty = 5

<child-element child-property="{{hostProperty}}">

in this child element / class, the hostproperty will be accessed via child-property

But this translates into `childProperty`.  Polymer maps attribute names + property names in a specific way:  

- Dash-case becomes camelCase as prop:  first-name > firstName

- cambelCase in attribute becomes lowercase in prop: firstName > firstname


__notes__

if binding to built-in attribute, such as href, src, etc? We add a `$` afterwards: 
 
<a href$="{{hostProperty}}">

to booleans? Use a `?` afterwards (or is it $?)

<a test? ="{{}}" >

built-in | href$
booleans | test?

 
  
| Type          | Lit Element         | Polymer   |
| ------------- | ------------------- | --------- |
| Text content  | <p>${...}</p>       | -         |
| Attribute     | <p id="${...}"></p> | -         |
| Boolean       | ?disabled="${...}"  | disabled? |
| Property      | .value="${...}"     | -         |
| Event handler | @event="${...}"     | -         |
| built-in      | -                   | href$     |


__STEPS__

1. parent assigns value to an attribute inserts into element

```js
     <my-test user-name="hello"></my-test>
```
2. child creates a property equivalent and uses property however it likes. 

```js
  static get properties() {
    return {
      userName: String
    }

    static get template() {
      return html`
        <div> {{userName}}  </div>
      `
    }

    miscellaneous() {
      if (whatever) {
        this.userName
      }
    }

  ```





https://mderriey.com/2015/11/03/properties-attributes-in-polymer/

https://stackoverflow.com/questions/42321542/how-to-pass-an-array-as-elements-attribute

### 4.properties/notify-reflect.md

**notify v reflect**

| polymer            | lit          | meaning                                                                             |
| ------------------ | ------------ | ----------------------------------------------------------------------------------- |
| reflectToAttribute | attribute    | adds attribute to dom / for CSS use & allows parent prop to pass down to child prop |
| notify             | custom-event | notifies parent of change - doesn't require reflect                                 |

**reflect (lit)**

```js
  @customElement('cs-textfield')

  @property({ type: Boolean, reflect: true, attribute: 'left-side' })
  leftSide: boolean = false;
```

`:host([left-side]) div { background-color: green }`

- now leftSide will appear as `left-side` in element tag 
- we can than style based on its presence. 


`<cs-textfield leftSide> </cs-textfield>`



**Notify (polymer)**

- this is used for 2-way binding (namely, upward data flow)
- when property changes, an event property-name-changed is fired.
- a change to `this.firstName` fires `first-name-changed`.
- these events don't bubble, so listneer must be added directly to element

In addition, 

Notify property in child `someProp`

use child element in parent element

pass in a `some-prop = "{{someProp}}"` as an attribute to child element



- child changes > adult changes (viceversa)



 * in polymer, special methods are sometimes used to notify of change:  
 * 

 nortifyPath 
 notifySplices -

 this.notifyPath('address') won't pickup a change on address.street

* behidn the scenes, it fires a propert-name-changed event
  - `this.firstName` changes, then `first-name-changed`fires 
  - `this.intersecting` changes, so `intersecting-changed` fires

__lit element__

- you do this functionality yourself via: 

* add event listener ( do it directly to element generating event since there's no bubbling) 

* dispatch custom event in child, listen in parent 

 

### 4.properties/observer-computed.md

__polymer / observer__

observers are called whenever this value changes
it passes in the new / old value 

```js
  active: { type: Boolean, observer: '_activeChanged'}
     
  // Observer method defined as a class method
  _activeChanged(newValue, oldValue) {
    this.toggleClass('highlight', newValue);
    num ++ // num increases with each change
    this.mod = newValue + num

  }
```

__polymer / computed__

- returns a new value for a particular 
- in instance of a "derived prop", result of combining other props / consuming data vs direct props which provides data. 

```js
  active: { type: Boolean, computed: '_activeChanged(otherProp)'}
     
  // maybe this prop maintains the sum of all other items... 
  _activeChanged(otherProp) {
    return otherProp + this.mod; 
  }
```



__litelement / computed__

- use update / updated lifecycle 

```js
updated(changedProperties) {
  if (changedProperties.has('a') || changedProperties.has('b') ) {
    this.a = this.b + this.c
  }
}
```
here, the arg is a map of all changed props.  If one of the provider props are included, then we should re-calculate the consuming prop: 

- use getter / setter
```js
get my-prop() {
  return prop1 + prop2
}

set prop-name(value) {

}

```

__both__
```js
@property ({ type: Boolean, computed:'test(edit)', observer: 'now'})
  canEdit: boolean;
  
  test(newV) {
   // takes another value and toggles it
   return !newV
  }

  now(nv, ov){
    // we can then observe when this ioccurs
    console.log('data list', this.canEdit)
  }
```

__non-observed subproperties__

- lit-element only sees changes to the reference to the array, 
- so if we only change a single item or a property on an object, this reference won't change. 
- reference is the "address in memory"
- to create a new address in memory, we can used Object.asign OR use a spread

Invokes effects: 

`this.owner = 'Jane';`

does not: 

`this.owner.age = 5`

requires

this.owner = { ...this.owner }

OR 

`this.set('address.street', 'Half Moon Street');`

ARRAYS? 

this.address = [ ...this.address ]

OR 

``this.push('users', { name: 'Maturin'});``

__litElement__


num | polymer                    | litElement
----|----------------------------|-------------------------------------
1   | observer:string            | updated or? << actually its update>>



- use update/updated lifecycle


  update(changed: Map<string, any>) {
    if (changed.has('selectedFile') || changed.has('showDrawer')) {
      this.drawerOpened = this.selectedFile === null || this.showDrawer;
    }

if DOM updated and rendered, this method called, which highlights any property changes.  
Use this to observe and act upon property changes.
`changedProperties` is a Map. Keys are the names of changed properties; Values are the corresponding previous values.
  

  The get() method returns a specified element from a Map object: 

```js
updated(changedProperties) {
  if (changedProperties && changedProperties.get("focused") === false) {
    // Focus the amount input field, each time focused changes from false
    this.shadowRoot.getElementById("amountInput").focus();
  }
}
```


https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map

 The has() method checks if a prop is present - it will be present if it has changed: 
updated(cp) {
  if (cp.has("))
}

looping throuhg: 

```js
    changedProperties.forEach((oldValue, propName) => {
      console.log(`${propName} changed. oldValue: ${oldValue}`);
    });
```

### 4.properties/options.md

Decorator (requires TypeScript or Babel)

export class MyElement extends LitElement {
  @property(options) 
  propertyName;
In either case, you can pass an options object to configure features for the property.

Property options
The options object can have the following properties:

attribute
Whether the property is associated with an attribute, or a custom name for the associated attribute. Default: true. See Configure observed attributes. If attribute is false, the converter, reflect and type options are ignored.

converter
A custom converter for converting between properties and attributes. If unspecified, use the default attribute converter.

hasChanged
A function that takes an oldValue and newValue and returns a boolean to indicate whether a property has changed when being set. If unspecified, LitElement uses a strict inequality check (newValue !== oldValue) to determine whether the property value has changed.

noAccessor
Set to true to avoid generating the default property accessor. Default: false.

reflect
Whether property value is reflected back to the associated attribute. Default: false. See Configure reflected attributes.

type
A type hint for converting between properties and attributes. This hint is used by LitElement’s default attribute converter, and is ignored if converter is set. If type is unspecified, behaves like type: String. See Use LitElement’s default attribute converter.

### 4.properties/poly_data_binding.md

Consumer / provider

A host provides data, which is consumed by the target
If one element is bound to the data of another, 
it will reflect automatically any change in data? 

Data binding

Host element (parent?)
Target element (child?)

<target-element target-property = "{{host-property}}>>

Binding 
- the equation / attribute within the start tag.  
- a binding is a kind of attribute
- an other kind: href="https://google.com" (here we are not binding properties) 
- we bind a host-element property to how this property will be represented in the target
- do we say a 'host-property is bound to a target-property' and vice versa? 

Observing

I can observe an element's propety for data changes
If it changes, I can take actions, called "property effects"
3 kinds of property effects (3 ways of acting on data changes)
- observer - a callback invoked
- computed - a virtual property computeddatabinding 
- annotations that update propes, attributes, textcontent of DOM node when data changes. 

Processes

- refer to the above html tag
- broswer parses this into an HTML object
- the attribute becoems a property on this object
- then the HTMLobject becomes a DOM node?

---

## 5.events/

### 5.events/events.md

set events

      this.dispatchEvent(new CustomEvent('selected-changed', {
        bubbles: true,
        cancelable: true,
        composed: true,
      }));



      const index = this.getIndexForEl_(e.target);
      const { item } = this.cache_[index];
      this.selected = item[this.itemValue];
      this.dispatchEvent(new CustomEvent('selection-updated', {
        detail: item[this.itemValue],
      }));

### 5.events/onChange.md

how to signal that textContent has changed? 

onchange property (study-fields mixin)

      <mdc-textfield
            label="Bp"
            id="Bp"
            name="Bp"
            type="text"
            value=""
            
            onchange = "{{onChange}}"
            data-study = "{{study}}"
            disabled = "[[!_canEditDemographics]]"    
            dynamic-width
            required> 
        </mdc-textfield>




datalist - remove "age unit" into label

---

## 6.composition/

### 6.composition/super.md

__super__

When do we need to call super()?

super() calls the constructor of the element's superclass (parent class). If an element's definition defines a class that extends another class and super() is not called explicitly, the element calls the constructor of the superclass by default.

When does this call need to be inside the constructor() function?

The proper place to call super() is inside the element's constructor() method.

And what are the consequences of not calling super() as appears in the case of the Shop app?

In the case where,

class MyElement extends Polymer.Element {...}
as in the case of the Shop App — the Polymer.Element constructor is called by default if super() is not called explicitly.


 

### 6.composition/whyCreateComp.md

----

 1. keep the textfield component generic. 
 
 Some of the styles are very specific to the context it is being used in rather than the state of the component. This makes the component less generic. See my comments below.


mdc-textfield.ts // :host([search]) #main 
 
 b. These can be moved to inbox-page in a mixin. For example, with the second one:

mdc-textfield.ts // :host([search]) #my-textfield

 2

Make a new component (like cs-clear-textfield) which contains the clear icon and texttfield in its shadow DOM and a property that determines whether the icon is before or after the textfield. That way text clearing logic can be contained and re-used even outside the inbox.


- moved the style to inboxpage as mixin
- change attribute 'search' to 'hide-label' AND it's a property in textfield - but not base... one is imported to the next... 
- 
 

We can talk about this when we meet, but essentially, but in _handleFlagchange, the chrome and ipad/safari event objects seemed to be built a little different. 

At one point, I created a flaggedStates object built around { Id: Flag, ... } for all the loaded studies, but when I refered to them in the <dom-if if="{{flaggedStates.item.Id}}"> but this didn't work either. 

id for that cell? 

---

## 6.life-cycles/

### 6.life-cycles/lifecycle-lit.md

__ORDER CALLED__

see app/src/index

1. constructor()
2. connectedCallback
4. update (n/a)
5. render
6. firstUpdated
7. updated

**constructor** - 
 - element created

**connected callback** 
- element inserted into DOM (so available to querying) / node present on document.  
- access to lightDOM.super 

**should update*** (optional) 
- called if requestUpdate() called 
- called if prop values change. 
- asks - should we run the render cycle? 
- parameter outputs: 
  - map of prop name + old value
- only updates if returns true.

  - here, create query assignments for easy access / prelim work, like auto focus.: 
    `this._form = this.shadowRoot.getElementById("form");`
  - if prop set here, element update triggered  
  - Use this only if there is no other way of calling declarative templates / functions via render

	```js
  shouldUpdate(changedProps) {
		return changedProps.has('person');
  }
  ```

**update** - n/a

- reflects property values to attributes 
- calls render to render DOM via lit-html. 
- Provided here for reference. 
- don’t override or call this method.  

**render** 
- element rendered on the screen  0 render 
- don't run side effects here. 

**firstUpdated***

**updated*** 

- after updating, we do what?


__What runs on a property change (order)__
    
- shouldupdate*
- render
- updated

__other things that run (under the hood? / behind the scene)__

someprop.hasChanged
reuestUpdate
performUpdate
updateComplete

__details:__

__what happens when value assigned to prop?__

- hasChanged called and returns true
- performUpdate called, which asks: is there a previous request pending? 
  - Yes ~ do nada; 
  - No ~ create a promise (a micro-task) to execute render - async way of ... 

__when a value assigned to a 2nd prop__

- hasChanged called, returns true,  
- performUpdate called, ... blah
- is updateComplete promise resolved? completes after update cycle... 
- when no tasks on the stack, we executed micro task: 
- shouldUpdate called, which gets props changed and their old values - this method evalutes all batched changes and based on that decide if upate hsould be done.  it always returns true, unless we want special logic to avoid update.  
- update called - which relfects changes to attributes to maintain synchrnoy between props and atrtributes - if prop defined with Reflects
- render called, which updates DOM
- firstUpdated runs if first time- another hook that lets us over-writeif we need to do initiliazation tasks after rendering
- updated called - another hook - always called
- updateComplete promise resolved. 


### 6.life-cycles/lifecycle-poly.md

__Order__ 

lifecycle


1. **constructor()**

- fires before  DOM loading & get properties()
- declare / define a property / default values
- manually setting event listeners for the element itself.

2. __attributeChangedCallback__
- if element's attributes are changed, appended, removed, or replaced.
- Invoked when component attribute changes.
- Can be called multiple times during the lifetime of an element.

3. __ready__ 
- what is this, really? 
- Called once, when element attached to the document.  
- fired only once so work can be overwritten 

4. __connectedCallback__- 
- invoked whenever elmement inserted into DOM. 
- adding document-level event listeners.  
- can be called multiple times unlike constructor 
- items need to be disconnected, else do elsewhere

# On Close

5. __disconnectedCallback__  
Invoked when a component is removed from the document’s DOM.
- removing event listeners added in connectedCallback.


 

All lifecycle methods need to call the super method.


### 6.life-cycles/lit-element-rendering.md

efficient rendering
le batches property updates
rerendering is done asynchronously
this is the update process

toAttribute - copies changes in property to toAttribute
fromAttribute - reverse: prop to toAttribute

hasChanged - checks to see if prop has changed 
setter - sets value to prop
getter - 

el.title = 'x' // before it was 'y'

- this fires the 'title' prop setter
- setter calls hasChanged, which returns true  
- since true, performUpdated called, which asks is previous request pending? 
- if there is - if a UI update is pending, it does nothing but get in line
- if there isn't it creates a micro-task (a promise) to execute the rendering 
- on the next round, the render is executed and the promise is fulfilled. 
- this use of a promise is called 'async rendering'
- if more prop changes occur before this render, they merely pile in line
- after we're done updating we say 'await el.updateComplete'
- thus it pauses until update cycle is over.
- since we have no commands, there are no more tasks on the stack
- thus, the microtask can execute.  (step 1): 
- it invokes shouldUpdate, whic recieves the props that have changed + their old values
- it will compare all these to see if a change should be done. 
- usually it reutrns true, but we can include instances where we want to avoid the update
- if shouldUpdate recieves a title value of 'no title' or undefined, then don't update.
- when shouldUpdate returns true, then update is executed, which reflect changes to attributes 
- then it calls render, updating the dom
- if first render, firstUpdated is called - allows us to submit initialization tasks
- then, updated fired.  after render
- then updateComplete promise gets resolved

Summary
- if you say a = "hello", this fires the setter for the prop 
- setter > hasChanged > perform/requestUpdate 
- peforemUpdate microtask consists of: 
  - shouldUpdate
  - update
  - render
  - updated 
  - resolve updateComplete 

  when you define a property, you allow litelement to control them such that any change to it will fire a setter.  


  manual rendering: requestUpdate 
we use this when we define our own setter and we want ta change in the property to cause a re-renderingconrolled props already have setters that evaluate if prop has changed, adn if so they are updated.
if we write our own setter, we lose that . 
so in the stter, we use. it. 

set title(value) {
  if (this._title !=== value) {
    const oldValue = this._title;
    this._title = value;
    this.requestUpdate('title', oldValue); // Called from within a custom property setter
  }
}

https://dev.to/julcasans/litelement-in-depth-the-update-lifecycle-18nk

polymer will not detect chages to sub-properties
does litelement have this issue?

next read long live... 

---

## 7.dependencies/

### 7.dependencies/lit-refactor.md

vaadin dialog - using the renderer function in lit-element:


1. create a function that renders html
2. create a bound prop - defined against its class
3. bind it in constructor
4. add it as a property to vaadin dialog element

https://vaadin.com/components/vaadin-dialog/html-api/elements/Vaadin.DialogElement


https://vaadin.com/forum/thread/17760006/events-from-vaadin-dialog-box-not-firing

https://glitch.com/edit/#!/vaadin-dialog-renderer?path=app.js%3A1%3A0


mwc-button clicks

1. add an eventhandlers to element @tap="${this._attemptLogin}"
2. add change handlers on mdc-textfield @change="${this.valueChange}"
3. in this function get equate:  source.id === 'username' ? (this._username = source.value) : (this._password = source.value);

** any eventhandler placed on an element has to be registered in the constructor like this: 
this._hideDebug = this._hideDebug.bind(this)

How to best hand super.update(sharedProps) so it's more like a computed? can we check this? 

https://github.com/Polymer/lit-element/issues/30

call `super.update()` at teh end to make sure computed properties are part of same render cycle

Since we can interpolate actual JavaScript expressions, we don't need any of the computed binding methods from our polymer-based implementation. We likewise don't need the property getters and setters from the vanilla version, since LitElement has its own mechanism for managing properties and attributes.


imports

add computed and observers to update

convert dom-if

render() {
    return html`
    ${elevationStyles}
    <div id="inputContainer">	    
    

    return html` 
      -  element tags follow
        - if you want to start js, then ${
          - if you want to include html inside this, html`

    
    return html`<div id="inputContainer">
      <cs-date date="{{startDate}}"></cs-date>	      <cs-date date="${this.startDate}"> </cs-date>
      <dom-if if="{{endDate}}">	      ${this.endDate ? html`- 
        <template>-<cs-date date="{{endDate}}"></cs-date></template>	       <cs-date date="${this.endDate}"></cs-date>
      </dom-if>	      ` : html``}
    </div>	    
  </div>



convert attributes

### 7.dependencies/material.md

https://material.io/components/menus#dropdown-menu

### 7.dependencies/material_components/

#### 7.dependencies/material_components/dialogBox.md

# DIALOG BOXES
1. add html
2. create query reference to its id
3. create a function that opens / closes
4. style using id

# VAADIN

1. html
```html
    <vaadin-dialog id="assignSiteDialog">
      <template>
        <vaadin-combo-box label="Site" items="[[_allowedSiteCodes]]" value="{{_selectedSiteForAssignment}}"></vaadin-combo-box>
        <div class="actions">
          <mwc-button dense on-tap="_closeSiteAssignmentDialog">Cancel</mwc-button>
          <mwc-button dense disabled="[[eqq(_selectedSiteForAssignment, '')]]" raised on-tap="_confirmSiteAssignment">Assign</mwc-button>
        </div>
      </template>
    </vaadin-dialog>
```
2. query reference

```javascript

$: {
    assignMDDialog: Element;
    assignSiteDialog: Element;
    readingMDComboBox: Element;
    settingsDrawer: Element;
  };
```

3. close/open functions

```javascript
  private _openSiteAssignmentDialog() {
    (this.$.assignSiteDialog as any).opened = true;

    const dialog = (this.$.assignSiteDialog as any);
    // The first focusable element is a div. I have found that it does not receive focus when the
    // dialog opens.
    dialog.$.overlay._cycleTab(1, 0);
  }

 private _closeSiteAssignmentDialog(): void {
    (this.$.assignSiteDialog as any).opened = false;
    this._selectedSiteForAssignment = '';
  }
```

# PAPER

√Use the dialog-dismiss and dialog-confirm attributes on interactive controls to close the dialog. If the user dismisses the dialog with dialog-confirm, the closingReason will update to include confirmed: true.
See PaperDialogBehavior and IronOverlayBehavior for specifics.

  1. our dialog box
  // 
```html
    <paper-dialog id="editStatementDialog" with-backdrop="">
      <div>
        <h3>Edit Statement</h3>
        <mdc-autogrow-textarea id="interpEditArea" value="{{_editStatementInput}}"></mdc-autogrow-textarea>
      </div>
      <div class="buttons">
        <mwc-button on-tap="_closeStatementDialog">Cancel</mwc-button>
        <mwc-button id="submitBtn" on-tap="_saveStatementHandler">Submit</mwc-button>
      </div>
    </paper-dialog>
```

2. setup query - a property reference to it
```javascript
  @query('#editStatementDialog')
  editStatementDialog: PaperDialogElement;
```

3. close / open functions for it that uses the reference.  These functions are called by the 'ontap of specific buttons.

```javascript
  private _closeStatementDialog(): void {
    this.editStatementDialog.close();
  }

  // open functino

    private _handleEditStatement({ detail: { text, index } }): void {
    this._editStatementInput = text;
    this._editStatementIndex = index;
    this.editStatementDialog.open();
  }
```

4. css 

```css
      #editStatementDialog {
        width: 75%;
        max-width: 800px;
      }

      #editStatementDialog mdc-autogrow-textarea {
        margin-top: 10px;
        width: 100%;
      }
```
    ------------------------------

        <paper-dialog id="udiDialog" with-backdrop="">
      <div>
        <h3>Our Mission Statementt</h3>
        <mdc-autogrow-textarea id="interpEditArea" value="{{_editStatementInput}}"></mdc-autogrow-textarea>
      </div>
      <div class="buttons">
        <mwc-button on-tap="udi_barcodeClose">Close</mwc-button>
      </div>
    </paper-dialog>

    ----------


  @query('#udiDialog')
  udiDialog: PaperDialogElement;

      private udi_barcodeOpen(): void {
    console.log("udi barcode open")
    this.udiBarcode.open()
  }

  private udi_barcodeClose(): void {
    console.log("udi barcode close")
    this.udiBarcode.close()
  }

#### 7.dependencies/material_components/grids.md

resultsTableLayout


div #resultTable

1. vaadin-grid properties
  - page-size
  - size
  on-tap
  theme

2. grid-column properties

  width 
  flex-grow
  id
  hidden

3. template / class = header

4. kinds of columns
  vaadin-checkbox
  vaadin-grid-sorter

5. column propeties
  direction
  on-sorter-changed


MINE

1. vaadin-grid

5. kinds of columns

  - gird-selection-column
  - grid-sort-column


- data is an array of objects saved to 'grid.items'

address: {street: "8170 Fallen Spring Path", city: "Five Brooks", state: "Mississippi", zip: "39548-5507", country: "USA", …}
email: "lucy.ward@company.com"
firstName: "Lucy"
lastName: "Ward"

grid.items.firstName
grid.items.address

so under column name, simply saying `path = "lastName"` would populate this with grid.items.lastName

since `grid.items.address` is more complex, then renderer is used.  This specifics sub-properties to be applied to column

grid-column properties
- flexGrow - cell width ratios

- path - item sub-property whose value gets displayed in colum body cells / also shown in column header if an explicit header / renderer not defined

- renderer - functoin for rendering cell content.  args: 

1.  root The cell content DOM element. Append your content to it.
2.  column The <vaadin-grid-column> element.
3.  rowData The object with the properties related with the rendered item, contains:

- rowData.index The index of the item.
- rowData.item The item.
- rowData.expanded Sublevel toggle state.
- rowData.level Level of the tree represented with a horizontal offset of the toggle button.
- rowData.selected Selected state.

#### 7.dependencies/material_components/iron_icons.md

class ExampleElement extends PolymerElement {
  static get template() {
    return html`
      <iron-icon icon="cs: save"></iron-icon>
    `;
  }
}

customElements.define('example-element', ExampleElement);

cs-icon.js

      <g id="save"><path d="M17 3H5c-1.11 0-2 .9-2 2v14c0 1.1.89 2 2 2h14c1.1 0 2-.9 2-2V7l-4-4zm-5 16c-1.66 0-3-1.34-3-3s1.34-3 3-3 3 1.34 3 3-1.34 3-3 3zm3-10H5V5h10v4z"></path></g>

    

icon: string | null | undefined
The name of the icon to use. The name should be of the form: iconset_name:icon_name.

src: string | null | undefined
If using iron-icon without an iconset, you can set the src to be the URL of an individual icon image file. Note that this will take precedence over a given icon attribute.

theme: string | null | undefined
The name of the theme to used, if one is specified by the iconset.

#### 7.dependencies/material_components/IronResizableBehavior.md

What is a behavior? 

a bhavior is an object that defines
- lifecycle callbacks
- declared properties
- defualt attributes
- observers
- event listeners

so it literally adds behavior to one of these. 
these are mixed into the baswe prototype
if mulitple behaviors define same function, the last one is used. 


mixins are now used instead.  

ironeresiazble beheavior

use in polymer element
it coordinates flow of resize events between eeemtns that controll size of children and elements that need to be notified when they are resized.

1
mixin the behavior

1. define hight / width properties
2. in cc, listen to 'iron-resize'.  when it fires, run a function that shows this.offsetWidth

The HTMLElement.offsetWidth read-only property returns the layout width of an element as an integer.

but, width only goes up to 100, and height is fixed.. 

IronResizableBehavior is a behavior that can be used in Polymer elements to coordinate the flow of resize events between 

1. ”resizers" (elements that control the size or hidden state of their children)
    1. Aka - vaadin-grid
2. "resizables" (elements that need to be notified when they are resized or un-hidden by their parents in order to take action on their new measurements).
    1. If you resize me, you need to let me know so that I can take action - that is, resize myself.

Elements that perform measurement should add the IronResizableBehavior behavior to their element definition and listen for the iron-resize event on themselves. This event will be fired when they become showing after having been hidden, when they are resized explicitly by another resizable, or when the window has been resized.
Note, the iron-resize event is non-bubbling.

#### 7.dependencies/material_components/vaadin_grid.md

https://cdn.vaadin.com/vaadin-elements/latest/vaadin-grid/demo/selection.html

https://www.webcomponents.org/element/vaadin/vaadin-grid/elements/vaadin-grid#method-expandItem

#### 7.dependencies/material_components/wc-works.md

# load the liberaries

import {PolymerElement, html} from '@polymer/polymer';
import '@polymer/iron-scroll-threshold/iron-scroll-threshold.js';

#class

class SampleElement extends PolymerElement {

# html

  static get template() {
    return html`
      <iron-scroll-threshold id="ironScrollTheshold" on-lower-threshold="_loadMoreData">
        <div>content</div>
      </iron-scroll-threshold>
    `;
  }

# helper function

  _loadMoreData: function() {
    console.log('lower-threshold triggered');
    // load async stuff. e.g. XHR
    setTimeout(() => {
      this.$.ironScrollTheshold.clearTriggers();
    });
  }
}
customElements.define('sample-element', SampleElement);

# what it means

1. id > identifies this wc
2. on-lower-threshold > this is a custom event called "lower-threshold" that is used with 'on-' > this will run the _loadMoreData function
3. _loadMoreData 
  - uses id to get element
  - uses 'clearTriggers()' which is a method

web comonents list examples and: 

1. properties 
2. methods
3. events

#properties

'scroll-target' as an attribute

 <x-element scroll-target="scrollable-element">
   <!-- Content-->
 </x-element>

'scroll-target' as a property 

elements reference: 

appHeader.scrollTarget = document.querySelector('#scrollable-element');



#events

used in addEventListener

an event such as iron-form-presubmit

form.addEventListener('iron-form-presubmit', function(event) {
  event.preventDefault();

** try vaadin-time-picker

  #styling 

  outer layer - refers to DOM
  inner layer - refers to custom styling

  app-header {
  --app-header-background-front-layer: {
    background-image: url(...);
  };
}

documentation

--app-box-background-front-layer	Applies to the front layer of the background	{

#### 7.dependencies/material_components/webComps.md

paper-item // one horizontal flexbox item

paper-item-body   // this will enclose multiple lines

<a>paper-item // serves asw a link (anchor wrap)

paper-listbox // you can enclose many buttons inside


import '@polymer/app-route/app-location.js';
import '@polymer/app-route/app-route.js';


This creates a side-menu and main screen area 
import '@polymer/app-layout/app-drawer-layout/app-drawer-layout.js';
import '@polymer/app-layout/app-drawer/app-drawer.js';
import '@polymer/app-layout/app-layout.js'; // contains hamburger, title
<app-header-layout>
<app-toolbar> - nav area
<app-header>
side-menu: 

import '@polymer/paper-item/paper-item.js';
import '@polymer/paper-listbox/paper-listbox.js';


main nav menu: 
import '@vaadin/vaadin-tabs/vaadin-tabs.js';
** these don't style // justify-content ?? space evenly

used for hamburger: 
import '@polymer/paper-icon-button/paper-icon-button.js';



import '@polymer/paper-input/paper-input'

import '@polymer/iron-icon/iron-icon.js';
import '@polymer/iron-icons/iron-icons.js';

import '@polymer/iron-pages/iron-pages.js';
iron-pages is used to select one of its children to show. One use is to cycle through a list of children "pages".

### 7.dependencies/mdc_vaadin/

#### 7.dependencies/mdc_vaadin/material_comp.md

.mdc-textfield--with-trailing-icon .mdc-text-field__input

.mdc-text-field__input

input  


padding-top: 20px

padding-bottom: 6px


mdc-textfields.ts
    :host([order-search]) #my-text-field {
      padding-left: 1px;
      padding-right: 1px;
      width: 120%
    }

// grid -- remove some padding between grid elements so that we can see the select button
// grid -- remove some padding in order number input so that we can see the value
site dropdown doesn't accept 'de-select all' yet it has an clear icon... 
// get the x to appear in the patient id
 
// using material-web-components
https://github.com/material-components/material-components-web-components/tree/master/packages/tab-bar

import MDCTabBarFoundation from '@material/tab-bar/foundation';

Understanding the Instructions: 

Slots: lists the elements that it accepts and handles, in this case, they are `mwc-tab`

Attributes: 

`activeIndex` is a number type that shows which tab is active - for this use, on-click, then you read the tab index, then make the corresponding change.  

CSS Custom Properties: none exist - we'd use the MDC custom properties - but how? 

Events: 
Event Name: MDCTabBar:activated	
Target: mwc-tab-bar	
Detail: {index: number}
Description: Emitted when a tab selection has been made.

This registers a listener for the MDCTabBar:activated event that will be emitted from mwc-tab-bar.  When it hears this, it will go to the tabChange function.  

  connectedCallback() {
    super.connectedCallback();
    const tab = this.shadowRoot.querySelector('mwc-tab-bar');
    tab.addEventListener(MDCTabBarFoundation.strings.TAB_ACTIVATED_EVENT, this.tabChange)
      -or-
        tab.addEventListener('MDCTabBar:activated', this.tabChange)
  }

This is similiar to placing an "on-click go to tabChange", which when happens the function is being called from the mwc-tab component rather than the cs-statement-tool component, so in the constructor, bind the listener

- a listener is a function that's called when a particular event type is called.  
- addEventListener is an EventTarget method that associates the listener with the eventtype. 

  constructor() {
    super();
    this.tabChange = this.tabChange.bind(this);
  }

  The listener: 

    tabChange(e){
    this._selectedTab = e.detail.index;
  }


.mdc-tab__text-label >> text turns yellow

mwc-tabindicator/sr/span
.mdc-tab-indicator__content
.mdc-tab-indicator__content--underline

#### 7.dependencies/mdc_vaadin/themes.md

vaadin themes


    :host([theme~="dialog"]) [part~="cell"] ::slotted(vaadin-grid-cell-content) {
      padding: 0px;
      margin-left: 5px;
      margin-right: 5px;
    }


you can have mutliple themes, so 

<vaadin theme="dialog excaliber whenever">... 

the ~= only checks for that one world

#### 7.dependencies/mdc_vaadin/vaadin_grid.md

root - the one column or cell

grid - whole grid

      const grid = this.shadowRoot.querySelector('vaadin-grid') as any;
      const { item } = grid.getEventContext(e);

getEventContext object contains: 
  rowData
  detailsOpened: false
  expanded: false
  index: 21
  item: {firstName: "Cooper", lastName: "Rivera", address: {…}, email: "cooper.rivera@company.com"}
  level: 0
  selected: false
 
item is a reference to the row, and can be used




Grid

https://cdn.vaadin.com/vaadin-grid/2.0.0-beta1/demo/row-details.html

https://vaadin.com/docs/v14/flow/binding-data/tutorial-flow-data-provider.html

https://vaadin.com/docs/v8/framework/components/components-grid.html

https://medium.com/vaadin-designers-and-developers/reinventing-the-data-grid-242e4a89ca62

https://meowni.ca/about/

#### 7.dependencies/mdc_vaadin/wrapCode.md

- learn to make these mdc-elements zx

wc-sass-render > compiles sass 

mwc - preferred - 


material comoents web has mdc stuff.. 
generic can be intergrated into framework
@material/tab

material-componets-web-components

mwc-tab .. litElements

how to write a cutoms wrapper... 


adapters and foundat

integrating mdc frameworks

mdc-textfield
importing mdctextfield 
polymer component
followed their html component
classes are dynamic based on stae
connected call back

cs-menu-surface more complex - wrapper and cusoomstimzing further - 

copyed mdcfoundation from mwc implementation

textfieldCss -- 



mwc -> wraps the mdc code

... 

mdc -> documentation exists

divs with classes = "mdc-..."
