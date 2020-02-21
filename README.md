# touchdesigner


## navigation

This is a basic example of how to navigate through video clips.  I'm still getting used to how to control state and data flow in TouchDesigner, so a lot of my solutions are very 'manual' using python.  I'm also working with JSON-style objects because that is what I'm used to doing at work and in other projects.  This file consists of three main components: data storage, keypress handling, and video output.

### data storage

I'm storing information about the video clips in a Table DAT that I'm using as a very basic SQL table.  Each row contains information about a different video clip, including a name, clip i.e. where to find the file (which is specific to my computer and username, will have to be edited to work correctly), and parent, which is the row number of the previous clip in the sequence.  I've structured this demo so it starts off with a dog and a cat clip, and selecting the dog will lead to more dog clips, and selecting the cat will lead to more cat clips.

The tabletojson container outputs a nested JSON structure, starting with the beginning clips (those that have no parents).  Pressing R on the keyboard will populate the Out DAT.

### keypress handling

I'm using a KeyboardIn DAT to simulate the sensors at the moment.  When you press a key, the callback DAT writes the key value to a Table DAT with just one cell.  Every time that cell changes, it triggers an Execute DAT that reads the information from the tabletojson container.  The Execute DAT only takes action if the keys 1, 2, or 3 are pressed.  Depending on the key pressed, it will set the File parameters of the moviefilein1 and moviefiledin2 TOPs.  If you press 3, it should reset the videos to the first two (dog & cat).  Thereafter, 1 selects the first video clip, and 2 selects the second video clip.  It then reads through all the choices, and finds the next set of video clips.


### video output

At the moment, I'm only outputting two video clips to make it simpler to test with.  I'm using a Layout TOP to place the clips side-by-side, but depending on the size / positioning of the clips another TOP might be preferable.  This currently ignores the fact that we will be using separate video device outputs.
