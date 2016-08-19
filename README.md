# First-Game
My attempt to make a game.
<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<style>
canvas {
    border:1px solid #d3d3d3;
    background-color: #f1f1f1;
}
</style>
</head>
<body onload="startGame()">
<script>

var redGamePiece, blueGamePiece, yellowGamePiece;

function startGame() {
    redGamePiece = new component(75, 75, "red", 10, 10);
    yellowGamePiece = new component(75, 75, "yellow", 10, 100);
    blueGamePiece = new component(75, 75, "blue", 10, 190);
    myGameArea.start();
}

var myGameArea = {
    canvas : document.createElement("canvas"),
    start : function() {
        this.canvas.width = 480;
        this.canvas.height = 270;
        this.context = this.canvas.getContext("2d");
        document.body.insertBefore(this.canvas, document.body.childNodes[0]);
        this.interval = setInterval(updateGameArea, 20);
    },
    clear : function() {
        this.context.clearRect(0, 0, this.canvas.width, this.canvas.height);
    }
}

function component(width, height, color, x, y) {
    this.width = width;
    this.height = height;
    this.x = x;
    this.y = y;
    this.update = function(){
        ctx = myGameArea.context;
        ctx.fillStyle = color;
        ctx.fillRect(this.x, this.y, this.width, this.height);
    }
}

    function updateGameArea() {
    myGameArea.clear();
    redGamePiece.x += 1;
    yellowGamePiece.x += 1; 
    yellowGamePiece.y += 1; 
    blueGamePiece.x += 1; 
    blueGamePiece.y -= 1; 
    redGamePiece.update();
    yellowGamePiece.update(); 
    blueGamePiece.update();
}
</script>
<p>Three components on one game area.</p>
<p>Notice that the stack order of the components depends on the order they were updated in the updateGameArea function. The blue game piece is updated last, and will be placed on top of the yellow, which will be placed on top of the red.</p>
</body>
</html>
