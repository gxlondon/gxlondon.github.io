
<html>
<head>
<title>Brent-o-Matic</title>
<link rel="shortcut icon" href="favicon.ico" type="image/x-icon" />
  <link rel="shortcut icon" href="favicon.ico" type="image/x-icon">
  <link rel="shortcut icon" href="/favicon.ico" type="image/x-icon">
  <link rel="shortcut icon" href="/favicon.ico" type="image/x-icon" />
<style>
// Ocultar o desocultar cabecera GitHub
//   header {
//  display: none;
//} 
   </style>
</head>
<body>
<!--   <p> <center><h1>Cierre del Brent</h1></center><p>  -->Introducir el precio con punto decimal (70.55)<p><br>
<!--  FORMULARIO DE ENTRADA DE DATOS EN HTML  --><center><table style="width:70%; border:0;"><tr><td style="width:30%">
  <b>Precio de ayer</b>:<br>
  <b>Precio de hoy</b>: 
    </td>
    <td style="width:20%">
      <input id="ayer" maxlength="6" size="5" style="text-align:center;"><br>
      <input id="hoy" maxlength="6" size="5" style="text-align:center;">
    </td>
<td style="width:50%">
  <form name="fomul"> 
Mes de referencia:<br> <select id="formulario" name="miSelect"> 
   <option value="enero">Enero</option>
   <option value="febrero">Febrero</option>
   <option value="marzo">Marzo</option>
   <option value="abril">Abril</option>
   <option value="mayo">Mayo</option>
   <option value="junio">Junio</option>
   <option value="julio">Julio</option>
   <option value="agosto">Agosto</option> 
   <option value="septiembre">Septiembre</option>
   <option value="octubre">Octubre</option>
   <option value="noviembre" selected>Noviembre</option>
   <option value="diciembre">Diciembre</option>
</select></form></td></tr></table></center>
<center><button id="say">¡Escribe!</button></center><br><div id="result"></div>
<script>

/* DEFINICIÓN DE OPERACIONES ARITMÉTICAS */
var ops = {
        sumar: function sumarNumeros(n1, n2) {
            return (parseFloat(n1) + parseFloat(n2));
        },

        restar: function restarNumeros(n1, n2) {
            return (parseFloat(n1) - parseFloat(n2));
        },
        
        multiplicar: function multiplicarNumeros(n1, n2) {
            return (parseFloat(n1) * parseFloat(n2));
        },

        dividir: function dividirNumeros(n1, n2) {
            return (parseFloat(n1) / parseFloat(n2));
        }


    };


/* ADQUIERE NÚMERO DE DÍA Y NÚMERO DE MES */
var date = new Date().getDate();
var d = new Date();

/* TRANSFORMA NÚMERO DE MES A TEXTO */
var month = new Array();
month[0] = "ene";
month[1] = "feb";
month[2] = "mar";
month[3] = "abr";
month[4] = "may";
month[5] = "jun";
month[6] = "jul";
month[7] = "ago";
month[8] = "sep";
month[9] = "oct";
month[10] = "nov";
month[11] = "dic";
var mes = month[d.getMonth()];

/* LEE LOS DATOS DEL FORMULARIO AL PULSAR EL BOTÓN */
function say_hi() {
    var ayer = document.getElementById('ayer').value;
    var hoy = document.getElementById('hoy').value;
    var mes_referencia = document.getElementById('formulario').value;

    /* RESTA EL PRECIO DE AYER MENOS DEL DE HOY */
    var diferencia = ops.restar(ayer, hoy);
 
    /* MULTIPLICA EL RESULTADO DE LA RESTA POR 100 */
    var diferencia100 = ops.multiplicar(diferencia, 100);
   
    if (diferencia<0) {  /* SI LA RESTA ES NEGATIVA, EL PRECIO HA SUBIDO */
       var diferenciaentera = ops.multiplicar(diferencia,-1); /* TRANSFORMA LA DIFERENCIA A POSITIVO */
      var diferencia_entera_dos = diferenciaentera.toFixed(2);
       var subebaja = 'sube';
       var masmenos = 'm\u00E1s';
       var incredesce = "incremento";

   } else {  /* SI LA RESTA ES POSITIVA, EL PRECIO HA BAJADO */
            var subebaja = 'baja'; 
            var masmenos = 'menos';
            var incredesce = 'descenso';

          var diferenciaentera = diferencia;
          var diferencia_entera_dos = diferencia.toFixed(2); /* DEJA LA DIFERENCIAC CON SOLO DOS DECIMALES */
}

/* CALCULA EL TANTO POR CIENTO */
 var dif100 = ops.multiplicar (diferenciaentera,100);
 var porcentaje = ops.dividir(dif100, ayer).toFixed(2);

/* REEMPLAZA LOS PUNTOS POR COMAS EN LOS RESULTADOS PARA MOSTRAR */
var porcentaje_coma = porcentaje.toString().replace(/\./g,','); 

var diferencia_entera_dos_coma = diferencia_entera_dos.toString().replace(/\./g,',');

var ayer_coma = ayer.toString().replace(/\./g,',');

var hoy_coma = hoy.toString().replace(/\./g,',');

/* IMPRIME EL TEXTO FINAL */

 var html1 = '<div style="background-color:AliceBlue; padding: 8px 8px 8px 8px;"><font style="font:16px courier;">PETR\u00D3LEO BRENT CIERRE <p> El petr\u00F3leo Brent ' + subebaja + ' un  ' + porcentaje_coma + ' %, hasta ' + hoy_coma + ' d\u00F3lares <p> Londres, ' + date + ' ' + mes + ' (EFE).- El precio del barril de petr\u00F3leo Brent para entrega en ' + mes_referencia + ' termin\u00F3 hoy en el mercado de futuros de Londres en ' + hoy_coma + ' d\u00F3lares, un  ' + porcentaje_coma + ' %  ' + masmenos + ' que al finalizar la sesi\u00F3n anterior.<br> El crudo del mar del Norte, de referencia en Europa, concluy\u00F3 la jornada en el International Exchange Futures con un ' + incredesce + ' de  ' + diferencia_entera_dos_coma + ' d\u00F3lares respecto a la \u00FAltima negociaci\u00F3n, cuando cerr\u00F3 en ' + ayer_coma + ' d\u00F3lares.</font></div>';

 
   
    document.getElementById('result').innerHTML = html1;
}
 
document.getElementById('say').addEventListener('click', say_hi);

</script>

