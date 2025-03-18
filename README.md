# p5.js Global Mode Issue

In global mode, p5.js attaches functions like `setup()` and `draw()` to the `window` object, making it easy for beginners but causing issues when multiple sketches are loaded on the same page.  
Here, `sketch2.js` overwrites `sketch1.js`. Only one sketch runs because they share the same global functions.

---

### Example

#### `index.html`
```html
<!DOCTYPE html>
<html>
  <head>
    <title>Global Mode Problem</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.9.0/p5.min.js"></script>
  </head>
  <body>

    <h3>Sketch 1</h3>
    <div id="sketch1"></div>

    <h3>Sketch 2</h3>
    <div id="sketch2"></div>

    <script src="sketch1.js"></script>
    <script src="sketch2.js"></script>

  </body>
</html>
```
with sketch1.js as:

```javascript
function setup() {
  let c = createCanvas(200, 200);
  c.parent('sketch1');
  background(255, 0, 0);
}

function draw() {
  ellipse(mouseX, mouseY, 50, 50);
}
```
& sketch2.js as:

```javascript
function setup() {
  let c = createCanvas(200, 200);
  c.parent('sketch2');
  background(0, 0, 255);
}

function draw() {
  rect(mouseX, mouseY, 50, 50);
}
```
![Global Mode Problem - Google Chrome 18-03-2025 17_37_27](https://github.com/user-attachments/assets/ef7e9238-2612-4478-9051-7eda191f7f0e)

We observe that only sketch2.js works, and sketch1.js gets overridden because both are in global mode.
This is the main problem with global mode—functions overwrite each other on the window object.
