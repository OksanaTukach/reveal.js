## Canvas
canvas is an HTML element which can be used to draw graphics via scripting (usually JavaScript). This can, for instance, be used to draw graphs, combine photos, or create simple (and not so simple) animations. 
The default size of the canvas is 300 pixels × 150 pixels (width × height). But custom sizes can be defined using the HTML height and width property. 
### Basic usage of canvas
The canvas is initially blank. To display something, a script first needs to access the rendering context and draw on it. The canvas element has a method called getContext(), used to obtain the rendering context and its drawing functions. getContext() takes one parameter, the type of context. For 2D graphics, such as those covered by this tutorial, you specify "2d" to get a CanvasRenderingContext2D.
The first line in the script retrieves the node in the DOM representing the canvas element by calling the document.getElementById() method. Once you have the element node, you can access the drawing context using its getContext() method.
## Drawing shapes with canvas
### The Grid
Normally 1 unit in the grid corresponds to 1 pixel on the canvas. The origin of this grid is positioned in the top left corner at coordinate (0,0). All elements are placed relative to this origin. So the position of the top left corner of the blue square becomes x pixels from the left and y pixels from the top, at coordinate (x,y). 
### Drawing rectangles
canvasonly supports two primitive shapes: rectangles and paths (lists of points connected by lines). 
There are three functions that draw rectangles on the canvas:
fillRect(x, y, width, height)
Draws a filled rectangle.
strokeRect(x, y, width, height)
Draws a rectangular outline.
clearRect(x, y, width, height)
Clears the specified rectangular area, making it fully transparent.
The fillRect() function draws a large black square 100 pixels on each side. The clearRect() function then erases a 60x60 pixel square from the center, and then strokeRect() is called to create a rectangular outline 50x50 pixels within the cleared square.
### Drawing Paths
To make shapes using paths, we take some extra steps:
1.	First, you create the path.
2.	Then you use drawing commands to draw into the path.
3.	Once the path has been created, you can stroke or fill the path to render it.

Here are the functions used to perform these steps:
beginPath()
Creates a new path. Once created, future drawing commands are directed into the path and used to build the path up.
Path methods
Methods to set different paths for objects.
closePath()
Adds a straight line to the path, going to the start of the current sub-path.
stroke()
Draws the shape by stroking its outline.
fill()
Draws a solid shape by filling the path's content area.
One very useful function, which doesn't actually draw anything but becomes part of the path list described above, is the moveTo() function. You can probably best think of this as lifting a pen or pencil from one spot on a piece of paper and placing it on the next.
moveTo(x, y)
For drawing straight lines, use the lineTo() method.
lineTo(x, y)
Draws a line from the current drawing position to the position specified by x and y.
To draw arcs or circles, we use the arc() or arcTo() methods.
arc(x, y, radius, startAngle, endAngle, anticlockwise)
Draws an arc which is centered at (x, y) position with radius r starting at startAngle and ending at endAngle going in the given direction indicated by anticlockwise (defaulting to clockwise).
arcTo(x1, y1, x2, y2, radius)
Draws an arc with the given control points and radius, connected to the previous point by a straight line.
Using images
## Importing images into a canvas is basically a two step process:
1.	Get a reference to an HTMLImageElement object or to another canvas element as a source. It is also possible to use images by providing a URL.
2.	Draw the image on the canvas using the drawImage() function.

The canvas API is able to use any of the following data types as an image source:
HTMLImageElement
These are images created using the Image() constructor, as well as any img element.
SVGImageElement
These are images embedded using the image element.
HTMLVideoElement
Using an HTML video element as your image source grabs the current frame from the video and uses it as an image.
HTMLCanvasElement
You can use another canvas element as your image source.
These sources are collectively referred to by the type CanvasImageSource.
## Transformations
The first of the transformation methods we'll look at is translate(). This method is used to move the canvas and its origin to a different point in the grid.
translate(x, y)
Moves the canvas and its origin on the grid. x indicates the horizontal distance to move, and y indicates how far to move the grid vertically.
The second transformation method is rotate(). We use it to rotate the canvas around the current origin.
rotate(angle)
Rotates the canvas clockwise around the current origin by the angle number of radians.
The rotation center point is always the canvas origin. To change the center point, we will need to move the canvas by using the translate() method.
The next transformation method is scaling. We use it to increase or decrease the units in our canvas grid. This can be used to draw scaled down or enlarged shapes and bitmaps.
scale(x, y)
Scales the canvas units by x horizontally and by y vertically. Both parameters are real numbers. Values that are smaller than 1.0 reduce the unit size and values above 1.0 increase the unit size. Values of 1.0 leave the units the same size.
## Basic animations
Since we're using JavaScript to control canvas elements, it's also very easy to make (interactive) animations. 
Probably the biggest limitation is, that once a shape gets drawn, it stays that way. If we need to move it we have to redraw it and everything that was drawn before it. It takes a lot of time to redraw complex frames and the performance depends highly on the speed of the computer it's running on.
### Basic animation steps
1.	Clear the canvas
Unless the shapes you'll be drawing fill the complete canvas (for instance a backdrop image), you need to clear any shapes that have been drawn previously. The easiest way to do this is using the clearRect() method.
2.	Save the canvas state
If you're changing any setting (such as styles, transformations, etc.) which affect the canvas state and you want to make sure the original state is used each time a frame is drawn, you need to save that original state.
3.	Draw animated shapes
The step where you do the actual frame rendering.
4.	Restore the canvas state
If you've saved the state, restore it before drawing a new frame.
### Controlling an animation
Shapes are drawn to the canvas by using the canvas methods directly or by calling custom functions. In normal circumstances, we only see these results appear on the canvas when the script finishes executing. For instance, it isn't possible to do an animation from within a for loop.
That means we need a way to execute our drawing functions over a period of time. There are two ways to control an animation like this
### Optimizing canvas
1. Pre-render similar primitives or repeating objects on an offscreen canvas <br> If you find yourself repeating some of the same drawing operations on each animation frame, consider offloading them to an offscreen canvas. You can then render the offscreen image to your primary canvas as often as needed, without unnecessarily repeating the steps needed to generate it in the first place.
2. Avoid floating-point coordinates and use integers instead<br> Sub-pixel rendering occurs when you render objects on a canvas without whole values.
This forces the browser to do extra calculations to create the anti-aliasing effect. To avoid this, make sure to round all co-ordinates used in calls to drawImage() using Math.floor(), for example.
3. Don’t scale images in drawImage<br> Cache various sizes of your images on an offscreen canvas when loading as opposed to constantly scaling them in drawImage()
4. Use multiple layered canvases for complex scenes
5. Use plain CSS for large background images
6. Scaling canvas using CSS transforms
### More tips
1. Batch canvas calls together. For example, draw a polyline instead of multiple separate lines.
2. Avoid unnecessary canvas state changes.
3. Render screen differences only, not the whole new state.
4. Avoid the shadowBlur property whenever possible.
5. Avoid text rendering whenever possible.
6. Try different ways to clear the canvas (clearRect() vs. fillRect() vs. resizing the canvas).
7. With animations, use window.requestAnimationFrame() instead of window.setInterval()
8. Be careful with heavy physics libraries.
