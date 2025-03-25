                               Angular

- framework mantain by google
- can build single page application
- angular version :- angularjs --> angular 18
- MVC at client side
M -> Model can put schema , interface
V -> View can put html content 
C -> Controller can put logic part in ts file
- AOT compiler

**JIT (Just-In-Time):**  
Compiles the application code during run time on the user's device. It results in slower startup because the code is being compiled as it executes, but it's useful for development as it allows dynamic changes.  

**AOT (Ahead-Of-Time):**  
Compiles the application code at build time before deployment. This leads to faster startup, better performance, and earlier error detection, making it ideal for production.

# environment

Install node js
then install angular cli npm install -g @angular/cli or @angular/cli@latest

npm cache clean or npm cache verfiy

ng version

# create angular project

ng new project_name

--> specify the port

> > ng serve --port 5233

--> this add ssr in existing angular project with not
ng add @angular/ssr

# ngModule and standalone component

before angular 14 if we create a compoennt , we need to declear it in module file 

![Alt text](./assests/angular/ngvsstandlaone)

lazy loading
if done lazy loading in ngmodule the whole mofule have to lazy load and in standalone component we even can lazy load a component

--> this create ngmodule project

> > ng new project_name --no-standalone

# Can Write Html And css direct in .ts file

```java
@Component({
  selector: 'app-root',
  // templateUrl: './app.component.html',
  // styleUrl: './app.component.css',
  styles:"",
  template:""
})
```
# user app-root  to another component 
import that compoennt in imports
then can user in html file <app-root></app-root>
# Interpolation <h1>{{name}}</h1>

```angular
import { Component } from '@angular/core'; import { RouterOutlet } from
'@angular/router'; @Component({ selector: 'app-root', templateUrl:
'./app.component.html', styleUrl: './app.component.scss' }) export class
AppComponent { name:string="Sachin" status:string="single" salary:number=30000
diableButton:boolean=true } in .html file
<h1>{{ name.toUpperCase() }} salary {{salary}]</h1>
```

# Property Binding

<button [disabled]="diableButton">Property Binding</button>

# Event Binding
<!-- <input type="text" (changeases)="onChange($event)"/> -->
<input type="text" (input)="onChange($event)"/>
onChange(e:Event){
const value=(e.target as HTMLInputElement).value;
}

# TwoWay data binding

<input type="text" [value]="inputVar" (input)="onChange($event)"/>

<h2>{{inputVar}}</h2>

onChange(e:Event){
const value=(e.target as HTMLInputElement).value;
this.inputVar=value;
}

## with FormsModule

import this first

import { FormsModule } from '@angular/forms';
imports:[FormsModule],

<input type="text" [(ngModel)]="inputVar"/>

# Iterate

1.  control flow syntax
    <div>
      @for(let user of users;track user._id){
        @if(user[0]=="s"){
       <h1>{{user}}</h1>
        }
      }
    </div>
    <div>
      @for(user of users;track user){
        @if(user[0]=="s"){
        <h1>{{user}}</h1>
        }
      }

        @for(user of users;track user){ @if(user[0]=="s"){

      <h1>{{ user }}</h1>
      }@else{
      <h1>no in league</h1>
      } }
    </div>

2.  directives
import NgFor
imports:[FormsModule,NgFor,NgIf,CommonModule],
or
imports:[FormsModule,CommonModule],
<div *ngFor="let user of users; trackBy: trackByFn">
  <h1>{{ user }}</h1>
</div>

---------- or -----------

<div *ngFor="let user of users; trackBy: trackByFn">
  <h1 *ngIf="user[0]=='s'">{{ user }}</h1>
</div>

# ng-template and else if 

ng-template is an Angular element used to define reusable, non-rendered content that can be conditionally or dynamically displayed in the DOM

<ng-template #headerTemplate>
  <h1>Welcome!</h1>
</ng-template>

<div>
  <p>Main content goes here.</p>
</div>

<ng-container *ngTemplateOutlet="headerTemplate"></ng-container>


<div *ngIf="condition1; else elseIf2">
  Condition 1 is true.
</div>
<ng-template #elseIf2>
  <div *ngIf="condition2; else elseIf3">
    Condition 2 is true.
  </div>
</ng-template>
<ng-template #elseIf3>
  <div *ngIf="condition3; else elseTemplate">
    Condition 3 is true.
  </div>
</ng-template>
<ng-template #elseTemplate>
  None of the conditions are true.
</ng-template>



# switch case
<div [ngSwitch]="true">
  <div *ngSwitchCase="condition1">Condition 1 is true.</div>
  <div *ngSwitchCase="condition2">Condition 2 is true.</div>
  <div *ngSwitchCase="condition3">Condition 3 is true.</div>
  <div *ngSwitchDefault>None of the conditions are true.</div>
</div>

# directive
directive is a class that allows you to attach behavior to elements in the DOM or modify their appearance and structure.

trackByFn(index:number,user:any){
return user;
}


constructor(){

}
> life cycle hook
ngOnInit(){

}
constructor --> ngOnInit()

# button
<button (click)="changeTitle"></button>

 class="titile"

button.titile{

}
or
.titile{

}

# Data passing from parent to child
<app-user-profile name="sachin"></app-user-profile>
<app-user-profile name="sachin" isSingle></app-user-profile>
function functionName(value){
return value;
}
@Input({alias:"userName",transform:functionName}) name=""

## booleanAttribute
@Input({alias:"userName",transform:booleanAttribute}) name=""


# data passing from child to parent  @Output and events
>> through events

in child
@Output() myEvent =new EventEmitter<string>(); import from core
<{name:string,id:number}>
sendData(){
  this.myEvent.emit("any string")
}
or
this.myEvent.emit({name:"",id:""});


add event listner in parent compoennt

(myEvent)="functionName($event)"

functionName(event:Event){
  console.log(event)
}

# pipe and custom pipe
* Date pipe
<p>{{ today | date }}</p>
<p>{{ today | date:'fullDate' }}</p>
<p>{{ today | date:'shortTime' }}</p>

Dec 9, 2024
Monday, December 9, 2024
11:30 AM

* Uppercase pipe
<p>{{ 'angular pipes' | uppercase }}</p>

ANGULAR PIPES

* lower case pipes
<p>{{ 'ANGULAR PIPES' | lowercase }}</p>

* titilecase pipe
<p>{{ 'angular pipes' | titlecase }}</p>

* currency pipe
<p>{{ 1234.56 | currency }}</p>
<p>{{ 1234.56 | currency:'USD':'symbol':'1.2-2' }}</p>
<p>{{ 1234.56 | currency:'INR':'symbol-narrow' }}</p>

$1,234.56
$1,234.56
₹1,234.56

* percent pipe
<p>{{ 0.25 | percent }}</p>
<p>{{ 0.25 | percent:'1.0-2' }}</p>

25%
25.00%


* Decimal pipe
<p>{{ 1234.567 | number }}</p>
<p>{{ 1234.567 | number:'1.0-2' }}</p>
<p>{{ 1234.5 | number:'2.2-3' }}</p>
{minIntegerDigits}.{minFractionDigits}-{maxFractionDigits}


1,234.567
1,234.57
01,234.500


* slice pipe
<p>{{ 'Angular Pipes' | slice:0:7 }}</p>
<p>{{ [1, 2, 3, 4, 5] | slice:1:3 }}</p>

* json pipe
<p>{{ { name: 'Angular', version: 17 } | json }}</p>

* keyValue pipe
<p *ngFor="let item of {name: 'Angular', version: 17} | keyvalue">
  {{ item.key }}: {{ item.value }}
</p>

name: Angular
version: 17

* async pipe
@Component({
  selector: 'app-root',
  template: `<p>{{ promiseData | async }}</p>`
})
export class AppComponent {
  promiseData = new Promise(resolve => setTimeout(() => resolve('Hello from Promise!'), 2000));
}

* i18nSelect Pipe

<p>{{ gender | i18nSelect:genderMap }}</p>

gender = 'male';
genderMap = {
  male: 'He is learning Angular.',
  female: 'She is learning Angular.',
  other: 'They are learning Angular.'
};

*  i18nPlural Pipe
<p>{{ messages.length | i18nPlural:messageMap }}</p>

messages = ['Message 1', 'Message 2'];
messageMap = {
  '=0': 'No messages.',
  '=1': 'One message.',
  other: '# messages.'
};
 -

## custom pipe
ng g p pipes/cutomPipe

import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'cutomPipe'
})
export class CutomPipePipe implements PipeTransform {

  transform(value: unknown, ...args: unknown[]): unknown {
    return null;
    // value will be contain teh actual value used in pipe
    args contain value that pass after pipename followed by : symbols
  }

}

to use this import this in imports in any module

# Custom directive
[style.backgroundColor]="colorNameFromTsFile"

use directive if want to use this functionality in many places

> ng g d directives/highlighter

import { Directive, HostBinding } from '@angular/core';

@Directive({
  selector: '[appHighligher]'
})
export class HighligherDirective {

  constructor() { }

  @HostBinding("style.backgroundColor")
  bgColor="red"

}


import { Directive, HostBinding, HostListener } from '@angular/core';

@Directive({
  selector: '[appHighligher]'
})
export class HighligherDirective {
  private isHighlighted = false;

  @HostBinding('style.backgroundColor') bgColor = 'red';

  @HostListener('click') toggleHighlight() {
    this.isHighlighted = !this.isHighlighted;
    this.bgColor = this.isHighlighted ? 'yellow' : 'red';
  }

  constructor() {}
}
------------ or -----------------

export class HighligherDirective {
el:ElementRef
  constructor(el:ElementRef){
    this.el=el
  }

  ---- or -------
  constructor(public el:ElementRef){}

  @HostBinding('style.backgroundColor') bgColor = 'red';

  @HostListener('mouseenter') toggleHighlight() {
   this.el.nativeElement.style.fontSize="50px"
  
  }
}

import directive in imports
<h1 appHighligher ></h1>

# Life cycle methods
Lifecycle hooks are special methods in Angular that let you run code at specific times in a component's life. 

## availabe in class in js file . it calls when an instance of a class created
contructor()

### implements OnInit
Use ngOnInit for initialization logic that runs once when the component is created.

ngOnInit(){
  // called when component in ready
  // initilise properties
  // when call initial api
}
constructor --> ngOnI
nit

### ngDoCheck: Custom Change Detection
Called during every change detection cycle, even if no data has changed.
After Angular's default change detection checks inputs.
ngDoCheck() {
  console.log('Custom change detection logic');
}


### implements OnDestroy
ngOnDestroy(){
  called when compoent on longer exist
}

## change when compoennt rerender
ngOnChanges(){

}

##  Logic to execute only when `specificValue` changes
ngOnChanges(changes: SimpleChanges): void {
    if (changes['specificValue'] && changes['specificValue'].previousValue !== changes['specificValue'].currentValue) {
      console.log('specificValue has changed:', changes['specificValue'].currentValue);
    }
}

The SimpleChanges object provides metadata about the changed properties, including:
* previousValue: The value before the change.
* currentValue: The new value.
* firstChange: A boolean indicating if this is the first change.

### ViewChild
template varibale
<h1 #myheading ></h1>

in js file
@ViewChild("myheading") myheading:ElementRef

this.myheading.nativeElement.fontSize

## ngAfterVeiwInit
ngAfterVeiwInit(){
  // this called when templete mount on the ui or template ready
}




Here is a detailed and sequential explanation of all Angular lifecycle hooks, their purpose, when they are called, and the correct order in which they execute:

Complete Angular Lifecycle in Order
The lifecycle hooks are triggered in the following sequence:

1. ngOnChanges()
When it’s called:
It is called whenever an @Input() property value changes.
Called before any other lifecycle hook and even before the component is initialized.
Purpose:
Respond to changes in input properties passed from a parent component.
Runs Before: ngOnInit.
Example:
typescript
Copy code
ngOnChanges(changes: SimpleChanges) {
  console.log('Input property changed:', changes);
}
2. ngOnInit()
When it’s called:
Called once after the component's input bindings (@Input) are set.
Runs after the first call to ngOnChanges.
Purpose:
Initialize the component after Angular has set the input properties.
Perform one-time initialization logic, such as fetching data.
Runs After: ngOnChanges.
Example:
typescript
Copy code
ngOnInit() {
  console.log('Component initialized');
}
3. ngDoCheck()
When it’s called:
Called during every change detection cycle, even if no data has changed.
After Angular's default change detection checks inputs.
Purpose:
Perform custom logic during change detection, especially for detecting changes in nested objects or arrays.
Runs After: ngOnInit.
Example:
typescript
Copy code
ngDoCheck() {
  console.log('Custom change detection logic');
}
4. ngAfterContentInit()
When it’s called:
Called once after Angular projects content into the component (via <ng-content>).
Purpose:
Respond to initialization of projected content.
Runs After: ngDoCheck.
Example:
typescript
Copy code
ngAfterContentInit() {
  console.log('Content projected into the component');
}
5. ngAfterContentChecked()
When it’s called:
Called after every check of the projected content.
Runs during every change detection cycle.
Purpose:
Perform custom actions after content has been checked.
Runs After: ngAfterContentInit.
Example:
typescript
Copy code
ngAfterContentChecked() {
  console.log('Projected content checked');
}
6. ngAfterViewInit()
When it’s called:
Called once after the component's view (and child components) has been fully initialized.
Purpose:
Perform actions that depend on the DOM or child components being fully rendered.
Runs After: ngAfterContentChecked.
Example:
typescript
Copy code
ngAfterViewInit() {
  console.log('View fully initialized');
}
7. ngAfterViewChecked()
When it’s called:
Called after every check of the component's view (and child views).
Runs during every change detection cycle.
Purpose:
Perform actions after the view has been checked.
Runs After: ngAfterViewInit.
Example:
typescript
Copy code
ngAfterViewChecked() {
  console.log('View checked');
}
8. ngOnDestroy()
When it’s called:
Called just before the component is destroyed.
Purpose:
Clean up resources like subscriptions, event listeners, or timers to prevent memory leaks.
Runs Last.
Example:
typescript
Copy code
ngOnDestroy() {
  console.log('Component destroyed');
}
Execution Order of Lifecycle Hooks
Here’s the exact sequence in which lifecycle hooks are called:

ngOnChanges (if there are @Input changes).
ngOnInit.
ngDoCheck.
ngAfterContentInit.
ngAfterContentChecked.
ngAfterViewInit.
ngAfterViewChecked.
ngOnDestroy (when the component is destroyed)

## HttpClient Service, DI & inject
user service to have organised http request and mantain globalState
ng g s services/nameoftheservice

inside service module
http:HttpClient
constructor(http:HttpClient){
  this.http=http
}
or 
private http=inject(HttpClient)
getJoke(){
  this.http.get().subscribe(data=>{
    console.log(data)
  })
}
construtor(jokeService:JokeService){}
this.jokeService.getJoke()
add provideHttpClient() in app.config.ts  in providers
##### Observale vs Promise

## state management using services

in services
private count=0

getCounter(){
  return this.count;
}

addCount(){
  this.count++;
}

>> to create a seperate instance we need to import services in providers:[] in compoennt

## signal in angular ( introduce in angular 16)
by default angular use zone.js

>> convert a variable to signal variable
private count =signal(0);

signals are of 2 type writable and readable signals

--> writable
when to get value -->
* this.count()
* this.count.set(5)
* this.count.set(this.count()+5)
* this.count.update((pre)=>pre+1)

--> readable
doubleCount:Signal<number>=computed(()=>this.count()*2);

when get this value , will return computed value

.doubleCount()

can we access any where if public 
services.doubleCount();

constructor(){
  effect(()=>{
    console.log(this.count(),"",this.doubleCount())
  })
}

>> convert input to signal 
name = input("",{
  alias:"",
  transform:functionNAME
})

this.name() in compoennt and name() in html

## Routing

in app.config

import {routes} from "./app.routes";
providers:[provideRouter(routes)]

in app.routes.ts

export const routes:Routes=[
  {path:"login",component:LoginComponent}
];

then add <router-outlet><router-outlet>

then import that in app.compoennt.ts
imports:[RouterOutlet]

<a routerLink="/" routerLinkActive="active"></a>

import this in import of that component
RouterLink, RouterLinkActive

## reactive and template driven forms


