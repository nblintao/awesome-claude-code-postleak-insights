# Awesome Claude Code Post-Leak Insights

A curated list of high-signal analyses, design notes, and discussions emerging from the Claude Code npm sourcemap leak of 2026-03-31.

Security researcher [Chaofan Shou](https://x.com/Fried_rice/status/2038894956459290963) discovered that Anthropic shipped a source map file in the Claude Code npm package, exposing the full unobfuscated TypeScript source (~1,900 files, 512K+ lines).

This is **not** a general Claude Code resource list, and it is **not** a mirror of leaked proprietary code.  
The focus here is narrower: collecting the most useful post-leak materials that help readers understand Claude Code’s architecture, safety model, workflow design, and extension surface.

> This event is still unfolding — the list is being actively maintained. If you’ve seen a high-quality post-leak analysis that isn’t listed here, PRs and Issues are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md) for details.

## Discussions

- [Hacker News thread](https://news.ycombinator.com/item?id=47584540) - Highlights include regex-based sentiment detection instead of using their own models, anti-distillation defenses in API requests, and a code quality teardown of `print.ts`.
- [r/LocalLLaMA thread](https://www.reddit.com/r/LocalLLaMA/comments/1s8ijfb/claude_code_source_code_has_been_leaked_via_a_map/) - The most upvoted thread on this leak. Includes a detailed hidden-features breakdown (KAIROS, Buddy, Undercover Mode, Coordinator Mode) and discussion on local-model integration possibilities.
- [r/ClaudeAI thread](https://www.reddit.com/r/ClaudeAI/comments/1s8ifm6/claude_code_source_code_has_been_leaked_via_a_map/) - Notable for a deep dive into the `cch` attestation mechanism (custom Bun runtime, Zig-compiled token generation), plus findings on Capybara model variants and frustration telemetry.

## Analysis
- [Fake tools, frustration regexes, undercover mode, and more](https://alex000kim.com/posts/2026-03-31-claude-code-source-leak/) — Focus: Security & Anti-Distillation Mechanisms
    - The most code-grounded post-leak analysis to date, with direct file and line references throughout. Covers the two-layer anti-distillation system (fake tool injection + cryptographically-signed connector-text summarization), the ~90-line Undercover Mode implementation, frustration detection via regex instead of a model, and the Zig-based `cch` attestation stack. Also flags a 250K-token autoCompact bug and the 5,594-line `print.ts` with a single 3,167-line function. Hit HN front page (1,054 points, 402 comments).
- [Claude Code’s Entire Source Code Was Just Leaked via npm Source Maps — Here’s What’s Inside](https://dev.to/gabrielanhaia/claude-codes-entire-source-code-was-just-leaked-via-npm-source-maps-heres-whats-inside-cjo) — Focus: Production Architecture & Tech Stack
    - A professional architectural audit from a developer's perspective. It deconstructs the current production-grade system, detailing five major subsystems: the Tool System, Query Engine, Multi-Agent Orchestration, IDE Bridge, and Persistent Memory. It highlights the engineering rationale behind choosing Bun, React+Ink, and Zod v4, while offering critical security lessons on build pipeline vulnerabilities.
- [Claude Code's Entire Source Code Got Leaked via a Sourcemap in npm, Let's Talk About it](https://kuber.studio/blog/AI/Claude-Code%27s-Entire-Source-Code-Got-Leaked-via-a-Sourcemap-in-npm%2C-Let%27s-Talk-About-it) — Focus: Future Roadmap & Hidden Features
    - A "treasure hunt" style deep-dive into the codebase's hidden secrets. This post prioritizes unreleased features and internal lore, covering the BUDDY Tamagotchi-style pet system, the KAIROS "always-on" proactive assistant, and the ULTRAPLAN 30-minute remote orchestration mode. It also uncovers Anthropic’s internal "Undercover Mode" and model codenames (Tengu, Fennec). Essential reading for anyone wanting to see where the product is headed next.
- [How an AI Reads the Web: A Deep Dive into Claude Code’s WebFetchTool](https://medium.com/@nblintao/how-an-ai-reads-the-web-a-deep-dive-into-claude-codes-webfetchtool-0abee4446343) — Focus: WebFetchTool Design
    - The first post-leak analysis to deep-dive into a single subsystem. Traces how WebFetchTool balances security (domain whitelisting, blacklist pre-checks, redirect sandboxing), performance (Haiku-based summarization, lazy-loaded Turndown), and copyright compliance across its 1,173-line implementation.
- [Claude Code Source Leak: Production AI Architecture Patterns from 512,000 Lines](https://discuss.huggingface.co/t/claude-code-source-leak-production-ai-architecture-patterns-from-512-000-lines/174846) — Focus: Context Compression & AutoDream
    - A concise, structured breakdown of two architecture patterns not covered elsewhere: the three-layer Context Compression pipeline (MicroCompact → AutoCompact → Full Compact) and the four-phase AutoDream memory consolidation flow. Brief but information-dense.
- [Claude Code source has been available for 13 months, and nothing happened — why?](https://thehuman2ai.com/blog/claude-code-source-leak) - A timeline piece tracing both leak incidents (2025-02 and 2026-03) and arguing why source visibility doesn’t threaten the product.

## More

Looking for broader coverage? See [MORE.md](MORE.md) for additional articles, news reports, and source mirrors that didn't make the curated list but may still be useful for broader context.

## License

MIT for original content in this repository.  
Linked articles, screenshots, quoted excerpts, and other third-party materials remain under their respective owners' terms.