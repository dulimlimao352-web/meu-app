<!DOCTYPE html>
<html>
<head>
    <title>Calculadora</title>
    <style>
        body { background: #1a1a2e; display: flex; flex-direction: column; align-items: center; padding: 20px; font-family: Arial; }
        .calc { background: #16213e; border-radius: 20px; padding: 20px; width: 320px; }
        .tela { background: #0f3460; color: white; font-size: 28px; text-align: right; padding: 15px; border-radius: 10px; margin-bottom: 10px; min-height: 50px; }
        .historico { background: #0f3460; color: #aaa; font-size: 12px; padding: 10px; border-radius: 10px; margin-bottom: 10px; max-height: 80px; overflow-y: auto; }
        button { background: #e94560; color: white; border: none; width: 70px; height: 60px; font-size: 18px; border-radius: 10px; margin: 3px; cursor: pointer; }
        .zero { width: 143px; }
        .igual { background: #0f3460; }
        .apagar { background: #ff6b35; }
        .ciencia { background: #533483; }
        .tema { background: #2d6a4f; width: 100%; margin-bottom: 10px; height: 40px; font-size: 14px; }
        body.claro { background: #f0f0f0; }
        body.claro .calc { background: #ffffff; }
        body.claro .tela { background: #e0e0e0; color: black; }
        body.claro .historico { background: #e0e0e0; color: #555; }
    </style>
</head>
<body>
    <div class="calc">
        <button class="tema" onclick="mudarTema()">🌙 Tema Claro/Escuro</button>
        <div class="historico" id="historico">Histórico de cálculos</div>
        <div class="tela" id="tela">0</div>
        <button class="ciencia" onclick="raiz()">√</button>
        <button class="ciencia" onclick="potencia()">x²</button>
        <button class="ciencia" onclick="digita('%')">%</button>
        <button class="apagar" onclick="apagar()">C</button>
        <button onclick="digita('7')">7</button>
        <button onclick="digita('8')">8</button>
        <button onclick="digita('9')">9</button>
        <button onclick="digita('/')">/</button>
        <button onclick="digita('4')">4</button>
        <button onclick="digita('5')">5</button>
        <button onclick="digita('6')">6</button>
        <button onclick="digita('*')">*</button>
        <button onclick="digita('1')">1</button>
        <button onclick="digita('2')">2</button>
        <button onclick="digita('3')">3</button>
        <button onclick="digita('-')">-</button>
        <button class="zero" onclick="digita('0')">0</button>
        <button onclick="digita('.')">.</button>
        <button onclick="digita('+')">+</button>
        <button class="igual" onclick="calcular()">=</button>
    </div>
    <script>
        let valor = '';
        let historico = [];

        function digita(n) {
            if (valor === '0') valor = '';
            valor += n;
            document.getElementById('tela').innerText = valor;
        }

        function calcular() {
            try {
                let resultado = String(eval(valor));
                historico.push(valor + ' = ' + resultado);
                if (historico.length > 5) historico.shift();
                document.getElementById('historico').innerHTML = historico.join('<br>');
                valor = resultado;
                document.getElementById('tela').innerText = valor;
            } catch {
                document.getElementById('tela').innerText = 'Erro';
                valor = '';
            }
        }

        function apagar() {
            valor = '';
            document.getElementById('tela').innerText = '0';
        }

        function raiz() {
            let resultado = String(Math.sqrt(parseFloat(valor)));
            historico.push('√' + valor + ' = ' + resultado);
            if (historico.length > 5) historico.shift();
            document.getElementById('historico').innerHTML = historico.join('<br>');
            valor = resultado;
            document.getElementById('tela').innerText = valor;
        }

        function potencia() {
            let resultado = String(Math.pow(parseFloat(valor), 2));
            historico.push(valor + '² = ' + resultado);
            if (historico.length > 5) historico.shift();
            document.getElementById('historico').innerHTML = historico.join('<br>');
            valor = resultado;
            document.getElementById('tela').innerText = valor;
        }

        function mudarTema() {
            document.body.classList.toggle('claro');
        }
    </script>
</body>
</html>
