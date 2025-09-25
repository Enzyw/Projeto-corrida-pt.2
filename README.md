let xJogador = [0, 0, 0, 0, 0, 0];  // todos começam no canto esquerdo
let yJogador = [75, 125, 175, 225, 275, 325]; // espaçamento entre eles

// Letras que representam os jogadores
let jogador = ["🦁", "🐯", "🐈", "🐕", "🐇", "🐢"];

// Teclas que controlam os jogadores
let teclas = ["a", "s", "d", "f", "g", "h"];

let quantidade = jogador.length;

function setup() {
  createCanvas(500, 400);
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
    background("#D2EBB5"); // verde quando ativo
  } else {
    background("rgb(238,178,178)"); // vermelho aguardando foco
    mostraInstrucoes();
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
      noLoop();
    }
  }
}

function keyReleased() {
  for (let i = 0; i < quantidade; i++) {
    if (key.toLowerCase() === teclas[i]) {
      xJogador[i] += random(10, 30);
    }
  }
}

// Nova função para instruções iniciais
function mostraInstrucoes() {
  fill(0);
  textSize(18);
  textAlign(CENTER, CENTER);
  text("Corrida dos 6 jogadores!", width / 2, height / 2 - 40);
  text("Pressione as teclas: A, S, D, F, G, H", width / 2, height / 2);
}
