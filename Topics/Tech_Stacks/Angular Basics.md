
# Understanding Angular: A Guide for Beginners

# Prerequisites
- HTML
- CSS
- TypeScript

## 1. What are Components?

### Definition
In Angular, components are the fundamental building blocks. They control a part of the UI for your application. Each component consists of three main parts:

- **Template**: This is the HTML part, defining how the component looks.
- **Class**: Written in TypeScript, it handles the data and behavior of the component.
- **Decorator**: This provides metadata about the component, like its selector and template URL.

For example

**list.component.ts** (files are stored as .ts, guess what ts stands for - hint: it's not Top Secret)
```
import { Component } from '@angular/core';

@Component({
  selector: 'app-list',
  template: `list.component.html`,
})
export class ListComponent {
    users = {
        { name: 'John', age: 20 },
        { name: 'Jane', age: 21 },
        { name: 'Jack', age: 22 },
    }
}
```

**list.component.html**
```
<ul>
    <li *ngFor="let user of users">
        {{ user.name }} is {{ user.age }} years old.
    </li>
</ul>
```

I think the easiest way to look at a Component is a Class which will be shown on your screen. It may be shown multiple times, and may require some different data to be shown. For example, a list of users may be shown on the screen, and each user may have a different name, age, and other information. The component is the class which will be used to show the user on the screen, and the data will be passed in to the component.


### Usage

You created a list component and some other cool looking components for your page. Now, how do you use it?

Not following angular conventions, you just put them in a mega html called

**app.component.html**
```
<app-list></app-list>
<app-cool-component></app-cool-component>
```

## 2. Component Interaction

### Inheritance
Components can inherit from other components, sharing functionalities like methods or properties. Think of it like a family tree where children inherit traits from their parents.

### Communication
- **Input**: Components can receive data from their parent using `@Input()`. It's like getting a present; the parent component sends it, and the child receives it.
- **Output**: To communicate back to the parent, a child component uses `@Output()` and EventEmitter. It's like the child sending a letter back home.

Imagine you wanted to dynamically input users into your list component and output the oldest user. You could do something like this:

**app.component.html**
```
<app-list [users]="usersFromAppComponent" (oldestUser)="oldestUser($event)"></app-list>
```
In Angular, `$event` represents the data emitted by an event. In our code, `$event` carries the data from the `oldestUser` event of `app-list` to the `oldestUser` method in the parent component, enabling inter-component communication.

**list.component.ts**
```
import { Component, Input, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-list',
  template: `list.component.html`,
})
export class ListComponent {
    @Input() users: any[];
    @Output() oldestUser = new EventEmitter<any>();

    getOldestUser() {
        let oldestUser = this.users[0];
        for (let user of this.users) {
            if (user.age > oldestUser.age) {
                oldestUser = user;
            }
        }
        this.oldestUser.emit(oldestUser);
    }
}
```

**list.component.html**
```
<ul>
    <li *ngFor="let user of users">
        {{ user.name }} is {{ user.age }} years old.
    </li>
</ul>
<button (click)="getOldestUser()">Get Oldest User</button>
```

Note we added a button to the list component, which when clicked will emit the oldest user to the parent component. `getOldestUser()` is a method that finds the oldest user and emits it to the parent component.

EventEmitter is a just fancy way of saying, well Event Emitter. It emits an event, which is the oldest user in this case. The parent component can listen to this event and do something with it.

You decorate the oldestUser property with `@Output()` to tell Angular that this property is an output property, and can be listened to by the parent component, and you decorate the users property with `@Input()` to tell Angular that this property is an input property, and can be passed in by the parent component.


## 3. Interaction with HTML, CSS, and Templates

### The Connection
- **HTML**: Defines the structure and layout of the component's view.
- **CSS**: Styles the component. Each component can have its styles, making it independent in terms of design.
- **Template**: The template (HTML) and styles (CSS) come together to form the visual part of the component.

## 4. What are Services?

### Definition
Services are classes that handle data and logic that isn't associated with views (components). They can be shared across components. 

### Usage
Use services for tasks like fetching data from a server or user authentication. It's like a delivery service for your app, carrying data and instructions where needed.

### Example
Let's say you want to fetch a list of users from a server. You could do something like this:

**user.service.ts**
```
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';

@Injectable()
export class UserService {
    constructor(private http: HttpClient) {}

    getUsers() {
        return this.http.get('https://my-cool-app.com/users');
    }
}
```

This simple-dimple service just calls an API, and returns the response. You can definetly add more logic to it, cook it up, and make it more complex as per your taste. 

## 5. What are Modules?

### Overview
Modules in Angular are containers that group related components, services, directives, and pipes. (Don't worry about directives and pipes for now). They can also be used to organize your app into separate functional areas. 

Suppose you have a website that has an about section, a contact section, and a home section. You can create a module for each section, and put the components, services, etc. related to that section in the module.

### Purpose
They help in organizing the app's functionality and managing dependencies.

### Usage
App Module is the classy module that is created by default when you create a new Angular app. It's the root module of the app, and it's where you import other modules.

Example of a module:

**about.module.ts**
```
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { AboutComponent } from './about.component';
import { OtherCoolAboutComponent} from './other-cool-about.component';

@NgModule({
  imports: [
    CommonModule
  ],
  declarations: [AboutComponent, OtherCoolAboutComponent],
})
export class AboutModule { }
```

## Additional Resources
- [Angular Docs](https://angular.io/docs)
- [Angular Tutorial](https://angular.io/tutorial)
- [Angular Cheatsheet](https://angular.io/guide/cheatsheet)
- [Angular Tutorial for Beginners](https://www.youtube.com/watch?v=2OHbjep_WjQ)
- [Angular Crash Course](https://www.youtube.com/watch?v=Fdf5aTYRW0E)





