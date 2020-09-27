# Page Builder

## Description

This is project based on Vue.js and does not contain additional libraries as it is quite simple to implement all of the functional on its own.
The `CHALLENGE.md` file contains a duplicate description of the task, each task has a status of execution or recommendation use.

## Description of the structure

This project has a typical structure adopted in the Vue.js community.
The project is located in the `SRC` folder.

- `App.js` - the main component as a wrapper of application
- `views` - root views of the project
- `layouts` - layout-component for views, they can be used without `import`
- `ui` - UI-components, which are globally in the project, they can be used without `import`
- `components` - all shared components of the project
- `styles` - `SCSS`-files
- `libs` - exported functions to preserve DIY ideology
- `assets` - static files, which can be used as part of a project
- `public` (outside of the `src` folder) - static files, which can be used as is

## Project setup
```
npm install
```

#### Compiles and hot-reloads for development:
```
npm run serve
```
This is the fastest way to run a project on a development computer.
http://localhost:5200/ - link for opening this project in a browser after start the command.

#### Compiles and minifies for production:
```
npm run build
```

#### Lints and fixes files:
```
npm run lint
```
