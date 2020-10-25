# Modular apps in Angular

## Introduction
Project structure is important to create a manageable application.
As it stands right now our small project is still growing, however it has a significant ammount of components already.
Here's a snapshot of it:
```
|-- app-routing.module.ts
|-- app.component.css
|-- app.component.html
|-- app.component.spec.ts
|-- app.component.ts
|-- app.module.ts
|-- user-create
|   |-- user-create.component.css
|   |-- user-create.component.html
|   |-- user-create.component.spec.ts
|   `-- user-create.component.ts
|-- user-edit
|   |-- user-edit.component.css
|   |-- user-edit.component.html
|   |-- user-edit.component.spec.ts
|   `-- user-edit.component.ts
`-- user-list
    |-- user-list.component.css
    |-- user-list.component.html
    |-- user-list.component.spec.ts
    `-- user-list.component.ts
```

Aside from being clutered that has generated its own set of problems, I'm sure you all have noticed that every merge, be it from master to feature branch, or from feature branch to master has merge conflicts.
The reason for that is that each time a new component is created, changes are made to `app.components.ts` and since we are all creating components, those changes don't play nice.
That's sign of a bad structure.

As such, there's a need to improve our project structure to minimize conflicts and enhance code navigation.

## Angular modules and components: brief intro

The building blocks that make up Angular's architecture are modules and components.
In short, there's a lot of information about those but I will try to go over the minimum necessary to address the structural issues previously mentioned.

### Components
Components are used to create views in angular.
A Component is made up of: style information (css), a template and JavaScript/Typescript.

The style file contains css for the component's html element.
The typescript file contains code which will execute as the template loads.
It's important to note that a componentat has a *selector* associated to it, check any `component.ts` file.
The selector is used to call that component from within a template, something like `<app-component></app-component>`.
The template contains HTML, Angular interpolation directives (`{{ user.name }}`) and selector tags to load other componentst.

A component is usually associated to a module.

### Modules
In short, a module is a typescript class annotated with `@NgModule`.
The `NgModule` annotation contains metadata regarding what that module contains, its properties are: `declarations`, `exports`, `imports`, `providers` and `bootstrap`.
Let's focus on `imports`, `declarations` and `exports`.

The `imports` property defines a list of **modules** that our module needs.
For instance, in our application we've had a need to use forms and as such we imported the `FormsModule` in the `app.module.ts`.
Note that there are two imports happening: `import { FormsModule } from '@angular/forms';` which occurs on the first few lines of `app.module.ts` and another one `@NgModule({imports: commonModules})` which happens inside the annotation.
In short, `import { FormsModule } from ...` is a mechanism for *javascript* to locate the `FormsModule` class and the NgModule import is a way for *Angular* to manage names exposed by a module.

The `declarations` keyword is used to specify which *components* will be made available in the current module.
As an exercise, remove a component from the `delcarations` array and try calling its selector in the html file.
The error generated from that is because every component that is going to be use by our module *must* be made visible in the `declarations` array.

Lastly, the `exports` array is used to control which *components* will be visible to *external modules* importing *this module*.
Reread that, seriously.

## Creating module and consuming it

### Creating module
Our goal is to collect a set of components and encapsulate those within a module.
The following steps will create an `user` module that contains 3 components: `create`, `list` and `edit`.
As a convenience, assume the current working directory to be `/src/app`, as such the path `user/` stands for `/src/app/user/`.

Starting with an empty project, the order of steps are:
1. Create module
2. Create components inside the module.
3. Configure `@NgModule`.
4. Routing inside a module

1 Create module

```
ng generate module user --routing=true
```
The previous command will create a new empty `user` module with routing in the app directory, the output will look like this:
```
.
|-- app-routing.module.ts
|-- app.component.css
|-- app.component.html
|-- app.component.spec.ts
|-- app.component.ts
|-- app.module.ts
`-- user
    |-- user-routing.module.ts
    `-- user.module.ts
```
The routing is optional, but since our module will contain routing, it saves a few keystrokes.

2 Create components inside the module.

First, let's create the user component which will be exported by the user module.
```
ng generate component user
```

Which will look like:
```
|-- app-routing.module.ts
|-- app.component.css
|-- app.component.html
|-- app.component.spec.ts
|-- app.component.ts
|-- app.module.ts
`-- user
    |-- user.component.css
    |-- user.component.html
    |-- user.component.spec.ts
    |-- user.component.ts
    |-- user-routing.module.ts
    `-- user.module.ts
```

The command generated the usual component files inside the user directory.

Next, the sub-components of user.
The following commands will generate the 3 components of interest.
```
ng generate component user/create 
ng generate component user/list 
ng generate component user/edit 
```
Angular cli allows the user to specify a prefix directory for generating components (it also works for modules).
The above commands generate a component inside the user module.
Here's the output:
```
|-- app-routing.module.ts
|-- app.component.css
|-- app.component.html
|-- app.component.spec.ts
|-- app.component.ts
|-- app.module.ts
`-- user
    |-- create
    |   |-- create.component.css
    |   |-- create.component.html
    |   |-- create.component.spec.ts
    |   `-- create.component.ts
    |-- edit
    |   |-- edit.component.css
    |   |-- edit.component.html
    |   |-- edit.component.spec.ts
    |   `-- edit.component.ts
    |-- list
    |   |-- list.component.css
    |   |-- list.component.html
    |   |-- list.component.spec.ts
    |   `-- list.component.ts
    |-- user.component.css
    |-- user.component.html
    |-- user.component.spec.ts
    |-- user.component.ts
    |-- user-routing.module.ts
    `-- user.module.ts
```

Using `ng generate component user/...` has the convenience of adding the created components to the `declarations` array inside `user.module.ts`.
```
$ cat user/user.module.ts
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { UserComponent } from './user.component';
import { EditComponent } from './edit/edit.component';

...

declarations: [UserComponent, EditComponent, ListComponent, CreateComponent],

```

3 Configure `@NgModule`

In order to call `user.component.ts` in the main application it must be added to the exports array in `user.module.ts`, as in:

```
@NgModule({
  declarations: [UserComponent, EditComponent, ListComponent, CreateComponent],
  imports: [
    CommonModule
  ],
    exports: [UserComponent]
})
export class UserModule { }

```

4 Routing inside a module

Internally our module might make use of the angular routing.
Since the module was created with routing, this makes things a bit easier.
Add the routes our component will use inside the `routes` array in `user-routing.ts`.

```
const routes: Routes = [
    {path: 'users/:id/edit', component: EditComponent},
    {path: 'users/create', component: CreateComponent},
    {path: 'users, component: ListComponent},
];

```

It's helpful to point out that a module is independent of the main application.
It needs to import its own dependencies such as Forms, Angular Material modules and so on.
The module is a mini-application inside the main application.

### Consuming the module

Now that we have the module created, to consume it we must import it in `app.module.ts`.

First the JS import `import { UserModule } from './user/user.module';` then the angular import:

```
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';

import { UserModule } from './user/user.module';

@NgModule({
  declarations: [
    AppComponent,
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    UserModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

With the module imported, we now have access to all names in the `user.module.ts`, namely the `user.component.ts` component.
So now it's possible to use `<app-user></app-user>` as a selector `app.component.html` (or any other modules that import the user module).
