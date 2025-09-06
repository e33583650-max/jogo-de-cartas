!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link rel="stylesheet" href="style.css">
</head>
<body>
<div id="jogo">
<div id="info-turno">Turno do Jogador 1</div>
<div class="player" id="player1">
<div class="cartas" id="cartas1"></div>
<div class="trio" id="trio1"></div>
</div>
<div class="player" id="player2">
<div class="cartas" id="cartas2"></div>
<div class="trio" id="trio2"></div>
</div>
<button id="proximo-turno">Passar Turno</button>
</div>
<script src="script.js"></script>
</body>
</html>

body{font-family:Arial,sans-serif;text-align:center;background:#f2f2f2}
#jogo{display:flex;flex-direction:column;align-items:center;gap:20px}
.player{border:2px solid #333;padding:10px;width:90%;background:#fff;border-radius:10px}
.cartas,.trio{display:flex;justify-content:center;gap:10px;flex-wrap:wrap;margin:10px 0}
.carta{border:1px solid #555;padding:5px;width:100px;background:#e0e0e0;border-radius:5px;cursor:pointer}
.carta p{margin:2px 0}
#proximo-turno{padding:10px 20px;font-size:16px;cursor:pointer}

const cartasJogador1=[
{nome:"Dragão",ataque:50,defesa:30,dano:40},
{nome:"Guerreiro",ataque:30,defesa:40,dano:25},
{nome:"Mago",ataque:40,defesa:20,dano:35},
{nome:"Arqueiro",ataque:35,defesa:25,dano:30},
{nome:"Cavaleiro",ataque:45,defesa:35,dano:30},
{nome:"Goblin",ataque:20,defesa:15,dano:10},
{nome:"Fênix",ataque:55,defesa:25,dano:45}
];
const cartasJogador2=[
{nome:"Troll",ataque:40,defesa:35,dano:30},
{nome:"Feiticeiro",ataque:45,defesa:25,dano:35},
{nome:"Elfo",ataque:35,defesa:20,dano:25},
{nome:"Orc",ataque:30,defesa:30,dano:25},
{nome:"Dragão Negro",ataque:55,defesa:30,dano:50},
{nome:"Golem",ataque:50,defesa:40,dano:35},
{nome:"Vampiro",ataque:45,defesa:25,dano:40}
];
let turno=1,trio1=[],trio2=[];
const cartas1Div=document.getElementById("cartas1");
const cartas2Div=document.getElementById("cartas2");
const trio1Div=document.getElementById("trio1");
const trio2Div=document.getElementById("trio2");
const infoTurno=document.getElementById("info-turno");
const proximoTurnoBtn=document.getElementById("proximo-turno");
function mostrarCartas(){
cartas1Div.innerHTML="";
cartasJogador1.forEach((carta,index)=>{
const div=document.createElement("div");
div.classList.add("carta");
div.innerHTML=`<p>${carta.nome}</p><p>Ataque:${carta.ataque}</p><p>Defesa:${carta.defesa}</p>`;
div.onclick=()=>selecionarCarta(1,index);
cartas1Div.appendChild(div);
});
cartas2Div.innerHTML="";
cartasJogador2.forEach((carta,index)=>{
const div=document.createElement("div");
div.classList.add("carta");
div.innerHTML=`<p>${carta.nome}</p><p>Ataque:${carta.ataque}</p><p>Defesa:${carta.defesa}</p>`;
div.onclick=()=>selecionarCarta(2,index);
cartas2Div.appendChild(div);
});
}
function selecionarCarta(jogador,index){
if(jogador===1&&trio1.length<3&&turno===1)trio1.push(cartasJogador1.splice(index,1)[0]);
if(jogador===2&&trio2.length<3&&turno===2)trio2.push(cartasJogador2.splice(index,1)[0]);
mostrarCartas();
mostrarTrio();
}
function mostrarTrio(){
trio1Div.innerHTML="";
trio1.forEach(carta=>{
const div=document.createElement("div");
div.classList.add("carta");
div.innerHTML=`<p>${carta.nome}</p><p>Ataque:${carta.ataque}</p><p>Defesa:${carta.defesa}</p>`;
trio1Div.appendChild(div);
});
trio2Div.innerHTML="";
trio2.forEach(carta=>{
const div=document.createElement("div");
div.classList.add("carta");
div.innerHTML=`<p>${carta.nome}</p><p>Ataque:${carta.ataque}</p><p>Defesa:${carta.defesa}</p>`;
trio2Div.appendChild(div);
});
}
proximoTurnoBtn.onclick=()=>{
if(turno===1&&trio1.length===3){turno=2;infoTurno.innerText="Turno do Jogador 2";}
else if(turno===2&&trio2.length===3){turno=1;infoTurno.innerText="Turno do Jogador 1";}
};
mostrarCartas();
mostrarTrio();


---
