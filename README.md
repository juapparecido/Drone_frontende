// Código HTML/CSS para controlar o drone
const char* htmlContent = R"rawliteral(
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Controle Drone</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }

        h1 {
            text-align: center;
            margin-top: 20px;
            color: blue;
            font-size: 2.5rem;
        }

        .controle {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 80vh;
        }

        .controleEsquerdo, .controleDireito {
            display: grid;
            grid-template-columns: 60px 60px 60px;
            grid-template-rows: 60px 60px 60px;
            gap: 10px;
            margin: 0 20px;
            grid-template-areas: 
                "cima cima cima"
                "esquerda centro direita"
                "baixo baixo baixo";
        }

        .controleEsquerdo button, .controleDireito button {
            width: 120px;
            height: 120px;
            background-color: #007bff;
            color: white;
            border: 2px solid #0056b3;
            font-size: 1.5rem;
            cursor: pointer;
            outline: none;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 5px;
            position: relative;
        }

        /* Ajuste das setas para tamanho e direção */
        .seta {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
        }

        .seta-cima {
            border-left: 25px solid transparent;
            border-right: 25px solid transparent;
            border-bottom: 40px solid black;
            width: 0;
            height: 0;
        }

        .seta-baixo {
            border-left: 25px solid transparent;
            border-right: 25px solid transparent;
            border-top: 40px solid black;
            width: 0;
            height: 0;
        }

        .seta-esquerda {
            border-top: 25px solid transparent;
            border-bottom: 25px solid transparent;
            border-right: 40px solid black;
            width: 0;
            height: 0;
        }

        .seta-direita {
            border-top: 25px solid transparent;
            border-bottom: 25px solid transparent;
            border-left: 40px solid black;
            width: 0;
            height: 0;
        }

        .controleEsquerdo .seta-cima { grid-area: cima; }
        .controleEsquerdo .seta-baixo { grid-area: baixo; }
        .controleEsquerdo .seta-esquerda { grid-area: esquerda; }
        .controleEsquerdo .seta-direita { grid-area: direita; }

        .controleDireito .seta-cima { grid-area: cima; }
        .controleDireito .seta-baixo { grid-area: baixo; }
        .controleDireito .seta-esquerda { grid-area: esquerda; }
        .controleDireito .seta-direita { grid-area: direita; }

        .controle button:hover {
            background-color: #0056b3;
        }

      #cimaEsquerdo { margin-top: -60px; margin-left: -92px; }
      #esquerdaEsquerda { margin-top: 58px; margin-left: -280px; }
      #direitaEsquerda { margin-top: 58px; margin-left: -114px; }
      #baixoEsquerda { margin-top: 106px; margin-left: -92px; }

      #cimaDireita { margin-top: -60px; margin-left: 188px; }
      #esquerdaDireita { margin-top: 58px; margin-right: -260px; }
      #direitaDireita { margin-top: 58px; margin-left: 166px; }
      #baixoDireita { margin-top: 105px; margin-left: 188px; }
    </style>
</head>
<body>

    <h1>Controle Drone</h1>

    <div class="controle">
        <div class="controleEsquerdo">
            <button id="cimaEsquerdo" onclick="sendCommand('up')">
                <div class="seta seta-cima"></div>
            </button>
            <button id="esquerdaEsquerda" onclick="sendCommand('left')">
                <div class="seta seta-esquerda"></div>
            </button>
            <button id="direitaEsquerda" onclick="sendCommand('right')">
                <div class="seta seta-direita"></div>
            </button>
            <button id="baixoEsquerda" onclick="sendCommand('down')">
                <div class="seta seta-baixo"></div>
            </button>
        </div>

        <div class="controleDireito">
            <button id="cimaDireita" onclick="sendCommand('up')">
                <div class="seta seta-cima"></div>
            </button>
            <button id="esquerdaDireita" onclick="sendCommand('left')">
                <div class="seta seta-esquerda"></div>
            </button>
            <button id="direitaDireita" onclick="sendCommand('right')">
                <div class="seta seta-direita"></div>
            </button>
            <button id="baixoDireita" onclick="sendCommand('down')">
                <div class="seta seta-baixo"></div>
            </button>
        </div>
    </div>

    <script>
        function sendCommand(cmd) {
            var xhr = new XMLHttpRequest();
            xhr.open("GET", "/control?cmd=" + cmd, true);
            xhr.onreadystatechange = function() {
                if (xhr.readyState == 4 && xhr.status == 200) {
                    console.log("Comando enviado: " + cmd);
                    console.log("Resposta do servidor: " + xhr.responseText);
                }
            };
            xhr.send();
        }
    </script>

</body>
</html>
)rawliteral";
