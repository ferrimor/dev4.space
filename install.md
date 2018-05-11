# Create a new project
1. `$ mkdir prjname`
1. `cd` into the new directory
1. Initialize NPM: `$ npm init --yes`
1. Install gulp and gulp-sass packages: `$ npm install -D gulp gulp-sass browser-sync`
1. Update `package.json`'s `scripts` section with this key-value pair: `"scripts": { "dev": "gulp" }`
1. Recreate this file structure in this directory:
  - `public` (directory)
    - `css` (directory)
    - `index.html` (file)
  - `scss` (directory)
    - `partials` (directory)
    - `styles.scss` (file)
  - `gulpfile.js` (file)
  - `package.json` (created by `npm init --yes`)
6. Add the following code into the `gulpfile.js` file:

  ```javascript
  var gulp        = require('gulp');
  var browserSync = require('browser-sync').create();
  var sass        = require('gulp-sass');

  // Static Server + watching scss/html files
  gulp.task('serve', function() {
  
    browserSync.init({
        server: "./public"
    });
  
    gulp.watch("scss/**/*.scss", ['sass']);
    gulp.watch("public/*.html").on('change', browserSync.reload);
  });

  // Compile sass into CSS & auto-inject into browsers
  gulp.task('sass', function() {
    return gulp.src("scss/styles.scss")
      .pipe(sass().on('error', sass.logError))
      .pipe(gulp.dest("public/css"))
      .pipe(browserSync.stream());
  });
  
  gulp.task('default', ['sass', 'serve']);
  ```
7. Add the following code into the file located at `scss/styles.scss`:
  ```css
  body {
    background-color: red;
    
    h1 {
      color: purple;
    }
  }
  ```
  
  note: this is just a test, dont ever actually nest starting with `body` element. 😬
1. Add the following code into the `public/index.html` file:

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Sass Gulp Workshop</title>
    <link rel="stylesheet" href="/css/styles.css">
  </head>
  <body>
    <h1>Hello Syntatically Awesome Style Sheets!</h1>
  </body>
  </html>
  ```

1. start developing with the command: `npm run dev`
