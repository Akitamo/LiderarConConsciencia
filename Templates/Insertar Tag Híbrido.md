<%*
// 1. Pedir el tag una sola vez y guardarlo en una variable
const tag = await tp.system.prompt("Nombre del tag?");

// 2. Comprobar si el usuario ha introducido un tag (y no ha cancelado)
if (tag) {
  // 3. Construir el texto final con un espacio al final
  const output = `#${tag} [tags:: ${tag}] `; 
  
  // 4. Insertar el texto
  tR += output;
} 
// Si el usuario cancela (tag es null), el script simplemente no hará nada.
%>

