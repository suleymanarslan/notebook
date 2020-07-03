## JavaScript

## Accessing Webcam

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>Display Webcam Stream</title>

    <style>
      html,
      body {
        width: 100%;
        height: 100%;
        margin: 0;
        padding: 0;
      }

      video {
        width: 100%;
        height: 100%;
        background-color: #666;
      }
    </style>
  </head>

  <body>
    <video autoplay="true"></video>
    <script type="text/javascript">
      var video = document.querySelector("video");

      if (navigator.mediaDevices.getUserMedia) {
        navigator.mediaDevices
          .getUserMedia({ video: true })
          .then(function(stream) {
            video.srcObject = stream;
          })
          .catch(function(err0r) {
            console.log("Something went wrong!");
          });
      }
    </script>
  </body>
</html>

```
