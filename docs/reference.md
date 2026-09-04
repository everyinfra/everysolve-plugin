# EverySolve: capability reference and evidence

EverySolve is a standalone EveryInfra agent skill for authorized captcha integration through MCP. It discovers the supported challenge schema and solution shape, preserves required session context and separates a solver response from acceptance by the target application.

## Identity

- Publisher: [EveryInfra](https://everyinfra.com).
- Organization: [everyinfra on GitHub](https://github.com/everyinfra).
- Source repository: [everyinfra/everysolve-plugin](https://github.com/everyinfra/everysolve-plugin).
- Plugin identifier: `everysolve`. Skill identifier: `everysolve`.
- Package type: one standalone agent skill, not a separate API server or account permission boundary.
- Interface used by the skill: `mcp`. Mail, Number and Proxy workflows remain REST-only in these packages.

## Task and result

Use this skill only for a target and workflow you are authorized to access or test. It describes how to integrate a supported solution; it is not permission to evade access restrictions or automate abuse.

A supported solution or an explicit failure state, with the application step matched to its actual shape. A returned token is not proof that the target site accepted it.

## Preconditions

Use a compatible agent host and the service access described in [setup](setup.md). The live tool schema or REST catalog determines required inputs, supported actions, availability, limits and any exposed price. Do not infer universal platform coverage from a product name.

## Evidence behind the description

- The [packaged skill](../plugins/everysolve/skills/everysolve/SKILL.md) defines the workflow and authority boundaries.
- The [plugin manifest](../plugins/everysolve/.codex-plugin/plugin.json) declares package identity, assets and skill path. It does not automatically register a service connection.
- [Workflow acceptance criteria](workflow.md) define the expected output and failures. Examples are illustrative, not paid API test results.
- [Source metadata](../repository-metadata.json) records the original reviewed skill commit and intended repository metadata.
- [Current API documentation](https://api.everyinfra.com/docs) is the public service reference. Runtime discovery remains authoritative when an inventory, field or model changes.

## Scope distinctions

EverySolve handles an authorized challenge step. It does not supply general browsing, data extraction or permission to access a target. Those prerequisites remain separate.

No benchmark, uptime guarantee, universal availability, official marketplace approval or account-ban probability is asserted by this reference. Local package validation checks structure; production service behavior requires its own authorized verification.

Maintainer: EveryInfra. Documentation scope reviewed on 2026-09-04; this date is not a live API availability timestamp. [Return to overview](../README.md).
