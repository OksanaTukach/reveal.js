## Canvas
<canvas> is an HTML element which can be used to draw graphics via scripting (usually JavaScript). This can, for instance, be used to draw graphs, combine photos, or create simple (and not so simple) animations. 
The default size of the canvas is 300 pixels × 150 pixels (width × height). But custom sizes can be defined using the HTML height and width property. 
### Basic usage of canvas
The canvas is initially blank. To display something, a script first needs to access the rendering context and draw on it. The <canvas> element has a method called getContext(), used to obtain the rendering context and its drawing functions. getContext() takes one parameter, the type of context. For 2D graphics, such as those covered by this tutorial, you specify "2d" to get a CanvasRenderingContext2D.
The first line in the script retrieves the node in the DOM representing the <canvas> element by calling the document.getElementById() method. Once you have the element node, you can access the drawing context using its getContext() method.
## Drawing shapes with canvas
### The Grid
Normally 1 unit in the grid corresponds to 1 pixel on the canvas. The origin of this grid is positioned in the top left corner at coordinate (0,0). All elements are placed relative to this origin. So the position of the top left corner of the blue square becomes x pixels from the left and y pixels from the top, at coordinate (x,y). 


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
