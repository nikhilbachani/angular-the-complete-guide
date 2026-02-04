# Angular - The Complete Guide
- Code repository for Angular - The Complete Guide course on [Udemy](https://www.udemy.com/course/the-complete-guide-to-angular-2/)
- Instructor: Maximilian Schwarzmüller
  - [@maxedapps](https://x.com/maxedapps)
  - [maximilian-schwarzmueller.com](https://maximilian-schwarzmueller.com)
  - [academind.com](https://academind.com)

## Getting Started
### What is Angular?
- Platform with 2 things:
  1. **Front-end JavaScript framework** (helps in building interactive, modern web UIs)
  2. Collection of **tools & features** that come with the framework (*CLI, debugging tools, IDE plugins*)

### Why Angular?
- Frameworks like Angular shine when apps get *complex*
- Simplify process of building complex, interactive web UIs, reasons:
  1. Can write **declarative code** (compared to **vanilla JS** = **imperative**)
      - *Declarative*: define **target state(s)** (in **Angular-specific markup**) and how they change based on certain events, Angular figures out the rest, NO *manual DOM element manipulation*
      - *Imperative*: write step-by-step instructions to be executed by the browser
  2. Separation of concerns via **components**:
      - Custom HTML elements
      - Reusable
      - Combination of markup, styling, and logic
      - Allow breaking complex UIs into simpler parts
      - Reduce complexity of overall UI, simplifies development
      - Allow sharing components &amp; logic between team
  3. Embraces SOME **object-oriented programming** concepts, principles
      - **Dependency injection**, **classes**
      - Helps in building *complex, scalable* apps
  4. Easier development with **TypeScript (TS)**: Angular uses TS (*superset* of JS)
      - JS with **strict and strong typing**, prevents unexpected value type changes, easier to catch simple errors early
      - NOT an Angular feature, can be used independently
      - Better code quality &amp; lesser errors

### Angular Evolution &amp; Stability
- Keeps evolving, but *stable* and *backward-compatible*
- Angular 1 = **AngularJS**, totally different framework
- Angular = Angular 2+, total rewrite of *AngularJS*
  - First version (Angular 2) released in 2016
  - New major version released every 6 months ever since
  - Every version is backward-compatible (MOST Angular 2 code would *still* work today)
  - Companies might still use older versions of Angular, NOT always latest

#### Important Angular releases
- Angular 14 - introduced **Standalone Components**
- Angular 16 - introduced **Signals**
- Added as *optional features* for backward compatibility
  - Not available with older versions

### Creating an Angular project
- Can't just create an empty folder with HTML and JS files
- Building an Angular project requires features which don't work in the browser out-of-the-box:
  - Uses **non-standard HTML syntax**
  - Uses *TypeScript* -> does NOT directly work on the browser (needs *conversion* to JS)
- Need to create a project that comes with tools to **compile**/translate it to code that browser can run and be optimized
- For this, the Angular team created the **Angular CLI (Command-Line Interface)**
  - Tool to *simplify* process of creating Angular projects
  - Also used behind-the-scenes by these projects when we run **development testing server** or **build the app for production** to perform compilation and optimizations

#### Installing Angular CLI
- Needed to create and work on Angular projects
1. Install [Node.js](https://nodejs.org/en/download) **LTS-version**
    - **JS runtime** which allows running JS *outside the browser*
    - NOT needed to write Node.js code here (Angular is NOT a *Node.js framework*, it's a **browser-side framework**)
    - Angular CLI needs Node.js to work
    - Also, we need **NPM (Node Package Manager)** which comes with Node.js to execute commands and install Angular
2. [Install Angular CLI](https://angular.dev/tools/cli/setup-local) globally
    - On Terminal: `npm install -g @angular/cli`
3. Navigate to the folder where project should be created
    - `cd angular-projects`
4. Create the new Angular project
    - `ng new first-angular-app --no-zoneless`
    - `ng` command is available after Angular CLI is installed
    - `new` command is a command supported by `ng` to create a new Angular project
    - Project name CANNOT have whitespaces, convention to keep it all *lowercase* and words separated by dashes
    - Choose the following for the questions asked (depend on Angular version) or confirm default choices by just hitting `Enter`:
      - **Zoneless**: N (not presented in older versions)
      - **Stylesheet format**: CSS
      - **Server-Side Rendering (SSR) enabled**: N

### Setting up a Development Environment
1. Install [VS Code](https://code.visualstudio.com)
    - Free and highly extensible IDE
    - Works on all OS
2. Go to Extensions and search for "Angular"
    - Install **Angular Language Service**
      - Provides better IDE support for Angular
      - Helps with finding errors
      - Offers code completions
    - (Optional) Install **Angular Essentials**
      - *Bundles* multiple useful Angular-related extensions
3. Running the project and previewing output
    - Open **Integrated Terminal** (uses default system terminal/CMD) in VS Code (already navigated to the project folder by default to be able to run it)
    - Start **local development server** using `npm start`
    - Executes a script which is part of this project which spins up a dev server, allowing us to preview website by going to `http://localhost:4200`
    - Shows *auto-generated* starting app (proves that app was created correctly)
    - ***IMP***: While working on our code, we should keep the dev server running (DO NOT quit it)
      - Automatically **watches for changes** (rebuilds on save, and reloads)
    - When done, can close it using `Ctrl + C`
