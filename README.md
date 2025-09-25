// Posições iniciais dos jogadores (todos começam no x=0, mas em linhas diferentes)
let xJogador = [0, 0, 0, 0, 0, 0, 0];
let yJogador = [75, 125, 175, 225, 275, 325, 375];

// Letras que representam cada jogador na tela
let jogador = ["A", "B", "C", "D", "E", "F", "G"];

// Teclas para cada jogador (uma tecla por personagem)
let teclas = ["a", "s", "d", "f", "g", "h", "j"];

let quantidade = jogador.length;

function setup() {
  createCanvas(500, 450);
  textSize(32);
}

function draw() {
  ativaJogo();
  desenhaJogadores();
  desenhaLinhaDeChegada();
  verificaVencedor();
}

function ativaJogo() {
  if (focused === true) {
    // Tela verde (jogo ativo)
    background("#D2EBB5");
  } else {
    // Tela vermelha (aguardando clique na tela ou foco da janela)
    background("rgb(238,178,178)");

    // Instruções iniciais
    fill(0);
    textSize(18);
    textAlign(CENTER, CENTER);
    text("Corrida dos 7 Jogadores!", width / 2, height / 2 - 40);
    text("Clique na tela para iniciar o jogo", width / 2, height / 2);
    text("Use as teclas A, S, D, F, G, H, J para correr!", width / 2, height / 2 + 40);
  }
}

function desenhaJogadores() {
  fill(0);
  for (let i = 0; i < quantidade; i++) {
    text(jogador[i], xJogador[i], yJogador[i]);
  }
}

function desenhaLinhaDeChegada() {
  fill("white");
  rect(width - 50, 0, 10, height);

  fill("black");
  for (let yAtual = 0; yAtual < height; yAtual += 20) {
    rect(width - 50, yAtual, 10, 10);
  }
}

function verificaVencedor() {
  for (let i = 0; i < quantidade; i++) {
    if (xJogador[i] > width - 50) {
      fill("black");
      textSize(32);
      textAlign(CENTER, CENTER);
      text(jogador[i] + " venceu!", width / 2, height / 2);
      noLoop(); // Para o jogo
    }
  }
}

function keyReleased() {
  for (let i = 0; i < quantidade; i++) {
    if (key.toLowerCase() === teclas[i]) {
      xJogador[i] += random(10, 30); // movimento aleatório
    }
  }
}
