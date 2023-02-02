# Integrating Syncfusion Angular Components with Angular and Electron Applications

This document helps you to create a simple Angular application with `Electron Framework` and `Syncfusion Angular UI components`.

## Prerequisites

Before getting started with the Angular project, make sure you have the following installed on your machine,

* [System requirements for Syncfusion Angular UI components](https://ej2.syncfusion.com/angular/documentation/system-requirement)
* Electron CLI version - `^22.x.x` or later

If you do not have the `Electron CLI` installed, refer to the [`Electron package`](https://www.npmjs.com/package/electron-cli) for instructions on how to install it.

## Getting started with Syncfusion Angular component

Follow the [documentation](https://ej2.syncfusion.com/angular/documentation/getting-started/angular-cli) to create an Angular application that includes Syncfusion Angular components.

## Create main.js file

Create a `main.js` file in the root folder of the project and update the below code, This file will serve as an entry-point for Electron and it is responsible for creating windows and handling all the system events that might occur in the app.

```typescript
const { app, BrowserWindow } = require('electron');
let win;

function createWindow() {
  win = new BrowserWindow({ width: 800, height: 600 });

  // Load the Angular app in the browser window
  win.loadFile('./dist/sample15/index.html');

  win.on('closed', () => {
    win = null;
  });
}

app.on('ready', createWindow);

app.on('window-all-closed', () => {
  if (process.platform !== 'darwin') {
    app.quit();
  }
});

app.on('activate', () => {
  if (win === null) {
    createWindow();
  }
});

```

## Update index.html

In the `/src/index.html` file, change `<base href="/">` to `<base href="./">`, so that the Electron can able to find the Angular files.

## Update package.json

Go to your root directory and find the package.json file. Open its content and add the following,

```typescript
"main":"main.js",
"scripts": { 
    "ng": "ng", 
    "start": "ng serve", 
    "build": "ng build", 
    "test": "ng test", 
    "lint": "ng lint", 
    "e2e": "ng e2e", 
    "electron-build": "ng build --configuration=production",
    "electron": "electron ." 
}, 
```

## Running the application

Finally, run the following command line to start the application. The Syncfusion Essential JS 2 menu component will be rendered in the Electron framework.

 ```bash
npm  run electron-build 
 
npm  run electron 
```