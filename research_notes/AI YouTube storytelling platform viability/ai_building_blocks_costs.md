# AI building blocks and API costs for a "story idea → multilingual YouTube video" platform (as observed 2026-11-14)

All prices in USD. "Observed 2026-11-14" means I fetched the vendor's own page on that date. Third-party aggregator figures are flagged as such and should be re-verified before budgeting; several aggregators carry reseller markups or stale snapshots.

## Key Question 1: Story ideation and scriptwriting (LLM APIs and story-writing tools)

### Takeaway
Scriptwriting is a fully commoditized stage: a 10-minute script plus scene breakdown, image prompts and two translations costs between about $0.02 (Haiku 5.5 / Gemini Flash-Lite) and about $1.50 (Claude Fable 5.1) in API tokens, i.e. well under 5% of the per-video bill. Consumer story tools (Sudowrite, NovelAI, Squibler, Plottr) are subscription apps aimed at human authors, not pipeline components.

### Cited Findings
- Anthropic official pricing (observed 2026-11-14): Claude Fable 5.2 $8 in / $40 out per MTok; Fable 5.1 $10 / $50; Opus 5.5 $4 / $20; Opus 5 $5 / $25; Sonnet 5.5 $2 / $10; Sonnet 4.6/4.5 $3 / $15; Haiku 5.5 $0.10 / $0.50 (prompts ≤100k tokens; $0.50/$2.50 above 100k); Haiku 4.5 $1 / $5. Cache hits for Fable 5.1 $0.25/MTok, Sonnet 5.5 $0.10/MTok. Batch API gives a flat 50% discount (e.g. Sonnet 5.5 batch $1 / $5, Haiku 5.5 batch $0.05 / $0.25). Fast mode is premium-priced (Fable 5.2 $16 / $80). — [Anthropic pricing docs](https://platform.claude.com/docs/en/about-claude/pricing)
- OpenAI official pricing (observed 2026-11-14), per 1M tokens in/out: gpt-5.6-sol $4 / $20; gpt-5.6-terra $2 / $12; gpt-5.6-luna $0.20 / $1.20; gpt-5.5 $5 / $30; gpt-5.4 $2.50 / $15; gpt-5.4-mini $0.75 / $4.50; gpt-5.4-nano $0.20 / $1.25; gpt-5.1 and gpt-5 $1.25 / $10; gpt-5-mini $0.25 / $2; gpt-5-nano $0.05 / $0.40. Batch is roughly half. — [OpenAI API pricing](https://developers.openai.com/api/docs/pricing)
- Google Gemini API official pricing (observed 2026-11-14), per 1M tokens in/out (paid tier): gemini-4-carbon and gemini-4-argon $2 / $10 (rising to $4 / $20 on Dec 1, 2026); gemini-4-hydrogen $1.50 / $7.50; gemini-3.8-flash and gemini-3.6-flash $0.75 / $3.75 (rising to $1.50 / $7.50 on Jan 1, 2027); gemini-3.5-flash-lite $0.30 / $2.50; gemini-3.1-flash-lite $0.25 / $1.50; gemini-2.5-flash-lite $0.10 / $0.40. gemini-2.5-pro and gemini-2.5-flash are deprecated and will route to newer models on Dec 1, 2026. Batch and Flex tiers are 50% off Standard. — [Gemini API pricing](https://aistudio.google.com/docs/pricing)
- Sudowrite is a fiction-focused AI drafting tool; its Hobby & Student plan is reported at $10/month annual or $19/month monthly (third-party, prices reported inconsistently). — [aipedia comparison](https://aipedia-en.pages.dev/compare/sudowrite-vs-novelcrafter-vs-novelai); [eesel.ai](https://www.eesel.ai/blog/ai-novel-writing-software)
- NovelAI is an open-ended storytelling plus image-generation app with lorebooks; cheapest paid tier "Tablet" is $10/month and it has a free plan (third-party). — [toolradar](https://toolradar.com/compare/novelai-vs-sudowrite)
- Plottr is a visual outlining app with no AI features ("every plan is labelled No AI"); Pro is about $15/month, $99/year or $699 lifetime (third-party). — [toolradar guide](https://toolradar.com/guides/best-ai-book-writing-tools)
- Squibler is positioned as an AI book/screenplay drafting tool with a permanent free tier; its paid tiers are reported inconsistently, with one reviewer noting its own pricing table and FAQ disagree. — [eesel.ai](https://www.eesel.ai/blog/ai-novel-writing-software); [startupstash](https://startupstash.com/alternatives/squibler/)

### Inferences
- Worked example for a 10-minute video (≈1,500 words of narration): ideation, outline, script, 60 shot descriptions/image prompts, 2 translations and QA passes plausibly consume ~50k input and ~20k output tokens. At official rates that is ≈$0.015 (Haiku 5.5), ≈$0.11 (gemini-3.8-flash), ≈$0.30 (Sonnet 5.5), ≈$0.34 (gpt-5.6-terra), ≈$1.50 (Fable 5.1). Batch mode halves these if the pipeline is asynchronous.
- None of the story-writing apps surfaced in my searches advertise a public API, so for a pipeline they are competitors/benchmarks for UX rather than building blocks; the differentiation they offer (lorebooks, beat outlining, "story bibles") is what the platform would have to rebuild on top of raw LLM calls.

### Gaps
- I did not find an official API or pricing page for Sudowrite, NovelAI, Plottr or Squibler in this pass; prices above are from third-party comparison sites that disagree with each other.

## Key Question 2: Image generation with character consistency

### Takeaway
Per-image cost is now $0.01–$0.15 from first-party APIs (Google Nano Banana family, BFL Flux, OpenAI gpt-image), so 60 finals with 2x retries is roughly $2–$20. Character consistency is solved "well enough" for stylized storytelling by reference-image conditioning (Nano Banana / Flux Kontext / Ideogram character reference) without training; LoRA training is the fallback for strict repeatability. Midjourney remains off the table for an API-driven product.

### Cited Findings
- Google Gemini API official per-image prices (observed 2026-11-14): gemini-nano-banana-2.1 $0.0336 (1K), $0.0504 (2K), $0.113 (4K), batch half price; gemini-3.1-flash-image $0.045 (0.5K), $0.067 (1K), $0.101 (2K), $0.151 (4K); gemini-3.1-flash-lite-image $0.0336 (1K); gemini-3-pro-image ("Nano Banana Pro") $0.134 (1K/2K), $0.24 (4K); gemini-2.5-flash-image $0.039 (shutdown Mar 15, 2027). Image output is billed as tokens ($60/1M for 3.1-flash-image, $120/1M for 3-pro-image). — [Gemini API pricing](https://aistudio.google.com/docs/pricing)
- Imagen 4 is reported at $0.02 (Fast), $0.04 (Standard), $0.06 (Ultra) per image (third-party; I did not see Imagen on the Gemini API pricing page sections I retrieved). — [Puter Gemini pricing guide](https://developer.puter.com/tutorials/gemini-api-pricing/)
- OpenAI gpt-image models are priced per token, not per image (observed 2026-11-14): gpt-image-2 $8 image input / $30 image output / $5 text input per 1M tokens; gpt-image-1.5 $8 / $32 / $5; gpt-image-1-mini $2.50 / $8 / $2. The page points to a calculator for per-image equivalents. — [OpenAI API pricing](https://developers.openai.com/api/docs/pricing)
- fal.ai marketplace per-image prices (observed 2026-11-14): FLUX.1 [dev] $0.025/MP, FLUX.1 [schnell] $0.003/MP, FLUX 2 $0.012/MP, FLUX 2 Edit $0.012 per processed MP, FLUX 2 Flash $0.005/MP; Nano Banana $0.0398, Nano Banana 2 $0.08, Nano Banana Pro $0.15 per image (note fal's Nano Banana 2 price is above Google's direct $0.067); Seedream V4.5 $0.04. — [fal.ai pricing](https://fal.ai/pricing)
- Flux Kontext (BFL) is reported at $0.04/image (Pro) and $0.08/image (Max), with Kontext Dev free for non-commercial use or $999/month for a commercial license; Kontext is marketed for "multi-turn, in-context editing with character and style consistency across sequential edits" (third-party, consistent across several sources). — [ucstrategies](https://ucstrategies.com/news/flux-1-kontext-pro-contextual-inpainting-api-specs-pricing-benchmarks-2026/); [invideo pricing roundup](https://invideo.io/blog/ai-image-model-pricing/)
- Ideogram API is reported at $0.025–$0.10 per image base, with the Character Reference feature adding cost: 3.0 Turbo + character reference $0.10, Default $0.15, Quality $0.20 (third-party; sources disagree on the exact surcharge). — [eesel Ideogram pricing](https://www.eesel.ai/blog/ideogram-pricing); [apiscout](https://apiscout.dev/guides/flux-vs-ideogram-vs-recraft-image-gen-api-2026)
- Midjourney still has no official public API; its Terms of Service prohibit automated access, and third-party "Midjourney APIs" wrap the Discord/web app with account-ban risk (third-party, multiple vendor blogs agree; no Midjourney primary source). — [unifically](https://unifically.com/blogs/midjourney-api); [apiframe](https://apiframe.ai/blog/best-midjourney-apis)
- Consistency techniques described by practitioners: (1) reference-image conditioning as the most accessible starting point; (2) a character LoRA trained on a curated image set (fal.ai offers training) when the same identity is needed across many prompts; (3) Flux Kontext editing of a canonical image as "the strongest no-training option"; (4) a layered multi-scene setup combining a reference image at frame 0, a character LoRA at inference and a fixed 50–80 word character prompt block across all scenes. — [LTX blog](https://ltx.io/blog/how-to-maintain-character-consistency-in-ai-video); [Martini guide](https://martini.art/en/blog/how-to-build-consistent-ai-character); [fluxnote](https://fluxnote.io/guides/how-to-get-consistent-characters-in-ai-video)
- One 2026 vendor comparison claims Google's Nano Banana and GPT-4o lead "hard consistency tests" with Flux Kontext and Midjourney trailing over long sequences — single vendor source, unverified. — [higgsfield](https://higgsfield.ai/blog/tools-for-consistent-ai-characters)

### Inferences
- 60 final images at 1K: ≈$2.02 (Nano Banana 2.1 standard) or ≈$1.01 (batch); ≈$4.02 (gemini-3.1-flash-image); ≈$8.04 (Nano Banana Pro); ≈$2.40 (Flux Kontext Pro, third-party price); ≈$0.72 (FLUX 2 at 1 MP on fal); ≈$6–$12 (Ideogram with character reference). Realistic with 1.5–2x regeneration for consistency failures: $2–$25 per video.
- Because image output is token-billed on Gemini and OpenAI, higher resolutions and edit/reference inputs raise cost non-linearly; a pipeline should generate at 1K and upscale in post if 4K is needed.
- Commodity status: yes for generation; "mostly solved" for consistency in stylized/illustrated looks via reference conditioning; still error-prone for photoreal human faces across many angles, which is where LoRA training adds a one-time per-character cost and latency.

### Gaps
- Could not retrieve BFL's or Ideogram's official pricing pages directly; figures are third-party.
- Per-image dollar equivalents for gpt-image-2 are not stated on OpenAI's page (token-billed); I did not run the calculator.
- Commercial-use terms: Flux Kontext Dev is non-commercial without a license (third-party report); I did not verify Ideogram's or BFL's current commercial terms text.

## Key Question 3: Video generation

### Takeaway
Video is the single largest and most volatile cost line: $0.025–$0.17 per second for the mid-tier (Kling 2.6/3.0, MiniMax H3, Runway Gen-4 Turbo, Gemini Omni Flash) and $0.40–$0.60/s for Veo 3.1 with audio, so 40 clips × 8 s (320 s) runs ≈$8–$200 before retries. The landscape shifted in 2026: OpenAI shut the Sora 2 Videos API on Sept 24, 2026, and Google retired the Veo 3.1 preview endpoints on the Gemini API on Oct 22, 2026 in favour of "Gemini Omni" video models.

### Cited Findings
- OpenAI announced Sora's discontinuation on March 24, 2026; the consumer app closed April 26, 2026 and the Videos API / Sora 2 and Sora 2 Pro models were removed on September 24, 2026 with no recommended replacement (multiple secondary sources quoting OpenAI help/deprecation pages). The current OpenAI pricing page lists no video model. — [The Decoder](https://the-decoder.com/openai-sets-two-stage-sora-shutdown-with-app-closing-april-2026-and-api-following-in-september/); [kingy.ai tracker](https://kingy.ai/ai-launch-tracker/openai-sora-videos-api-shutdown-september-24-2026/); [OpenAI API pricing](https://developers.openai.com/api/docs/pricing)
- Historical Sora 2 API rates (pre-shutdown, third-party): Sora 2 ≈$0.10/s at 720p; Sora 2 Pro $0.30/s (720p), $0.50/s (1024p), $0.70/s (1080p); batch halved. — [benchlm](https://benchlm.ai/media-pricing/sora); [eesel](https://eesel.ai/blog/sora-2-in-the-api-pricing)
- Google Gemini API (observed 2026-11-14) now lists "Gemini Omni" video models rather than Veo: gemini-omni-1.2-flash at $12 per 1M video output tokens ≈ $0.07/s at 720p (≈$0.023/s at 360p, ≈$0.209/s at 4K with upsampling), input $1.50/1M; gemini-omni-1.1-flash $17.50/1M ≈ $0.10/s, auto-routing to 1.2-flash on Dec 3, 2026. — [Gemini API pricing](https://aistudio.google.com/docs/pricing)
- The Veo 3.1 preview models (veo-3.1-generate-preview, -fast-, -lite-) were shut down on the Gemini API on October 22, 2026 with Gemini Omni Flash as the suggested replacement; one source reports Vertex AI GA models veo-3.1-generate-001 / fast-generate-001 have a shutdown "on or after November 17, 2026" (unconfirmed against Google). Veo 4 was not announced at I/O 2026 per an August 2026 report. — [aiengineerguide retirement note](https://aiengineerguide.com/tools/model-retirements/veo-3-1-generate-preview/); [aiidelist migration guide](https://aiidelist.com/blog/veo-3-1-preview-api-shutdown-omni-flash-migration); [aireiter on Veo 4](https://aireiter.com/blog/veo-4)
- Veo 3.1 per-second prices as published before the shutdown (third-party snapshots, Sept–Nov 2026): Standard $0.40/s (720p/1080p), $0.60/s (4K); Fast $0.10/s (720p), $0.12/s (1080p), $0.30/s (4K) [one source says $0.15/$0.35]; Lite $0.05/s (720p), $0.08/s (1080p). On fal: $0.20/s without audio, $0.40/s with audio, Lite $0.03/$0.05; fal's Veo pages said the endpoints would be deprecated Nov 17, 2026. — [benchlm Veo](https://benchlm.ai/media-pricing/veo); [Decrypt on Veo 3.1 Lite](https://decrypt.co/363077/google-veo-3-1-lite-cuts-api-costs-half-openai-sora?amp=1); [teamday fal pricing](https://www.teamday.ai/blog/fal-ai-pricing-2026)
- Kling official developer pricing (kling.ai doc, via search): Kling 3.0 ≈$0.084/s (720p, no audio), $0.112/s (1080p, no audio), $0.126/s (720p with native audio), $0.168/s (1080p with audio), $0.42/s (4K); Kling 3.0 Turbo $0.112/s (720p) and $0.14/s (1080p) with audio; Kling 2.6 $0.042/s (720p) and $0.07/s (1080p) without audio, $0.14/s (1080p with audio), $0.168/s with voice control. Resellers list lower rates that do not match the official page. — [Kling API pricing doc](https://kling.ai/document-api/pricing/base/video.md); [flexprice note on clip-based billing](https://flexprice.io/pricing-index/kling-ai)
- fal.ai per-second video prices (observed 2026-11-14): Kling 2.5 Turbo Pro and 2.6 Pro $0.07/s; Kling 3 Pro/Standard and Kling O3 $0.14/s; MiniMax H3 Max $0.05/s, H3 Max Turbo $0.025/s; FLUX 3 Max video $0.085/s; PixVerse V6 $0.005/s; Grok Imagine Video $0.05/s (1.5: $0.01/s); Seedance 2.0 Fast $0.0112 per 1k tokens, Mini $0.007 per 1k tokens. fal's pricing page does not state clip length limits, audio inclusion or resolution. — [fal.ai pricing](https://fal.ai/pricing)
- Runway developer API bills credits at $0.01 each; Gen-4 Turbo works out to $0.05/s and Gen-4.5 to $0.12/s; base Gen-4 is app-only (third-party). — [unifically Runway Gen-4](https://unifically.com/blogs/runway-gen-4); [perkstack](https://perkstack.co/blog/cheapest-runway-gen-4-turbo-api)
- Luma Ray: conflicting third-party figures — Ray 3 ≈$0.10–$0.30/s; Ray-2 ≈$0.08/s; one source quotes a 5-s clip at $0.15 (540p) to $1.20 (1080p). — [reelmind](https://reelmind.ai/blogs/ai-video-generator-pricing-in-2026-runway-gen-4-5-veo-3-1-sora-2-pika-2-5-luma-r); [developersdigest](https://www.developersdigest.tech/blog/image-video-generation-api-pricing-2026)
- Hailuo/MiniMax via resellers ≈$0.01/s (512p), $0.04/s (768p), $0.08/s (1080p); Wan 2.5 listed at ≈$0.05/s with "verify on fal" (third-party). — [apiframe video pricing](https://apiframe.ai/blog/ai-video-api-pricing-2026); [dev.to research post](https://dev.to/buildandcodewithraman/ai-video-creation-models-research-15n3)
- Pika: no reliable API per-second price found; one guide gives $0.05–$0.15/s without saying whether that is API or subscription. — [rangy pricing guide](https://rangy.ai/blog/ai-video-pricing-explained)

### Inferences
- 320 s of generated video (40 × 8 s) at official/marketplace rates: ≈$8 (MiniMax H3 Turbo), ≈$13.4 (Kling 2.6 720p no audio), ≈$16 (Runway Gen-4 Turbo, MiniMax H3 Max, Veo 3.1 Lite at $0.05), ≈$22.4 (Kling 2.6 Pro 1080p no audio; Gemini Omni 1.2 Flash 720p), ≈$35.8 (Kling 3.0 1080p no audio), ≈$38.4 (Runway Gen-4.5), ≈$53.8 (Kling 3.0 1080p with audio), ≈$128 (Veo 3.1 with audio at $0.40/s, where still available), ≈$192 (4K Veo). With a realistic 1.5–2x regeneration rate for failed shots the video line is ≈$12–$250.
- Native audio adds 50–100% on Kling and doubles Veo on fal; a narrated story video does not need per-clip native audio (narration and music are added in assembly), so the no-audio tiers are the right comparison.
- Most APIs cap single clips at 5–10 s (Kling 5/10 s per third-party; Sora 4–12 s or up to 20 s with extension before shutdown), so a 10-minute video is inherently a stitching problem; it is cheaper to animate only ~30–50% of runtime and use Ken Burns pans over stills for the rest.
- Commodity status: text/image-to-video at 720p is commodity priced but not commodity quality; shot-to-shot continuity (same character, same set) remains the hard part and drives the retry multiplier. Vendor churn (Sora gone, Veo 3.1 endpoints retiring, Omni replacing Veo) argues for routing through an aggregator (fal/Replicate) with a model-abstraction layer.

### Gaps
- Could not load Google Cloud Vertex AI's pricing page (fetch returned only the title), so current official Veo 3.1 GA per-second prices and Vertex shutdown dates are unverified.
- fal's page gives no clip-length, resolution or audio details; Kling 2.6's billing unit (per second vs per 5/10 s clip) is disputed between the official page and a third-party site.
- No official Pika, Luma, Wan or MiniMax first-party price sheets were retrieved.
- Commercial-rights text for each video vendor was not fetched; none of the sources I reviewed contradicted commercial use on paid tiers, but this needs reading of each ToS.

## Key Question 4: Text-to-speech and voice cloning

### Takeaway
Narration is cheap and commoditized: ten minutes (~9,000 characters) costs ≈$0.14 on OpenAI tts-1, Azure Neural, Fish Audio or Gemini 3.8 Flash TTS, and ≈$0.36–$0.72 on ElevenLabs (Flash/v4 Turbo vs v3/v4). Language coverage ranges from 29 (ElevenLabs v2) to 90+ (ElevenLabs v4, Scribe). Voice cloning is available via API on ElevenLabs by referencing a cloned voice ID.

### Cited Findings
- ElevenLabs API pricing (observed 2026-11-14, per 1,000 characters): v4 $0.08 (90+ languages); v4 Turbo $0.04 (90+); v3 $0.08 (70+, 5,000-char limit); v3 Conversational $0.04; v2 Multilingual $0.08 (29 languages, 10,000-char limit); Flash/Turbo $0.04 (32 languages, 40,000-char limit). The page quotes ≈$0.08/min for multilingual models and ≈$0.04/min for Flash/Turbo/v4 Turbo. API usage is billed in USD, not credits; cloned voices can be referenced by ID through the API. Plans: Free (10k chars), Starter $6 (75k), Creator $22 (275k), Pro $99 (1.238M), Scale $299 (3.738M), Business $990 (12.375M). Startup Grant: 12 months free with 33M characters. — [ElevenLabs API pricing](https://elevenlabs.io/pricing/api)
- OpenAI TTS (observed 2026-11-14): tts-1 $15 per 1M characters; tts-1-hd $30 per 1M characters; gpt-4o-mini-tts $0.60/1M text input tokens and $12/1M audio output tokens. — [OpenAI API pricing](https://developers.openai.com/api/docs/pricing)
- Google Gemini TTS (observed 2026-11-14, per 1M tokens in/out): gemini-3.8-flash-tts $0.50 / $9 (rising to $1 / $18 on Jan 1, 2027), ≈$0.00225 per 10 s of audio; gemini-3.8-flash-lite-tts $0.50 / $6; gemini-2.5-flash-preview-tts $0.50 / $10; gemini-2.5-pro-preview-tts $1 / $20; batch half price. — [Gemini API pricing](https://aistudio.google.com/docs/pricing)
- Azure TTS Neural ≈$15–16 per 1M characters, Neural HD ≈$22 (reduced from $30 in March 2026), with a 500k-character free monthly tier (third-party). — [fast.io TTS comparison](https://fast.io/resources/best-ai-text-to-speech-tools-2026/); [Speechify comparison](https://speechify.ai/compare/build/text-to-speech)
- Fish Audio ≈$15 per 1M API characters (vendor's own blog, not independent). — [Fish Audio comparison](https://fish.audio/blog/text-to-speech-api-comparison-pricing-features/)
- Cartesia Startup plan ≈$39–$49 per 1M characters (credit-based; third-party, July–Nov 2026). — [invideo TTS pricing](https://invideo.io/blog/ai-voice-model-pricing/); [apiframe TTS](https://apiframe.ai/blog/best-text-to-speech-apis-2026)
- PlayHT ≈$80 per 1M API characters (third-party). — [clonemyvoiceai](https://clonemyvoiceai.pages.dev/compare/fish-audio-vs-playht/)
- fal.ai TTS marketplace (observed 2026-11-14, per 1k chars): MiniMax Speech 2.8 HD $0.10, Speech 2.8 Turbo $0.06, Gemini 3.1 Flash TTS $0.05, Chatterbox $0.025, Kokoro $0.02, xAI TTS $0.015, Inworld TTS-1.5 Max $0.01. — [fal.ai pricing](https://fal.ai/pricing)

### Inferences
- 10 minutes of narration ≈ 9,000 characters: OpenAI tts-1 ≈$0.135; tts-1-hd ≈$0.27; Gemini 3.8 Flash TTS ≈$0.135 (≈$0.27 after Jan 1, 2027); Azure Neural ≈$0.14; Fish ≈$0.14; Cartesia ≈$0.35–$0.44; ElevenLabs Flash/v4 Turbo ≈$0.36; ElevenLabs v3/v4 ≈$0.72; PlayHT ≈$0.72. Three language versions multiply these by 3: ≈$0.40–$2.20.
- ElevenLabs' v4/v4 Turbo (90+ languages) removes the 29-language ceiling of v2 Multilingual, which matters for a "3 language versions" product; the cheaper engines (OpenAI, Azure, Fish) are fine for narration but have fewer expressive controls, so quality is the trade-off rather than price.

### Gaps
- Did not verify Cartesia, Fish, PlayHT or Azure official pricing pages directly.
- ElevenLabs' page does not distinguish instant vs professional voice cloning per plan; commercial-use terms per plan were not stated except "Commercial use licensing on Starter+ plans" for Music.

## Key Question 5: AI dubbing and lip sync

### Takeaway
For a narrated story video whose visuals are AI images/clips (no on-screen speaking human), full "dubbing" is unnecessary: re-narrating the translated script via TTS costs ≈$0.15–$0.75 per language, versus $0.50/min (ElevenLabs Dubbing v1) to $2.20/min (Dubbing v2) ≈ $5–$22 per language for a 10-minute video. Lip sync (Sync Labs lipsync-2 at $2.40–$3.00/min; sync-3 at $6.40–$8.00/min) is only needed if a talking character is on screen, and is still the hard, expensive stage.

### Cited Findings
- ElevenLabs Dubbing (observed 2026-11-14): v1 $0.33/min with watermark, $0.50/min without (29 languages); v2 $2.20/min (92 languages). Billed per minute. — [ElevenLabs API pricing](https://elevenlabs.io/pricing/api)
- Third-party guides state dubbing is billed per source minute per target language (10 min × 3 languages = 30 minutes); I could not verify the per-language detail on the official page. — [seedance.tv dubbing calculator](https://www.seedance.tv/blog/elevenlabs-dubbing-cost-per-minute); [startpinch comparison](https://startpinch.com/guides/dubbing-api-pricing-comparison)
- Sync Labs official model page (observed 2026-11-14, per second at 25 fps): lipsync-1.9.0-beta $0.02–$0.025 (≈$1.20–$1.50/min, generic lip movements); lipsync-2 $0.04–$0.05 (≈$2.40–$3.00/min, 512×512, "most natural, preserves each speaker's style"); lipsync-2-pro $0.067–$0.083 (≈$4.02–$4.98/min, diffusion super-resolution, better with beards/teeth); sync-3 $0.107–$0.133 (≈$6.42–$7.98/min, 4K native, handles profiles/obstructions). Billing is per output frame. Max video duration depends on plan (1 min Hobbyist to 30 min Scale+); lipsync-2/2-pro split longer videos into 30–40 s chunks and can time out with many scene changes or no detectable faces. — [Sync Labs lipsync models](https://sync.so/docs/models/lipsync)
- fal.ai lists sync lipsync v2 at $3 per minute of video (reseller rate above Sync's own). — [fal.ai sync-lipsync v2](https://fal.ai/models/fal-ai/sync-lipsync/v2)
- HeyGen: API usage is billed through a USD wallet separate from Studio plan credits; free API credits were removed in February 2026. Third-party figures for video translation conflict: ≈$2/min at API rates (lip-synced), 5 credits/min speed vs 10 credits/min precision, audio-only dubbing 2 credits/min; a HeyGen help-center excerpt lists a "Speed — Audio Only (no lip sync)" dub at $0.57/min. — [HeyGen API plans help article](https://intercom.help/heygen/en/articles/10060327-new-heygen-api-plans); [eesel HeyGen pricing](https://www.eesel.ai/blog/heygen-pricing); [fluxnote HeyGen translation guide](https://fluxnote.io/guides/heygen-video-translation-guide)
- Rask AI: plan prices reported inconsistently (Creator $39–$60/month for 25 minutes ≈$2.40/min; lip sync from a $99/month Creator Pro plan; extra minutes $3); API access is on Business tier with no public API price list (third-party). — [perso.ai Rask review](https://perso.ai/blog/rask-ai-dubbing-review-2026-features-pricing-how-it-compares); [Capterra](https://www.capterra.com/p/10006163/Rask-AI/)
- Papercup and Deepdub are enterprise-only with custom quotes; Papercup's former customers reportedly now go through RWS (third-party). — [rework dubbing tools comparison](https://resources.rework.com/tools/ai-video/best-ai-dubbing-tools-2026); [Papercup pricing](https://papercup.com/pricing)
- Perso.ai dubbing "starts at $0.11 per dubbed minute" (vendor claim via third-party roundup). — [rework comparison](https://resources.rework.com/tools/ai-video/best-ai-dubbing-tools-2026)

### Inferences
- Two extra languages for a 10-minute video: re-narration path ≈$0.30–$1.50 (TTS) + ≈$0.10 LLM translation; ElevenLabs Dubbing v1 (no watermark) ≈$10; Dubbing v2 ≈$44; HeyGen ≈$40 (unverified); adding lip sync for on-screen speakers with lipsync-2 ≈$48–$60, sync-3 ≈$128–$160.
- Dubbing APIs are designed for human-recorded source video (preserving voice timbre, background separation); for AI-narrated content the platform already owns the script and voice, so the "dubbing" stage collapses into translate-then-TTS, which is a large structural cost advantage.
- Lip sync remains "still hard": per-frame billing, 512×512 native resolution on lipsync-2, chunking and timeouts on scene changes; it should be reserved for close-up dialogue shots.

### Gaps
- Could not confirm from ElevenLabs' page whether dubbing minutes are charged per target language.
- No official HeyGen api-pricing page retrieved; figures conflict across sources.
- No Rask API price list; Papercup/Deepdub publish no rates.

## Key Question 6: Automated editing/assembly and captions

### Takeaway
Assembly is fully commodity: FFmpeg is free, Remotion is free for companies of up to three people and $0.01 per render ($100/month minimum) above that, and hosted render APIs cost ≈$0.13–$0.30 per output minute (Shotstack) or ≈$0.20/min (JSON2Video). Captions for 30 minutes of audio (3 languages) cost ≈$0.10–$0.20 via Whisper/AssemblyAI/ElevenLabs Scribe, or nothing if timestamps are taken from the TTS step.

### Cited Findings
- Remotion license (observed 2026-11-14): free for individuals and companies of up to three people with unlimited commercial use; "Remotion for Automators" (batch/automated video products) is $0.01 per render with a $100/month minimum (10,000 renders = $100), no developer seats needed; "Remotion for Creators" $25/month per seat; Enterprise from $500/month. The license page does not mention Lambda render costs. — [Remotion license](https://www.remotion.dev/license)
- Shotstack: entry plan $39/month for 200 credits where 1 credit = 1 minute at up to 1080p; Pro $99 for 750 minutes (≈$0.13/min, allows 4K); pay-as-you-go quoted at $0.30/min or $0.20/min on subscription (third-party, some competitor-authored). — [wireflow Shotstack pricing](https://www.wireflow.ai/blog/shotstack-pricing); [Creatomate vs Shotstack](https://creatomate.com/compare/shotstack-alternative)
- Creatomate bills 1 credit per 100 million pixels, so 1080p30 ≈37 credits/min and 2,000 credits ≈54 minutes; cheaper at 720p, more expensive than Shotstack/JSON2Video at 1080p+ (third-party). — [wireflow Creatomate pricing](https://www.wireflow.ai/blog/creatomate-pricing)
- JSON2Video bills 1 credit per second at any resolution; Startup plan $99.95 for 500 minutes (≈$0.20/min); voiceovers and subtitles included at no extra credits (vendor and third-party). — [JSON2Video plans](https://json2video.com/docs/v2/reference/credits/plans); [motionbox alternatives](https://motionbox.io/blog/best-json2video-alternatives-in-2026)
- Transcription (observed 2026-11-14, OpenAI): Whisper $0.006/min; gpt-4o-transcribe $0.006/min; gpt-4o-mini-transcribe $0.003/min; gpt-transcribe $0.0045/min. — [OpenAI API pricing](https://developers.openai.com/api/docs/pricing)
- ElevenLabs Scribe v3/v2 speech-to-text $0.20/hour (90+ languages), Scribe v3 Live $0.22/hour (observed 2026-11-14). — [ElevenLabs API pricing](https://elevenlabs.io/pricing/api)
- AssemblyAI Universal ≈$0.15/hour; Universal-3.5 Pro async $0.0035/min (≈$0.21/hour) as of July 2026 with a 10% in-region price rise effective July 1, 2026; Deepgram Nova-3 ≈$0.26/hour batch to $0.46/hour streaming; Groq-hosted Whisper large-v3-turbo ≈$0.02/hour (third-party). — [costbench transcription benchmarks](https://costbench.com/stats/ai-transcription-apis-pricing-2026/); [dev.to transcription pricing](https://dev.to/eli_9c82b7dfe52c1bc371ffe/ai-transcription-pricing-2026-whisper-vs-deepgram-vs-assemblyai-2eec)
- YouTube captions.insert costs 400 quota units per call (per the official method reference surfaced in search). — [captions.insert reference](https://developers.google.com/youtube/v3/docs/captions/insert)

### Inferences
- Rendering three 10-minute 1080p versions: FFmpeg on own compute ≈ cents; Remotion ≈$0.03 in license fees (plus compute) once above the free tier; Shotstack ≈$4–$9; JSON2Video ≈$6; Creatomate ≈$6–$8 at 1080p.
- Captioning 30 minutes of narration: Whisper ≈$0.18; AssemblyAI ≈$0.08–$0.11; Scribe ≈$0.10. Word-level timestamps from TTS (ElevenLabs returns alignment) can eliminate this step entirely for the narration track.
- Editorial decisions (shot timing to narration beats, transitions, title cards) are deterministic template work in Remotion/FFmpeg and are not a cost or feasibility risk.

### Gaps
- Shotstack/Creatomate/JSON2Video official pricing pages were not fetched directly; the figures come from competitor and aggregator blogs.
- Editframe pricing was not found in this pass.
- Deepgram's exact Nova-3 rate conflicts across sources ($0.26 vs $0.46/hour).

## Key Question 7: Music and SFX

### Takeaway
Only ElevenLabs Music ($0.15/min, commercial license on Starter+ plans) and Google Lyria ($0.04–$0.08 per song) offer self-serve APIs with clear commercial terms; Suno's developer API is a curated, invite-only beta with no public pricing, and Udio has no API. Epidemic Sound now has a partner API with a free prototyping tier and global, perpetual safelisting of end-user content, but publishes no self-serve rates.

### Cited Findings
- ElevenLabs Music API: $0.15 per minute, 5-minute limit per generation, $1.50 per finetune; "Commercial use licensing on Starter+ plans"; Sound Effects $0.12/min and royalty-free (observed 2026-11-14). — [ElevenLabs API pricing](https://elevenlabs.io/pricing/api)
- Google Lyria (observed 2026-11-14, paid tier only): lyria-3.5 (full song) $0.08 per song; lyria-3-clip-preview (30 s) $0.04; lyria-3-pro-preview $0.08; Lyria 3 is described as legacy. — [Gemini API pricing](https://aistudio.google.com/docs/pricing)
- Suno announced on July 1, 2026 that it is "exploring" a developer API via a curated partner intake form; as of later 2026 reports it was still assessing applications, had named no partners, and Suno v6 launched with no public developer API. — [Digital Music News](https://www.digitalmusicnews.com/2026/07/03/suno-is-opening-an-api-partner-program/); [Music Business Worldwide](https://www.musicbusinessworldwide.com/sunos-new-mcp-tool-lets-users-make-songs-inside-chatgpt-claude-and-gemini-as-its-developer-api-gets-a-sign-in-portal-but-remains-in-beta); [orcarouter on Suno v6](https://www.orcarouter.ai/blog/suno-v6-launch)
- Udio has no official public API; downloads were reportedly still switched off as of October 2026 and training-data lawsuits are ongoing (third-party). — [apiframe music API pricing](https://apiframe.ai/blog/ai-music-api-pricing-2026); [chartlex](https://www.chartlex.com/blog/marketing/ai-music-generator-comparison-2026)
- Epidemic Sound developer API (observed 2026-11-14): self-serve free tier with immediate API key, no contract or credit card, full catalog for prototyping, unspecified usage limits; "Content safelisted with the Epidemic Sound API is licensed globally, forever"; sublicensing to end users supported; end users need no Epidemic account; catalog 55,000+ tracks and 250,000+ SFX; no prices on the page (Business and Enterprise plans). Partners announced in 2026 include VEED (May 5), Blaze AI (Feb), Veel (June 22) and Elevate.io. — [Epidemic Sound developers](https://www.epidemicsound.com/business/developers/); [VEED press release](https://corporate.epidemicsound.com/press-and-media/press-releases/2026/veed-partners-with-epidemic-sound-to-bring-world-class-music-and-sound-to-its-global-creator-community/)
- fal.ai lists a generic "Music generator" at $0.02/min (observed 2026-11-14). — [fal.ai pricing](https://fal.ai/pricing)
- Artlist offers a "Music API" to integrate its catalog, but no 2026 pricing or partner list surfaced. — [apievangelist Epidemic listing (context)](https://providers.apievangelist.com/providers/epidemic-sound/)

### Inferences
- Music for a 10-minute video: ≈$1.50 via ElevenLabs Music (10 min) or ≈$0.24 via three Lyria 3.5 songs; SFX ≈$0.12/min on ElevenLabs. Epidemic's catalog is the lowest-legal-risk choice for YouTube (safelisting avoids Content ID claims) but pricing is negotiated.
- Generated music is the "copyright-safe" path only on paid tiers with explicit commercial grants (ElevenLabs Starter+, Google paid tier); Suno/Udio are not usable as pipeline components today.

### Gaps
- Epidemic Sound partner API pricing and Artlist API pricing are not public.
- Lyria "per song" length limits were not stated in the retrieved excerpt.

## Key Question 8: YouTube Data API v3 — quota, audit, OAuth, multi-language audio

### Takeaway
Upload economics changed materially in 2025–2026: videos.insert dropped from ≈1,600 units to ≈100 (Dec 4, 2025) and then moved into its own bucket of 100 uploads/day at 1 unit each (June 1, 2026); on Nov 2, 2026 Google removed the rule forcing uploads from unaudited projects to private. A compliance audit is still required for any quota above default. Multi-language audio tracks are a YouTube Studio feature with no exposed field in the Data API videos resource.

### Cited Findings
- Default quota (observed 2026-11-14): "100 search.list calls, 100 videos.insert calls, and 10,000 units per day combined for all other endpoints"; a video upload costs 1 unit (in its bucket); other write operations usually cost 50 units; every request costs at least one unit; extra quota via the Quota extension request form. — [YouTube Data API getting started](https://developers.google.com/youtube/v3/getting-started)
- Revision history (observed 2026-11-14): Dec 4, 2025 — videos.insert quota cost changed "from approximately 1600 units to approximately 100 units"; June 1, 2026 — "transitioning to a granular quota system", videos.insert and search.list "charged to their own respective quota buckets"; Nov 2, 2026 — videos uploaded via videos.insert from unverified API projects "are no longer restricted to private viewing mode", reversing the July 28, 2020 policy; if status.privacyStatus is omitted the default is public, though creator account settings may default some uploads to private. No 2025–2026 entries cover multi-language audio tracks. — [YouTube Data API revision history](https://developers.google.com/youtube/v3/revision_history)
- Older guidance (pre-Nov 2026) still widely repeated: videos.insert = 1,600 units, 6 uploads exhaust the day, unaudited uploads forced private. — [Quota calculator](https://developers.google.com/youtube/v3/determine_quota_cost?hl=en); [Blotato summary of changes](https://www.blotato.com/blog/youtube-api-pricing)
- All requests for additional quota must go through a compliance audit via the "YouTube API Services Audit and Quota Extension Form"; developers audited within the last 12 months use a re-request path; failed audits can be appealed; Google states only that the team "will get back to you as soon as possible". — [Quota and Compliance Audits guide](https://developers.google.com/youtube/v3/guides/quota_and_compliance_audits?hl=en); [Audit form](https://support.google.com/youtube/contact/yt_api_form?hl=en); [YouTube terms revision history](https://developers.google.com/youtube/terms/revision-history?authuser=7)
- The videos resource has no property for multiple/dubbed audio tracks; closest fields are snippet.defaultAudioLanguage (language of the default track), read-only fileDetails.audioStreams[], and the localizations object for translated titles/descriptions (observed 2026-11-14). — [videos resource reference](https://developers.google.com/youtube/v3/docs/videos)
- Multi-language audio upload is documented only as a YouTube Studio workflow (Settings > Upload Defaults > Advanced Settings > "Upload Multi-Language Audio Tracks", one audio file per language); one third-party blog claims up to 30 languages per video. — [perso.ai technical setup](https://perso.ai/blog/youtube-audio-tracks-technical-setup-(2025)); [dev.to playbook](https://dev.to/jondavis/shipping-multilingual-audio-tracks-to-youtube-and-everywhere-else-a-devs-playbook-3ch0); [Metricool](https://metricool.com/youtube-multi-language-audio-tracks-now-available-for-more-creators/)
- Captions can be uploaded via captions.insert at 400 units per call. — [captions.insert](https://developers.google.com/youtube/v3/docs/captions/insert)

### Inferences
- A new project can now publish up to 100 public videos per day per API project without an audit, which removes the 2020–2025 "6 uploads/day and all private until audited" blocker for a startup's MVP; the audit remains the gate for scaling past 100/day or for other-endpoint quota beyond 10,000 units.
- Multilingual delivery via API therefore means either (a) three separate video uploads (one per language, 3 uploads of the 100/day), or (b) one upload plus manual Studio attachment of extra audio tracks; the second cannot be automated with the public Data API as of the documents I read. Localized titles/descriptions and caption tracks can be automated (localizations; captions.insert at 400 units, so 3 languages = 1,200 units of the 10,000 daily).
- The channel-level upload limit (YouTube's own anti-spam cap on verified vs unverified channels) is distinct from API quota; I did not find a documented number.

### Gaps
- OAuth verification requirements for the youtube.upload scope (sensitive-scope app verification, brand verification) were not researched in this pass; the compliance audit page did not surface them.
- No Google document found that states a channel-level daily upload cap or that multi-language audio tracks are (or are not) on the API roadmap; the "not available via API" conclusion is inferred from the absence of any such property in the videos resource.
- The Nov 2, 2026 revision wording was read via summarization of the revision history page; the exact paragraph should be quoted directly before being cited in a legal/compliance context.

## Key Question 9: Rough total cost per 10-minute video (script + ~60 images or ~40 clips + narration + 2 extra languages)

### Takeaway
At November 2026 API rates a 10-minute AI story video costs roughly $3 (stills-only, cheap TTS, re-narrated languages) to $50 (40 mid-tier video clips, ElevenLabs narration) to $250+ (Veo-class video with audio, ElevenLabs Dubbing v2). Video generation is 60–75% of the mid and premium budgets; every other stage combined is under $10.

### Cited Findings
- Unit prices used below are those cited in Questions 1–8 (Anthropic, OpenAI and Gemini pricing pages; ElevenLabs API pricing; fal.ai pricing; Kling pricing doc; Sync Labs docs; Remotion license; observed 2026-11-14 unless flagged third-party). — [Anthropic](https://platform.claude.com/docs/en/about-claude/pricing); [OpenAI](https://developers.openai.com/api/docs/pricing); [Gemini](https://aistudio.google.com/docs/pricing); [ElevenLabs](https://elevenlabs.io/pricing/api); [fal.ai](https://fal.ai/pricing); [Kling](https://kling.ai/document-api/pricing/base/video.md); [Sync](https://sync.so/docs/models/lipsync); [Remotion](https://www.remotion.dev/license)

### Inferences
Assumptions: 10-minute runtime; ~1,500-word / ~9,000-character script; 60 still images at 1K or 40 clips × 8 s = 320 s of generated video (remaining runtime covered by pans over stills); 1.5x regeneration factor on images and video; captions in 3 languages; music bed; three rendered masters; uploaded as three separate videos (no API for multi-audio tracks).

| Stage | Budget tier | Mid tier | Premium tier |
|---|---|---|---|
| LLM (script, prompts, translations) | $0.02 (Haiku 5.5) | $0.30 (Sonnet 5.5) | $1.50 (Fable 5.1) |
| Images, 60 finals × 1.5 | $3.00 (Nano Banana 2.1 $0.0336) | $6.00 (gemini-3.1-flash-image $0.067) | $12.00 (Nano Banana Pro $0.134) |
| Video, 320 s × 1.5 | $0 (stills + Ken Burns) | $34 (Kling 2.6 Pro / Gemini Omni 1.2 Flash ≈$0.07/s) | $192 (Veo 3.1 with audio $0.40/s, third-party price; or $81 Kling 3.0 1080p with audio) |
| Narration, 3 languages | $0.42 (OpenAI tts-1 / Gemini 3.8 Flash TTS ≈$0.14 each) | $2.16 (ElevenLabs v3/v4 $0.72 each) | $0.72 (ElevenLabs source) + $44 (Dubbing v2, 2 languages × 10 min × $2.20) |
| Lip sync | $0 | $0 | $0 (none needed) — add $48–$60 per 10 min of talking-head footage ×2 languages if used (lipsync-2) |
| Captions, 30 min | $0.10 (AssemblyAI ≈$0.2/hr) | $0.18 (Whisper $0.006/min) | $0.18 |
| Music/SFX | $0.24 (3 Lyria 3.5 songs) | $1.50 (ElevenLabs Music 10 min) | $2.70 (Music + 10 min SFX) |
| Assembly, 3 masters | ~$0.05 (FFmpeg compute) | $0.03 + compute (Remotion Automators) or ~$6 (JSON2Video/Shotstack) | ~$6 (hosted render) |
| YouTube upload | $0 (3 of 100 daily inserts) | $0 | $0 |
| **Total** | **≈$3.8** | **≈$44–$50** | **≈$260 (≈$150 with Kling 3.0 instead of Veo)** |

- Commodity stages (price is low and falling, many interchangeable vendors): scriptwriting, TTS narration, transcription/captions, assembly/rendering, upload. Semi-commodity: still-image generation (cheap, but consistency needs engineering). Still hard / expensive: multi-shot video generation with continuity (largest cost line, highest retry rate, vendor churn), lip sync for on-screen speakers, and automated multi-language audio attachment on YouTube (no API).
- Structural cost advantage of AI-native stories: because the platform owns the script and voice, "dubbing" becomes translate + TTS (~$0.50 for two extra languages) instead of $10–$44 of dubbing-API minutes; this only breaks if the product adds human presenters or lip-synced characters.
- Price-direction risk: Google has announced increases effective Dec 1, 2026 (Gemini 4 text 2x) and Jan 1, 2027 (Gemini 3.8 Flash text and TTS 2x), while Veo 3.1 Lite and Kling resellers have pushed video prices down; budgets should be re-run quarterly.

### Gaps
- All totals exclude engineering/orchestration compute, storage/egress, failed-generation costs beyond the assumed 1.5x, and human QA time.
- Veo 3.1 current availability/pricing on Vertex AI is unverified (page failed to load); the premium tier may need to substitute Kling 3.0, Runway Gen-4.5 or Gemini Omni at 4K.
- Per-image dollar cost for OpenAI gpt-image-2 and per-second cost for Seedance 2.0 (token-billed) were not computed.
