# CLAUDE.md: titan-web

The TITAN web UI: sign-in, chat, node management and every domain in a browser. It is published as an image that contains the built files only; the node's nginx serves them.

Read and follow, in this order:

1. [Rules for AI agents](shared/docs/development/ai-agents.md) — what you may
   and may not do. They override your defaults.
2. [Development rules](shared/docs/development/rules.md) — how we work, for
   every repository.
3. [Documentation index](shared/docs/README.md) — product, architecture,
   decisions, build plan.

`shared/` is the `titan-shared` submodule. Never edit files under it from this
repository; change `titan-shared` through its own pull request.

## Stack and commands

- TypeScript in strict mode; ESLint with zero warnings; Prettier; unit tests; end-to-end tests in Chromium, Firefox and WebKit under the node's real security headers.
- Design tokens come from `shared/design/`.

Commands are added here as the code arrives.

## Rules specific to this repository

- The page runs under a strict Content-Security-Policy with Trusted Types: no inline scripts, no `eval`, no third-party assets. Check every new library with an end-to-end test under the CSP.
- The session lives only in an HttpOnly cookie; never read or store a token in JavaScript or browser storage.
- Every user-visible string goes through the translation layer; English, Russian and Ukrainian first.
- Losing the connection never clears data on screen and never shows a full-page spinner; writes are never queued.
- Never render server text as raw HTML; Markdown only through a sanitising renderer.

## Before committing

Run this checklist before every commit
([development rules, "Before committing"](shared/docs/development/rules.md#before-committing)).
The commands are settled as the code arrives.

1. The format check, lint (zero warnings) and type check pass.
2. Unit tests pass for the screens and files the commit touches. The full
   suite runs in CI.
3. If dependencies or the build configuration changed: the production build
   succeeds.
4. If a library was added or the security headers changed: the end-to-end
   test under the CSP passes in at least one browser.
5. If user-visible text changed: every language file has the same keys.
6. If Markdown or the `shared/` pointer changed:
   `python3 shared/scripts/check_links.py .` prints nothing.
