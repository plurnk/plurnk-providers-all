# @plurnk/plurnk-providers-all

Batteries-included bundle for [plurnk-service](https://github.com/plurnk/plurnk-service)'s provider resolution. **It ships no code** — it's a single dependency that pulls in every first-party `@plurnk/plurnk-providers-*` daughter, **flat**, so one install surfaces them all to the framework's `discover()` scan.

```
npm i @plurnk/plurnk-providers @plurnk/plurnk-providers-all
```

Bundles:

| package | provider |
|---|---|
| `@plurnk/plurnk-providers-openrouter` | openrouter |
| `@plurnk/plurnk-providers-ollama` | ollama |
| `@plurnk/plurnk-providers-google` | google |
| `@plurnk/plurnk-providers-cloudflare` | cloudflare |
| `@plurnk/plurnk-providers-xai` | xai |

Standard OpenAI-compatible providers (`openai`, `groq`, `deepseek`, `mistral`, `together`, `fireworks`, `deepinfra`, `anthropic`, `bedrock`) need **no** package — the framework instantiates them directly from a frozen table (first-party Claude and AWS Bedrock included, via their bearer OpenAI-compat endpoints). This bundle is only the bespoke daughters.

## Why a bundle, not framework deps

The framework ([`@plurnk/plurnk-providers`](https://github.com/plurnk/plurnk-providers)) stays **contract-only** so it has no circular deps and so its `discover()` scan can find providers at the top level of `node_modules`. This aggregator depends on the daughters *directly* (not through the framework), so npm hoists them flat — discovery sees them. A **third party** publishes their own provider under their own scope (`@acme/llm-provider-foo`, declaring `plurnk.kind:"provider"`) and installs it alongside; the same scan finds it, no bundle membership required. The bundle is just the convenient default, never a gate.

Want a subset? Skip this and depend on the individual provider packages you want — discovery treats them identically.
