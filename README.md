# CS-Engine
The engine for building 2D games

> Please no pull requests/forks on this project. This is a personal project of mine. Not made to compete with other game development solutions. Meant as read-only

# What's included

    cs-engine/
    ├── engine/
    │   ├── style.css
    │   ├── script.js
    │   └── template.html
    └── example/
        ├── bird
        ├── cube
        └── warrior

# Setup
The engine only requires the CSS and Javascript file. Here is a template for a basic project

    <!DOCTYPE html>
    <html>
        <head>
            <!-- Title/Meta Setup -->
            <title>cs-engine</title>
            <meta name="viewport" content="width=device-width, height=device-height, initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0, user-scalable=no, shrink-to-fit=no">

            <!-- Game Engine -->
            <link rel="stylesheet" type="text/css" href="/engine/css.css" />
            <script src='/engine/scr_core.js'></script>

            <!-- Objects -->
            <script src='objects/obj_player.js'></script>

            <!-- Scripts -->
            <script src='scripts/scr_player.js'></script>
         </head>
         <body>
            <!--Game Area-->
            <div id="view"></div>
            <script>
               cs.init({
                  canvas: 'cs-view',
                  sprites: [
                     { location: 'sprites/spr_player' }
                  ],
                  loaded: function(){
                     //Camera Settings
                     cs.camera.setup({
                        width:144,
                        height:256,
                        maxWidth:300,
                        maxHeight:200,
                        lock: true
                        })
                        //Room Setup
                        cs.room.setup(800, 256)

                        cs.room.start = function(){
                           //Create Objects
                           cs.obj.create({ type: 'obj_player', attr: { 50, 50 }})
                        }
                    }
                })
            </script>
         </body>
      </html>

# Loading Sprites
Load a sprite using `cs.sprite.load`

      cs.sprite.load([Object: options])

      //Example options none are required!
      options = {
         path: [Required String: path to file]
         name: [Optional String (File Name): Override the filename and set sprite name]
         frames: [Optional Number (1): How many frames in the sprite sheet],
         width: [Optional Number (IMG Width): The width of a frame],
         height: [Optional Number (IMG Height): The width of a frame],
         xoff: [Optional Number (0): The horizontal offset when drawing],
         yoff: [Optional Number (0): The vertical offset when drawing]
      }

# Loading Objects
Use a `.js` file include it in your `index.html`

    <script src="cscript/_objects/obj_something.js"></script>

Inside the new JS file you can create the object by using:

    cs.objects['obj_name'] = {
        create: [required Function: run this when we create the object]
        step: [required Function: run this each every frame of the game]
    }

To create the object use `cs.obj.create()`

    cs.obj.create({
        type: [required String: object type],
        x: [optional Number (0): x position to create the object],
        y: [optional Number (0): y position to create the object]
    })

# Drawing Functions
CS Engine has functions for drawing sprites, shapes, and text.

### Sprites:
Draw sprites using `cs.draw.sprite`

    cs.draw.sprite({
        spr: [Required String: The name of the sprite],
        x: [Required Number: The x position],
        y: [Required Number: the y position],
        width: [Optional Number (Frame Width): The width to draw the sprite],
        height: [Optional Number (Frame Height): The height to draw the sprite],
        scaleX: [Optional Number (1): Horizontal scaling],
        scaleY: [Optional Number (1): Vertical scaling]
    })

### Text:

    cs.draw.text({
        x: [Required Number: x position],
        y: [Required Number: y position],
        text: [Required String: The text to draw]
    })


### Shapes:

    //Rectangle
    cs.draw.fillRect({
        x: [Required Number: x position to start drawing],
        y: [Required Number: y position to start drawing],
        width: [Required Number: width of the drawing],
        height: [Required Number: height of the drawing],
    })

    cs.draw.strokeRect({
        x: [Required Number: x position to start drawing],
        y: [Required Number: y position to start drawing],
        width: [Required Number: width of the drawing],
        height: [Required Number: height of the drawing],
    })

    //Line
    cs.draw.line({
      x1: [Required Number: coordinate 1 x position],
      y1: [Required Number: coordinate 1 y position],
      x2: [Required Number: coordinate 2 x position],
      y2: [Required Number: coordinate 2 y position]
    })

### Draw Settings

    cs.draw.settings({
        alpha: [Optional Number (1): 0 being invisible 1 being fully visible],
        width: [Optional Number (1): line width for stroke functions],
        font: [Optional String ('12px Arial'): Font setting],
        color: [Optional String ('#000'): Hex value of color,
        textAlign: [Optional String ('start'): start/middle/end horizontal align,
        textBaseline: [Optional String ('top'):  top/bottom/middle/baseline vertical align,
        lineHeight: [Optional Number (10): line height spacing,
        operation: [Optional String ('source-over'): set canvas manual on draw operations
    })

Note: The draw settings are reset after any drawing event! They are layer specific and the layer resets after each draw event. You should use these right before your drawing event

# The Game Camera
The game camera is the area the game and GUI is drawn to. The GUI and Game are drawn to hidden canvases separately then drawn to the view/camera canvas. There are a couple settings that can be tweeked to change the view.

The maxWidth and maxHeight set the maximum literal pixel size of the canvas. The engine will then try to get the closest aspect ratio to the size you set. Then it will be stretched with CSS to make fill the entire screen.


    maxWidth : 500
    maxHeight : 400
