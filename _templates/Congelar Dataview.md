<%*
const dv = app.plugins.plugins["dataview"].api;
// Pedimos solamente la ruta del archivo, que es el único dato 100% fiable
const query = `
TABLE WITHOUT ID file.path
WHERE startswith(file.name, "1Slide")
SORT file.name ASC
`;
const result = await dv.query(query);

if (result.successful) {
  const markdownList = result.value.values
    .map(row => {
      // row[0] ahora contiene la ruta completa, ej: "Carpeta/Mi Archivo.md"
      const path = row[0]; 
      
      // 1. Extraemos el nombre del archivo de la ruta
      const filename = path.split('/').pop(); 
      
      // 2. Quitamos la extensión ".md" para obtener el texto a mostrar
      const displayText = filename.slice(0, -3);
      
      // 3. Construimos el enlace Markdown estándar y final
      return `- [${displayText}](./${encodeURI(path)})`;
    })
    .join("\n");
  
  tR += markdownList;
} else {
  tR += "Error: La consulta de Dataview falló.";
}
%>


