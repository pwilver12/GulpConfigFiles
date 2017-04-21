# GulpConfigFiles
A utility repo for initializing a new git repository equipped with Gulp, built in and compatible with ES6 (thanks to [Mark Goodyear's helpful writeup](https://markgoodyear.com/2015/06/using-es6-with-gulp/))!

### 1. Create a home for this repository
At your user root directory `~/` make sure you have a `/github` directory.

```
$ cd ~ # Change directories to your user root
$ mkdir github && cd github # Create the github directory and go to it
```

Create an `/apps` directory there and clone this repo.

```
$ mkdir apps && cd apps
$ git clone git@github.com:pwilver12/GulpConfigFiles.git
```

_**NOTE:** You can alternatively place this cloned repo on your machine in any location you'd like. If so, ensure that you update the file paths in step #2 accordingly (specifically, for the initial pull from this repo and the file copy `cp` lines)._

### 2. Update your bash or `.zshrc` profile
Let's update your `~/.bash_profile` or `~/.zshrc` file with a nifty `project_init` function, used in a new project directory to create the necessary directories and files to get you started. If you are using [zsh](https://wiki.archlinux.org/index.php/zsh) and `~/.zshrc` does not yet exist in your root, you will need to create one.

(If you don't know what `zsh` is, we're probably working with a `.bash_profile`.)

Open `~/.bash_profile` or `~/.zshrc` in your favorite text editor and add this function:

```
project_init() {
  echo "#### 1. Pulling down the most recent config files."
  cd ~/github/apps/GulpConfigFiles
  git pull origin master
  echo "#### 2. Switching back to the new project"
  cd -
  echo "#### 3. Creating project directories and files"
  mkdir src src/js src/js/modules src/sass src/sass/partials src/views src/views/pages src/views/partials build build/js build/css build/html
  touch src/js/index.js src/sass/styles.sass src/views/pages/index.ejs
  cp -r ~/github/apps/GulpConfigFiles/.eslintignore .
  cp -r ~/github/apps/GulpConfigFiles/.eslintrc .
  cp -r ~/github/apps/GulpConfigFiles/.gitignore .
  cp -r ~/github/apps/GulpConfigFiles/.babelrc .
  cp -r ~/github/apps/GulpConfigFiles/package.json .
  cp -r ~/github/apps/GulpConfigFiles/gulpfile.babel.js .
  echo "#### 4. Deleting some extra stuff"
  rm -rf node_modules
  echo "#### 5. Don't forget to npm install!"
}
```

Save and open up your command line (or reload your profile if your terminal is already open: `source ~/.bash_profile` or `source ~/.zshrc`).

### 3. Start your project
Navigate to an existing project directory, or create a new one. Call `project_init` and get to work!

```
$ cd new-project OR mkdir new-project && cd new-project
$ project_init
$ npm install
```
Always remember to `npm install` once the init script has completed. This will ensure that your `gulpfile.babel.js` works as expected.

### 4. Gulp...
At this point, you shouldn't need to do anything more than call `gulp` in the command line. This will kick off the build processes for your `sass`, `js` and `ejs` assets.

### 5. ESlint goodness..
I've added support for `eslint`, a command line utility to check the validity and integrity of your JavaScript code (supports both ES5 and ES6 formats). A prerequisite is that you have the following libraries installed globally (no way around this for now):

```
npm install -g eslint eslint-plugin-jsx-a11y eslint-config-airbnb eslint-plugin-import eslint-plugin-react
```
