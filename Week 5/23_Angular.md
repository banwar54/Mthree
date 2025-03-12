# Angular Introduction & Routing Guide for Beginners

## Table of Contents
- [Introduction to Angular](#introduction-to-angular)
- [Getting Started](#getting-started)
- [Installation on Ubuntu](#installation-on-ubuntu)
- [Introduction to Routing](#introduction-to-routing)
- [Creating Components for Routing](#creating-components-for-routing)
- [Setting Up Basic Routing](#setting-up-basic-routing)
- [Summary](#summary)

## Introduction to Angular

Angular is a platform and framework for building single-page client applications using HTML and TypeScript. It's developed and maintained by Google and provides a comprehensive solution including:

- **Component-based architecture** — Think of components as building blocks for your app, like LEGO pieces that fit together
- **Robust templating system** — A powerful way to create dynamic HTML based on your data
- **Dependency injection** — A design pattern that makes your code more modular and easier to test
- **End-to-end tooling** — Tools that help you develop, test, and deploy your application
- **Integrated best practices** — Built-in solutions for common web development challenges

>  Angular is like a complete toolkit for building websites that feel more like apps. Unlike traditional websites where each page loads separately, Angular helps you create smooth experiences where only the necessary parts of the page update.

Angular emphasizes modularity, testability, and maintainability, making it a powerful choice for building complex web applications.

## Getting Started

Before diving into Angular, you should have a basic understanding of:
- **HTML, CSS, and JavaScript** — The fundamental building blocks of web development
- **TypeScript fundamentals** — A "superset" of JavaScript that adds type checking (don't worry, we'll explain as we go!)
- **Object-oriented programming concepts** — Basic understanding of classes and objects

>  If you're not familiar with TypeScript or object-oriented programming, don't worry too much. You can learn these concepts as you go, and we'll provide explanations for key concepts.

Angular applications are built using components, which are the basic building blocks. Each component consists of:
- A **TypeScript class** that defines behavior (what the component does)
- An **HTML template** that defines the UI (what the component looks like)
- **CSS styles** that define appearance (how the component is styled)

>  Think of a component like a custom HTML element that you create yourself. For example, you might create a "product-card" component that shows product information, and then reuse it throughout your application.

## Installation on Ubuntu

Follow these exact steps to set up Angular on Ubuntu:

### 1. Install Node.js and npm

>  Node.js is a JavaScript runtime that allows you to run JavaScript on your computer (not just in a browser). npm (Node Package Manager) helps you install and manage JavaScript libraries.

Angular requires Node.js version 14.x or higher and npm version 6.x or higher.

```bash
# Update package lists to make sure you're getting the latest versions
sudo apt update

# Install Node.js and npm
sudo apt install nodejs npm

# Verify installation by checking the versions
# This will show you which versions were installed
node --version
npm --version
```

### 2. Install Angular CLI and Update npm

>  Angular CLI (Command Line Interface) is a tool that helps you create, manage, and build Angular projects. It saves you a lot of time by automating common tasks.

Install the Angular CLI globally and update npm to the latest version:

```bash
# Install Angular CLI globally (making it available anywhere on your system)
sudo npm install -g @angular/cli

# Update npm to version 11.2.0
sudo npm install -g npm@11.2.0

# Verify Angular CLI installation
# This shows you have successfully installed Angular CLI
ng version
```

### 3. Create a New Angular Project

>  Here we're creating your first Angular project! The CLI will set up all the necessary files and configurations for you.

```bash
# Create a new project named "first-hello-world"
# This process might take a few minutes as it downloads and sets up everything
ng new first-hello-world

# Navigate to project directory
cd first-hello-world/

# Start the development server
# This will run your application on a local server
ng serve
```

After running `ng serve`, your application will be available at `http://localhost:4200/`. Open this URL in your browser to see your new Angular app running!

>  When you run `ng serve`, Angular starts a development server that "watches" your files. When you make changes to your code, the browser will automatically refresh to show your changes!

## Introduction to Routing

>  "Routing" is how we navigate between different pages or views in an Angular application without actually loading a new HTML page. It's what makes Angular apps feel fast and responsive.

Routing in Angular allows navigation between different components/views in your application without refreshing the entire page. This creates a more responsive, app-like user experience.

### Why Routing is Important

- **Single Page Application (SPA)**: Allows navigation without page reloads, making your app feel fast and smooth
- **Bookmarkable URLs**: Users can bookmark specific states/views of your application
- **Browser history support**: The back and forward buttons in the browser work as expected
- **Code organization**: Helps organize your application into logical sections or "pages"

>  Think of traditional websites where clicking a link causes the entire page to reload. In Angular, routing lets users move between different parts of your application immediately, without that reload delay - more like using a desktop app than a website.

## Creating Components for Routing

>  Before we set up routing, we need to create the components we'll navigate between. Think of these as different "pages" in your application.

For our basic routing example, we'll create three components: Home, About, and Contact.

```bash
# Create components using Angular CLI
ng generate component home
# "generate component" can be shortened to "g c"
ng g c about
ng g c contact
```

>  These commands tell Angular CLI to automatically create the files needed for new components. This saves you from having to create each file manually.

When you run these commands, Angular CLI will:
1. Create a new folder for each component under `src/app/`
2. Generate four files for each component:
   - `.html` template file (what the component looks like)
   - `.css` style file (how the component is styled)
   - `.ts` TypeScript class file (how the component behaves)
   - `.spec.ts` testing file (for testing the component)
3. Update the necessary module files to include these new components

For example, after running `ng g c home`, you'll have:
```
src/app/home/
├── home.component.html  (The HTML template)
├── home.component.css   (The component's styles)
├── home.component.ts    (The TypeScript code)
└── home.component.spec.ts (Testing file)
```

### Component Files Explained

Let's look at a typical component file structure:

**home.component.ts**:
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-home',  // This defines the HTML tag for this component: <app-home>
  templateUrl: './home.component.html',  // Points to the HTML template file
  styleUrls: ['./home.component.css']    // Points to the CSS file(s)
})
export class HomeComponent {
  title = 'Welcome to the Home Page';  // A property we can use in our template
}
```

>  This TypeScript file defines a class for our component. The `@Component` part is called a "decorator" and it provides Angular with metadata about the component. The `selector` is how you'll use this component in HTML, like `<app-home></app-home>`.

**home.component.html**:
```html
<div class="home-container">
  <h1>{{ title }}</h1>  <!-- This displays the value of the 'title' property from our TypeScript file -->
  <p>This is the home page of our Angular application.</p>
</div>
```

>  Notice the `{{ title }}` syntax? This is called "interpolation" and it's how Angular displays dynamic data from your TypeScript file in your HTML. The value will change if you change the `title` property in the TypeScript file.

## Setting Up Basic Routing

>  Now that we have our components, we need to set up routing so we can navigate between them. This involves several files, but don't worry—we'll go through each one!

### 1. Configure the Routes in app.routes.ts

>  This file defines which component should be displayed for each URL path.

Your project already has an `app.routes.ts` file rather than an app-routing.module.ts. Edit this file to define your routes:

```typescript
import { Routes } from '@angular/router';
import { HomeComponent } from './home/home.component';
import { AboutComponent } from './about/about.component';
import { ContactComponent } from './contact/contact.component';

export const routes: Routes = [
  // Redirect empty path to 'home'
  { path: '', redirectTo: 'home', pathMatch: 'full' },
  
  // When URL is '/home', show HomeComponent
  { path: 'home', component: HomeComponent },
  
  // When URL is '/about', show AboutComponent
  { path: 'about', component: AboutComponent },
  
  // When URL is '/contact', show ContactComponent
  { path: 'contact', component: ContactComponent },
  
  // Wildcard route - catches all other URLs and redirects to home
  // This is like a 404 page, but we're redirecting instead
  { path: '**', redirectTo: 'home' }
];
```

>  This file maps URLs to components. For example, when a user visits `/about`, Angular will display the `AboutComponent`. The empty path (`''`) redirects to the home page, and the wildcard path (`**`) catches any URLs that don't match our defined routes.

### 2. Update the App Component Template

>  The app component is the main component that contains everything else. We'll add navigation links and a special element called `router-outlet` that will display the currently active component.

Edit your `app.component.html` file to add the router outlet and navigation:

```html
<div class="container">
  <header>
    <h1>My Angular Application</h1>
    <nav>
      <ul>
        <!-- routerLink is Angular's way of creating links between routes -->
        <!-- routerLinkActive adds a CSS class when this route is active -->
        <li><a routerLink="/home" routerLinkActive="active">Home</a></li>
        <li><a routerLink="/about" routerLinkActive="active">About</a></li>
        <li><a routerLink="/contact" routerLinkActive="active">Contact</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <!-- router-outlet is where the component for the current route will be displayed -->
    <router-outlet></router-outlet>
  </main>

  <footer>
    <p>&copy; 2025 My Angular Application</p>
  </footer>
</div>
```

>  
> - `routerLink` is Angular's replacement for the regular `href` attribute. It navigates without reloading the page.
> - `routerLinkActive` adds a CSS class (in this case, "active") when that route is currently active.
> - `<router-outlet></router-outlet>` is a placeholder where Angular will insert the component that corresponds to the current URL.

### 3. Add Some Styling in app.component.css

>  This is just some basic CSS to make our application look nicer. The important part is the `.active` class, which will be applied to the active navigation link.

Edit your `app.component.css` file to add some basic styling:

```css
.container {
  max-width: 1200px;
  margin: 0 auto;  /* Centers the container */
  padding: 0 20px;
}

header {
  padding: 20px 0;
  border-bottom: 1px solid #eee;
}

nav ul {
  display: flex;  /* Makes the navigation horizontal */
  list-style: none;
  padding: 0;
}

nav li {
  margin-right: 20px;
}

nav a {
  text-decoration: none;
  color: #333;
  font-weight: bold;
}

/* This style is applied to the active route link */
nav a.active {
  color: #3f51b5;  /* Changes color when link is active */
}

main {
  padding: 20px 0;
  min-height: 400px;
}

footer {
  border-top: 1px solid #eee;
  padding: 20px 0;
  text-align: center;
}
```

### 4. Update the App Component TypeScript File

>  This file defines the main component class and imports everything we need. Notice the `imports` array—this is where we tell Angular about the components and directives we're using.

Ensure your `app.component.ts` file is properly set up:

```typescript
import { Component } from '@angular/core';
// Import the router directives we need
import { RouterOutlet, RouterLink, RouterLinkActive } from '@angular/router';
// Import our components
import { HomeComponent } from './home/home.component';
import { AboutComponent } from './about/about.component';
import { ContactComponent } from './contact/contact.component';

@Component({
  selector: 'app-root',  // This component will be used as <app-root> in index.html
  standalone: true,      // This is a "standalone" component (new in recent Angular versions)
  imports: [
    // Import the router directives
    RouterOutlet,        // Enables <router-outlet>
    RouterLink,          // Enables routerLink directive
    RouterLinkActive,    // Enables routerLinkActive directive
    // Import our components
    HomeComponent,
    AboutComponent,
    ContactComponent
  ],
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  title = 'first-hello-world';
}
```

>  In newer versions of Angular, components can be "standalone," which means they don't need to be part of a module. We need to explicitly import any directives or components we use in the template, which is what the `imports` array does.

### 5. Setup Main.ts File

>  This is the entry point for your Angular application. It bootstraps (starts up) the main component.

Make sure your `main.ts` file is properly configured to use the routes:

```typescript
import { bootstrapApplication } from '@angular/platform-browser';
import { appConfig } from './app/app.config';
import { AppComponent } from './app/app.component';

// Bootstrap the AppComponent with the configuration from appConfig
bootstrapApplication(AppComponent, appConfig)
  .catch((err) => console.error(err));
```

>  This file is the starting point of your application. It tells Angular to start your app with the `AppComponent` and apply the configuration from `appConfig`.

### 6. Create or Update App Config File

>  This configuration file is where we enable the router for our application.

You'll need to create or edit an `app.config.ts` file to provide the routes:

```typescript
import { ApplicationConfig } from '@angular/core';
import { provideRouter } from '@angular/router';
import { routes } from './app.routes';

export const appConfig: ApplicationConfig = {
  providers: [
    // This enables routing in our application using the routes we defined
    provideRouter(routes)
  ]
};
```

>  The `providers` array is where we configure services for our application. Here, we're providing the router service with our routes configuration.

## Understanding Key Routing Concepts

### Route Configuration

>  Let's break down the properties you can use when defining routes:

- **path**: The URL path for the route (what comes after the domain in the URL)
- **component**: The component to display for this route
- **redirectTo**: URL to redirect to (useful for default routes)
- **pathMatch**: How to match the URL 
  - 'full': The entire URL must match exactly
  - 'prefix': The URL should start with the path (default)
- **children**: Nested routes (for more complex applications)

### Router Directives

>  Angular provides several directives (special attributes) for working with routing:

- **routerLink**: Directive for navigation links (replacement for href)
- **routerLinkActive**: Adds a CSS class when the link's route is active
- **router-outlet**: Placeholder where the matched component will be displayed

### Navigation Methods

>  Besides links, you can navigate programmatically (from your TypeScript code):

```typescript
import { Router } from '@angular/router';

export class MyComponent {
  // Inject the Router service
  constructor(private router: Router) {}
  
  // Method to navigate programmatically
  navigateToAbout() {
    this.router.navigate(['/about']);
  }
}
```

>  This is useful when you want to navigate after some event (like form submission) or based on certain conditions.

## Summary

This guide has covered the essentials of getting started with Angular and implementing basic routing:

1. **Angular Installation**: We set up Angular on Ubuntu using the specific commands:
   ```
   sudo npm install -g @angular/cli
   sudo npm install -g npm@11.2.0
   ng version
   ng new first-hello-world
   cd first-hello-world/
   ```

2. **Component Creation**: Used Angular CLI's `ng generate component` command to create components for our routing example:
   ```
   ng g c home
   ng g c about
   ng g c contact
   ```

3. **Routing Implementation**: Configured routes using the existing file structure:
   - Defined routes in `app.routes.ts`
   - Used the `<router-outlet>` in `app.component.html` to display components
   - Created navigation links with `routerLink`
   - Handled redirects and 404 routes

>  Now you have a basic Angular application with multiple "pages" (components) and the ability to navigate between them without page reloads. This is the foundation of a Single Page Application!

By following this guide, you've created a basic Angular application with multiple routes that allows users to navigate between different views without page reloads, providing a smooth, app-like user experience.

To build on this foundation, you might explore:
- **Route parameters** for dynamic routes (like viewing specific products by ID)
- **Route guards** for controlling access (like protecting pages that require login)
- **Lazy loading** for better performance (loading components only when needed)
- **Nested routes** for complex UIs (like having sub-pages within a page)

>  Don't feel overwhelmed! Start with what we've covered here, and as you get comfortable, you can explore these more advanced concepts one by one.