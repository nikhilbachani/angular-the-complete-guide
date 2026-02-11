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
    - `main.ts` is compiled to JS by Angular CLI and then run (since TS can't run directly in the browser)
- `main.ts` executes the `bootstrapApplication()` function provided by the Angular package
  - This function wants an Angular component (`AppComponent`)
  - ***IMP***: It then takes that component and looks for it in the `index.html` and tries to replace the **tag** for that custom component with the markup defined by that component
    - Currently, it is the `AppComponent` which is coming (**imported**) from `./app/app.component` file
    - If we follow that path, we end up on `app.component.ts`
    - ***IMP***: The `.ts` is missing from the import path since for TS files, we should OMIT the file extension
- `app.component.ts` has a **class** (*feature of modern JS*, NOT TS-specific) called `AppComponent`
  - This class in Angular creates such a custom HTML element
  - It does that because it's not just a class, it also has an `@Component` **decorator** (*TS feature*) above it which adds **metadata** to what it is attached to (the class)
  - ***IMP***: Angular uses *decorators* to add metadata
- The `@Component` decorator comes from the `@angular/core` package in the Angular framework
  - This decorator converts a standard class into an Angular component (treated as a custom HTML element by Angular)
  - This decorator receives an object (`{}`) with some configuration for the component
    1. `selector` property: tells Angular which **element/tag** it should look at in the HTML code to be replaced by this component and its *markup*
    2. `templateUrl` property: external file that stores the markup (**template**) of this component, every component has markup
    3. `styleUrl` property: path to external file that stores styles **specific** to this component, ONLY apply to this component's markup
