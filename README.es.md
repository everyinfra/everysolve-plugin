# EverySolve — Flujos de CAPTCHA autorizados con el esquema descubierto en vivo

<!-- rq223-banner -->
<p align="center"><img alt="EverySolve — Flujos de CAPTCHA autorizados con el esquema descubierto en vivo" src="assets/banner-es.jpg" width="100%"></p>

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/hero-dark.svg">
    <source media="(prefers-color-scheme: light)" srcset="assets/hero-light.svg">
    <img alt="En un formulario de inicio de sesión, el agente detecta un desafío Turnstile, envía la URL y la clave del sitio al solucionador y devuelve el token a su propio flujo." src="assets/hero-light.svg" width="100%">
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
  &nbsp;<b>Dale una estrella al repo principal y recibe $1 de saldo.</b> <a href="https://everyinfra.com/es/docs?utm_source=github&utm_medium=readme&utm_campaign=everysolve-plugin&utm_content=star_line#quickstart">Cómo reclamarlo →</a>
</p>

<p align="center"><a href="README.md">English</a> · <a href="README.zh-CN.md">简体中文</a> · <b>Español</b></p>

> [!TIP]
> **Este repositorio contiene una sola skill: EverySolve.** El plugin completo de EveryInfra (10 skills, el servidor MCP remoto en `https://api.everyinfra.com/mcp` y la configuración para Claude Code, Codex, Cursor y VS Code) está en **[everyinfra/everyinfra-agent-plugins](https://github.com/everyinfra/everyinfra-agent-plugins)**. Los botones de arriba conectan el servidor MCP; la instalación del plugin en cada entorno está en el repo principal.

[Configuración](docs/setup.md) · [Flujo de trabajo](docs/workflow.md) · [Prompts](examples/prompts.md) · [Referencia de capacidades](docs/reference.md) · [Documentación de la API](https://api.everyinfra.com/docs) <sub>(en inglés)</sub>

<sub>Las cifras de la imagen salen del catálogo en vivo del 2026-10-24; la referencia es siempre el catálogo en vivo y el esquema de las herramientas.</sub>

EverySolve es una skill independiente de EveryInfra para integrar CAPTCHA autorizados a través de MCP. Descubre el esquema del desafío y la forma de la solución, conserva el contexto de sesión necesario y separa la respuesta del solucionador de la aceptación por parte de la aplicación de destino.

Úsala solo en sitios y flujos que tienes permiso para automatizar, por ejemplo uno que administras. Resolver el desafío no da acceso al sitio: esa autorización va aparte.

## Qué puedes hacer

- Ver qué tipos de desafío se admiten hoy y qué parámetros pide cada uno.
- Reunir solo las entradas que exige el desafío y conservar la sesión o el proxy cuando el contrato lo requiere.
- Aplicar la solución devuelta según su forma real dentro del flujo autorizado.

## Instalación

Es un paquete independiente con una sola skill y un flujo de trabajo **MCP**; no es un servicio nuevo. Necesita un entorno de agente compatible y el acceso configurado que describe la [guía de configuración](docs/setup.md). Validar el paquete en local no demuestra que la API esté disponible.

Revisa el contenido del repositorio y luego instálalo en Codex. Estos comandos añaden un catálogo respaldado por GitHub, no un aval de ningún marketplace oficial:

```bash
codex plugin marketplace add everyinfra/everysolve-plugin
codex plugin add everysolve@everysolve-plugin
```

Para una copia local, cambia la fuente del primer comando por `.`. La [guía de configuración](docs/setup.md) también cubre Claude Code y la conexión al servicio, que va aparte.

Con el acceso configurado, prueba:

> Para este sitio que administro, revisa los tipos de desafío admitidos y enumera las entradas obligatorias. Todavía no resuelvas nada.

Este primer prompt solo inspecciona o prepara. Revisa cualquier operación de pago o efecto externo antes de seguir.

## Cómo funciona

1. Confirma la autorización para el destino exacto y la operación pedida.
2. Usa `everyinfra_list_captcha_types` para conocer el tipo, los parámetros, la disponibilidad y la forma de la solución.
3. Reúne solo las entradas obligatorias; conserva el proxy o la identidad de sesión si el contrato vigente lo exige.
4. Llama a `everyinfra_solve_captcha` solo para el destino aprobado y un desafío admitido.
5. Interpreta la forma de la solución y aplícala solo dentro del flujo autorizado que le corresponde.

**Un buen resultado:** una solución admitida o un estado de fallo explícito, aplicados según su forma real. Un token devuelto no prueba que el sitio lo haya aceptado.

## Límites y seguridad

- No se garantiza una tasa de resolución ni compatibilidad universal con todos los tipos de desafío.
- No se reutilizan tokens entre destinos o sesiones distintos.
- Nada de adivinar tipos no admitidos, accesos no autorizados ni flujos de abuso de cuentas.

El paquete trae una sola skill: no concede permisos ni registra una segunda conexión MCP. No pongas credenciales en prompts, archivos del repositorio, capturas ni registros compartidos. Descubrir, ejecutar, cobrar y obtener un resultado externo final son estados distintos. Consulta la [política de seguridad](SECURITY.md).

## Preguntas frecuentes y validación

Las preguntas frecuentes, la comprobación sin conexión (`python3 scripts/validate.py`) y la guía para contribuir están en el [README en inglés](README.md#frequently-asked-questions).

Mantenido por [EveryInfra](https://everyinfra.com/es?utm_source=github&utm_medium=readme&utm_campaign=everysolve-plugin&utm_content=footer). Licencia [Apache-2.0](LICENSE).
