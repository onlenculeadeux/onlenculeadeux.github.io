<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>On l'encule à deux</title>

        <style>
            @import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@800&display=swap');

            * {
                margin: 0;
                padding: 0;
                font-family: 'Monstserrat', sans-serif;
            }

            .ph {
                width: 250px;
                height: 250px;
                position: absolute;
                background-color: transparent;
                border: 5px solid rgba(200, 200, 200, 0.5);
                border-radius: 10px;
                cursor: pointer;
            }

            body {
                display: flex;
                flex-direction: column;
                justify-content: space-evenly;
                width: 100vw;
                height: 100vh;
            }

            #canvas {
                width: 688px;
                height: 688px;
                align-self: center;
            }

            #download {
                align-self: center;
                padding: 10px 100px;
                border-radius: 5px;
                font-size: 20px;
                background-color: #2ecc71;
                color: white;
                cursor: pointer;
            }
        </style>
        <script data-ad-client="ca-pub-6769638584371826" async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
    </head>

    <body onload="draw()">
        <canvas id="canvas" width="688" height="688" crossorigin="anonymous"></canvas>
        <div id="sq1ph" class="ph"></div>
        <div id="sq2ph" class="ph"></div>
        <input type="file" id="sq1" hidden />
        <input type="file" id="sq2" hidden />
        <div id="download" onclick="download()">Télécharger l'image</div>
    </body>

    <script>
        let canvas = document.getElementById('canvas')
        let URL = window.webkitURL || window.URL
        let ctx = null
        let max_width = 250
        let max_height = 250

        let sq1 = document.getElementById("sq1")
        let sq2 = document.getElementById("sq2")

        let sq1ph = document.getElementById("sq1ph")
        let sq2ph = document.getElementById("sq2ph")

        function draw() {
            ctx = canvas.getContext('2d')
            
            let img = new Image()

            img.onload = function() {
                ctx.drawImage(img, 0, 0)
            }
            img.crossOrigin = 'Anonymous'
            img.src = 'pnl.webp'
        }

        function addImage1(e) {
            let url = URL.createObjectURL(e.target.files[0])
            let img = new Image()

            img.onload = () => {
                ctx.drawImage(img, 60, 80, 250, 250)
                sq1ph.style.opacity = '0'
            }
            img.src = url
        }

        function addImage2(e) {
            let url = URL.createObjectURL(e.target.files[0])
            let img = new Image()

            img.onload = () => {
                ctx.drawImage(img, 375, 100, 250, 250)
                sq2ph.style.opacity = '0'
            }
            img.src = url
        }

        sq1ph.onclick = () => {
            sq1.click()
        }

        sq2ph.onclick = () => {
            sq2.click()
        }

        let phPos = () => {
            sq1ph.style.left = (canvas.offsetLeft + 60) + 'px'
            sq2ph.style.left = (canvas.offsetLeft + 375) + 'px'
            sq1ph.style.top = (canvas.offsetTop + 80) + 'px'
            sq2ph.style.top = (canvas.offsetTop + 100) + 'px'
        }

        let download = () => {
            let link = document.createElement('a')

            link.download = 'winamax.png'
            link.href = document.getElementById('canvas').toDataURL("image/png")
            link.click()
        }

        window.onresize = phPos

        phPos()

        sq1.addEventListener('change', addImage1, false)
        sq2.addEventListener('change', addImage2, false)
    </script>
</html>