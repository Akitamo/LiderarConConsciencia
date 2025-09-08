<%*
const dv = app.plugins.plugins["dataview"].api;
const query = `
TABLE WITHOUT ID file.path
WHERE startswith(file.name, "1Slide")
SORT file.name ASC
`;
const result = await dv.query(query);

if (result.successful) {
  const markdownList = result.value.values
    .map(row => {
      const path = row[0]; // La ruta completa del archivo
      const filename = path.split('/').pop(); // Extraemos SÓLO el nombre del archivo
      const displayText = filename.slice(0, -3);
      
      // --- LA LÍNEA CORREGIDA ---
      // Usamos 'filename' en lugar de 'path' para construir el enlace relativo.
      return `- [${displayText}](./${encodeURI(filename)})`;
    })
    .join("\n");
  
  tR += markdownList;
} else {
  tR += "Error: La consulta de Dataview falló.";
}
%>


