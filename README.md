# Unity tool for AR.js
This tool is in it's early stages, but is meant to help the user to build an AR.js project using Unity to help make the 3D object placement a breeze. This project is by no means complete, and currently only supports adding basic shapes to the scene, changing the shapes' colors or textures, simple linear animations, and the ability to click an object to trigger an animation or open a webpage.

## Setup
Drop the main folder into the Assets folder within your Unity project, and make sure the name is "ARjs_Unity". Currently, the name and placement of the folder is important, or else it won't work. After this has been added to your project, download the [AR.js project from GitHub](https://github.com/jeromeetienne/AR.js). Take the "AR.js-master" folder and drop that into the Assets folder as well. Again, name and placement of the folder matters.

## Usage


### Changing the Image Target
There are two menu items for this. "AR.js/Image Target/1. Generate Image Target" and "AR.js/Image Target/2. Apply Generated Image". The first one will open up the website where you can go to generate both the image and the .patt file that you will need. The second one, should only be used after you already have an ImageTarget in scene. It will open another window where you will need drag and drop both the .patt file and the target image you created. Then hit update. If you don't alter anything before hitting update, it will reset the target to the default HIRO image target. 

### Adding Objects
Right click the Hierarchy to add an image target, then right click the image target to add a shape.

### Texturing Objects
You can right click in your assets to create a new material, and put a texture under its "albedo" option, or simply change the color of the material. Then you can drag and drop this material onto your object.

### Button Objects
Select the object in question that you want to make into a button. Then click the "AR.js" menu item, and select "Make Button." You can then change the URL that the button links to in the inspector when the object is selected.

### Animating Objects
Select the object that you want to animate, click the "AR.js" menu item, and select "Make Animation." This will add two scripts to the object. The one you will need to use for adding keyframes to your animation is the Custom List script [(that I modified from this original post)](https://forum.unity.com/threads/display-a-list-class-with-a-custom-editor-script.227847/). 

You can move your object anywhere and record that as a point (change the FrameTime to change when the object is supposed to get to that position). It will then be added to a list of keyframes. Note: you need to have at least one keyframe at time 0. After adding it to the list, each keyframe can be expanded and edited. If you want to check what that keyframe actually looks like, you can click "Set Transform from Frame," and it will set the transform of your object to what was recorded to that frame. If you move your object around a bit, and click "Update Transform" it will change the position, rotation, and scale for that keyframe to the objects current transform. You can change the time of the keyframe and it will be reordered in the list of keyframes to be chronological. After you have all your keyframes, Click "Export Animation." This will create a JSON file of all the keyframes you have made for the animation. If you then click the play button, you can see what your animation looks like.

There is a loop option, and a click option that you can enable. If checked, the "Loop Animation" option will cause the animation to loop. The "On Click" option will make the animation trigger upon your click (though only when you finally compile to HTML, and not when you click play in the Unity Editor).

### Compiling to HTML
Click the "AR.js" menu item, then click "Compile Files." This will create a file located in Assets>AR.js-master>aframe>{Active Scene Name}>index.html

This is the final file and can be opened in a browser to view the AR experience using the default "Hiro" marker provided from Jerome's AR.js GitHub. If you open it in FireFox, you don't have to worry about running it on a localhost server for it to work properly.

## How it Works
The CompileFile.cs script is where the majority of the work happens. It's just a lot of loops and conditional statements that goes through ever object attached to the ImageTarget in scene, and adds HTML text to a StringBuilder accordingly then saves the giant string as a file called index.html

The Animations could use simplified a fair bit. Currently, you create a KeyFrame list for the object and when you export it, it creates a file specific to the object in Assets>Animations>JsonExports. Then when you either run the scene in Unity, or compile the HTML file, it will read back in the KeyFrame list from the json text file. This is unecessary and will be changed in the future. As well as merging the Animation helper and Custom List scripts.

## Acknowledgments
A huge shout out to Jerome Etienne for enabling Augmented Reality through any web browser. [GitHub again](https://github.com/jeromeetienne/AR.js)

Thank you to ForceX for the [Custom List template](https://forum.unity.com/threads/display-a-list-class-with-a-custom-editor-script.227847/) I'm using to make the KeyFrame list easily editable.

Also thank you to Or-Aviram for his [Draw Field on condition](https://forum.unity.com/threads/draw-a-field-only-if-a-condition-is-met.448855/). Which I'm not actively using, but the code is added to my project and I anticipate that I will be using it eventually.

## Demonstration

[![Using AR.js Unity Converter](http://i.imgur.com/DiMMC4R.jpg)](https://youtu.be/PYs_Y1U2_DI)
