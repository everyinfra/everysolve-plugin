# EverySolve plugin

Handle authorized captcha workflows with EverySolve MCP. Discover supported challenge types, preserve required session context and interpret the returned solution shape.

This package contains only `everysolve`. It is a skills-only plugin: configure the approved EveryInfra service connection in the host before using it. It does not install other skills, register a new MCP server or broaden API permissions.

A supported solution or an explicit failure state, with the application step matched to its actual shape. A returned token is not proof that the target site accepted it.

- No guaranteed solution rate or universal support for challenge types.
- No token reuse across unrelated targets or sessions.
- No unsupported-type fallback guesses, unauthorized access or account-abuse workflows.

Repository documentation and installation guidance accompany the source checkout. Current API documentation: https://api.everyinfra.com/docs
