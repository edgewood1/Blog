# Consolidated Angular Documentation

---
## From: JS-UI libs/Angular/0.Get-started/1.commands.md
---

1. install command line interface

`npm install -g @angular/cli@latest`

2. create a new app

`ng new my-app`

3. answer questions
- routing?
- stylesheet?

4. add material angular

5. set up single file components: 

src/app/app.component
====
clean up component to delete seperate html/css

@Component({
  selector: 'app-root',
  template: `<div>{{hello}}</div>`,
  styles: ['div { color: green }']
})

in angular.json  

no space after the colon, please:

```json
schematics: {
    "@schematics/angular:component": {
      "inlineStyle": true,
      "inlineTemplate": true
    }
}
```
6. Run to create other components: 

`ng g c habit-detail`

add `-d` flag for dry run of what files might be created.

without schamtics to create only comp and spec

`ng g c habit-list --inlineTemplate --inlineStyle`  

7. run app

- go to src/app folder, where components live: app.component.ts

`ng serve`

- alternative port:

`ng serve --port 4201`

---
## From: JS-UI libs/Angular/0.Get-started/2.single-file commands.md
---

Multi-file vs single-file

__Three methods of creating a single-file component__

1. component has seperate template (html) and style (css) files
=============================

change: 

```js
templateUrl > points to a file
styleUrls: ['./app.component.css`]
```
to this:

```js
template: `<h1>{{title}}</h1>
styles: ['h1 {color: blue}']
```

Delete css / html files; css/html used in the js file 
Now appfolder only has component + spec + module; 

run:

`ng generate component habit-list`

This creates css, html, spec, component.

<hr>

2. create single-file from a command: 
=============================

`ng g c habit-list --inlineTemplate --inlineStyle`  

creates only component and spec

<hr>

3. make it default behavor:
============================= 

angular.json  

no space after the colon, please:

```json
schematics: {
    "@schematics/angular:component": {
      "inlineStyle": true,
      "inlineTemplate": true
    }
}
```
Run: 

`ng g c habit-detail`

add `-d` flag for dry run of what files might be created.

---
## From: JS-UI libs/Angular/0.Get-started/3.material.md
---


https://material.angular.io/components/categories


CDK - component dev kit

 

ng add @angular/material

- angular material
- cdk
- angular animations
- 

in app.module.ts file.

import { MatSliderModule } from '@angular/material/slider';

@NgModule ({
  imports: [
    MatSliderModule,
  ]
})
class AppModule {}

You may have to 

Add the <mat-slider> tag to the app.component.html like so:

<mat-slider min="1" max="100" step="1" value="50"></mat-slider>

---
## From: JS-UI libs/Angular/0.Get-started/4. egghead-app.md
---

Your data: 

  habits = [
    {
      id: 1,
      title: 'Check in with parents once a week'
    },
    {
      id: 2,
      title: 'Record 2 videos per day'
    },
    {
      id: 3,
      title: 'Work on side project 5 hours/week'
    },
    {
      id: 4,
      title: 'Write for 20 minutes a day'
    }
  ];

  Create new project

  ng new angular-tour-of-heroes
  ng serve (requires adv node)

  src/app

change: 

```js
templateUrl > points to a files
styleUrls: ['./app.component.css`]
```
to this:

```js
template: `<h1>{{title}}</h1>
styles: ['h1 {color: blue}']
```

Now delete css / html files; Now appfolder only has component + spec + module; 

In the /app folder:

 

ng g c habit-list --inlineTemplate --inlineStyle

make it permanent:

angular.json  

no space after the colon, please:

```json
schematics: {
    "@schematics/angular:component": {
      "inlineStyle": true,
      "inlineTemplate": true
    }
}
```
Run: 

now you can run ng g c without the flags... 

in app.component: 

__PASS DATA TO CHILD__

import { HabitListComponent } from './habit-list/habit-list.component';

in template: 
    <app-habit-list></app-habit-list>

in app-habit-list add: 

<app-habit-list [title]='title'></app-habit-list>
 title = 'my-appd2';

 in app-habit-list: 

   template: `
    <p>
      {{title}}
    </p>

 notes
 ====
 [] - brackets: property binding (input)
 () - parenthesis: event-listener (output);

__PASS ARRAY OF DATA TO CHILD__

// app

- add array of objects called `habits`

<app-habit-list *ngFor="let habit of habits" [habit]='habit'></app-habit-list>


// habit-list

  template: `
    <p>
      {{habit.title}}
    </p>

__add data to service__


create a habit service

`ng g s habit`

this creates a new file:

**app/habit.service.ts**

import observables:

`import { of, Observable } from 'rxjs';`

of - converts arguments to an observable sequence

  getHabits(): Observable<any> {
    return of(this.habits)
  }

Emit variable amount of values in a sequence and then emits a complete notification.


add data

__component__

import { HabitService } from './habit.service';

inject service: 

```js
  constructor(private habitService: HabitService) {
  }
```

  now its accessible as `this.habitService`

  what is private? no access outside this class. 

  Basically, adding an access modifier (public/private/protected/readonly) to a constructor parameter will automatically assign that parameter to a field of the same name.

  now it doesn't have to be declared like `habits`

delete data

how to get data when component loads? 
We need OnInit

```js
import { Component, OnInit } from '@angular/core';
export class AppComponent implements OnInit {
``

A lifecycle hook that is called after Angular has initialized all data-bound properties of a directive. Define an ngOnInit() method to handle any additional initialization tasks.

```js
export class AppComponent implements OnInit {
  ngOnInit(): {
 ... 
  }
}
```
ngOnInit()
A callback method that is invoked immediately after the default change detector has checked the directive's data-bound properties for the first time, and before any of the view or content children have been checked. It is invoked only once when the directive is instantiated.

```js
  ngOnInit(): {
      this.habitService.getHabits()
      .subscribe((habits) => {this.habits = habits})
  }
```

this.habitService is the class
getHabits() returns an Observable
we can subscribe to it, which returns an item
we assign that to this.habits
we bind the prop to the template

==================

input via form
========

1. get teh ReactiveForms module.  This helps us manage form state:

   -  import the form module to **app.module**

   `import { ReactiveFormsModule } from '@angular/forms';`

   - add to imports array: 

   ```js
   @NgModule({
    ...
     imports: [BrowserModule, ReactiveFormsModule],

   ```

   - formBuilder is a "service" that provides methods for generating controls (inputs)
- import the class and inject the service
- generate form contents (markup)

`import { FormBuilder } from '@angular/forms';`

pass it into the constructor

```js
 constructor(private formBuilder: FormBuilder) {
    ....
    });
```

add your model to the constructor body:

    this.habitForm = this.formBuilder.group({
      title: '',
    });

add template

<form>
<input type="text" placeholder="add habit"/>
<button type="submit"> add </button>
</form>

add event listener, 
whihc passes the form instance value to OnSubmit method

  <form (ngSumbit) = OnSubmit(habitForm.value)>


  // title needed what goes in input? what field? 
  <input formControlName="title" type="text" placeholder="add habit"/>


emit an event with value info

add EventEmitter and Output from @angular/core NOT events or protractor (sometimes it auto-imports)

still in form...

```js
@Output() addHabit = new EventEmitter();
```

Emmit to parent

```js
OnSubmit(val: any) {
  this.addHabit.emit(val)
  this.habitForm.reset();
}
```
parent is listening: 

  <app-habit-form (addHabit) = "onAddHabit($event)"></app-habit-form>

  onAddHabit(x: any) {
    console.log(x)
    this.habitService.addHabit(x);

service is has tthe addHabit method, to where we've moved the logic: 

  addHabit(val:any) {
    const id = this.habits.length + 1;
    val.id = id;
    this.habits.push(val)
    
    
  }


add async pipe so we don't have to unsubscribe

this: 
<app-habit-list *ngFor="let habit of habits"></app-habit-list>
  ngOnInit() {
    this.habitService.getHabits()
      .subscribe((habits) => {this.habits = habits})
  }


becomes: 
<app-habit-list *ngFor="let habit of habits | async"></app-habit-list>
this.habits = this.habitService.getHabits()


add datatypes

ng generate interface


ng g i <filename>

ng g i habit


=== 

optional props in interface...

app.component

ngOnInit 
we map through what's returned from the service in order to add an optional 'streak' property - it's true if count is higher than 3

in app.list, we can use that to style: 


    <p [style.color] = "habit.streak ? 'red' : 'black'">
      {{habit.title}} (Count: {{ habit.count }})
    </p>

scoped vs global styles

src/styles.css
- add global styles
- make classes globally available
vs
src/app/component
- scoped


=============

create an api call... 

app.module.ts

import { HttpClientModule } from '@angular/common/http';

add to ... ? 

habit.service
import { HttpClient } from '@angular/common/http';
  constructor(private http: HttpClient) {}


  getHabits(): Observable<Habit[]> {
    return this.http.get<Habit[]>('/api/habits');
  }

leads to CORS

hitting localhost3001 from localhost4200 and server not setup to allow this... 

fix on server side? 

in production, the server will be on the same domain. so don't touch server

instead setup a proxy



new file

src/proxy.conf.json

{
  "/api": {
    "target": "http://localhost:3001",
    "secure": false
  }
}

this will make the call to / from 4200 - to our express server... 

// tell angular about
'
angular.json

scroll to architect section
serve: {
  options: {
    ....,
    'proxyConfig': 'src/proxy.conf.json
  }
}

see "proxying to a backend" 

https://angular.io/guide/build

======create a post

on server: 

app.post('/api/habits', function (req, res) {
  let habit = req.body;
  habit.id = data.habits.length + 1;
  habit.count = 0;
  data.habits.push(habit);
  res.send(habit);
});

on the service: 

   return this.http
    .post<Habit>('/api/habits', val)

    src/app/component - 

      onAddHabit(x: Habit) {
    // this.habitService.addHabit(x);
    this.habitService.addHabit(x).subscribe();
  }

================ refetching data with subjects

Subject - an event emitter that can have many listeners
it can multi-cast.  list to one thing and trigger something else to happen

listens for when habit completes and tells x to refire

---
## From: JS-UI libs/Angular/0.Get-started/mvc.md
---


model - store
view - template + browser
controller - class (components + directives)

sometimes model combined with the controller - 

store can be

- service
- redux


---
## From: JS-UI libs/Angular/1. Components/1. components.md
---


__Component__

component = class + template

__3 parts of a file__

- import statements
- @Component() decorator >> template + css
- exported typescript class 

__Multifile__

1. import

`import { Component } from '@angular/core';`

2. decorator

```js
@Component({
  selector: 'my-app' // name of component-tag
  templateUrl: './app.component.html',  // path to html
  styleUrls: [ './app.component.css' ]  // path to css 
})
```
2-B. single-file decorator

```js
@Component({
  selector: 'my-app',
  template: `
    <p>hello</p>
    <div>why</div>
  `,
  styles: [
    'p {background: blue; color: white}', 
    'div {background: red} '
  ]
})
 
``` 

__How to use this?__

import 'filename'

<my-app></my-app>

---
## From: JS-UI libs/Angular/1. Components/2.lifecycle.md
---

1. order
2. import component



__regular__

ngOnChanges()	
  
- data-bound input properties re/set. 
- The method receives a SimpleChanges object of current and previous property values.
- this happens very frequently, so any operation you perform here impacts performance significantly. See details in Using change detection hooks in this document.
- Called before ngOnInit() (if the component has bound inputs) and whenever one or more data-bound input properties change.
- if your component has no inputs or you use it without providing any inputs, the framework will not call ngOnChanges().

__on-load__

ngOnInit()	
- Initialize the directive or component after Angular first displays the data-bound properties and sets the directive or component's input properties. 
- See details in Initializing a component or directive in this document.
- Called once, after the first ngOnChanges(). 
- ngOnInit() is still called even when ngOnChanges() is not (which is the case when there are no template-bound inputs).

__regular__

ngDoCheck()	
- Detect and act upon changes that Angular can't or won't detect on its own. 
- See details and example in Defining custom change detection in this document.
- Called immediately after ngOnChanges() on every change detection run, and immediately after ngOnInit() on the first run.

__once / on-load__

ngAfterContentInit()	
- Respond __after__ Angular projects external content into the component's view, or into the view that a directive is in.
- See details and example in Responding to changes in content in this document.
- Called once after the first ngDoCheck().

__regular__

ngAfterContentChecked()	
- Respond after Angular checks the content projected into the directive or component.
- See details and example in Responding to projected content changes in this document.
- Called after ngAfterContentInit() and every subsequent ngDoCheck().

__once / on-load__

ngAfterViewInit()	
- Respond after Angular initializes the component's views and child views, or the view that contains the directive.
- See details and example in Responding to view changes in this document.
- Called once after the first ngAfterContentChecked().

__regular__
ngAfterViewChecked()	
- Respond after Angular checks the component's views and child views, or the view that contains the directive.
- Called after the ngAfterViewInit() and every subsequent ngAfterContentChecked().

__once__
ngOnDestroy()	
- Cleanup just before Angular destroys the directive or component. Unsubscribe Observables and detach event handlers to avoid memory leaks. See details in Cleaning up on instance destruction in this document.
- Called immediately before Angular destroys the directive or component.

---
## From: JS-UI libs/Angular/1. Components/3.parent-child.md
---


<parent-component>
  <child-component></child-component>
</parent-component>


__DOWNWARD COMMUNICATION__

 - use property binding 

`[item]="currentItem`

`[item]` - the value it will have in child component
`currentItem` - value in parent

__parent__

```js
<app-item-detail [item]="currentItem"></app-item-detail>
export class AppComponent {
  currentItem = 'Television';
}
```

__child__

- register `item` as in-coming property
- use it in template: `{{item}}`


  ```js
  <p> Today's item: {{item}} </p>
  export class ItemDetailComponent {
    @Input() item = ''; // decorate the property with @Input()
  }
  ```

---
## From: JS-UI libs/Angular/1. Components/4.child-parent.md
---


__UPWARD COMMUNICATIONS__

1. defined a new event emitter w/ output decorator
2. create a function that emits this emitter
3. on click, call this function

output - allows data to go from child to parent: 
 
__child__

    ```js
    export class ItemOutputComponent {
      // create an event emitter
      @Output() newItemEvent = new EventEmitter<string>();

      addNewItem(value: string) {
        // emits value from the event object ~ value must be a string
        this.newItemEvent.emit(value);
      }
    }
    ```
add a template reference variable `#newItem` to <input> element
Now in template use `newItem` as a reference to that element
get the value via `newItem.value`
on click this value passed to the emitter 
    ```html
      <label for="item-input">Add an item:</label>
      <input type="text" id="item-input" #newItem>
      <button (click)="addNewItem(newItem.value)">Add to parent's list</button>
    ```

---
## From: JS-UI libs/Angular/2. Templates/0.intro.md
---


EVENT-BINDING

  <button (click)="onSave($event)">Save</button>
  __pass in event object__

```js
<button (click)="onSave($event)">Save</button>
```

Comparison ~ lit-element: 
<button @click='() => { this.delete() }'>

============
 
__list of angular events__

 instead of `onChange` we use `change`

TEXT-INTERPOLATION

- insert a value into a string template
- use {{ value }}
- {{ can also resolve any expression, ie 1+1 }}
- interpolated expressions have a context - component, refering to `this.x` or template: either an input variable or reference variable


javascript: 
const a = `hello ${name}`

angular: 
<h3>Current customer: {{ currentCustomer }}</h3>

PROPERTY BINDING

this.itemImageUrl = '/hello';
<img alt="x" [src]="itemImageUrl">

element - img
attributes - alt, src (static / initializers)
element property - img.alt, img.src (dynamic / change)
component property - property defined in the component `this.myprop`  

[] 
- left-side: if attibute, accesses its element property
- right-side: refers to current component property

<child-component [childProp]="parentItem">
[]
- leftside: since there is no own div property called `childProp`, this refers to a child component property (`childComponent.childProp`)
- right-side: refers to current component pproperty

__property binding 2__

    This binds teh child property `item` to the string `"currentItem"`

    `<app-item-detail item="currentItem"></app-item-detail>`

    This binds the child property `item` to the parent property `currentItem`

    `<app-item-detail [item]="currentItem"></app-item-detail>`

__propety binding 3: directional__


property-binding: accessing the attributes DOM prop (binding 1) and binding it to a component property.

1 way binding: if right-side changes, then the left-side changes
- if `parentItem` changes in parent comp, then `childComp.childProp` changes in child comp
- effect: one-way binding from the component to the template. 


2 way binding: if left-side changes, then the right side changes too. 
- if `childComponent.childProp` changes, then `parentItem` in parent will change
- [()] or ngModel- two-way


 ====misc


__prop binding 2: style bindings__

<button kendoButton ... [style.backgroundColor]="'rebeccaPurple'"></button>

<button kendoButton ... [style.backgroundColor]="isActive ? 'rebeccaPurple' : 'white'"></button>

__prop binding 3: class bindings__

<button kendoButton ... [class.active]="isActive"></button>


---
## From: JS-UI libs/Angular/2. Templates/1.interpolation.md
---

 
Template - this refers to the html 

__template statement__ 

 - methods or properties used in HTML 
 - deleteHero() is a template statement
 - <button (click) = "deleteHero()">
 - can use ; but not bit-wise operators, pipes, or increment operators

__template expression__ 

- javascript expression what goes between {{ template-expression }}

```js
  <p>{{hi()}}</p>
  <p>{{1+1}}</p>
  hi = () => 1+1
```

__statement contentx__

- sc refers to the component instance - this is the scope of a statement's reach
- sc aloso refers to properties of template's own context

<button type="button" *ngFor="let hero of heroes" (click)="deleteHero(hero)">{{hero.name}}</button>

Template context names take precedence over component context names. In the preceding deleteHero(hero), the hero is the template input variable, not the component's hero property.

__template context__

expressions have a context that include

1. component properties `recommended` and the expression `itemImageUrl2` refer to properties of the AppComponent instance

    <h4>{{recommended}}</h4>
    <img [src]="itemImageUrl2">

2. props of the template's context, such as template input variables or template referene varaibles

__template input variable__

The following example uses a **template input variable** of `customer`.

    <ul>
      <li *ngFor="let customer of customers">{{customer.name}}</li>
    </ul>


__template reference variable__

This next example features a **template reference variable**, `#customerInput`.
 
<label>Type something:
  <input #customerInput>{{customerInput.value}}
</label>

 Template reference variables—use special variables to reference a DOM element within a template.

Template expression operators—learn about the pipe operator, |, and protect against null or undefined values in your HTML.

Within the template, `customerInput` is now a reference to this input element.

   <input #customerInput>{{customerInput.value}}

It has observation properties - below, if username.value ever becomes 'god' then it will display this question:

<input type="text" #username>
<p *ngIf="username.value === 'god'">Who you trying to fool?</p>

Also, see viewChild.

__ViewChild can also be sued as a template reference__

@ViewChild('username') // turns template reference variable into a component property
console.log(this.username);

__alternative if TRV didn't exist__

That way, the DOM can basically watch other parts of itself without you having to use any javascript logic yourself (it still gets used.. you just aren't the one writing it). Otherwise, you'd have to write that like this:

<input type="text" id="username" [ngModel]="username" (ngModelChange)="checkForGod()">
<p *ngIf="usernameIsGod">Who you trying to fool?</p>

Then in your controller:

checkForGod() { usernameIsGod = username === 'god' }
 

https://www.pluralsight.com/guides/how-to-use-template-reference-variables-in-angular

======

you should always have a name and id on your inputs, even if you have template variables.

id - good for styling, however, better to use ngClass / ngStyle

---
## From: JS-UI libs/Angular/2. Templates/1.template.md
---

 
Template - this refers to the html 

__template statement__ 

 - methods or properties used in HTML 
 - deleteHero() is a template statement
 - <button (click) = "deleteHero()">
 - can use ; but not bit-wise operators, pipes, or increment operators

__template expression__ 

- javascript expression what goes between {{ template-expression }}

```js
  <p>{{hi()}}</p>
  <p>{{1+1}}</p>
  hi = () => 1+1
```

__statement contentx__

- sc refers to the component instance - this is the scope of a statement's reach
- sc aloso refers to properties of template's own context

<button type="button" *ngFor="let hero of heroes" (click)="deleteHero(hero)">{{hero.name}}</button>

Template context names take precedence over component context names. In the preceding deleteHero(hero), the hero is the template input variable, not the component's hero property.

__template context__

expressions have a context that include

1. component properties `recommended` and the expression `itemImageUrl2` refer to properties of the AppComponent instance

    <h4>{{recommended}}</h4>
    <img [src]="itemImageUrl2">

2. props of the template's context, such as template input variables or template referene varaibles

__template input variable__

The following example uses a **template input variable** of `customer`.

    <ul>
      <li *ngFor="let customer of customers">{{customer.name}}</li>
    </ul>


__template reference variable__

This next example features a **template reference variable**, `#customerInput`.
 
<label>Type something:
  <input #customerInput>{{customerInput.value}}
</label>

 Template reference variables—use special variables to reference a DOM element within a template.

Template expression operators—learn about the pipe operator, |, and protect against null or undefined values in your HTML.

Within the template, `customerInput` is now a reference to this input element.

   <input #customerInput>{{customerInput.value}}

It has observation properties - below, if username.value ever becomes 'god' then it will display this question:

<input type="text" #username>
<p *ngIf="username.value === 'god'">Who you trying to fool?</p>

Also, see viewChild.

__ViewChild can also be sued as a template reference__

@ViewChild('username') // turns template reference variable into a component property
console.log(this.username);

__alternative if TRV didn't exist__

That way, the DOM can basically watch other parts of itself without you having to use any javascript logic yourself (it still gets used.. you just aren't the one writing it). Otherwise, you'd have to write that like this:

<input type="text" id="username" [ngModel]="username" (ngModelChange)="checkForGod()">
<p *ngIf="usernameIsGod">Who you trying to fool?</p>

Then in your controller:

checkForGod() { usernameIsGod = username === 'god' }
 

https://www.pluralsight.com/guides/how-to-use-template-reference-variables-in-angular

======

you should always have a name and id on your inputs, even if you have template variables.

id - good for styling, however, better to use ngClass / ngStyle

---
## From: JS-UI libs/Angular/2. Templates/1b.prop-attribute.md
---

__attributes vs DOM/element properties__

Angular data binding works with DOM properties not HTML attributes.

- Attributes initilalize DOM props.  
- They won't change with value changes. 
- change a value? target the DOM prop 

For example:

`<input type="text" value="Sarah">`

- change the value
- check `input.getAttribute('value')`
- the attribute `value` remains the same, but the DOM prop has changed 

__attribute vs property binding__

2 ways of setting boolean DOM props

- set the DOM prop to true or false

`<input [disabled]="condition ? true : false">`

- reinitialize the attribute (accessible via the `attr` prefix: "attribute binding syntax"

`<input [attr.disabled]="condition ? 'disabled' : null">`

* above, remember, `attr` refers to initialization, not ongoing change.

__attributes 2__

There's not always a straight mapping between attribute and DOM prop:
- id has 1:1 mapping
- aria-* has no prop equivalent
- textContent DOM prop has no attr equivalent


 
1. attribute binding

<tr><td [attr.colspan]="1 + 1">One-Two</td></tr>

Single class binding	
[class.sale]="onSale"	
onSale = true

Multi-class binding	[class]="classExpression"	
classExpression = "my-class-1 my-class-2 my-class-3"

3. style

<nav [style.background-color]="expression"></nav>

pipes - transform values

The chained hero's birthday is
{{ birthday | date | uppercase}}

custom-peipes - next





---
## From: JS-UI libs/Angular/2. Templates/2-c.piping.md
---


Pipes 

- transform strings for display
- they are functions
- used in template expressions `{{}}`
- they accept an input value and return a transformed value
- only need to declare a pipe once
- there are built-in and custom pipes
- they look like this: `|`
- they are used along with hte pipe name.
- below is an example of a date pipe:

<p>date: {{ birthdate | date }}</p>
...
  birthdate = '04-29-1970'

This will show: "date: Apr 29, 1970"

You can pass in parameter values via a colon: 

{{ amount | currency }}
...
amount = '55' // $55

{{ amount | currency : 'EUR' }} // will change dollar sign to a euro sign

slice - multiple parameters
slice() takes 2 parameters: 1, 3

<p> date: {{ date | slice:1:3}}</p>

date = [1, 2, 3]

Pipe chaining

{{ birthday | date | uppercase}}

Creating pipes for custom data transformations

Detecting changes with data binding pipes?

  template: `
    <p>{{getName()}}</p>
    <div>why</div>
    <button (click)="delete()">Click me</button>
    <p> date: {{ date.a.b | percent: '3.2-5'}}</p>
  `,
  styles: ['p {background: blue; color: white}', 'div {background: red} '],
})
export class AppComponent {
  myname: string = 'Angular ' + VERSION.major;
  date = { a: {b: 1}};
  getName() {
    return this.myname;
  }

  delete() {
    console.log('delete');
    this.date.a.b += 1;
  }

---
## From: JS-UI libs/Angular/2. Templates/4. pass-data.md
---


Looping through an array

__parent__

`<app-habit-list></app-habit-list>`

- define array as a class field 

```js
  habits = [
    {
      id: 1,
      title: 'Check in with parents once a week'
    },
```

- use loop directive: *ngFor = let `template-ref` of `componentProp`
- [chidPropName] = "template ref"
  your repeating habit-item, which just prints a question repeatedly.
  your using this in habit-list
  in habit list your feeding it habits

```js
      <app-habit-item 
        *ngFor="let habit of habits"
        [habit]='habit'
        >
      </app-habit-item>
```
__child__

```js
import { Component, OnInit, Input } from '@angular/core';

@Component({...
<li>{{habit.title}}</li>
})

export class... {
  @Input() habit  = {
    title: '',
    id: 0
  };
}


__add new components need to be added to app.module in__

- declarations array
- imports


---
## From: JS-UI libs/Angular/2.Classes/prv-pub-fields.md
---

above, the class contains a "public field declaration"
such fields are an alternative to constructor definitions.  Both are instance props.  Fields can be private: `#currentCustomer`

---
## From: JS-UI libs/Angular/3. Directives/1. structural/1. structural.md
---

Structural directives shape or reshape the DOM's structure, by adding, removing, and manipulating elements. 

---
## From: JS-UI libs/Angular/3. Directives/1. structural/4.ngIf-for-switch.md
---

ngIf

x=true
<p *ngIf="x">hello</p>

When x is false, this will disappear

ngIfElse

Guarding against null

if `currentCustomer` doesn't exist, then the dependent text content is ruined.  Therefore, don't bother displaying:

<div *ngIf="currentCustomer">Hello, {{currentCustomer.name}}</div>

Use the NgFor directive to present a list of items.

When working with an array called 'items' whose items are objects such that each object is: 

{name: 'abc'}

ngFor can be used to list items - this will just list names

<div *ngFor="let item of items">{{item.name}}</div>

repeating a component view

This loops through the `items` array
each item in this array is passed into the component

<app-item-detail *ngFor="let item of items" [item]="item"></app-item-detail>


This has to be set up in app-item-detail as: 

`@Input() item: {name: string}`
<h1 *ngIf="item">Hello {{item.name}}</h1>

Getting the index

<div *ngFor="let item of items; let i=index">{{i + 1}} - {{item.name}}</div>

This will print: 
1 - mel
2 - jon


stopped here: 

Repeating elements when a condition is true

---
## From: JS-UI libs/Angular/3. Directives/1. structural/ngFor.md
---

<div *ngFor="let product of products">

  <h3>
    <a [title]="product.name + ' details'">
      {{ product.name }}
    </a>
  </h3>

  <p *ngIf="product.description">
    Description: {{ product.description }}
  </p>

</div>


*ngFor, the <div> repeats for each product in the list.
*ngIf - <p> shows if condition exists

extras
======

[ ] - property binding syntax; this assigns the value to a property within the class.  this property must be registered.  You can also use this in a template expression.



---
## From: JS-UI libs/Angular/4. Services (DI)/1. dependencies.md
---

dependency
- a relative term
- typically, it means a thing that is dependent on another thing to work
- in code, its nearly the opposite. 
- a node module is a dependency because it is used by our main program
- in reality, they are interdependent
- our main program doesn't depend on it - it could use another module
- however, the module requires some program in order to work. 
- the module is "turned on " by another program - our main program

---
## From: JS-UI libs/Angular/4. Services (DI)/2.services.md
---

 

Service 
- any value, function, feature needed by an application
- a class with a narrow purpose

__component vs. service__

component 
- view related
- presents props and methods for data binding in order to mediate between teh template (view) and app logic (model)


service 
- function related; written to be used by any component
- handles certain tasks related to view logic, egg: 
  - fetch data from server
  - validate user input
  - log directly to the console.

This service depends on two other services
it returns an updated array `this.heros`
 
create a habit service

`ng g s habit`

this creates a new file:

**app/habit.service.ts**

To this, you can import methods (operators, observerables) 

---
## From: JS-UI libs/Angular/4. Services (DI)/3.di.md
---


dependency injection

- used to provide components with services needed
- components "consume" services
- we inject a service into our component
- our services are dependencies
-  thus, it has access to this service class.
 
Register providers in the @Injectable(), or in the @NgModule() or @Component() decorators

1. At root level, a single, shared instance of HeroService injected to any class that asks for it 

- `ng generate service` - register a provider with the root injector for your service by including provider metadata in the `@Injectable()` decorator.  

  @Injectable({
  providedIn: 'root',
  })

2. same instance availabe to all componets in NgModule (both BackendService and Logger get the same instance)

@NgModule({
  providers: [
  BackendService,
  Logger
 ],
 ...
})

3. New instance for each new instance that requests

- register a service provider in the providers property of the @Component() metadata.

@Component({
  selector:    'app-hero-list',
  templateUrl: './hero-list.component.html',
  providers:  [ HeroService ]
})

---
## From: JS-UI libs/Angular/4. Services (DI)/5.service-injector.md
---

// service


```js
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: /* injector goes here */
})
export class TemplateService {
  constructor() { }
}

```


An injectable is a decorator tha tis added to the consumer of the dependency.  

Injector looks like this; it takes an object

`@Injectable()`


the object contains metadata w/ the following keys that tell the injector where to find its resources:

- `providedIn` ~ specifies which injector to register with
- `providers` (for directives, components, modules)

providedIn

- default is root (as in the root injector of the app)
- this makes the service available anywhere.

PROVIDER:
- in the services folder
- tags class with `@Injectable()` decorator

```js
import { Injectable } from '@angular/core';

@Injectable()
export class LoggerService {
  callStack: string[] = [];

  addLog(message: string): void {
    this.callStack.push(message) 
    console.log(this.callStack);
  }
}
```

CONSUMER uses the `providers` key in the `Component` decorator:
- if there is no Component decorator, we could use the Injectable decorator


```js
import { LoggerService } from '../services/logger';

@Component({
  selector: 'my-app',
  template: `
    <div #one id='one'>one</div>  
    <button (click) = "onClick(one)">heelo</button>
    `,
  providers: [LoggerService],
})
export class AppComponent {
  constructor(private logger: LoggerService) {}
  onClick(a) {
    this.logger.addLog('hola');
  }
}


---
## From: JS-UI libs/Angular/4. Services (DI)/6.constructors.md
---

https://www.techiediaries.com/angular-10-constructor-parameters-inject-optional/

---
## From: JS-UI libs/Angular/4. Services (DI)/7.directives.md
---

References to the DOM can instantiate from any class. Keep in mind that references are still services. They differ from traditional services in representing the state of something else. These services include functions to interact with their reference.

Directives are in constant need of DOM references. Directives perform mutations on their host elements through these references


ng generate directive highlight


// directives/highlight.directive.ts
```js
import { Directive, ElementRef, Renderer2, Input } from '@angular/core';

@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective {
  constructor(
    private renderer: Renderer2,
    private host: ElementRef
  ) { }

  @Input() set appHighlight (color: string) {
    this.renderer.setStyle(this.host.nativeElement, 'background-color', color);
  }
}
```

1. The @Directive() decorator's configuration property specifies the directive's CSS attribute selector, [appHighlight].

2. Import ElementRef from @angular/core. ElementRef grants direct access to the host DOM element through its nativeElement property.

3. Add ElementRef in the directive's constructor() to inject a reference to the host DOM element, the element to which you apply appHighlight.

4. Add logic to the HighlightDirective class that sets the background to yellow.

---
## From: JS-UI libs/Angular/4. Services (DI)/misc.md
---

injecotr
- decorator

provider
- an object that tells injector how to get dependency

---
## From: JS-UI libs/Angular/5.Decorators/1.viewChild.md
---

https://nishugoel.medium.com/using-viewchild-in-angular-de1854a51872

https://nishugoel.medium.com/using-viewchild-in-angular-de1854a51872

best:

https://blog.angular-university.io/angular-viewchild/

verybest: 

https://stackoverflow.com/questions/48343082/mat-menu-and-button-in-different-components

adding type: 

https://stackoverflow.com/questions/51471850/what-type-should-viewchild-variables-have

 @ViewChild() decorator configures a view query.
 - used to get the first element or the directive matching the selector from the view DOM. 
 - provides the instance of another component or directive in a parent component and then parent component can access the methods and properties of that component or directive.

params: 
- child component name
- directive name
- template variable

we can
- get a child component from the parent componet

For example, if a library ships with a component or directive with a public non-input or non-output property you’d like to change, these decorators would allow you to access and modify them. 

These decorators are also helpful in exposing providers configured in child components to inject dependencies ( like services, configuration values, etc. ) that the main component may not have access to.


ElementRef - like document.getElementById('myId');
- used in only some decorators
- used in basic DOM abstraction
- access basic native element present in DOM

TemplateRef
- access DOM elmeent within template
- structural directive uses this
- can contain many element refs

---
## From: JS-UI libs/Angular/5.Decorators/2.input.md
---

To pass an item (habit) into a component: 

@Input()
habit;

Now constructor knows that habit will be passed in.

How do we pass it in? 
1. we loop through the array, assigning each item a prop: 

`let habit of habits`

2. we pass the item in: square brackets

`[habit] = 'habit'`

<!-- parent -->

habits = [{}, {}]

<app-habit-item #ngFor='let habit of habits' [habit]='habit'></app-habit-item>

<!-- child -->

@Input();
habit;

Decorators are habit

=====

we can bind values between component

parent
<app-item-detail [childItem]="parentItem"></app-item-detail>

child
@Input() childItem = '';

Inputs and Outputs—share data between the parent context and child directives or components

---
## From: JS-UI libs/Angular/5.Decorators/3.output.md
---


__parent__


// target output

```js
template: <app-habit-form (addHabit) ="onAddHabit($event)">

onAddHabit(e) {
  console.log(e);
}
```
// create an output

__child: addHabitForm__

import { EventEmitter } from '@angular/core'

@Output() addHabit = new EventEmitter<any>();

onSubmit(newHabit) {
  this.addHabit.emit(newHabit)
}


---
## From: JS-UI libs/Angular/5.Decorators/observable.ts
---

observable

import ngIniit
import { Observable } from 'rxjs'
import { HabitService } from DataTransfer... 

export class HabitList implement OnInit {

habits = []

// inject data
constructor(private habitService: HabitService) {}

// after constructor, subscribe to the getData method
// so when that changes getHabits is called
ngOnInit(): void {
  this.habitService.getHabits().subscribe(habits => {
    this.habits = habits;
  })
}

// we can call and get all habits
getHabits(): observable<any> {
  return of(this.habits);
}

/// use an async pipe ... 

---
## From: JS-UI libs/Angular/8.forms/5. reactive-forms.md
---

Forms

What is a form? 

a container for different kinds of user inputs
the form gathers these inputs and sends them to a server, defined by the `action` attribute. 

1. get teh ReactiveForms module.  This helps us manage form state:

   -  import the form module to **app.module**

   `import { ReactiveFormsModule } from '@angular/forms';`

   - add to imports array: 

   ```js
   @NgModule({
    ...
     imports: [BrowserModule, ReactiveFormsModule],

   ```

2. build model on a component

- models are describes the data used in teh view.  It handles user interactions such as clicking, scrolling, etc.  IE - it holds data and provides methods to work with the data.   

- In the class, you'll need a field property that will represent the model in the form
- here, we declare the field - it is undefined. 

`habitForm`

3. import the formBuild from the same angular/forms directory

- what are "form controls"? controls are the ways a user can interact with a UI (or form).  Control types include: buttons, checkboxes, radio buttons, menus, text input, file select, hidden controls, object controls.

- formBuilder is a "service" that provides methods for generating controls (inputs)
- import the class and inject the service
- generate form contents (markup)

`import { FormBuilder } from '@angular/forms';`

4. use the form builder

Forms have several realted controls.  ReactiveForms provides 2 ways of grouping such controls into a single input form: 

- group - tracks teh form state of a group of controls.  If one changes, we know.  Each control is tracked by name.
- form array - allows for adding / removing controls at run time.

create a formGroup instance in the constructor

pass the formBuilder into the constructor: 
- this person uses an "access modifier" on the parameter.  
- This will automatically assign that paramter to a field of the same name.  
- Private means access is limited.
- below, why not just: https://angular.io/guide/reactive-forms
 
```js
 constructor(private formBuilder: FormBuilder) {
    ....
    });
```

associate it with the model / view (ie, define the group).  
- below, `habitForm` is our model.
- `group` is the method on the `FormBuilder`
- parameter: object
- object: formControlName: default value (type inferred) 

```js
  constructor(private formBuilder: FormBuilder) {
    this.habitForm = this.formBuilder.group({
      title: '',
    });
```
5. create the form in the template: 

<form>
<input type="text" placeholder="add habit"/>
<button type="submit"> add </button>
</form>

Some form terms: 

formBuilder - this is a service
.group - method on service that does x
habitForm - our instance of group containing model

formGroup - we bind instance to this, which associates form with formGroup
Tracks the value and validity state of a group of FormControl instances.

formControlName - give form a name .. why?
Syncs a FormControl in an existing FormGroup to a form control element by name.



6. bind form to form group.  the value is from constructor. 

<form [formGroup] = 'habitForm'>

7. bind textfield to titlefield

<input formControlName="title">

Syncs a FormControl in an existing FormGroup to a form control element by name.



8. bind submit event using ngSubmit
parentheiss mean its an event or output

`<form (ngSubmit) = "OnSubmit(habitForm.value)"></form>`

`habitForm.value` is an object that contains all the values of our form as defined in the model (object) passed into `formBuild.group()`

9. define function

```js
  onSubmit(newHabit: Test) {
    const id = this.habits.length + 1;
    newHabit.id = id;
    this.habits.push(newHabit)
  }
```

10: add a Type for `newHabits`: 

```js
type Test = {
  id: number,
  title: string,
}
```

11. apply it to `habits`

`habits: Test[] = [ ... ]`

---
## From: JS-UI libs/Angular/RxJs/1. intro/0.pull-push.md
---




pull systems - 

production - defines a function; left in the dark
consumption - calls the function

push system

producer - 
consumer - in the dark about when data will be passed; an observer


promises vs observables

promises - return only one value

observable - return multiple values in a stream (over time)

---
## From: JS-UI libs/Angular/RxJs/1. intro/1.arrays-streams.md
---


__difference between array / stream__

array 
- const a = [1, 2, 3]
- all data already known + accessible

stream
- const a = ?
- data hasn't arrived yet.
- we don't know when it will end 
- on-going events
- an async array
- example: 

a ---b-c---------d------e

=====
we can add an event listener to sequence
when even happens, we react to it by doing something


---
## From: JS-UI libs/Angular/RxJs/1. intro/2.next.md
---

Two terms
1. observable - object consumed or observed
2. observer - subject /producer

__import the constructor__

`import { Observable } from 'rxjs';`

__create an observer__
__Observer__
- an object
- returned by observable
- defines our 3 notification types (the following methods)

const observer = {
  next: (x) => console.log(x),
  error: (x) => console.log('error', x),
  complete: () => console.log('complete')
}

 
__define the subscriber function__
  
- @params: our observer
- this function calls our notification types

    ```js
    let a = 0
    const sub = (observer => {
      setInterval(() => {
        a+=1;
        if (a<10) {
          observer.next(a)
        } else {
          observer.complete();
        }
        
      }, 1000)
    });
    ```

__create the observable__

- below, we use the Observagle constructor
- params: the subscriber function
- returns: observable instance
- we will observe our subscriber function
- which is returned as an observable instance
 
`const $obs = new Observable(sub)`

__begin the observation__

- do this by calling the subscribe method on the observable

`$obs.subscribe(observer);`

OR 

```js
async function test() {
  const y =  await $obs.subscribe(observer);
  console.log(y)
}
test();
```

__overview__

1. create an observer
2. set up observer within the subscriber
3. subscriber is the value-emitter (producer)
4. pass the subscriber into the observable (1)
5. this creates an observable instance
6. the observable is the consumer
7. call subscribe on the observable while passing in the observer (or logging method?) (2)

8. Declare Observable


__compare this to a promise__

const prom = ((res, rej) => {
  setTimeout(() => {
      res(a)
  }, 4000)
})

const $p = new Promise(prom)

__Another way of creating an observable is using the create method on the constructor__

https://medium.com/geekculture/6-ways-to-create-observables-with-rxjs-be93367e3f69

__operators__

- these transform the output of the observable (aka, the provider)
- observable publishes values to the observer's next method

they provide data for consumers, such as subscribers.
 
- we can unsubscribe from this sub.

`subscription.unsubscribe()`


 



---
## From: JS-UI libs/Angular/RxJs/1. intro/3.others.md
---



```js
const a = [1, 2, 3, 4]

// create observable
// pass in the observer, which defines notification methods
const $hello = new Observable((obs => {
  obs.next(a);  
  obs.complete();
}))
// subscribe to observable
$hello.subscribe(val => console.log(val))
```

PROCESS

1. create an observer
2. set up observer within the subscriber
3. subscriber is the value-emitter (producer)
4. pass the subscriber into the observable (1)
5. this creates an observable instance
6. the observable is the consumer
7. call subscribe on the observable while passing in the observer (or logging method?) (2)

8. Declare Observable


```js
// the observerable / the
// subscriber is passed into the observable
// it is the method that prodcues the log data
// this return an observable instance
const avenger$ = new Observable(() => {
  console.log('EndGame is near')
});
```
2. subscribe to overservable, which returns a subscription object
```js
// call subscribe on this instance
// log the result
// returned in a subscription obj for unsubscribing

let subscribeAvenger = avenger$.subscribe((result) => {
  console.log(result)
});
```
3. Unsubscribe from subscription object to prevent memory leak

`subscribeAvenger.unsubscribe();`

---
## From: JS-UI libs/Angular/RxJs/1. intro/9.creators.md
---

 __Creation__ 
 these operators turn an object into an observable

 ie, a stream 

 ========================

 - create: aliast to the constructor ~ this is deprecated.  use new Observable() instead. 



 - interval: returns an Observable that emits an infinite sequence of ascending integers, with a constant interval of time of your choosing between those emissions. 

 - fromEvent: Creates an Observable that emits events of a specific type coming from the given event target.

 - of(...items) ~ returns an observable instance that synchronoosly delivers the values provided as argumnts
 - emits value without processing
 - from: allows processing

of(a)
.subscribe(val => console.log(val))


- from(iterable) - converts its arguments to an observable instance - often used to convert an array to an obserable.  l


onboarding this 

3rd week


---
## From: JS-UI libs/Angular/RxJs/2.operators/1.general.md
---

 

Kinds of operators

 __Creation__ operators allow the creation of an observable from nearly anything. From generic to specific use-cases you are free, and encouraged, to turn everything into a stream.

 - interval: returns an Observable that emits an infinite sequence of ascending integers, with a constant interval of time of your choosing between those emissions. 

 - fromEvent: Creates an Observable that emits events of a specific type coming from the given event target.

 - of(...items) ~ returns an observable instance that synchronoosly delivers the values provided as argumnts
- from(iterable) - converts its arguments to an observable instance - often used to convert an array to an obserable.  


https://angular.io/guide/observables

 __Utility__ - provide a specific utility

 tap - Used to perform side-effects for notifications from the source observable
Used when you want to affect outside state with a notification without altering the notification
tap(nextOrObserver: function, error: function, complete: function): Observable

__Transformation__ as a value changes, we can tranform it

map - used like map js

switchMap  - allows me to connect two observables such that 1 is cancelled / restarted

obs1.switchMap(event => {
  return obs2  // cancels old subscriptions
}).subscribe(v=>console.log(v))

//emit (1,2,3,4,5)
const source = from([1, 2, 3, 4, 5]);
//add 10 to each value
const example = source.pipe(map(val => val + 10));
//output: 11,12,13,14,15





========
We'll see how to provide dependencies as constructor parameters to components or services and use the @Optional and @Inject decorators for adding optional dependencies or create injection tokens to pass parameters to services.

In Angular 10 and previous versions, the constructor has a special use besides its typical use. Since Angular uses dependency injection for wiring various artifacts such as components and services, the injector makes use of the constructor to inject the dependencies into the class which can a component, or a service, etc. Angular resolves providers you declare in your constructor. This is an example:

https://www.techiediaries.com/angular-10-constructor-parameters-inject-optional/



__operators: static v instance__

static / instant methods of observable class

static / geneators

Rx.Observable.<operator> 
- 10-15 of these
- create a new observable without any input

instance operators

- Rx. Observable.prototype.<operator>
- we already have an observable and we want to to things with this
- this scope is the input Observable


---
## From: JS-UI libs/Angular/RxJs/2.operators/2-c.pipe-async2.md
---

__with observables__

__4 parts: initialize, onload run obserbale

```js
// 1. initialize
  observableData: number;
  observer: Observable<number> = null;
  subscription: Subscription;
 

// 2. onload subscribe to transformer
constructor() {
  this.subscribeObservable();
}

subscribeObservable() {
  this.observer = this.getObservable();
  this.subscription = this.observer.subscribe((v) => (this.observedData = v));
}

// waits 1 second
// take the first 10
// multiply each
// subscribe - executes observable
//  ie notify `v` of any changes
// v is assigned to `this.observableData`
// observerables return a subscription
// we need to destroy this subsciption when we're done
// subscribe returns a subscription.unsubscribe() which you call to stop notiications.

  getObservable() {
    return interval(1000)
      .pipe(
        take(10),
        map((v) => v * v)
      )
  }

  ```

---
## From: JS-UI libs/Angular/RxJs/3.subjects/a.md
---


__subject__
- a type of observable 
- observables are unicast by design; subjects are multicast.
 -implements both observable and observer

 var source = new Subject();
source.map(x => ...).filter(x => ...).subscribe(x => ...)
source.next('first')
source.next('second')


behaviorSubject
- type of subject that:
- needs an initial value as it must always returna value on subscription ven if it hasn't recieved a next()
- on subscription, it returns the last value of the subject


- an object
- it maintains a list of dependents called observers?
- notifies them of state changes
exercise

---
## From: JS-UI libs/Angular/RxJs/3.subjects/behaviorSubject.md
---

BehaviorSubject is a type of subject, a subject is a special type of observable so you can subscribe to messages like any other observable. The unique features of BehaviorSubject are:

It needs an initial value as it must always return a value on subscription even if it hasn't received a next()
Upon subscription, it returns the last value of the subject. A regular observable only triggers when it receives an onnext
at any point, you can retrieve the last value of the subject in a non-observable code using the getValue() method.
Unique features of a subject compared to an observable are:

It is an observer in addition to being an observable so you can also send values to a subject in addition to subscribing to it.
In addition, you can get an observable from behavior subject using the asObservable() method on BehaviorSubject.

Observable is a Generic, and BehaviorSubject is technically a sub-type of Observable because BehaviorSubject is an observable with specific qualities.

Example with BehaviorSubject:

// Behavior Subject

// a is an initial value. if there is a subscription 
// after this, it would get "a" value immediately
let bSubject = new BehaviorSubject("a"); 

bSubject.next("b");

bSubject.subscribe(value => {
  console.log("Subscription got", value); // Subscription got b, 
                                          // ^ This would not happen 
                                          // for a generic observable 
                                          // or generic subject by default
});

bSubject.next("c"); // Subscription got c
bSubject.next("d"); // Subscription got d
Example 2 with regular subject:

// Regular Subject

let subject = new Subject(); 

subject.next("b");

subject.subscribe(value => {
  console.log("Subscription got", value); // Subscription wont get 
                                          // anything at this point
});

subject.next("c"); // Subscription got c
subject.next("d"); // Subscription got d
An observable can be created from both Subject and BehaviorSubject using subject.asObservable().

The only difference being you can't send values to an observable using next() method.

In Angular services, I would use BehaviorSubject for a data service as an angular service often initializes before component and behavior subject ensures that the component consuming the service receives the last updated data even if there are no new updates since the component's subscription to this data.

https://stackoverflow.com/questions/39494058/behaviorsubject-vs-observable

BehaviorSubject (or Subject ) stores observer details, runs the code only once and gives the result to all observers .

https://stackoverflow.com/questions/43118769/subject-vs-behaviorsubject-vs-replaysubject-in-angular

---
## From: JS-UI libs/Angular/RxJs/3.subjects/intro.md
---


```js
const x = new observable(sub => sub.next('a'))
```

__Space: Unicast vs. Multicast__

unicast 
- the subscriber function runs anew for each subscriber
- "a" emitted once for each subscriber
- each observer recieves the same produced values


multicast 
- the subscriber runs once for all subscribers
- each observer recieves the same produced value


__Time: hot vs cold__

hot 
- later subscribers will only get later emissions
- a subscriber gets emissions from the moment he subscribes
- he won't get past emissions
- a single stream
- another view: code gets executed even if there's no subscriber.

cold
- stream recreated for each new subscriber
- cosde gets executed when at least one observer present

usually:

| -    | unicast | multi |
| ---- | ------- | ----- |
| hot  | -       | x     |
| cold | x       | -     |
 
 
__Observables vs Subjects: Unicast + Multicast__


__Observables are unicast by design: each gets own instance:__

- each subscription receives the different values as observables developed as unicast by design.
- sub func runs once for **each** subscriber > each gets different results

  ```js
    import {Observable} from 'rxjs';

    let obs = Observable.create(observer=>{
      observer.next(Math.random());
    })

    // instance 1

    obs.subscribe(res=>{
      console.log('subscription a :', res); //subscription a :0.2859800202682865
    });

    // instance 2

    obs.subscribe(res=>{
      console.log('subscription b :', res); //subscription b :0.694302021731573
    });
```

__Subjects are multicast by design.: each gets same instance:__

- Subjects are similiar to an event-emitter
- it does not invoke for each subscription 
- subscriber func runs once for **all** subscribers
- each gets same output

  ```js
  import {Subject} from 'rxjs';

  let obs = new Subject();

  // both the subscription are got the same output value!.

  obs.subscribe(res=>{
    console.log('subscription a :', res); // subscription a : 0.91767565496093
  });

  obs.subscribe(res=>{
    console.log('subscription b :', res);// subscription b : 0.91767565496093
  });

  obs.next(Math.random());

  ```

  __Hot v Cold__

In multicast example, if `obs.next()` ran between subscriptions, then first would get it, but not the second

In unicast, `obs.next()` can only run before subscriptions, and all get it


__part 2__

| Observable                                                  | Subject                                        | Column C |
| ----------------------------------------------------------- | ---------------------------------------------- | -------- |
| Cold: Code executed if at least one observer.               | hot: code executes even if no observer         |
| http gets called for each observer / code runs for each obs | miss all values broadcast before obs created   |
| ie stream gets resent for each new subscriber               | ie later submissions get later emissions.      | C1       |
| -                                                           | -                                              | C2       |
| Uni-directional: Observer cant assign value to observable.  | bi-directional: observer can                   | C3       |
| Unicast: subscriber runs anew for all subscribers           | multi: subscriber runs once for all subscriber |
 
 

subject?
multicast, can cast values to multiple subscribers and can act as both subscribers and emmitter

https://stackoverflow.com/questions/47537934/what-is-the-difference-between-observable-and-a-subject-in-rxjs

---
## From: JS-UI libs/Angular/RxJs/2-c.pipe-async1.md
---

__async pipe w/ promises__


to render results of promise / observable: 

- wait for callback
- sotre the result in a vairable
- bind variable in the template

```js
  // 2. bind the result vairable in the template
  <p> {{ promiseData }} </p>

export class AppComponent {
  promiseData:string;

  // 1. wait for callback / store results in promiseData
  constructor() {
    this.getPromise()
    .then((v) => this.promiseData = v as string);
  }

  getPromise() {
    return new Promise((res, rej) => {
      setTimeout(() => res('done'), 3000)
    })
}
```
w/async pipe, we can use things directly in template without the above.

- change binding property to Promise
- 

it accepts as argument an observable or promise
calls subscribe or attaches a then h andler
waits for async results before passing result to caller

demo: 

```js
    
// 2. which we insert directly into our template
// will this not 
<p> {{ promise | async }} </p>

export class AppComponent {
  promise:Promise<string>;

  // 1. we returned store promise directly into property
  constructor() {
    this.promise = this.getPromise() as Promise<string>;
  }
```


---
## From: JS-UI libs/Angular/RxJs/2-observ-promises.md
---

Promises and Observables both handle the asynchronous call only.

Here are the differences between them:

__Observable__

- Emits multiple values over a period of time
- Is not called until we subscribe to the Observable
Can be canceled by using the unsubscribe() method
Provides the map, forEach, filter, reduce, retry, and retryWhen operators

__Promise__

- handles / Emits only a single value at a time
- uses only .then / .catch operators

---
## From: JS-UI libs/Angular/RxJs/4.master.md
---



```js

// prop template
  <p> {{ observedData }} </p>

export class AppComponent {
  // define fields
  observedData: number;
  observer$: Observable<number> = null;
  subscription: Subscription;

  constructor() {
    this.subscribeObservable();
  }

  // creates observable
  getObservable() {
    return interval(1000) // observerble
      .pipe(  // operators
        take(10),
        map((v) => v * v)
      )
  }

  // creates observer object + subscribe
  subscribeObservable() {
    this.observer$ = this.getObservable();
    this.subscription = this.observer$.subscribe((v) => (this.observedData = v)); // save observerd values to var
  }

  // destroy
  ngOnDestroy() {
    console.log('des')
    if (this.subscription) {
    this.subscription.unsubscribe();
    }
  }


// how to change this w/a pipe

---
## From: JS-UI libs/Angular/RxJs/7.mulit-casting.md
---


an observable creates a new instance (observer?)
multiple observers can subscribe to this instance.  

multicasting - broadcasting to a list of many in a single executation.  
- don't register multiplelisteners but re-use the first listener and send values to each subscriber.



two listeners
- each get sent the full broadcast


one listneer 
- if add .5 sec later, 


===

@Component({
  selector: 'my-app',
  template: ``,
  styles: [],
})
export class AppComponent {
  observer = {
    next(num) {
      console.log(num);
    },
    complete() {
      console.log('Finished sequence');
    },
  };

  static arr = [1, 2, 3];

  // This function runs when subscribe() is called
  sequenceSubscriber(observer: Observer<number>) {
    // synchronously deliver 1, 2, and 3, then complete

    AppComponent.arr.forEach((e) => {
      observer.next(e)
      
    });
    observer.complete();

    // unsubscribe function doesn't need to do anything in this
    // because values are delivered synchronously
    return { unsubscribe() {} };
  }
  sequence = new Observable(this.sequenceSubscriber);
  // sequence2 = new Observable(this.sequenceSubscriber);
  constructor() {
    this.sequence.subscribe(this.observer);
    setTimeout(() => {
      this.sequence.subscribe(this.observer);
    }, 250);
  }
}

---
## From: JS-UI libs/Angular/RxJs/README.md
---


https://adrianmejia.com/data-structures-for-beginners-trees-binary-search-tree-tutorial/

https://nemo-ufes.github.io/gufo/

https://www.w3.org/TR/2012/REC-owl2-primer-20121211/#Classes_and_Instances

https://math.stackexchange.com/questions/2522116/is-category-theory-more-abstract-than-set-theory-or-proof-theory

https://www.positronx.io/getting-started-with-reactive-programming-with-rxjs-in-javascript/

https://medium.com/angular-in-depth/the-best-way-to-unsubscribe-rxjs-observable-in-the-angular-applications-d8f9aa42f6a0

https://www.tallan.com/blog/2021/01/08/survival-guide-for-the-new-angular-developer/

https://ng-girls.gitbook.io/todo-list-tutorial/workshop-todo-list/installations/stackblitz

https://chriszempel.com/posts/twowaydb/

https://www.youtube.com/watch?v=uWwvkzWZ6IM&ab_channel=CodeCraftMastery

https://codecraft.tv/courses/angular/pipes/async-pipe/

https://dmitripavlutin.com/javascript-classes-complete-guide/#3-fields


---
## From: JS-UI libs/Angular/RxJs/unsubscribe.md
---

http://www.zephyrfloat.com/floatation

For this question there are two kinds of Observables - finite value and infinite value.

http Observables produce finite (1) values and something like a DOM event listener Observable produces infinite values.

If you manually call subscribe (not using async pipe), then unsubscribe from infinite Observables.

Don't worry about finite ones, RxJs will take care of them.

Sources:

I tracked down an answer from Rob Wormald in Angular's Gitter here.

He states (I reorganized for clarity and emphasis is mine):

if its a single-value-sequence (like an http request) the manual cleanup is unnecessary (assuming you subscribe in the controller manually)

i should say "if its a sequence that completes" (of which single value sequences, a la http, are one)

if its an infinite sequence, you should unsubscribe which the async pipe does for you

Also he mentions in this YouTube video on Observables that "they clean up after themselves..." in the context of Observables that complete (like Promises, which always complete because they are always producing one value and ending - we never worried about unsubscribing from Promises to make sure they clean up XHR event listeners, right?)

Also in the Rangle guide to Angular 2 it reads

In most cases we will not need to explicitly call the unsubscribe method unless we want to cancel early or our Observable has a longer lifespan than our subscription. The default behavior of Observable operators is to dispose of the subscription as soon as .complete() or .error() messages are published. Keep in mind that RxJS was designed to be used in a "fire and forget" fashion most of the time.

When does the phrase "our Observable has a longer lifespan than our subscription" apply?

It applies when a subscription is created inside a component which is destroyed before (or not 'long' before) the Observable completes.

I read this as meaning if we subscribe to an http request or an Observable that emits 10 values and our component is destroyed before that http request returns or the 10 values have been emitted, we are still OK!

When the request does return or the 10th value is finally emitted the Observable will complete and all resources will be cleaned up.

If we look at this example from the same Rangle guide we can see that the subscription to route.params does require an unsubscribe() because we don't know when those params will stop changing (emitting new values).

The component could be destroyed by navigating away in which case the route params will likely still be changing (they could technically change until the app ends) and the resources allocated in subscription would still be allocated because there hasn't been a completion.

In this video from NgEurope Rob Wormald also says you do not need to unsubscribe from Router Observables. He also mentions the http service and ActivatedRoute.params in this video from November 2016.

The Angular tutorial, the Routing chapter now states the following:

The Router manages the observables it provides and localizes the subscriptions. The subscriptions are cleaned up when the component is destroyed, protecting against memory leaks, so we don't need to unsubscribe from the route params Observable.

Here's a discussion on the GitHub Issues for the Angular docs regarding Router Observables where Ward Bell mentions that clarification for all of this is in the works.

I spoke with Ward Bell about this question at NGConf (I even showed him this answer which he said was correct) but he told me the docs team for Angular had a solution to this question that is unpublished (though they are working on getting it approved). He also told me I could update my SO answer with the forthcoming official recommendation.

The solution we should all use going forward is to add a private ngUnsubscribe = new Subject(); field to all components that have .subscribe() calls to Observables within their class code.

We then call this.ngUnsubscribe.next(); this.ngUnsubscribe.complete(); in our ngOnDestroy() methods.

The secret sauce (as noted already by @metamaker) is to call takeUntil(this.ngUnsubscribe) before each of our .subscribe() calls which will guarantee all subscriptions will be cleaned up when the component is destroyed.

Example:

import { Component, OnDestroy, OnInit } from '@angular/core';
// RxJs 6.x+ import paths
import { filter, startWith, takeUntil } from 'rxjs/operators';
import { Subject } from 'rxjs';
import { BookService } from '../books.service';

@Component({
    selector: 'app-books',
    templateUrl: './books.component.html'
})
export class BooksComponent implements OnDestroy, OnInit {
    private ngUnsubscribe = new Subject();

    constructor(private booksService: BookService) { }

    ngOnInit() {
        this.booksService.getBooks()
            .pipe(
               startWith([]),
               filter(books => books.length > 0),
               takeUntil(this.ngUnsubscribe)
            )
            .subscribe(books => console.log(books));

        this.booksService.getArchivedBooks()
            .pipe(takeUntil(this.ngUnsubscribe))
            .subscribe(archivedBooks => console.log(archivedBooks));
    }

    ngOnDestroy() {
        this.ngUnsubscribe.next();
        this.ngUnsubscribe.complete();
    }
}
Note: It's important to add the takeUntil operator as the last one to prevent leaks with intermediate Observables in the operator chain.

More recently, in an episode of Adventures in Angular Ben Lesh and Ward Bell discuss the issues around how/when to unsubscribe in a component. The discussion starts at about 1:05:30.

Ward mentions "right now there's an awful takeUntil dance that takes a lot of machinery" and Shai Reznik mentions "Angular handles some of the subscriptions like http and routing".

In response Ben mentions that there are discussions right now to allow Observables to hook into the Angular component lifecycle events and Ward suggests an Observable of lifecycle events that a component could subscribe to as a way of knowing when to complete Observables maintained as component internal state.

That said, we mostly need solutions now so here are some other resources.

A recommendation for the takeUntil() pattern from RxJs core team member Nicholas Jamieson and a TSLint rule to help enforce it: https://ncjamieson.com/avoiding-takeuntil-leaks/

Lightweight npm package that exposes an Observable operator that takes a component instance (this) as a parameter and automatically unsubscribes during ngOnDestroy: https://github.com/NetanelBasal/ngx-take-until-destroy

Another variation of the above with slightly better ergonomics if you are not doing AOT builds (but we should all be doing AOT now): https://github.com/smnbbrv/ngx-rx-collector

Custom directive *ngSubscribe that works like async pipe but creates an embedded view in your template so you can refer to the 'unwrapped' value throughout your template: https://netbasal.com/diy-subscription-handling-directive-in-angular-c8f6e762697f

I mention in a comment to Nicholas' blog that over-use of takeUntil() could be a sign that your component is trying to do too much and that separating your existing components into Feature and Presentational components should be considered. You can then | async the Observable from the Feature component into an Input of the Presentational component, which means no subscriptions are necessary anywhere. Read more about this approach here.

Share
Improve this answer
Follow
edited Nov 25 at 16:49

jonrsharpe
103k2020 gold badges192192 silver badges352352 bronze badges
answered Dec 16 '16 at 4:11

seangwright
15k66 gold badges3939 silver badges4949 bronze badges
When a route is navigated away from, then the child router for that route is destroyed. I guess this is why it's not necessary to unsubscribe from router events. – 
Günter Zöchbauer
 Jan 17 '17 at 20:21
What about local subjects, which are created by a component (e.g. for in-component logic/wiring up): Should complete() be called on these subjects in ngOnDestroy? That would cleanup the subscriptions and each subscription would have the possibility to clean up, what ever it used, in its complete-handler, right? – 
Lars
 Jan 29 '17 at 11:25
@Lars I believe local subjects get cleaned up automatically since they are created within the scope of the parent component but the Angular team is going to be recommending the approach I have detailed above in "Edit 3". – 
seangwright
 Apr 9 '17 at 23:41
19
Calling complete() by itself doesn't appear to clean up the subscriptions. However calling next() and then complete() does, I believe takeUntil() only stops when a value is produced, not when the sequence is ended. – 
Firefly
 Apr 11 '17 at 8:53
4
@seangwright A quick test with a member of type Subject inside a component and toggling it with ngIf to trigger ngOnInit and ngOnDestroy shows, that the subject and its subscriptions will never complete or get disposed (hooked up a finally-operator to the subscription). I must call Subject.complete() in ngOnDestroy, so the subscriptions can clean up after themselves. – 
Lars
 Apr 11 '17 at 9:17
1
@Firefly You are correct - added this to my answer above. @Lars Thanks for for doing the test. I thought local Subjects might be in the set of observables that Angular will clean up for you, if that's not the case then the above solution should be used. – 
seangwright
 Apr 12 '17 at 10:07
5
Your --- Edit 3 is very insightful, thanks! I just have a followup question: if using the takeUnitl approach, we never have to manually unsubscribe from any observables? Is that the case? Furthermore, why do we need to call next() in the ngOnDestroy, why not just call complete()? – 
uglycode
 Apr 22 '17 at 10:21
2
@uglycode With this approach you never have to unsubscribe unless you want further custom control of your subscriptions. Look at @Firefly's comment above. Calling complete() does not trigger takeUntil(). But it does clean up the ngUnsubscribe Subject. So next() cleans up all the others and complete() cleans up itself. – 
seangwright
 Apr 22 '17 at 17:24
@seangwright The documentation for takeUntil says that it listens for the observable to either emit a value or a complete notification, so it seems like just calling complete on the subject is enough. – 
spongessuck
 Apr 26 '17 at 15:14
@spongessuck The docs do seem to be contradictory, but looking at the RxJS 5 docs Returns the values from the source observable sequence until the other observable sequence or Promise produces a value. Looking at the source when the takeUntil Observer calls next the source completes. @firefly mentions above that calling complete() alone doesn't seem to do the trick. – 
seangwright
 Apr 26 '17 at 19:54
7
@seangwright That's disappointing; the additional boilerplate is annoying. – 
spongessuck
 Apr 27 '17 at 20:30
@spongessuck There is a decorator you can use to handle some of the boilerplate github.com/NetanelBasal/angular2-take-until-destroy. I prefer the more explicit approach, but it's a preference. – 
seangwright
 Apr 28 '17 at 22:52
first nice post,... my question is if you have a source for your newest edit (EDIT 3), if so could you append it to your answer, thx in advance – 
Nickolaus
 May 22 '17 at 13:27
@Nickolaus Thanks! I've tried to collect as much information here as possible. My source was a conversation with Ward Bell at NGConf this year. The official sources have not yet been published in the Angular.io docs (as shown by this thread). Unfortunately, this is the best I can do at the moment. You could tweet at ward and ask him about the status on the docs. – 
seangwright
 May 22 '17 at 16:41 
what if I'm subscribing to valueChanges of a FormControl that is a part of a given component? Do I still need to unsubscribe? – 
Dmitry Efimenko
 May 26 '17 at 19:28
1
@Dmitry It depends. If that subscription is the valueChanges Observable combined with other observables that outlive the lifetime of the component, then yes, you should use the above pattern. But if you are only subscribing to the valueChanges Observable then it will be destroyed/cleaned up when the component (and the form) are destroyed. – 
seangwright
 May 26 '17 at 22:43
4
Edit 3 discussed in context of events at medium.com/@benlesh/rxjs-dont-unsubscribe-6753ed4fda87 – 
HankCa
 May 29 '17 at 2:07
If following the above pattern what would I spy on to unit test 'ngOnDestroy'? Does this same pattern apply if I'm using ReplaySubject to create an observable from an array that changes? The array is in a service that's meant to live throughout the app's existence. The subscriber for the most part will also have the same lifetime, but in some instances could be destroyed and later reinitialized. – 
Jens Bodal
 Jun 8 '17 at 15:29 
1
@seangwright, thanks for staying on top of this answer! I have a question that I am still not entirely clear on. If I create a new Subject, should we also be unsubscribing from these too? I haven't been able to find any answers or blog posts that has cleared this up for me. – 
bmd
 Jun 13 '17 at 13:49
1
@bmd Take a look at @Lars's comment where it is mentioned that local Subjects do not complete when a component is destroyed unless .complete() is called on them. This is an example of where having an ngUnsubscribe: Subject<void> would help manage all other subscriptions (whether from Observables provided by DOM events, injectable services or other local Subjects). – 
seangwright
 Jun 13 '17 at 21:31
Ok, this is very interesting. So did I understand that correctly: I should NOT call this.subscription.unsubscribe() on EVERY subscription, but just need to implement the .takeUntil() method to every Observable and call a .complete() in the ngOnDestroy() method only once? Can you please confirm? – 
dave0688
 Dec 19 '17 at 16:15 
@dave0688 that is correct. You can keep track of and call .unsubscribe() on every subscription (via for ... of), but using .takeUntil(sub) or .pipe(takeUntil(sub)) is the more rxjs-ish approach – 
seangwright
 Dec 19 '17 at 21:26
@seangwright - I am now trying this solution (edit 3). If I console.log(this.ngUnsubscribe) before the 'this.ngUnsubscribe.next()' I see that the observers property of it is an array with 0 items. does it make sense? – 
Batsheva
 Jan 8 '18 at 13:02 
@seangwright I'm a bit confused as to when to use the lettable operator version of takeUntil. In my component, I have subscriptions to observables returned from a service which makes httpclient requests. In those requests, I use the pipe (tap, catchError, etc). Is that when that version should be used? – 
Alex
 Jan 22 '18 at 0:01
@seangwright. Well After a bit more research, I learned that HTTP requests are finite observables and therefore don't have to be unsubscribed. However, I'd still like to see from fleshed out examples of the two forms of takeUntil. – 
Alex
 Jan 22 '18 at 0:17
2
@Alex That is correct, HTTP requests, as explained in my answer above, are finite. But that doesn't mean that an observable that starts out as finite will always result in a finite stream. The RxJs operators allow you to manipulate the stream or data so an initial http request could become an infinite stream of numbers or simulated mouse clicks. This is why the above pattern is recommended. No matter what new operators you add to your http observable you are guaranteed it will be cleaned up. – 
seangwright
 Jan 22 '18 at 2:43
@Alex Lettable operators are a bundle/syntax change, not a functional change. You would use them when using a new enough version of RxJs (^5.5.0) to help ensure you import only what is needed per ES module (ie per file). blog.angularindepth.com/… – 
seangwright
 Jan 22 '18 at 2:45
1
Why isn't this "official solution" part of the framework yet? – 
thorn0
 Feb 14 '18 at 15:58
2
@thorn Good question. It might be that the Angular team wants us to default to letting subscriptions manage themselves using features of the framework (async pipe). RxJs allows you do go a long way towards not having to call unsubscribe() when used with async pipe by combining and manipulating Observables within your component. You can also often async pipe a value into a dumb component's @Input() and work with the raw value from that point forward. I find the ngUnsubscribe() solution helpful when Observables get very complex but I don't know if it should be the default solution. – 
seangwright
 Feb 14 '18 at 17:39
I don't understand why do we still need to do this.ngUnsubscribe.complete();. No one from outside is referencing this subject . And all the subscriptions which touched that subject,were completed. So why ? – 
Royi Namir
 Mar 29 '18 at 20:13
1
@RoyiNamir The whole idea of this approach is to have a way to clean up all Subscriptions that are being managed manually (not by AsyncPipe) in the component. We connect all subscriptions to this one resource (ngUnsubscribe) and when it is cleaned up the rest will be too. But we still have to clean up ngUnsubscribe. If we don't complete() ngUnsubscribe then it will continue to live on after the component is disposed. – 
seangwright
 Mar 29 '18 at 22:20
Isnt myobj is released when comp is destroyed? – 
Royi Namir
 Mar 30 '18 at 3:53
@seangwright you're wrong. No need to complete stackoverflow.com/questions/49569089/… – 
Royi Namir
 Mar 30 '18 at 6:04
@RoyiNamir You are correct. It appears you don't need to ngUnsubscribe.complete(). I still think it's a good habit. – 
seangwright
 Mar 30 '18 at 20:41 
Why not use a class variable? private alive = true ... .takeWhile(() => this.alive) And in the ngOnDestroy() set to false: this.alive = false. I don't see why we need to use another Subject... – 
danger89
 Apr 29 '18 at 1:12 
2
Any news on the Angular docs team publishing their 'undocumented' solution (a year later)? – 
ElliotSchmelliot
 May 25 '18 at 17:10 
1
It's worth to mention that the takeUntil operator should be the last to avoid leaks with intermediate observables in the operator chain. – 
NoNameProvided
 Jun 15 '18 at 6:56
2
Is this solution still valid for angular 6 with new version of Rxjs? – 
Anthony
 Jun 15 '18 at 14:07
@NoNameProvided Correct - more details about that in this medium post blog.angularindepth.com/… – 
seangwright
 Jun 15 '18 at 17:16
@Anthony Other than lettable operators now being called pipeable operators, I believe everything detailed should still apply. You will want to use the import { takeUntil } from 'rxjs/operators' instead of the mutating import import 'rxjs/add/operator/takeUntil'; – 
seangwright
 Jun 15 '18 at 17:18
1
@seangwright Why do I getting this Generic type Subject<T> requires 1 type argument(s) by following this approach, did I missed something? Thanks – 
Roxy'Pro
 Jun 29 '18 at 7:19
1
@Roxy'Pro you just need to add an argument to template Subject (even if you are not going to use it), so that you have, e.g., Subject<boolean>. That is: private ngUnsubscribe: Subject<boolean> = new Subject(); – 
Jago
 Jul 2 '18 at 10:04
1
I found this guide online which explains it well: github.com/ueler/angular-rxjs-unsubscribe – 
Ynv
 Feb 10 '20 at 21:07
Does not the destroying of the Component also clean up the Subject automatically? Would it not be sufficient to only use .next()? I've worked on a few large stacks where we use this trick, but we don't complete(). Since the Subject is declared as a local variable in the component, and Angular destroys local variables in any component that is destroyed, why is complete() necessary? – 
Lars Holdaas
 Feb 27 '20 at 8:00
1
Is it still in 2020 relevant? Or in Angular 10 something has changed? – 
tillias
 Oct 6 '20 at 9:01
@tillias This is still relevant if you are subscribing to Observables in code and you want a consistent way to ensure they are cleaned up when the component/directive are destroyed. However, the recommended approach to Observables is to use the | async pipe in the template. Using a state management library like Akita or NgRx will result in most Observables being bound to the template and not subscribed to in code. – 
seangwright
 Oct 14 '20 at 1:00
Ben mentions that there are discussions right now to allow Observables to hook into the Angular component lifecycle events (...). Does anyone know where/if we'll see the fruit of these discussions? Cheers! – 
Joel Balmer
 May 6 at 10:39
Add a comment

122

You don't need to have bunch of subscriptions and unsubscribe manually. Use Subject and takeUntil combo to handle subscriptions like a boss:

import { Subject } from "rxjs"
import { takeUntil } from "rxjs/operators"

@Component({
  moduleId: __moduleName,
  selector: "my-view",
  templateUrl: "../views/view-route.view.html"
})
export class ViewRouteComponent implements OnInit, OnDestroy {
  componentDestroyed$: Subject<boolean> = new Subject()

  constructor(private titleService: TitleService) {}

  ngOnInit() {
    this.titleService.emitter1$
      .pipe(takeUntil(this.componentDestroyed$))
      .subscribe((data: any) => { /* ... do something 1 */ })

    this.titleService.emitter2$
      .pipe(takeUntil(this.componentDestroyed$))
      .subscribe((data: any) => { /* ... do something 2 */ })

    //...

    this.titleService.emitterN$
      .pipe(takeUntil(this.componentDestroyed$))
      .subscribe((data: any) => { /* ... do something N */ })
  }

  ngOnDestroy() {
    this.componentDestroyed$.next(true)
    this.componentDestroyed$.complete()
  }
}
Alternative approach, which was proposed by @acumartini in comments, uses takeWhile instead of takeUntil. You may prefer it, but mind that this way your Observable execution will not be cancelled on ngDestroy of your component (e.g. when you make time consuming calculations or wait for data from server). Method, which is based on takeUntil, doesn't have this drawback and leads to immediate cancellation of request. Thanks to @AlexChe for detailed explanation in comments.

So here is the code:

@Component({
  moduleId: __moduleName,
  selector: "my-view",
  templateUrl: "../views/view-route.view.html"
})
export class ViewRouteComponent implements OnInit, OnDestroy {
  alive: boolean = true

  constructor(private titleService: TitleService) {}

  ngOnInit() {
    this.titleService.emitter1$
      .pipe(takeWhile(() => this.alive))
      .subscribe((data: any) => { /* ... do something 1 */ })

    this.titleService.emitter2$
      .pipe(takeWhile(() => this.alive))
      .subscribe((data: any) => { /* ... do something 2 */ })

    // ...

    this.titleService.emitterN$
      .pipe(takeWhile(() => this.alive))
      .subscribe((data: any) => { /* ... do something N */ })
  }

  ngOnDestroy() {
    this.alive = false
  }
}
Share
Improve this answer
Follow
edited Sep 28 '20 at 23:03
answered Mar 9 '17 at 12:35

metamaker
1,99722 gold badges1616 silver badges1717 bronze badges
2
If he just use a bool to keep the state, how to make "takeUntil" works as expected? – 
Val
 Apr 24 '17 at 3:38
7
I think there is a significant difference between using takeUntil and takeWhile. The former unsubscribes from the source observable immediately when fired, while the latter unsubscribes only as soon as next value is produced by the source observable. If producing a value by the source observable is a resource consuming operation, choosing between the two may go beyond style preference. See the plunk – 
Alex Che
 Aug 22 '17 at 16:40
2
@AlexChe thanks for providing interesting plunk! This is very valid point for general usage of takeUntil vs takeWhile, however, not for our specific case. When we need to unsubscribe listeners on component destruction, we are just checking boolean value like () => alive in takeWhile, so any time/memory consuming operations are not used and difference is pretty much about styling (ofc, for this specific case). – 
metamaker
 Aug 31 '17 at 10:28 
2
@metamaker Say, in our component we subscribe to an Observable, which internally mines some crypto-currency and fires a next event for an every mined coin, and mining one such coin takes a day. With takeUntil we will unsubscribe from the source mining Observable immediately once ngOnDestroy is called during our component destruction. Thus the mining Observable function is able to cancel it's operation immediately during this process. – 
Alex Che
 Aug 31 '17 at 14:19 
2
OTOH, if we use takeWhile, in the ngOnDestory we just set the boolean variable. But the mining Observable function might still work for up to one day, and only then during it's next call will it realize that there are no subscriptions active and it needs to cancel. – 
Alex Che
 Aug 31 '17 at 14:23 
Show 8 more comments

101

The Subscription class has an interesting feature:

Represents a disposable resource, such as the execution of an Observable. A Subscription has one important method, unsubscribe, that takes no argument and just disposes the resource held by the subscription.
Additionally, subscriptions may be grouped together through the add() method, which will attach a child Subscription to the current Subscription. When a Subscription is unsubscribed, all its children (and its grandchildren) will be unsubscribed as well.

You can create an aggregate Subscription object that groups all your subscriptions. You do this by creating an empty Subscription and adding subscriptions to it using its add() method. When your component is destroyed, you only need to unsubscribe the aggregate subscription.

@Component({ ... })
export class SmartComponent implements OnInit, OnDestroy {
  private subscriptions = new Subscription();

  constructor(private heroService: HeroService) {
  }

  ngOnInit() {
    this.subscriptions.add(this.heroService.getHeroes().subscribe(heroes => this.heroes = heroes));
    this.subscriptions.add(/* another subscription */);
    this.subscriptions.add(/* and another subscription */);
    this.subscriptions.add(/* and so on */);
  }

  ngOnDestroy() {
    this.subscriptions.unsubscribe();
  }
}
Share
Improve this answer
Follow
edited Aug 17 '18 at 20:21
answered May 3 '17 at 12:00

Steven Liekens
11.4k66 gold badges5252 silver badges7878 bronze badges
1
I'm using this approach. Wondering if this is better than using the approach with takeUntil(), like in the accepted answer.. drawbacks ? – 
Manuel Di Iorio
 Sep 19 '17 at 20:28
1
No drawbacks that I'm aware of. I don't think this is better, just different. – 
Steven Liekens
 Sep 19 '17 at 20:56
3
See medium.com/@benlesh/rxjs-dont-unsubscribe-6753ed4fda87 for further discussion on the official takeUntil approach versus this approach of collecting subscriptions and calling unsubscribe. (This approach seems a lot cleaner to me.) – 
Josh Kelley
 Mar 29 '18 at 20:31
5
One small benefit of this answer: you don't have to check if this.subscriptions is null – 
user2023861
 Aug 24 '18 at 19:58
3
Just avoid the chaining of add methods like sub = subsciption.add(..).add(..) because in many cases it produces unexpected results github.com/ReactiveX/rxjs/issues/2769#issuecomment-345636477 – 
Evgeniy Generalov
 Sep 29 '18 at 13:51 
Show 1 more comment

42

Some of the best practices regarding observables unsubscriptions inside Angular components:

A quote from Routing & Navigation

When subscribing to an observable in a component, you almost always arrange to unsubscribe when the component is destroyed.

There are a few exceptional observables where this is not necessary. The ActivatedRoute observables are among the exceptions.

The ActivatedRoute and its observables are insulated from the Router itself. The Router destroys a routed component when it is no longer needed and the injected ActivatedRoute dies with it.

Feel free to unsubscribe anyway. It is harmless and never a bad practice.

And in responding to the following links:

(1) Should I unsubscribe from Angular 2 Http Observables?
(2) Is it necessary to unsubscribe from observables created by Http methods?
(3) RxJS: Don’t Unsubscribe
(4) The easiest way to unsubscribe from Observables in Angular
(5) Documentation for RxJS Unsubscribing
(6) Unsubscribing in a service is kind of pointless since there is no chance of memory leaks
(7) Do we need to unsubscribe from observable that completes/errors-out?
(8) A comment about the http observable
I collected some of the best practices regarding observables unsubscriptions inside Angular components to share with you:

http observable unsubscription is conditional and we should consider the effects of the 'subscribe callback' being run after the component is destroyed on a case by case basis. We know that angular unsubscribes and cleans the http observable itself (1), (2). While this is true from the perspective of resources it only tells half the story. Let's say we're talking about directly calling http from within a component, and the http response took longer than needed so the user closed the component. The subscribe() handler will still be called even if the component is closed and destroyed. This can have unwanted side effects and in the worse scenarios leave the application state broken. It can also cause exceptions if the code in the callback tries to call something that has just been disposed of. However at the same time occasionally they are desired. Like, let's say you're creating an email client and you're triggering a sound when the email is done sending - well you'd still want that to occur even if the component is closed (8).
No need to unsubscribe from observables that complete or error. However, there is no harm in doing so(7).
Use AsyncPipe as much as possible because it automatically unsubscribes from the observable on component destruction.
Unsubscribe from the ActivatedRoute observables like route.params if they are subscribed inside a nested (Added inside tpl with the component selector) or dynamic component as they may be subscribed many times as long as the parent/host component exists. No need to unsubscribe from them in other scenarios as mentioned in the quote above from Routing & Navigation docs.
Unsubscribe from global observables shared between components that are exposed through an Angular service for example as they may be subscribed multiple times as long as the component is initialized.
No need to unsubscribe from internal observables of an application scoped service since this service never get's destroyed, unless your entire application get's destroyed, there is no real reason to unsubscribe from it and there is no chance of memory leaks. (6).

Note: Regarding scoped services, i.e component providers, they are destroyed when the component is destroyed. In this case, if we subscribe to any observable inside this provider, we should consider unsubscribing from it using the OnDestroy lifecycle hook which will be called when the service is destroyed, according to the docs.
Use an abstract technique to avoid any code mess that may be resulted from unsubscriptions. You can manage your subscriptions with takeUntil (3) or you can use this npm package mentioned at (4) The easiest way to unsubscribe from Observables in Angular.
Always unsubscribe from FormGroup observables like form.valueChanges and form.statusChanges
Always unsubscribe from observables of Renderer2 service like renderer2.listen
Unsubscribe from every observable else as a memory-leak guard step until Angular Docs explicitly tells us which observables are unnecessary to be unsubscribed (Check issue: (5) Documentation for RxJS Unsubscribing (Open)).
Bonus: Always use the Angular ways to bind events like HostListener as angular cares well about removing the event listeners if needed and prevents any potential memory leak due to event bindings.
A nice final tip: If you don't know if an observable is being automatically unsubscribed/completed or not, add a complete callback to subscribe(...) and check if it gets called when the component is destroyed.

Share
Improve this answer
Follow
edited Oct 2 '18 at 12:00
answered Aug 7 '18 at 18:03

Mouneer
11.2k22 gold badges3434 silver badges4545 bronze badges
Answer for No. 6 is not quite right. Services are destroyed and their ngOnDestroy is called when the service is provided at a level other than the root level e.g. provided explicitly in a component that later gets removed. In these cases you should unsubscribe from the services inner observables – 
Drenai
 Sep 9 '18 at 7:50 
@Drenai, thanks for your comment and politely I don't agree. If a component is destroyed, the component, service and the observable will be all GCed and the unsubscription will be useless in this case unless you keep a reference for the observable anywhere away from the component (Which is not logical to leak the component states globally despite scoping the service to the component) – 
Mouneer
 Sep 11 '18 at 16:02 
If the service being destroyed has a subscription to an observable belonging to another service higher up in the DI hierarchy, then GC won't occur. Avoid this scenario by unsubscribing in ngOnDestroy, which is always called when services are destroyed github.com/angular/angular/commit/… – 
Drenai
 Sep 11 '18 at 22:54
Well said @Drenai but I am talking originally about higher level services that live as long as the app is running and never destroyed. But certainly your point is valid regarding to scoped services. So thanks again and I will edit the answer to include a note about scoped services and to eliminate any ambiguity. – 
Mouneer
 Sep 29 '18 at 12:47
3
@Tim First of all, Feel free to unsubscribe anyway. It is harmless and never a bad practice. and regarding your question, it depends. If the child component is initiated multiple times (For example, added inside ngIf or being loaded dynamically), you must unsubscribe to avoid adding multiple subscriptions to the same observer. Otherwise no need. But I prefer unsubscribing inside the child component as this makes it more reusable and isolated from how it could be used. – 
Mouneer
 Oct 8 '18 at 17:03
Show 3 more comments

19

It depends. If by calling someObservable.subscribe(), you start holding up some resource that must be manually freed-up when the lifecycle of your component is over, then you should call theSubscription.unsubscribe() to prevent memory leak.

Let's take a closer look at your examples:

getHero() returns the result of http.get(). If you look into the angular 2 source code, http.get() creates two event listeners:

_xhr.addEventListener('load', onLoad);
_xhr.addEventListener('error', onError);
and by calling unsubscribe(), you can cancel the request as well as the listeners:

_xhr.removeEventListener('load', onLoad);
_xhr.removeEventListener('error', onError);
_xhr.abort();
Note that _xhr is platform specific but I think it's safe to assume that it is an XMLHttpRequest() in your case.

Normally, this is enough evidence to warrant a manual unsubscribe() call. But according this WHATWG spec, the XMLHttpRequest() is subject to garbage collection once it is "done", even if there are event listeners attached to it. So I guess that's why angular 2 official guide omits unsubscribe() and lets GC clean up the listeners.

As for your second example, it depends on the implementation of params. As of today, the angular official guide no longer shows unsubscribing from params. I looked into src again and found that params is a just a BehaviorSubject. Since no event listeners or timers were used, and no global variables were created, it should be safe to omit unsubscribe().

The bottom line to your question is that always call unsubscribe() as a guard against memory leak, unless you are certain that the execution of the observable doesn't create global variables, add event listeners, set timers, or do anything else that results in memory leaks.

When in doubt, look into the implementation of that observable. If the observable has written some clean up logic into its unsubscribe(), which is usually the function that is returned by the constructor, then you have good reason to seriously consider calling unsubscribe().

Share
Improve this answer
Follow
edited Dec 1 '16 at 7:14
answered Dec 1 '16 at 7:09

Chuanqi Sun
9731111 silver badges2424 bronze badges
Add a comment

9

Angular 2 official documentation provides an explanation for when to unsubscribe and when it can be safely ignored. Have a look at this link:

https://angular.io/docs/ts/latest/cookbook/component-communication.html#!#bidirectional-service

Look for the paragraph with the heading Parent and children communicate via a service and then the blue box:

Notice that we capture the subscription and unsubscribe when the AstronautComponent is destroyed. This is a memory-leak guard step. There is no actual risk in this app because the lifetime of a AstronautComponent is the same as the lifetime of the app itself. That would not always be true in a more complex application.

We do not add this guard to the MissionControlComponent because, as the parent, it controls the lifetime of the MissionService.

I hope this helps you.

Share
Improve this answer
Follow
edited Jun 20 '20 at 9:12

CommunityBot
111 silver badge
answered Jun 29 '16 at 11:08

Cerny
16533 bronze badges
4
as a component you never know whether you're a child or not. therefore you should always unsubscribe from subscriptions as best practice. – 
SeriousM
 Oct 29 '16 at 17:57
2
The point about MissionControlComponent is not really about whether it's a parent or not, it's that the component itself provides the service. When MissionControl gets destroyed, so does the service and any references to the instance of the service, thus there is no possibility of a leak. – 
ender
 Nov 10 '16 at 20:44
Add a comment

6

Based on : Using Class inheritance to hook to Angular 2 component lifecycle

Another generic approach:

export abstract class UnsubscribeOnDestroy implements OnDestroy {
  protected d$: Subject<any>;

  constructor() {
    this.d$ = new Subject<void>();

    const f = this.ngOnDestroy;
    this.ngOnDestroy = () => {
      f();
      this.d$.next();
      this.d$.complete();
    };
  }

  public ngOnDestroy() {
    // no-op
  }

}
Expand snippet
And use :

@Component({
    selector: 'my-comp',
    template: ``
})
export class RsvpFormSaveComponent extends UnsubscribeOnDestroy implements OnInit {

    constructor() {
        super();
    }

    ngOnInit(): void {
      Observable.of('bla')
      .takeUntil(this.d$)
      .subscribe(val => console.log(val));
    }
}
Expand snippet
Share
Improve this answer
Follow
edited Feb 23 '18 at 14:54
answered Apr 12 '17 at 11:04

JoG
83222 gold badges99 silver badges1616 bronze badges
1
This does NOT work correctly. Please be careful when using this solution. You are missing a this.componentDestroyed$.next() call like the accepted solution by sean above... – 
philn
 Feb 23 '18 at 12:00
@philn Should we use this.destroy$.next() and this.destroy$.complete() in ngOnDestroy() when using takeUntil? – 
Fredrick
 Dec 26 '20 at 15:31
it nicely works as is. the only missing thing is error handling. if components ngOnInit fails (it is f() in the code), the d$ still should emit. try/finally block is needed there – 
IAfanasov
 Sep 14 at 7:42

---
## From: JS-UI libs/Angular/0.material-api.md
---

Form field < name of compoennt

import {MatFormFieldModule} from '@angular/material/form-field';

Examples of Directives
- MattError
- MatFormField
- MatHint
- MatLabel

__Directive details (matformfield__

Selector: mat-form-field

Exported as: matFormField

Properites
@Input()
appearance:

Methods:

<mat-form-field appearance="fill">

Methods
close

__Example of classes__
- MatFormFieldControl: An interface which allows a control to work inside of a MatFormField.

__example of an interface__
 MatFormFieldDefaultOptions
Represents the default options for the form field that can be configured using the MAT_FORM_FIELD_DEFAULT_OPTIONS injection token.
__example of constants__
MAT_FORM_FIELD
MAT_PREFIX


---
## From: JS-UI libs/Angular/9.custom-types.md
---



ng generate interface


ng g i <filename>

ng g i habit
