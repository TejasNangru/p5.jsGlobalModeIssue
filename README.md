# p5.jsGlobalModeIssue
In global mode, p5.js attaches functions like setup() and draw() to the window object, making it easy for beginners but it creates issue when multiple sketches are loaded on the same page.
Here, sketch2.js overwrites sketch1.js. Only one sketch runs because they share the same global functions.

For example:
This is our index.html file

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

with sketch1.js as:

function setup() {
  let c = createCanvas(200, 200);
  c.parent('sketch1');
  background(255, 0, 0);
}

function draw() {
  ellipse(mouseX, mouseY, 50, 50);
}

& sketch2.js as:

function setup() {
  let c = createCanvas(200, 200);
  c.parent('sketch2');
  background(0, 0, 255);
}

function draw() {
  rect(mouseX, mouseY, 50, 50);
}

We observe that only the sketch2.js works, and the sketch1.js gets overridden as they are in global-mode,
This is the main problem of global mode, that is the reason we use instance mode

