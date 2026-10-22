# Recon: live agent UI, animation, and 3-level observability (Receipts)

Date: 2026-10-21. Type: technical + choosing between candidates. Mode: parallel web search (Exa, SearXNG not needed) plus `opencli twitter search`. Access date for every source: 2026-10-21. Claims marked (unverified) were not confirmed from a fetched page. Nothing here is from training data alone.

## Answer (one paragraph)

Build the live claim table with Motion (MIT) using the small `m` + `LazyMotion` path for row enter, state-change and expand animations, and copy shadcn's new `Trace` / AI Elements patterns (copy-in code, no runtime package) as the visual language for the steps inside a receipt. Do not adopt a chat framework (assistant-ui, CopilotKit, AI SDK `useChat`) as the backbone: Receipts is a table of claims, not a chat thread, so a plain Hono `streamSSE` event stream reduced into React state is simpler and keeps the bundle small. Use a three-level reveal modeled on what current AI search products, agent-activity logs and eval-platform trace views do: level 1 a glance (one live row with a status chip), level 2 the receipt (words vs source line, link, a short step list), level 3 the full trace (tool inputs/outputs, latency, tokens, retrieval scores) behind an explicit "Show full trace" control plus a link to the Langfuse trace.

## Ranked recommendations

| # | Tool | What it is for in Receipts | Free / license | Bundle note | Source |
|---|------|----------------------------|----------------|-------------|--------|
| 1 | Motion for React (`m`, `LazyMotion`, `AnimatePresence`, layout) | Rows entering, status-chip changes, receipt expand/collapse, reduced-motion handling | MIT core; Motion+ is a separate paid tier we do not need | `motion` component cannot tree-shake below 43 kB; `m` + `LazyMotion` is just over 5 kB initial; `useAnimate` mini 3.3 kB | https://motion.dev/docs/react-reduce-bundle-size ; https://github.com/motiondivision/motion/ |
| 2 | shadcn `Trace` + AI Elements patterns (Tool, Reasoning, Chain of Thought, Inline Citation, Sources, Plan) | Visual shape of the step list and the citation hover in the receipt; one consistent line shape per step | Copy-in via the shadcn CLI (`npx shadcn@4.22.1 add trace`, the version `STACK.md` pins; the repo uses npm); page says "no package to install"; license not stated on the page (verify in repo before copying) | No runtime package; cost is the copied source plus shadcn primitives | https://ui.shadcn.com/docs/ai-elements ; https://ui.shadcn.com/docs/components/base/trace |
| 3 | Hono `streamSSE` + own event reducer (no library) | Server pushes `claim.state`, `tool.step`, `claim.done` events; client reduces into rows | Hono is already in stack | Zero client library; Hono docs note Wrangler may need `Content-Encoding: Identity` for streaming | https://hono.dev/docs/helpers/streaming |
| 4 | AutoAnimate (`@formkit/auto-animate`) | Fallback if Motion layout animation proves heavy: zero-config add/remove/move for the row list | MIT (LICENSE page); respects reduced motion | 1.9 kB claimed in 2022 launch post (possibly stale) | https://auto-animate.formkit.com/ ; https://dev.to/justinschroeder/introducing-autoanimate-add-motion-to-your-apps-with-a-single-line-of-code-34bp |
| 5 | Hand-built trace waterfall (CSS bars) for level 3 | Latency per tool step; modeled on eval-platform timeline views and the waterfall components trending on X | Own code; the trending third-party component's license and price were not stated on its page, so do not copy it | None | https://affectui.com/components/trace-waterfall |
| 6 | Langfuse trace link (public trace) | Level 3 "open the real trace" for power users | `setActiveTraceAsPublic` makes the whole trace viewable by link and cannot be undone programmatically; Hobby limits for this not verified | None (outbound link) | https://js.reference.langfuse.com/functions/_langfuse_tracing.setActiveTraceAsPublic.html ; https://langfuse.com/docs/observability/features/url |
| 7 | Vercel AI SDK UI hooks (`useChat`, tool parts) | Only worth it if we model events as UIMessage tool parts. Tool parts expose a `state`, and tool-call streaming is on by default since AI SDK 5 | Open source (SDK); 7.0 migration guide exists | `useChat` defaults to POST `/api/chat`; chat-shaped, so extra adapter code for a claims table | https://ai-sdk.dev/docs/ai-sdk-ui/chatbot-tool-usage ; https://ai-sdk.dev/docs/ai-sdk-ui/transport ; https://ai-sdk.dev/docs/migration-guides/migration-guide-7-0 |
| 8 | Skip for now: assistant-ui, CopilotKit / AG-UI, json-render, React Spring, Rive, Lottie | Chat-thread or model-composed-UI tools that do not match a fixed claims table | assistant-ui: MIT (README). CopilotKit repo LICENSE text is MIT-style; AG-UI license not separately verified. json-render: Vercel Labs, license unverified | assistant-ui scaffolds Next.js, has a Vite plugin for its `"use generative"` directive; Rive adds a WASM runtime and pays off only at about 3-5+ animations (vendor-adjacent blog); dotLottie is MIT | https://github.com/assistant-ui/assistant-ui ; https://github.com/assistant-ui/assistant-ui/tree/main/packages/vite ; https://github.com/copilotkit/copilotkit/blob/main/LICENSE ; https://github.com/ag-ui-protocol/ag-ui/ ; https://json-render.dev/ ; https://unicornicons.com/blog/lottie-vs-rive-performance ; https://charmotion.app/guides/rive-vs-lottie |

## What is trending on X (2026-10, via opencli)

1. Trace waterfall components are hot: @flohoeller, "Trace waterfall component, see where your agent's time goes" (1,597 likes, 2026-10-21). https://x.com/i/status/2112823884689133905
2. Step-by-step agent trace views: @DataChaz on a traces view that rebuilds a session with each tool call, args, output, cost and latency, arguing that agents you can't see can't be debugged (2026-10-21). https://x.com/i/status/2113038914147803615
3. Progressive disclosure for agents is being discussed, mostly about tool/capability exposure, not UI: @AiCamila_ (2026-08-18). https://x.com/i/status/2089739080011817235 (treat as opinion, low signal)
4. Generative UI via json-render has high engagement: @ctatedev posts (7,794 likes, 2026-09-18). https://x.com/i/status/2101022101750571357
5. Agent-app component kits (AI Elements plus newer kits) are being compared: @vikingmute (2026-08-12). https://x.com/i/status/2087447507995668929

X is anecdotal; it shows direction, not adoption numbers.

## Three-level disclosure pattern

Level 1, glance (everyone, default). One row per claim: claim text, status chip that animates through checking, fetching source, searching passage, then the label. Rows appear and settle with Motion. No numbers except maybe a single running count. Basis: an AI search team reported in a LangChain case study that users wait longer when intermediate progress is shown, and that detail should stay behind expandable steps until the user is curious (paraphrased).

Level 2, receipt (click a row). The report's words vs the exact source line, a link to the line, and a short list of agent steps (tool name, one-line result). Shape the steps like shadcn `Trace` lines so each one looks the same. https://ui.shadcn.com/docs/components/base/trace

Level 3, full trace (explicit control inside the receipt, or a dedicated page). Per tool call: full input and output, latency bars, tokens, retrieval scores, plus a link to the Langfuse trace. Basis: eval-platform trace views show spans with inline duration, tokens and cost, a timeline, and a detail panel per span; Langfuse separates an Aggregated overview from an Expanded "as it ran" view, which maps to level 2 vs level 3. https://langfuse.com/docs/observability/features/agent-graphs

Examples that behave this way:

1. A data-platform vendor's agent-activity component: collapsed by default to one shimmering status row, expandable at any time mid-run, auto-collapses to a short summary when complete.
2. Chat assistants' reasoning views: concise reasoning that collapses when done, full reasoning hidden by default (March 2025, possibly stale). https://www.digestibleux.com/p/how-ai-models-show-their-reasoning
3. Reasoning UX guidance: auto-collapse on the first answer token is the core of the pattern; the summary carries the value, detail is for the minority (Aug 2026). https://multigrid.ai/learn/reasoning-ux
4. AI search "pro" modes: plan shown step by step, steps click open for detail, citations show snippets on hover.
5. Eval-platform and Langfuse trace UIs (level 3 reference, above).

Design rules that follow (my synthesis, not sourced): keep the choice sticky per visitor; keep level 3 off the main thread so the page is not slowed; show honest data only (no invented scores, per AGENTS.md).

Versions: Motion and AutoAnimate are additions to `STACK.md`, not swaps; Winston pins them and records them if adopted.

## Fit with constraints

1. React 19 + Vite SPA: Motion, AutoAnimate and shadcn copy-in code are client-only and need no Next.js. assistant-ui's CLI scaffolds Next.js but also has a Vite plugin (https://github.com/assistant-ui/assistant-ui/tree/main/packages/vite).
2. SSE from a Cloudflare Worker: Hono `streamSSE` supports it (https://hono.dev/docs/helpers/streaming). Workers CPU time excludes time waiting on network such as fetch and DB calls (https://developers.cloudflare.com/workers/platform/limits/), so a streaming run mostly waiting on LLM and source fetches should fit the 10 ms budget, but the real number needs a smoke test (unverified for our workload). Note the repo's AGENTS.md already says Workers requests have 10 ms of CPU.
3. Free and no card: every recommended item is open source or copy-in.
4. Bundle: stay on `m` + `LazyMotion`; importing `motion` breaks the savings, since the full component preloads all its features (Motion doc above).
5. Accessibility: Motion and AutoAnimate both document reduced-motion support (AutoAnimate: official page; Motion: `useReducedMotion` in same doc). Honor it.

## Open questions

1. Which `LazyMotion` feature pack (`domAnimation` vs `domMax`) includes layout animations, and what is the real gzip size for our build? Not confirmed; measure in a spike.
2. What license covers shadcn `Trace` / AI Elements source? The docs page does not state one; check the GitHub repo before copying.
3. Do we make Langfuse traces public (irreversible per trace, shows full content) or render level 3 from our own stored step data and only link out for the sample report? Also confirm the Hobby plan allows this.
4. FR10 needs the check to keep running after the tab closes, but a streamed Worker response stops when its client disconnects. The stream can only show progress; the check itself needs a driver that outlives the request (Winston). Is a heartbeat or an `event: ping` needed so Workers/proxies do not buffer SSE (Hono notes Wrangler buffering workarounds)? Test on the deployed Worker.
5. Do we want the `ai` SDK data stream at all, or only `ai` on the server and our own event schema on the wire?
6. Which sample-report claim count keeps Motion layout animation smooth on a low-end phone? Needs a quick test.
