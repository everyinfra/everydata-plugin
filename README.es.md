# EveryData — Consulta datos públicos estructurados con MCP

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/hero-dark.svg">
    <source media="(prefers-color-scheme: light)" srcset="assets/hero-light.svg">
    <img alt="El agente lee el catálogo en vivo, elige TikTok y su acción de búsqueda, revisa el parámetro obligatorio y los campos, llama a la API y recibe registros en JSON." src="assets/hero-light.svg" width="100%">
  </picture>
</p>

<p align="center">
  <a href="https://cursor.com/en/install-mcp?name=everyinfra&config=eyJ1cmwiOiJodHRwczovL2FwaS5ldmVyeWluZnJhLmNvbS9tY3AiLCJoZWFkZXJzIjp7IkF1dGhvcml6YXRpb24iOiJCZWFyZXIgPEFQSSBLZXk%2BIn19"><img src="https://img.shields.io/badge/Instalar_en_Cursor-2F363D?style=for-the-badge&logo=cursor&logoColor=white" alt="Instalar en Cursor"></a>
  <a href="https://vscode.dev/redirect/mcp/install?name=everyinfra&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.everyinfra.com%2Fmcp%22%2C%22headers%22%3A%7B%22Authorization%22%3A%22Bearer%20%3CAPI%20Key%3E%22%7D%7D"><img src="https://img.shields.io/badge/Instalar_en_VS_Code-0065A9?style=for-the-badge&logo=githubcopilot&logoColor=white" alt="Instalar en VS Code"></a>
  <a href="https://github.com/everyinfra/everyinfra-agent-plugins/blob/main/i18n/README.es.md#claude-code"><img src="https://img.shields.io/badge/Claude_Code-un_comando-B4532A?style=for-the-badge&logo=claude&logoColor=white" alt="Claude Code: un comando"></a>
  <a href="https://github.com/everyinfra/everyinfra-agent-plugins/blob/main/i18n/README.es.md#codex"><img src="https://img.shields.io/badge/Codex-un_comando-2F363D?style=for-the-badge" alt="Codex: un comando"></a>
</p>

<p align="center">
  <a href="https://github.com/everyinfra/everyinfra-agent-plugins/stargazers"><img src="https://img.shields.io/github/stars/everyinfra/everyinfra-agent-plugins?style=social" alt="GitHub stars of everyinfra-agent-plugins"></a>
  &nbsp;<b>Dale una estrella al repo principal y recibe $1 de saldo.</b> <a href="https://everyinfra.com/es/docs?utm_source=github&utm_medium=readme&utm_campaign=everydata-plugin&utm_content=star_line#quickstart">Cómo reclamarlo →</a>
</p>

<p align="center"><a href="README.md">English</a> · <a href="README.zh-CN.md">简体中文</a> · <b>Español</b></p>

> [!TIP]
> **Este repositorio contiene una sola skill: EveryData.** El plugin completo de EveryInfra (10 skills, el servidor MCP remoto en `https://api.everyinfra.com/mcp` y la configuración para Claude Code, Codex, Cursor y VS Code) está en **[everyinfra/everyinfra-agent-plugins](https://github.com/everyinfra/everyinfra-agent-plugins)**. Los botones de arriba conectan el servidor MCP; la instalación del plugin en cada entorno está en el repo principal.

[Configuración](docs/setup.md) · [Flujo de trabajo](docs/workflow.md) · [Prompts](examples/prompts.md) · [Referencia de capacidades](docs/reference.md) · [Documentación de la API](https://api.everyinfra.com/docs) <sub>(en inglés)</sub>

<sub>Las cifras de la imagen salen del catálogo en vivo del 2026-10-24; la referencia es siempre el catálogo en vivo y el esquema de las herramientas.</sub>

> **Actualización (2026-10-09):** se retiraron las dos herramientas de limpieza de datos. Para limpiar, clasificar,
> extraer o resumir los datos que recopilas, usa la [API de IA](https://everyinfra.com/en/products/ai):
> `POST /api/v1/chat/completions`, compatible con OpenAI, también disponible como la herramienta MCP
> `everyinfra_chat`. Es gratuita para las cuentas que han recargado saldo, con límites por minuto que dependen
> del total recargado.

EveryData es una skill independiente de EveryInfra para consultar datos públicos estructurados a través de MCP. Antes de pedir registros, descubre qué acciones existen hoy y cuál es su esquema en vivo, de modo que los parámetros obligatorios, los campos devueltos y los límites de paginación salen del contrato real de la API y no de una suposición.

Úsala para una consulta acotada en la que importan más los registros que una respuesta en prosa: una entidad, una lista de registros públicos o una acción concreta de una plataforma. Lo que se puede consultar hoy lo decide el catálogo en vivo.

## Qué puedes hacer

- Encontrar la acción compatible con la tarea antes de elegir parámetros.
- Revisar los campos obligatorios, los filtros opcionales y el tamaño máximo de página.
- Devolver los registros disponibles y distinguir entre respuestas vacías, parciales y fallidas.

## Instalación

Es un paquete independiente con una sola skill y un flujo de trabajo **MCP**; no es un servicio nuevo. Necesita un entorno de agente compatible y el acceso configurado que describe la [guía de configuración](docs/setup.md). Validar el paquete en local no demuestra que la API esté disponible.

Revisa el contenido del repositorio y luego instálalo en Codex. Estos comandos añaden un catálogo respaldado por GitHub, no un aval de ningún marketplace oficial:

```bash
codex plugin marketplace add everyinfra/everydata-plugin
codex plugin add everydata@everydata-plugin
```

Para una copia local, cambia la fuente del primer comando por `.`. La [guía de configuración](docs/setup.md) también cubre Claude Code y la conexión al servicio, que va aparte.

Con el acceso configurado, prueba:

> Busca la capacidad de datos públicos vigente para esta plataforma y enumera los parámetros obligatorios antes de hacer cualquier petición de pago.

Este primer prompt solo inspecciona o prepara. Revisa cualquier operación de pago o efecto externo antes de seguir.

## Cómo funciona

1. Usa `everyinfra_list_capabilities` para identificar la plataforma y la acción adecuadas.
2. Lee el esquema en vivo de la acción y los campos de disponibilidad, `max_limit` y precio que devuelva.
3. Relaciona la petición con los parámetros obligatorios; si de verdad falta un dato, pregunta en lugar de inventarlo.
4. Llama a `everyinfra_call_api` con la consulta autorizada y respeta el contrato de paginación vigente.
5. Devuelve los campos útiles e indica qué resultados son parciales, qué campos faltan y qué se cobró.

**Un buen resultado:** registros con los campos pedidos cuando existen y una explicación clara de lo que falta o quedó a medias. Una página correcta no equivale a cubrir toda la plataforma.

## Límites y seguridad

- No hay un inventario de plataformas fijado en el código ni promesa de campos que no estén en el esquema en vivo.
- No se garantiza la completitud histórica, ni registros privados, ni acceso sin restricciones a una plataforma.
- Esta skill no promete un CSV validado; si el entregable es un archivo, usa el flujo de exportación (Data Export).

El paquete trae una sola skill: no concede permisos ni registra una segunda conexión MCP. No pongas credenciales en prompts, archivos del repositorio, capturas ni registros compartidos. Descubrir, ejecutar, cobrar y obtener un resultado externo final son estados distintos. Consulta la [política de seguridad](SECURITY.md).

## Preguntas frecuentes y validación

Las preguntas frecuentes, la comprobación sin conexión (`python3 scripts/validate.py`) y la guía para contribuir están en el [README en inglés](README.md#frequently-asked-questions).

Mantenido por [EveryInfra](https://everyinfra.com/es?utm_source=github&utm_medium=readme&utm_campaign=everydata-plugin&utm_content=footer). Licencia [Apache-2.0](LICENSE).
