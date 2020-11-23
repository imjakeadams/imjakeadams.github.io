<!DOCTYPE HTML>
<html>
  <head>
    <!--http://www.sitepoint.com/forums/showthread.php?1055755-Count-Down-and-Make-sound-play-on-click-->
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
    <title>Play sound after countdown</title>
    <script src="http://code.jquery.com/jquery-latest.min.js" type="text/javascript"></script>
  </head>
  
  <body>
    <button id="myButton">Start</button> <br /> 
    <span id="count"></span>
    
    <script>
      function countdown(number){  
        $("#count").html(number);
        if (number === 5){
          d.resolve();  
        } else {
          number += 1;
          window.setTimeout(function() {
            countdown(number);
          }, 1000);
        }
        return d.promise();
      }
      
      function waitForAudioToFinish(audioElement){
        if (!audioElement.paused){
          setTimeout(function(){
            waitForAudioToFinish(audioElement)
          }, 500);
        } else {
          d1.resolve();
        }
      }
      
      function playSong(src){
        var audioElement = document.createElement('audio');
        audioElement.setAttribute('src', src);
        audioElement.setAttribute('autoplay', 'autoplay');
        audioElement.play();
        waitForAudioToFinish(audioElement);
        return d1.promise();
      }
      
      var d = new $.Deferred();
      var d1 = new $.Deferred();
      
      $("#myButton").on("click", function(){
        $(this).prop("disabled", true);
        $.when(countdown(5)).then(function() { 
          playSong("Ping.aiff")
          .then(function() { $("#myButton").prop("disabled", false) });
        })
      });
    </script>
  </body>
</html>