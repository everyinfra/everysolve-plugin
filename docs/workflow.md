# EverySolve workflow and acceptance criteria

## Intended outcome

A supported solution or an explicit failure state, with the application step matched to its actual shape. A returned token is not proof that the target site accepted it.

## Execution contract

1. Confirm authorization for the exact target and requested operation.
2. Use everyinfra_list_captcha_types to discover type, parameters, availability and solution form.
3. Collect only required challenge inputs; preserve proxy or session identity where the live contract requires it.
4. Call everyinfra_solve_captcha only for the approved target and supported challenge.
5. Interpret the returned solution shape and apply it only within the matching authorized workflow.

## Failure handling

If discovery or catalog access fails, stop before a paid action. Read required fields from the current schema instead of copying a remembered payload. Report unavailable capabilities and denied account scopes as distinct conditions. Do not broaden keys, repeatedly retry a permanent error or substitute an unrelated mechanism without disclosure.

- No guaranteed solution rate or universal support for challenge types.
- No token reuse across unrelated targets or sessions.
- No unsupported-type fallback guesses, unauthorized access or account-abuse workflows.

## Worked request boundaries

### Scenario 1

> For this site that I administer, inspect the supported challenge types and list required inputs. Do not solve anything yet.

Accepted behavior: preserve the stated scope; discover the required contract and stop at the explicit no-action boundary. Any broader operation requires new authority.

### Scenario 2

> Review this authorized integration: explain whether the returned solution is a token, cookie or another shape and how that affects the next step.

Accepted behavior: preserve the stated scope; discover the required contract and stop at the explicit no-action boundary. Any broader operation requires new authority.

### Scenario 3

> A challenge solution failed in my authorized test. Check the required session context before proposing another paid attempt.

Accepted behavior: preserve the stated scope; discover the required contract and stop at the explicit no-action boundary. Any broader operation requires new authority.


These are illustrative prompts, not captured API responses or claims of successful live execution. They deliberately avoid guessed JSON payloads and fabricated prices. See [prompt acceptance fixtures](../examples/acceptance.json) for the offline safety assertions.

## Result review

A supported solution or an explicit failure state, with the application step matched to its actual shape. A returned token is not proof that the target site accepted it.

Check original results rather than relying on the agent's summary alone. Preserve response status and evidence only to the extent safe; redact personal or secret fields. If billing is absent from the response, say it is not observable there rather than inferring a charge from HTTP success.

## Related decision

EverySolve handles an authorized challenge step. It does not supply general browsing, data extraction or permission to access a target. Those prerequisites remain separate.

Return to [README](../README.md) or [setup](setup.md).
