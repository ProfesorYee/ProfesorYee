



var main=null;
var font=null;
var copy1=null;
var copy2=null;
var copy3=null;
var copy4=null;
var copy5=null;
var copy6=null;
var spy;


function uploadmain(){
  var canvas1=document.getElementById("canvas1");
  var mainimage=document.getElementById("upmain");
  main=new SimpleImage(mainimage);
  main.drawTo(canvas1);
  copy1=new SimpleImage(mainimage);
  copy2=new SimpleImage(mainimage);
  copy3=new SimpleImage(mainimage);
  copy4=new SimpleImage(mainimage);
  copy5=new SimpleImage(mainimage);
}

function uploadfont(){
  var canvas2=document.getElementById("canvas2");
  var fontimage=document.getElementById("upfont");
  font=new SimpleImage(fontimage);
  font.drawTo(canvas2);
  copy6=new SimpleImage(fontimage);
}

function combine(){
  var canvas1=document.getElementById("canvas1");
  for(var pixel of copy1.values()){
    if(pixel.getGreen()>pixel.getRed()+pixel.getBlue()){
      var pixel2=font.getPixel(pixel.getX(),pixel.getY());
      pixel.setGreen(pixel2.getGreen());
      pixel.setRed(pixel2.getRed());
      pixel.setBlue(pixel2.getBlue());
    }
  }
  copy1.drawTo(canvas1);
}


function borrar(){
  var canvas1=document.getElementById("canvas1");
  main.drawTo(canvas1);
}

function gris(){
  var canvas1=document.getElementById("canvas1");
  for(var pixel of copy2.values()){
    var avg=(pixel.getBlue()+pixel.getRed()+pixel.getGreen())/3;
    pixel.setGreen(avg);
    pixel.setRed(avg);
    pixel.setBlue(avg);
  }
  copy2.drawTo(canvas1);
}

function rainbow(){
  var canvas1=document.getElementById("canvas1");
  var raya=main.getHeight()/7;
  for(var pixel of copy3.values()){
    var avg=(pixel.getBlue()+pixel.getRed()+pixel.getGreen())/3;
    if(pixel.getY()<raya){
      if(avg<128){
        pixel.setRed(2*avg);
        pixel.setGreen(0);
        pixel.setBlue(0);
      }
      else{
        pixel.setRed(255);
        pixel.setGreen(2*avg-255);
        pixel.setBlue(2*avg-255);
      }
    }
    else if (pixel.getY()>raya && pixel.getY()<2*raya){
      if(avg<128){
        pixel.setRed(2*avg);
        pixel.setGreen(0.8*avg);
        pixel.setBlue(0);
      }
      else{
        pixel.setRed(255);
        pixel.setGreen(1.2*avg-51);
        pixel.setBlue(2*avg-255);
      }
    }
    else if(pixel.getY()>2*raya && pixel.getY()<3*raya){
      if(avg<128){
        pixel.setRed(2*avg);
        pixel.setGreen(2*avg);
        pixel.setBlue(0);
      }
      else{
        pixel.setRed(255);
        pixel.setGreen(255);
        pixel.setBlue(2*avg-255);
      }
    }
    else if(pixel.getY()>3*raya && pixel.getY()<4*raya){
      if(avg<128){
        pixel.setRed(0);
        pixel.setGreen(2*avg);
        pixel.setBlue(0);
      }
      else{
        pixel.setRed(2*avg-255);
        pixel.setGreen(255);
        pixel.setBlue(2*avg-255);
      }
    }
    //blue
    else if(pixel.getY()>4*raya &&pixel.getY()<5*raya){
      if(avg<128){
        pixel.setRed(0);
        pixel.setGreen(0);
        pixel.setBlue(2*avg);
      }
      else{
        pixel.setRed(2*avg-255);
        pixel.setGreen(2*avg-255);
        pixel.setBlue(255);
      }
    }
    else if(pixel.getY()>5*raya && pixel.getY()<6*raya){
      if(avg<128){
        pixel.setRed(0.8*avg);
        pixel.setGreen(0);
        pixel.setBlue(2*avg);
      }
      else{
        pixel.setRed(1.2*avg-51);
        pixel.setGreen(2*avg-255);
        pixel.setBlue(255);
      }
    }
    else if(pixel.getY()>6*raya){
      if(avg<128){
        pixel.setRed(1.6*avg);
        pixel.setGreen(0);
        pixel.setBlue(1.6*avg);
      }
      else{
        pixel.setRed(0.4*avg+153);
        pixel.setGreen(2*avg-255);
        pixel.setBlue(0.4*avg+153);
      }
    }
    
  }
  
  copy3.drawTo(canvas1);
}


function esconder(){
  var canvas3=document.getElementById("canvas3");
  
  for(var pixel of copy5.values()){
    var pixel2=copy5.getPixel(pixel.getX(),pixel.getY());
    pixel.setGreen(Math.floor(pixel2.getGreen()/16)*16);
    pixel.setBlue(Math.floor(pixel2.getBlue()/16)*16);
    pixel.setRed(Math.floor(pixel2.getRed()/16)*16);
  }
  
  //copy5.drawTo(canvas3);
  var canvas4=document.getElementById("canvas4");
  
  for(var pixel of copy6.values()){
    var pixel2=copy6.getPixel(pixel.getX(),pixel.getY());
    pixel.setGreen(pixel2.getGreen()/16);
    pixel.setRed(pixel2.getRed()/16);
    pixel.setBlue(pixel2.getBlue()/16);
  }
  
  //copy6.drawTo(canvas4);
  spy=new SimpleImage(main.getWidth(),main.getHeight());
  for(var pixel of spy.values()){
    var base=copy5.getPixel(pixel.getX(),pixel.getY());
    var trick=copy6.getPixel(pixel.getX(),pixel.getY());
    pixel.setGreen(base.getGreen()+trick.getGreen());
    pixel.setBlue(base.getBlue()+trick.getBlue());
    pixel.setRed(base.getRed()+trick.getRed());
  }
  
  spy.drawTo(canvas3);
  
}


function decifrar(){
  var canvas4=document.getElementById("canvas4");
  var spycopy=new SimpleImage(spy);
  
  for(var pixel of spycopy.values()){
    var pixel2=spycopy.getPixel(pixel.getX(),pixel.getY());
    pixel.setBlue((pixel2.getBlue()%16)*16);
    pixel.setRed((pixel2.getRed()%16)*16);
    pixel.setGreen((pixel2.getGreen()%16)*16);
  }
  
  spycopy.drawTo(canvas4);
}

