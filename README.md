**这是div**

<div id="anim">Click here to start animation</div> 

**这是样式**

####anim {

  position:absolute;
  left:0px;
  width:150px;
  height:150px;
  background: blue;
  font-size: larger;
  color: white;
  border-radius: 10px;
 padding: 1em;
}

> requestAnimFrame 的 兼容

window.requestAnimFrame = (function(){

         return  window.requestAnimationFrame || 
         window.webkitRequestAnimationFrame || 
          window.mozRequestAnimationFrame || 
          window.oRequestAnimationFrame || 
          window.msRequestAnimationFrame || 
          function(/* function FrameRequestCallback */ callback, /* DOMElement Element */ element){
            window.setTimeout(callback, 1000 / 60);
          };
})();


var elem = document.getElementById("anim");
var startTime = undefined;

function render(time) {

  if (time === undefined)
    time = Date.now();//最新的时间 是不断变化的
  if (startTime === undefined)
    startTime = time;//当时单击的时间 是不变的

  elem.style.left = ((time - startTime)/10 % 500) + "px";
}

elem.onclick = function() {

    (function animloop(){
      render();
      requestAnimFrame(animloop, elem);
    })();

};

