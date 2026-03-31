# Awesome Claude Code Post-Leak Insights

A curated list of high-signal analyses, design notes, and discussions emerging from the Claude Code leak (2026-03-31).

On 2026-03-31, security researcher [Chaofan Shou](https://x.com/Fried_rice/status/2038894956459290963) discovered that Anthropic shipped a source map file in the Claude Code npm package, exposing the full unobfuscated TypeScript source (~1,900 files, 512K+ lines).

This is **not** a general Claude Code resource list, and it is **not** a mirror of leaked proprietary code.  
The focus here is narrower: collecting the most useful post-leak materials that help readers understand Claude Code’s architecture, safety model, workflow design, and extension surface.

> This event is still unfolding — the list is being actively maintained. If you’ve seen a high-quality post-leak analysis that isn’t listed here, PRs and Issues are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md) for details.

## Contents

- [Discussions](#discussions)
- [Analysis](#analysis)

## Discussions

- [Hacker News thread](https://news.ycombinator.com/item?id=47584540) - Highlights include regex-based sentiment detection instead of using their own models, anti-distillation defenses in API requests, and a code quality teardown of `print.ts`.
- [r/LocalLLaMA thread](https://www.reddit.com/r/LocalLLaMA/comments/1s8ijfb/claude_code_source_code_has_been_leaked_via_a_map/) - The most upvoted thread on this leak. Includes a detailed hidden-features breakdown (KAIROS, Buddy, Undercover Mode, Coordinator Mode) and discussion on local-model integration possibilities.
- [r/ClaudeAI thread](https://www.reddit.com/r/ClaudeAI/comments/1s8ifm6/claude_code_source_code_has_been_leaked_via_a_map/) - Notable for a deep dive into the `cch` attestation mechanism (custom Bun runtime, Zig-compiled token generation), plus findings on Capybara model variants and frustration telemetry.

## Analysis

- [Kuberwastaken / claude-code](https://github.com/Kuberwastaken/claude-code) - The most detailed post-leak breakdown so far, covering the 40+ tool system, 46K-line Query Engine, multi-agent swarm orchestration, and unreleased features (BUDDY, KAIROS, ULTRAPLAN, Coordinator Mode).
- [Claude Code’s Entire Source Code Was Just Leaked via npm Source Maps — Here’s What’s Inside](https://dev.to/gabrielanhaia/claude-codes-entire-source-code-was-just-leaked-via-npm-source-maps-heres-whats-inside-cjo) - A readable first-wave summary of the sourcemap exposure and key findings. Note: the author promotes his own product (Hermes IDE) throughout.

## License

MIT for original content in this repository.  
Linked articles, screenshots, quoted excerpts, and other third-party materials remain under their respective owners' terms.