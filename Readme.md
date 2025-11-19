<!doctype html>
<html lang="es">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Easter Egg — Suero y Lanzamiento</title>
<style>
body{font-family:Arial,sans-serif;background:#0d1117;color:white;padding:20px;text-align:center;}
h1{font-size:22px;margin-bottom:10px;}
h2{font-size:20px;margin-top:40px;}
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(140px,1fr));gap:12px;max-width:800px;margin:20px auto;}
.card{background:#161b22;padding:10px;border-radius:8px;cursor:pointer;}
.card img{width:100%;height:120px;object-fit:contain;border-radius:6px;background:#111;}
#resultado{margin-top:20px;font-size:20px;font-weight:700;text-align:center;max-width:400px;margin-left:auto;margin-right:auto;}
</style>
</head>
<body>
<h1>¿Qué palabras tienes en tu partida?</h1>
<p>Pulsa sobre cada letra inicial de tus palabras para ver el objeto correspondiente.</p>
<div class="grid" id="grid"></div>
<div id="resultado"></div>

<h2>Lanzamiento del cohete</h2>
<p>Pulsa sobre una secuencia de imágenes para ver los números asociados.</p>
<div class="grid" id="grid-rocket"></div>
<div id="resultado-rocket"></div>

<script>
// Símbolos y objetos asociados con tooltip
const symbols = [
  {symbol:'https://raw.githubusercontent.com/Rafayp8/AshedEasyGuide/main/imagenes/%3E.png', object:'https://raw.githubusercontent.com/Rafayp8/AshedEasyGuide/main/imagenes/huesos.png', tooltip:'Obtención: 1. Tira un hacha al pie de un cadaver colgado en el granero. 2. Cuando el pie esta en el suelo quemalo con un Molotov'},
  {symbol:'https://raw.githubusercontent.com/Rafayp8/AshedEasyGuide/main/imagenes/L.png', object:'https://raw.githubusercontent.com/Rafayp8/AshedEasyGuide/main/imagenes/niebla.png', tooltip:'Obtención: Usa la mejora del rayo del coche contra unos objetos morados que aparecen en la niebla, ademas de soltar restos soltaran esta parte'},
  {symbol:'https://raw.githubusercontent.com/Rafayp8/AshedEasyGuide/main/imagenes/C.png', object:'https://raw.githubusercontent.com/Rafayp8/AshedEasyGuide/main/imagenes/hongo.png', tooltip:'Obtención: 1. En la cocina de la cabaña del lago Blackwood coge un bote de esporas. 2. Interactua con el bote en un caballo que esta fuera de la granja y espera 3 rondas'},
  {symbol:'https://raw.githubusercontent.com/Rafayp8/AshedEasyGuide/main/imagenes/C%20con%20punto.png', object:'https://raw.githubusercontent.com/Rafayp8/AshedEasyGuide/main/imagenes/ojos.png', tooltip:'Obtención: Mata a un zombie especial (Denizen) con la trampa de cuchillas'},
  {symbol:'https://raw.githubusercontent.com/Rafayp8/AshedEasyGuide/main/imagenes/L%20con%20punto.png', object:'https://raw.githubusercontent.com/Rafayp8/AshedEasyGuide/main/imagenes/oso.png', tooltip:'Obtención: Mata a un oso (Zursa) con el rayo del coche'}
];

const grid = document.getElementById('grid');
const resultado = document.getElementById('resultado');
let seleccion = [];

symbols.forEach(item=>{
  const card = document.createElement('div');
  card.className='card';
  const img = document.createElement('img');
  img.src = item.symbol;
  img.title = item.tooltip; // tooltip al pasar cursor
  card.appendChild(img);
  card.onclick = ()=>{
    if(seleccion.length >=3){
      seleccion = [];
    }
    if(!seleccion.includes(item.object)){
      seleccion.push(item.object);
      mostrarSeleccion();
    }
  };
  grid.appendChild(card);
});

function mostrarSeleccion(){
  resultado.innerHTML = '';
  seleccion.forEach(objImg=>{
    const imgEl = document.createElement('img');
    imgEl.src = objImg;
    imgEl.style.width = '100px';
    imgEl.style.margin = '5px';
    imgEl.title = symbols.find(s=>s.object === objImg)?.tooltip || '';
    resultado.appendChild(imgEl);
  });
}

// Lanzamiento del cohete - solo una opción activa a la vez
const rocketItems = [
  {label:'weapon.png', numbers:[22,4,0,15,14,13], url:'https://raw.githubusercontent.com/Rafayp8/AshedEasyGuide/main/imagenes/weapon.png'},
  {label:'launch.png', numbers:[11,0,20,13,2,7], url:'https://raw.githubusercontent.com/Rafayp8/AshedEasyGuide/main/imagenes/launch.png'},
  {label:'rocket.png', numbers:[17,14,2,10,4,19], url:'https://raw.githubusercontent.com/Rafayp8/AshedEasyGuide/main/imagenes/rocket.png'},
  {label:'engine.png', numbers:[4,13,6,8,13,4], url:'https://raw.githubusercontent.com/Rafayp8/AshedEasyGuide/main/imagenes/engine.png'}
];

const gridRocket = document.getElementById('grid-rocket');
const resultadoRocket = document.getElementById('resultado-rocket');
let seleccionRocket = [];

rocketItems.forEach(it=>{
  const card = document.createElement('div');
  card.className='card';
  const img = document.createElement('img');
  img.src = it.url;
  img.alt = it.label;
  card.appendChild(img);
  card.onclick = ()=>{
    seleccionRocket = [it.numbers];
    mostrarRocket();
  };
  gridRocket.appendChild(card);
});

function mostrarRocket(){
  resultadoRocket.innerHTML = '';
  seleccionRocket.forEach((nums)=>{
    resultadoRocket.innerHTML += nums.join(' - ') + '<br>';
  });
}
</script>
</body>
</html>
