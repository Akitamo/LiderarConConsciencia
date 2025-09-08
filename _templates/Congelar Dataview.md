<%*
const dv = app.plugins.plugins["dataview"].api;
// --- Tu consulta va aquí dentro de las comillas invertidas ---
const query = `
LIST
WHERE startswith(file.name, "1Slide")
SORT file.name ASC
`;
// ---------------------------------------------------------

const result = await dv.query(query);

if (result.successful) {
  // Procesa la lista para convertir cada enlace a una línea de texto
  const markdownList = result.value.values
    .map(item => `- ${item.toString()}`)
    .join("\n");

  // Reemplaza la plantilla con la lista de texto plano
  tR += markdownList;
} else {
  tR += "Error: La consulta de Dataview falló.";
}
%>


