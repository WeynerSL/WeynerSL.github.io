<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Para mi amada Melany</title>
    <style>
        body {
            background-image: url('Foto 1.png');
            background-size: contain;
            background-repeat: no-repeat;
            background-position: center;
            background-color: black;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            font-family: 'Arial', sans-serif;
        }
        .carta {
            width: 300px;
            height: 200px;
            background: url('Foto 2.png') no-repeat center;
            background-size: cover;
            position: relative;
            cursor: pointer;
            transition: transform 0.5s ease-in-out;
        }
        .carta::after {
            content: "Presione para abrir";
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-weight: bold;
            color: white;
            background-color: rgba(0, 0, 0, 0.5);
            padding: 5px;
            border-radius: 5px;
        }
        .carta.abierta::after {
            content: "";
        }
        .carta.abierta {
            background: url('Foto 3.png') no-repeat center;
            background-size: cover;
            height: 400px;
            animation: abrir 1s ease-in-out;
        }
        .texto {
            display: none;
            position: absolute;
            top: 20px;
            left: 10%;
            right: 10%;
            bottom: 20px;
            text-align: justify;
            font-size: 16px;
            color: #4a2c2a;
            font-family: 'Courier New', monospace;
            overflow-y: auto;
            max-height: 300px;
            padding: 10px;
            background: rgba(255, 255, 255, 0.9);
            border-radius: 10px;
        }
        .carta.abierta .texto {
            display: block;
        }
        .boton, .boton-blanco {
            margin-top: 20px;
            padding: 10px;
            background-color: rgba(0, 0, 0, 0.5);
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
            display: none;
        }
        .carta.abierta + .boton {
            display: block;
        }
        .carta.abierta + .boton + .boton-blanco {
            display: block;
        }
        .galeria {
            display: none;
            width: 100vw;
            height: 100vh;
            background-color: black;
            position: fixed;
            top: 0;
            left: 0;
            justify-content: center;
            align-items: center;
            flex-direction: column;
        }
        .galeria img {
            max-width: 100%;
            max-height: 100%;
        }
        .galeria .controles {
            position: absolute;
            bottom: 20px;
            display: flex;
            justify-content: center;
            gap: 10px;
        }
        .mutear {
            position: absolute;
            top: 10px;
            right: 10px;
            background: none;
            border: none;
            cursor: pointer;
            font-size: 24px;
            color: white;
        }
    </style>
</head>
<body>
    <div class="carta" onclick="abrirCarta()">
        <div class="texto" id="texto">
            <p><strong>Para mi mujer amada: Melany Natalia Castro Vega.</strong></p>
            <p>Hola amor mío, hoy es un día muy especial para nosotros, ya que cumplimos 9 grandiosos años juntos. Hoy elaboré este pequeño detalle y quede guardado en Internet y solo para nosotros para el resto de nuestras vidas. </p>
            <p>Tan solo quiero agradecer la mujer tan maravillosa que eres, lo encantadora y adorable que eres como mujer, pareja, hermana e hija y no dudo que madre si en algún momento de nuestras vidas Dios lo permite. Has sido una parte demasido importante mi vida, puesto que mi mente y corazón siempre están contigo bailando en mi ser, siempre de visualizo con una sonrisa preciosa y exageradamente tierna, si tierna, sí tuviera que elegir una palabra para describirte sería tierna, tienes unos ojos preciosos siempre, pero aún más cuando me miras de cerquita detenidamente y se te muestra una leve sonrisa en tu rostro, en donde irradias pura ternura.</p>
            <p>Quiero formar mi vida contigo, quiero darte todo de mí, quiero desgastar todos los chineos y cuidados en tí, quiero, no desgastar, sino más bien disfrutar y aprovechar todo mi tiempo en tí. Estoy seguro y creo en Dios y en tí en que vamos a vivir hasta viejitos juntos, siempre juntos.</p>
        </div>
        </div>
    </div>
    <button class="boton" onclick="cerrarCarta()">Presione para regresar</button>
    <button class="boton-blanco" onclick="verGaleria()">Presione para ver un pequeño trayecto de nuestra vida</button>

    <div class="galeria" id="galeria">
        <button class="mutear" onclick="toggleAudio()">🔊</button>
        <audio id="audio" loop>
            <source src="Pista 1.mp3" type="audio/mpeg">
            <source src="Pista 2.mp3" type="audio/mpeg">
            <source src="Pista 3.mp3" type="audio/mpeg">
            <source src="Pista 4.mp3" type="audio/mpeg">
            Tu navegador no soporta el elemento de audio.
        </audio>
        <img id="imagen-galeria" src="Foto 4.jpg">
        <div class="controles">
            <button onclick="cambiarImagen(-1)">Anterior</button>
            <button onclick="cambiarImagen(1)">Siguiente</button>
            <button onclick="cerrarGaleria()">Regresar</button>
        </div>
    </div>

    <script>
        let imagenes = [];
        for (let i = 4; i <= 94; i++) {
            imagenes.push(`Foto ${i}.jpg`);
        }
        let indice = 0;
        let audio = document.getElementById('audio');
        let isMuted = false;

        function abrirCarta() {
            let carta = document.querySelector('.carta');
            let texto = document.getElementById('texto');
            carta.classList.add('abierta');
            texto.scrollTop = 0;
        }
        function cerrarCarta() {
            let carta = document.querySelector('.carta');
            carta.classList.remove('abierta');
        }
        function verGaleria() {
            document.getElementById('galeria').style.display = 'flex';
            audio.play();
        }
        function cerrarGaleria() {
            document.getElementById('galeria').style.display = 'none';
            audio.pause();
        }
        function cambiarImagen(direccion) {
            indice = (indice + direccion + imagenes.length) % imagenes.length;
            document.getElementById('imagen-galeria').src = imagenes[indice];
        }
        function toggleAudio() {
            isMuted = !isMuted;
            audio.muted = isMuted;
            document.querySelector('.mutear').textContent = isMuted ? '🔇' : '🔊';
        }
    </script>
</body>
</html>
