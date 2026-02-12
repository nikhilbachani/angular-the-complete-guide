# Angular Essentials
## Concepts Covered
- Understanding Angular Project Structure
- Working with Components
- Handling User Events
- Rendering & Updating Dynamic UI Content

## Starting Project
- [Link](https://github.com/mschwarzmueller/angular-complete-guide-course-resources/blob/main/attachments/02-essentials/01-starting-project.zip)
- Created with Angular CLI
- Comes with a bunch of *config files* and an `src/` folder with more files &amp; folders
- *NOTE*: Depending on CLI version, *new* projects might contain a `public/` folder with a `favicon.ico`
- This project does NOT have a `public/` folder (`favicon.ico` file is in the `src/` folder)
  - This and other small differences exist because different CLI versions create different starting projects
  - Angular code we write will be the same

### Analyzing the Project Structure
- *Root-level* files = all **configuration files**
  1. Some **TypeScript config**:
      - **tsconfig.app.json**, **tsconfig.json**, **tsconfig.spec.json**
      - These files control:
        - compilation of *TS -> JS* (triggered **automatically** by CLI) under the hood by Angular CLI
        - TS *strictness* (how quickly TS complains about *potential errors*)
      - ***IMP***: NO need to change in MOST cases
  2. **package.json** and **package-lock.json**
      - Manage *dependencies* for our app
      - Contain `@angular` dependencies to be able to use features from these packages in code
  3. **angular.json**
      - Extra config settings for Angular CLI and Angular-provided tools
      - ***IMP***: NO need to change in MOST cases
  4. **.editorconfig**
      - Rules (formatting, etc.) for the code editor
  5. **.gitignore**
      - Relevant if using **Git** for *version control*
- ***IMP***: `src/` folder
  - Has `app/` folder where we store our Angular **component code**
    - Depending on Angular CLI version used for project creation, files may be named differently
    - Ex:`app.ts` (newer, default since Angular 20) vs. `app.component.ts` (older, Angular 2+, default up until Angular 20)
    - We can name our code files whatever we want, does NOT affect code or behavior of Angular
  - Bunch of other files &amp; folders:
    - **styles.css**: Sets up **global styles** (apply to entire web app across ALL components)
    - **index.html**: **Main HTML file** loaded when visitors come to our website
    - **main.ts**: **First** code file to be executed when our Angular app loads up in the browser
    - **assets/**: Can be used to store images (like a *logo*) to use in the website

### Running the Starting Project
1. Errors are shown in `main.ts` since the project has NOT installed the dependencies in **package.json**
2. Run `npm install` in the terminal after downloading the project
    - Installs all dependencies in **package.json**
    - Only need to do this ONCE, not every time we work on the project
    - Ignore warnings if there are NO errors
3. Start dev server to preview app
    - `npm start`
    - Uses `ng serve` (uses Angular CLI) *internally*
    - Visit address in browser to verify app is working

## Understanding Components &amp; How Content ends up on the Screen
- `index.html` (in `src/`) is loaded by the browser when visitors visit the website
  - This file is almost empty
  - `<body>` element contains only 1 HTML element (`<app-root>`)
  - This `<app-root>` is NOT a *standard* HTML element
    - The browser on its own cannot understand this element
    - ***IMP***: This is where Angular comes in (code in `main.ts` is run when website loads up)
    - However, in `index.html` there are no JS imports (`<script>`)
    - But, if we visit the loaded website and click `View Page Source`, we can see the `<script>` tags **injected** automatically by the Angular CLI when we build and run the app
    - `main.ts` is compiled to JS (`main.js`) by Angular CLI and then run (since TS can't run directly in the browser)
- `main.ts` executes the `bootstrapApplication()` function provided by the Angular package
  - This function wants an Angular component (`AppComponent`)
  - ***IMP***: It then takes that component and looks for it in the `index.html` and tries to replace the **element tag** for that custom component with the markup defined by that component
    - Currently, it is the `AppComponent` which is coming (**imported**) from `./app/app.component` file
    - If we follow that path, we end up on `app.component.ts`
    - ***IMP***: The `.ts` is missing from the import path since for TS files, we should OMIT the file extension
- `app.component.ts` has a **class** (* standard feature of modern JS*, NOT TS-specific) called `AppComponent`
  - This class in Angular creates such a component/custom HTML element
  - It does that because it's not just a class, it also has an `@Component` **decorator** (*TS feature*) above it which adds **metadata** to what it is attached to (the class)
  - ***IMP***: Angular uses *decorators* to add metadata
- The `@Component` decorator comes from the `@angular/core` package in the Angular framework
  - ***IMP***: This decorator converts a standard class into an Angular component (treated as a custom HTML element by Angular)
  - This decorator receives an object (`{}`) with some configuration for the component
    1. `selector` property: tells Angular which **element/tag** it should look at in the HTML code to be replaced by this component and its *markup*
    2. `templateUrl` property: external file that stores the markup (**template**) of this component, every component has template/markup
    3. `styleUrl` property: path to external file that stores styles **specific** to this component, ONLY apply to this component's markup

## Creating our First Custom Component
- In the [finished demo app](https://github.com/mschwarzmueller/angular-complete-guide-course-resources/tree/main/attachments/02-essentials):
  - We can split the page into *multiple UI blocks* or *separate HTML elements*:
    1. Header
    2. Sidebar with every tab can be a separate HTML element
    3. Main area
    4. "Add Task" dialog
  - So we have multiple building blocks that make up the overall UI
  - ***IMP***: When working with Angular, we build those building blocks as individual **components** and then compose them together to get the overall UI

### Building the Header component
- We already have the `AppComponent` (main component of this app)
  - This component is made up of **3 files** which work together (standard in Angular, components are created as separate multiple files working together)
- Add new file for header component: `header.component.ts` (or `header.ts` for Angular 20+)
  - *REM*: This is ONLY a *recommended convention*, we can name the component anything we want
  - By convention, name SHOULD start with something that identifies/describes the component (ex: `header`)
  - Followed by a dot (`.`), followed by what will be stored in the file (a `component` here), followed by the file extension (`.ts`) since we are using TS (builds on top of JS)
- In `header.component.ts`:
  1. We need a class since components are just classes enhanced by the `@Component` decorator
      - ***IMP***: The class MUST be **exported** (`export` keyword) so that it can be used in other files as well
      - Name of the class by convention will be `HeaderComponent` (starts with identifier followed by the type/what it is)
      - Followed by `{}` to define **class body** (empty for now)
  2. To convert this class to a component, we need to import the `Component` decorator from the Angular framework's `core` package
  3. Add the decorator `@Component` followed by parentheses (`()`)

## Configuring the Custom Component
- Between the `()`, we pass the configuration for the component:
  1. `selector` (to select elements, REQUIRED) to tell Angular which elements on the screen will be *replaced* by this component
      - ***Convention***: Select elements by a tag that consists at least 2 words separated by a `-`, ex: `app-header`
      - ***Reason***: Using just 1 word could clash with built -in HTML elements (ex: `<header>`)
        - Using `header` would override the default `header` element in HTML
      - The **prefix** `app` is just common choice, we could use whatever
  2. `template` (REQUIRED if not using `templateUrl`) defines **markup**/content which should be displayed by that component
      - Could be defined in-line as a string by writing the markup in quotes (ex: `'<h1>Hello World</h1>'`)
      - But, this is NOT recommended, ONLY use for very simple (2-3 lines) HTML code
      - In general, recommended to use `templateUrl` property to point to an **external HTML file**
      - `templateUrl` needs to contain a string defining the **relative path** (relative from this TS file) for the file containing markup (HTML) for this component
      - Create `header.component.html` (convention to use same name as TS file, but change extension to `.html`)
      - Now relative path will be `./header.component.html` (same folder as TS file)
  3. Add simple markup in `header.component.html`
  4. Add `standalone` property: marks the component as a **standalone component** (set to `true`, *recommended*)
      - ***IMP***: Depending on Angular version, this might be set to `true` *automatically* (Angular 19+), can be omitted in such a case
      - ***IMP***: For Angular <19, default will be `false` (creates a **module-based component**) which we do NOT want (set to `true` is the modern way of building Angular components)
      - ***IMP***: Standalone components are EASIER to use and tie together
