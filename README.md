# A Step-by-Step Guide to Adding Bootstrap to an Angular Project

## Introduction
Bootstrap is a popular open-source front-end framework that provides a collection of CSS and JavaScript components for building responsive and mobile-first web applications. If you're working on an Angular project and want to leverage the power of Bootstrap, this step-by-step guide will walk you through the process of adding Bootstrap to your Angular application.

## Prerequisites
Before we begin, make sure you have a basic understanding of Angular and have an Angular project set up on your development environment. Also, ensure that you have Node.js and npm (Node Package Manager) installed on your machine.

## Step 1: Install Bootstrap via npm
To add Bootstrap to your Angular project, open your terminal or command prompt and navigate to your project's root directory. Then, run the following command to install Bootstrap:

```shell
npm install jquery bootstrap bootstrap-icons
```

This command will download the Bootstrap packages and its dependencies and save them in your project's `node_modules` directory.

## Step 2: Configure Angular to Use Bootstrap
Next, open your Angular project in your preferred code editor. Locate the `angular.json` file in the root directory of your project. This file contains the configuration for your Angular project. Look for the `"styles"` property within the `"architect"` object and add the path to Bootstrap's CSS files:

```json
"styles": [
  "node_modules/bootstrap/scss/bootstrap.scss",
  "node_modules/bootstrap-icons/font/bootstrap-icons.css",
  "src/styles.css",
],
```

By adding the path to the Bootstrap CSS file, you're instructing Angular to include Bootstrap's styles in your project.

## Step 3: Add Bootstrap JavaScript Dependencies
Bootstrap relies on JavaScript for some interactive components, such as dropdowns and modals. To include Bootstrap's JavaScript dependencies, go back to the `angular.json` file and find the `"scripts"` property within the `"architect"` object. Add the paths to the Bootstrap JavaScript files as shown below:

```json
"scripts": [
  "node_modules/jquery/dist/jquery.min.js",
  "node_modules/bootstrap/dist/js/bootstrap.min.js"
],
```

***Make sure to include the jQuery library before the Bootstrap JavaScript file, as Bootstrap requires jQuery to function correctly.***

## Step 4: Install Angular Native Support
Now we will install the `@ng-bootstrap/ng-bootstrap` library which contains native Angular support:

```shell
npm install @ng-bootstrap/ng-bootstrap
```

## Step 5: Add Module Libraries
After install, we will import the `NgbModule` module. Change the `app.module.ts` file and add the lines as below:

```ts
import { NgbModule } from '@ng-bootstrap/ng-bootstrap';

imports: [
  BrowserModule,
  NgbModule,
  AppRoutingModule,
],
```

## Step 6: Include NgbModule
Now we will remove the contents of the `AppComponent` class from the `src/app/app.component.ts` file. Import the `NgbModal` service and create the `open` method to open a modal as below.

```ts
import { Component } from '@angular/core';
import { NgbModal } from '@ng-bootstrap/ng-bootstrap';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss'],
})
export class AppComponent {

  constructor(private modalService: NgbModal) {
  }

  public open(modal: any): void {
    this.modalService.open(modal);
  }

}
```

## Step 7: Implement HTML
Next we will remove the contents of the `src/app/app.component.html` file. Add some components in the HTML to view and test the components as below.

```html
<nav class="navbar navbar-expand-sm navbar-light bg-light">
  <div class="container-fluid">
    <a class="navbar-brand" href="#">
      <h1>Angular Bootstrap</h1>
    </a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav me-auto mb-2 mb-lg-0">
        <li class="nav-item">
          <a class="nav-link active" aria-current="page" href="#">Home</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="#">Link</a>
        </li>
        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-bs-toggle="dropdown" aria-expanded="false">
            Dropdown
          </a>
          <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
            <li><a class="dropdown-item" href="#">Action</a></li>
            <li><a class="dropdown-item" href="#">Another action</a></li>
            <li><hr class="dropdown-divider"></li>
            <li><a class="dropdown-item" href="#">Something else here</a></li>
          </ul>
        </li>
        <li class="nav-item">
          <a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Disabled</a>
        </li>
      </ul>
      <form class="d-flex">
        <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
        <button class="btn btn-outline-success" type="submit">Search</button>
      </form>
    </div>
  </div>
</nav>
<div class="container-fluid py-3">
  <div class="row my-3">
    <div class="col">
      <label for="exampleFormControlInput1" class="form-label">Email address</label>
      <input type="email" class="form-control form-control-sm" id="exampleFormControlInput1" placeholder="name@example.com">
    </div>
  </div>
  <div class="row my-3">
    <div class="col">
      <label for="exampleFormControlTextarea1" class="form-label">Example textarea</label>
      <textarea class="form-control form-control-sm" id="exampleFormControlTextarea1" rows="3"></textarea>
    </div>
  </div>
  <div class="row my-3">
    <div class="col">
      <div class="form-check form-switch">
        <input class="form-check-input" type="checkbox" id="flexSwitchCheckDefault">
        <label class="form-check-label" for="flexSwitchCheckDefault">Default switch checkbox input</label>
      </div>
    </div>
  </div>
  <div class="row my-3">
    <div class="col">
      <button class="btn btn-sm btn-outline-primary" (click)="open(demoModal)">Launch demo modal</button>
    </div>
  </div>
</div>

<ng-template #demoModal let-modal>
  <div class="modal-header">
    <h4 class="modal-title" id="modal-basic-title">Profile update</h4>
    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close" (click)="modal.dismiss('Cross click')"></button>
  </div>
  <div class="modal-body">
    <form>
      <div class="form-group">
        <label for="dateOfBirth">Date of birth</label>
        <div class="input-group">
          <input id="dateOfBirth" name="dateOfBirth" class="form-control" placeholder="yyyy-mm-dd" ngbDatepicker #dp="ngbDatepicker">
          <button type="button" class="btn btn-outline-secondary bi bi-calendar" (click)="dp.toggle()"></button>
        </div>
      </div>
    </form>
  </div>
  <div class="modal-footer">
    <button type="button" class="btn btn-outline-dark" (click)="modal.close('Save click')">Save</button>
  </div>
</ng-template>
```

## Step 8: Verify Bootstrap Integration
To verify that Bootstrap has been successfully added to your Angular project, start your development server by running the command:

```shell
npm start
```

Open your project in a web browser, and you should see that Bootstrap styles are applied. You can also test Bootstrap components and features to ensure that the JavaScript functionality is working as expected.

## Conclusion:
In this tutorial, we've covered the steps to add Bootstrap to an Angular project. By following these steps, you can quickly integrate Bootstrap's CSS and JavaScript components into your Angular application, enabling you to build responsive and visually appealing user interfaces.

Remember to refer to the Bootstrap documentation for further guidance on using its components, customizing styles, and leveraging additional features to enhance your Angular project. Happy coding!

Note: This article was built using Angular version 2 or later. The steps may vary slightly if you're using an older version of Angular.