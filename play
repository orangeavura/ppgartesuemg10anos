// Variáveis das frases
let frases = ["PPGARTES", "10 ANOS", "UEMG"];
let posicaoY = [];

// Controle de Bezier
let controlX = [100, 300, 500, 1000];
let controlY = [100, 400, 200, 400];

// Controle de cor de fundo e letras
let corFundo;
let intervaloTrocaCores = 30;
let tempoUltimaTroca = 0;
let coresLetras = [];

// Variável para salvar GIF
let gifContador = 0;
let salvarGIF = false;

// Definindo o espaçamento entre as linhas
let espacoEntreLinhas = 150; // Ajuste este valor para alterar o espaçamento

function setup() {
  createCanvas(1000, 1000);  // Tamanho fixo de 1000x1000 pixels
  textFont('Arial', 120);
  textStyle(BOLD);
  textAlign(LEFT, CENTER);  // Alinhamento à esquerda
  frameRate(30);
  noStroke();
  resetPosicoes();
  resetCoresLetras();
  corFundo = color(0);  // Inicia com fundo preto
}

function draw() {
  // Desenha o fundo
  background(corFundo);

  // Verifica se é hora de trocar as cores das letras
  if (millis() - tempoUltimaTroca > intervaloTrocaCores * 1000 / 30) {
    resetCoresLetras();
    tempoUltimaTroca = millis();
  }

  // Desenho das frases rolantes com controle Bezier
  for (let i = 0; i < frases.length; i++) {
    desenhaFraseBezier(frases[i], posicaoY[i]);
    posicaoY[i] += 2;
    if (posicaoY[i] > height + 50) {  // Adiciona um pouco de margem inferior
      posicaoY[i] = -50;  // Faz a frase reaparecer no topo com uma margem
    }
  }

  // Controle para salvar o "GIF" (na prática, salva uma imagem)
  if (salvarGIF) {
    saveCanvas('frame-' + nf(gifContador, 4), 'png');
    gifContador++;
    if (gifContador > 60) {
      salvarGIF = false;
      gifContador = 0;
    }
  }
}

// Função para desenhar a frase com curva Bezier
function desenhaFraseBezier(frase, y) {
  // Centraliza a frase no eixo X (horizontalmente)
  let larguraFrase = textWidth(frase);  // Calcula a largura total da frase
  let x = 0;  // Alinhado à esquerda

  for (let i = 0; i < frase.length; i++) {
    let c = frase.charAt(i);

    // Cálculo de Bezier para o movimento da letra
    let offsetX = bezierPoint(controlX[0], controlX[1], controlX[2], controlX[3], map(i, 0, frase.length, 0, 1));
    let offsetY = bezierPoint(controlY[0], controlY[1], controlY[2], controlY[3], map(i, 0, frase.length, 0, 1));

    // Definindo a cor da letra
    fill(coresLetras[i % coresLetras.length]);

    // Centraliza a letra e ajusta a posição usando o texto total e o controle Bezier
    text(c, x + offsetX, y + offsetY);
  }
}

// Reinicia posições das frases
function resetPosicoes() {
  for (let i = 0; i < frases.length; i++) {
    posicaoY[i] = random(-100, height);
  }
}

// Reinicia cores das letras
function resetCoresLetras() {
  coresLetras = [];
  for (let i = 0; i < 10; i++) {
    coresLetras.push(color(random(255), random(255), random(255)));
  }
}

// Controles de teclado
function keyPressed() {
  if (key === 'b') {
    corFundo = color(random(255), random(255), random(255));  // Muda o fundo para uma cor aleatória
  }

  if (key === 'g') {
    salvarGIF = true;
  }

  if (key === '+') {
    intervaloTrocaCores = max(1, intervaloTrocaCores - 5);  // Diminui o intervalo de troca de cores
  }

  if (key === '-') {
    intervaloTrocaCores += 5;  // Aumenta o intervalo de troca de cores
  }
}

// Controles de mouse para os pontos de controle Bezier
function mouseDragged() {
  controlX[0] = mouseX;
  controlY[0] = mouseY;
}
