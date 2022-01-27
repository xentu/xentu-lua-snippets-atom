Xentu Lua Snippets for Atom
======

This extension provides code snippets for the Xentu game engine for use in Atom.
Supports keywords, properties, functions, and also constants for things like Keyboard & Mouse.

Some features are not yet added, such as class properties and functions, these will be provided soon. For now now refer to the documentation if you get stuck, found at https://docs.xentu.net

This package is part of the Xentu game engine project: https://xentu.net

```
```

Running a Xentu game from Atom
----

If you have the Xentu SDK installed, you can enhance your coding experience by
adding a few shortcuts to your Atom editor. Here is a script that can be added
under *File -> Init Script...* that allows you to launch a game from within the
editor:

```coffeescript
# adds a function to allow running a Xentu game within Atom.
spawn = require('child_process').spawn
atom.commands.add 'atom-text-editor', 'xentu-play', ->
	file = atom.workspace.getActiveTextEditor().getPath()
	dir = atom.project.getDirectoryForProjectPath(file).path
	proc = spawn('xentusdk', ['play'], { cwd: dir })
	proc.stdout.on "data", (uint8array) ->
		data = new TextDecoder().decode(uint8array)
		console.log data
	proc.stdout.on "close", () ->
		console.log "Game Ended"
```

Once you've added the code above, restart Atom, then when you are editing your `game.lua` file, use `CTRL+SHIFT+P` and type "Xentu Play" to launch your game. Optionally also use `CTRL+SHIFT+I` to show the Atom developer console also before running the play command to see the console output.

Happy coding!