# Angular Essentials

## Starting Project
- [Link](https://github.com/mschwarzmueller/angular-complete-guide-course-resources/blob/main/attachments/02-essentials/01-starting-project.zip)
- Created with Angular CLI
- Comes with a bunch of config files and an `src/` folder with more files &amp; folders
- Depending on CLI version, *new* projects might contain a `public/` folder with a `favicon.ico`
- This project does NOT have a `public/` folder (`favicon.ico` file is in the `src/` folder)
  - This and other small differences exist because different CLI versions create different starting projects

### Analyzing the Project Structure
- Root-level files = all **configuration files**
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
      - Rules (formatting, etc.) for the code edditor
  5. **.gitignore**
      - Relevant if using **Git** for *version control*
- ***IMP***: `src/` folder
  - Has `app/` folder where we store our **component code**
    - Depending on Angular CLI version used for project creation, files may be named differently
    - Ex:`app.ts` (newer, default since Angular 20)) vs. `app.component.ts` (older, Angular 2+, default up until Angular 20)
    - Can name our code files whatever we want, does NOT affect code or behavior of Angular
  - Bunch of other files &amp; folders:
    - **styles.css**: Sets up **global styles** (apply to entire web app across ALL components)
    - **index.html**: Main HTML file loaded when visitors come to our website
    - **main.ts**: **First** code file to be executed when our Angular app loads up in the browser
    - **assets/**: Can be used to store images to use in the website

### Running the Starting Project
1. Errors are shown since the project has NOT installed the dependencies in **package.json**
2. Run `npm install` in the terminal after downloading the project
    - Installs all dependencies in **package.json**
    - Only need to do this ONCE, not every time we work on the project
    - Ignore warnings if there are NO errors
3. Start dev server to preview app
    - `npm start`
    - Uses `ng serve` (uses Angular CLI) *internally*
    - Visit address in browser to verify app is working

## Understanding Components
- `index.html` (in `src/`) is loaded by the browser when visitors visit the website
  - This file is almost empty
  - `<body>` element contains only 1 HTML element (`<app-root>`)
  - This `<app-root>` is NOT a standard HTML element
    - The browser on its own cannot understand this element
    - This is where Angular comes in (code in `main.ts` is run when website loads up)
  - However, in `index.html` there are no JS imports (`<script>`)
  - If we visit the loaded website and click `View Page Source`, we can see the `<script>` tags injected by the Ang uar CLI