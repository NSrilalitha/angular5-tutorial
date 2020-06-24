# angular5-tutorial

To learn angular 5, refer below links.

There is a 1hour angular 5 course avaialble in Udemy
https://www.udemy.com/course/angular-5/

https://www.freecodecamp.org/news/want-to-learn-angular-heres-our-free-33-part-course-by-dan-wahlin-fc2ff27ab451/
https://scrimba.com/p/pQxesM/ce4baHb

Overview of Angular 5
=====================
1. Installation
================

node -v

npm -v

npm install @angular/cli -g

ng -v
this gives current anuglar version installed

create new project
ng new ng5 --style=scss --routing

to start the project use below command
ng serve

one command prompt should open always with ng serve, so that the application will be running

2. Angular 5 components
========================

1. To create component using Angular CLI use below command
   ng generate component home -> this creates component called home
   
   For component it creates following files
   src/app/home/home.component.html
   src/app/home/home.component.spec.ts
   src/app/home/home.component.ts
   src/app/home/home.component.scss
   
   and updates src/app/app.module.ts
   
   
   home.component.ts
   ------------------
   first import section
   
   eg: import { Component, OnInit } from '@angular/core';
   
   defining component
   
   eg:
   @Component({
		selector: 'app-home',
		templateUrl: './home.component.html',
		styleUrls: ['./home.component.scss']
   })
   
   export component
   
   eg: export class HomeComponent implements OnInit {
   
			constructor() { }
			
			ngOnInit() {
			}
       }
   
   shorthands for generate is g and for component is c.
   so we can write generate command as shown below
   
   ng g c about -> this create component called about
   
3. Templating and Styling
=========================

For templating we have to modify component.html
eg: home.component.html

for styling update scss files
eg: home.component.scss

for global styling we can modify
styles.scss

4. Interpolation, property & event binding
==========================================

Interpolation:
-------------
eg: {{ itemCount }} 

itemCount should declared in home.component.ts file as shown below
itemCount: number = 4


property binding :
----------------
lets define btnText in ts file as shown below
btnText: String = 'Add an item';

now use this btnText in html file using interpolation as shown below
<input type="submit" class="btn" value={{ btnText}} >

we can use btnText in html using property binding as shown below
<input type="submit" class="btn" [value]="btnText">

two-way data binding :
-------------------
[(ng-model)] = "goalText"

inorder to perform two-way data binding we need to import FormsModule in app.module.ts
and it should be avaialble in imports section of app.module.ts

eg: import { FormsModule } from '@angular/forms';

event binding :
-------------

(click)="addItem()"

this click event should be mentioned in parenthesis.

addItem() function should be declared in home.component.ts file

eg: addItem() {
		this.goals.push(this.goalText);
		this.goalText = '';
		this.itemCount = this.goals.length;
    }
	
ngOnInit() is the life cycle hook. whenever component loads ngOnInit() function
gets executed

eg: lets say we have array defined in ts file
   goals = [];
   
   this goals gets dynamically updated through form submission through click event
   
   now inorder to print this goals , we have to iterate through array.
   
   in html file we have to ngFor to iterate over goals array and use interpolation to display its values
   
   <p class="life-container" *ngFor="let goal of goals">
      {{ goal }}
   </p>


5. Animations:
==============
Inorder to use animations we have to install animations library using CLI as shown below

npm install @angular/animations@latest --save

run as administrator and run this commmand if you get any error

Inorder to use animations now import BrowserAnimationsModule in app.module.ts

eg: import { BrowserAnimationsModule } from '@angualr/platform-browser/animations';

and add this entry in imports section

eg:
 imports: [
    BrowserModule,
    AppRoutingModule,
    FormsModule,
    BrowserAnimationsModule
 ]

Now inorder to use animation functions, import them in home component ts file as shown below

eg: import { trigger, style, transition, animate, keyframes, query, stagger } from '@angular/animations';

And animations should reside in @Component section after styleUrls


6. Routing
============
For routing we need to update in app-routing.module.ts

here import components whatever we want to rounte

and declare routes const and specify paths for components

eg:
const routes: Routes = [
	{
		path: '',
		component: HomeComponent
	},
	{
		path: 'about/:id',
		component: AboutComponent
	}
];


Inorder to retrieve any query params or path params in the url in component,

import router as shown below
import { Router } from '@angular/router';
 
go to about.component.ts and modify constructor as shown below

constructor(private route: ActivatedRoute, private router: Router) {
 this.route.params.subscribe(res => console.log(res.id));
}

inorder to navigate to another component from one component we can use event binding
with router as well

eg: 
sendMeHome() {
  this.router.navigate(['']);
}

7. Services 
============

Services are generally used to share data among multiple components or to make http calls.

To create service use CLI with below command
ng generate service data

 it creates following files
  src/app/data.service.spec.ts
  src/app/data.service.ts
  
Components generally decorated with Component decorator.

Services decorated with Injectable decorator

import { Injectable } from '@angular/core';

@Injectable()

export class DataService {
	
	constructor() { } 

}


Services should be updated in app.module.ts

we have to import that service and it should be avaialble in providers section

8. App Deployment
==================

Use Angular CLI to build the application
ng build

dist folder will be created

ng build --prod

this creates very less files in dist folder

we can deploy dist folder to server we want

or we can use github pages to publish the app

create a repository in github and push the application to github

and then run build command again with --base-href as shown below

ng build --prod --base-href="https://designcourse.github.io/ng5"

next run below command

angular-cli-ghpages
