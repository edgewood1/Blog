KO - allows to link a data model to a UI
MVVM - a design pattern for building a UI

**Model** 

- App’s stored data + all possible operations.

**View model**

- a list of items to display in view
- A list of method to add/remove items (event handlers)

```js
let vm = {person: 'mel'}
```

**View**

- refers to the template 
- displays / applies view model info 

In KO, we use data-bind attribute, which isn’t native KO

```html
<div> hello, 
  <span data-bind=“text: person”></span>
</div>
```

To activate the binding: 

```ko.applyBindings(myViewModel);```

Observables

- view-model properties can be declared as oservables
- now, when model property `person` changes, so does the view (the UI).
- observables are JS objects that notify subscribers about changes

```js
let vm = {
  person: ko.observable(person)
}
```

In your code, you can also: 

Read a prop: 

`vm.person()`

Write a new value to the observable: 

`vm.peson('john')`

or 

`vm.person('john').age(40)`

Stopped at "explicitly subscribing to observable"



computed observable

- functions depenent on other observables
- Auto-update whenever these update

`this.fullname = ko.computed(()=> this.firstName() + this.lastName();`

***** to see logs on docker

docker logs container --follow

if you add a new console.log >> 

stop and play a container. 

anonymizeAndPull


