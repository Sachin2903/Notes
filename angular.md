                               Angular

- framework mantain by google
- can build single page application
- angular version :- angularjs --> angular 18
  MVC at client side
  AOT compiler

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

![Alt text](./assests/angular/ngvsstandlaone)

lazy loading
if done lazy loading in ngmodule the whole mofule have to lazy load and in standalone component we even can lazy load a component

--> this create ngmodule project

> > ng new project_name --no-standalone

# AOT vs JOT

--> create a component

> > ng g c components/user-profile
> > ng generate component \_\_\_

## to use the component in any .html file

need to add the compoent in imports of component.ts file

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
      @for(let user of users;track user){
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

trackByFn(index:number,user:any){
return user;
}
