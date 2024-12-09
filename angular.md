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
Compiles the application code during runt  ime on the user's device. It results in slower startup because the code is being compiled as it executes, but it's useful for development as it allows dynamic changes.  

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
