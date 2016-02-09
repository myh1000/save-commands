# Save-commands package for Atom editor

This package allows you to define parametrized shell commands
to be automatically run, in sequence, whenever a file matching glob pattern is saved.  
This effectively eliminates the need for file watchers, and simplifies your build process.
You can define as many globs and commands as you want.
The command(s) and their output will be displayed in a panel at the bottom of the screen. Hit 'Esc' to dismiss the panel.

Right click on a tree view file and select "Run batch save-commands" to run all commands mapped to this file. Selecting a folder will run proper run commands on all files contained in it (recursively).

### How to use

Create save-commands.json file in your project's root folder
Create one entry for each command you wish to run, and assign it to a glob like this:  
glob : command {parameter}

Here is an example of save-commands.json file
```
{
	"commands": [
		"*.coffee : coffee -c {relFullPath}",
		"src/**/*.coffee : coffee -c -o dist{relPathNoRoot} {relFullPath}",
		"src/**/client/**/*.coffee : gulp browserify",
		"src/client/**/*.jade   : jade -P {relPath}{filename} -o dist{relPathNoRoot}",
		"src/client/**/*.jade   : gulp createTemplateCache",
		"src/server/**/*.jade : copy {relPath}{filename} dist{relPathNoRoot}",
		"src/**/*.styl   : gulp compileStylus",
		"src/**/*-spec.coffee : mocha src{relPathNoRoot}{name}.coffee --compilers coffee:coffee-script/register",
		"src/**/*.coffee : gulp runSpec --file=src{relPathNoRoot}{name}-spec.coffee --require coffee-script/register --compilers coffee:coffee-script/register"
	]
}
```
You can add "cwd" property to define custom working directory. By default, it is your project root.
If you get errors when saving a file, double check your save-commands.json file to make sure it is formatted properly.

### Available parameters:  
- absPath: absolute path of the saved file (without file name)  
- relPath: relative path of the saved file (without file name)  
- relFullPath: like relPath but with filename
- relPathNoRoot: relative path without top folder  
- filename: file name and extension  
- name: file name without extension  
- ext: file extension  
- sep: os specific path separator

## Related packages

### [Make coffee](https://github.com/JsonHunt/make-coffee)

Great tool when you are migrating a project from JavaScript to CoffeeScript. Adds an option 'Make me a coffee' to .js files in tree-view.
