# Building a world-class scrollytelling AI explainer: complete research brief

**The optimal approach combines Leon Furze's three-layer AI Iceberg as the narrative spine, proven pedagogical techniques from the best visual AI explainers, scrollytelling patterns pioneered by the NYT and perfected by Bartosz Ciechanowski, all built on an Astro + GSAP ScrollTrigger + inline SVG stack deployed to Cloudflare Pages.** This architecture requires only two npm dependencies, generates all visuals programmatically, and gives an AI coding agent maximum autonomy. What follows is every detail needed to write a comprehensive CLAUDE.MD instruction file.

---

## Area 1: Leon Furze's AI Iceberg — the narrative backbone

Leon Furze, an Australian educator and PhD candidate at Deakin University, published "The AI Iceberg: Understanding ChatGPT" on **May 18, 2023** at `leonfurze.com/2023/05/18/the-ai-iceberg-understanding-chatgpt/`. The model expanded into Chapter 1 of his bestselling book *Practical AI Strategies* (Amba Press, January 2024) and anchors Lesson 1 of his online course "Introduction to Generative AI in Education." The iceberg image is available at `leonfurze.com/wp-content/uploads/2023/05/AI-Iceberg-full.png` and is freely usable in presentations with URL credit.

### The three-layer model plus two extended elements

**Layer 1 — The Dataset (underwater bulk, hidden below the waterline).** Furze writes: *"The bulk of the iceberg, hidden underwater, represents the vast dataset on which the LLM is trained. This data forms the bedrock of the model's knowledge and capabilities. It's vast and mostly unseen during any interaction with the model, but it's always there, informing every output."* He notes GPT-4 trained on roughly **13 trillion tokens** — "about 1,600 times the population of Earth." Known data sources include Common Crawl, The Pile, Wikipedia, GitHub, and social media. Much data is proprietary. This layer carries "plenty of side effects, including the kind of bias and discrimination" central to AI ethics discussions.

**Layer 2 — The LLM (above the waterline, the visible iceberg).** This is "the result of the training process fuelled by the vast dataset beneath." The book version adds three technical processes: (1) **tokenization** — text broken into machine-readable numerical code; (2) **weighting** — connections between tokens assigned probability values; (3) **transformer architecture and attention mechanism** — introduced in 2017 by Google researchers, allowing the model to "zoom out" and pay "attention" to larger groups of tokens. Furze notes LLMs are often called "black boxes" because internal connections are "so massively complex that no human or team of humans could possibly unravel everything going on inside."

**Layer 3 — Applications like ChatGPT (the snowman sculpture sitting on top).** Furze: *"Picture a carefully sculpted snowman sitting on top of the iceberg. This represents an application like ChatGPT, built on top of the general LLM. The snowman is a more specialised figure carved from the raw material of the iceberg, just as ChatGPT is a version of the GPT model fine-tuned specifically for conversational tasks."* The chatbot layer includes system messages (rules for every interaction) and **RLHF** (reinforcement learning from human feedback), where humans judge outputs as positive, negative, harmful, correct, or incorrect. The snowman metaphor itself was suggested by ChatGPT when Furze ran his analogy through the model — he'd originally described it as "a little flag sticking out of the top."

**Extended element: The Ocean** represents the internet at large — "the vast environment from which the dataset is sourced." **Extended element: Sharks** symbolize threats — misinformation, bias, toxic content, and data privacy issues that "can influence the dataset and, subsequently, the behaviour of the LLM."

### Pedagogical reasoning behind the framing

Furze chose the iceberg deliberately. He writes: *"I'm deliberately avoiding any kind of analogy that represents the AI as magical, mythical, human, or godlike — we've seen enough of them."* The iceberg emphasizes **hidden infrastructure** — there's vastly more beneath the surface than what users interact with. It connects naturally to ethics discussions about training data sourcing, bias, copyright, and privacy. He jokes: *"After fifteen years working in secondary education, I do know that if you can't express it as an iceberg, a pyramid, or a Venn diagram then it's not worth expressing."* In a 2024 paper in the *Journal of Interactive Media in Education*, Furze and co-authors used **Conceptual Metaphor Theory** aligned to UNESCO's AI competency framework, selecting pedagogically appropriate metaphors (iceberg, black box, mirror, funhouse mirror) to teach Critical AI Literacy.

### Related frameworks from Furze worth incorporating

- **AI Assessment Scale (AIAS)**: 5 levels from "No AI" to "Full AI," co-developed with Mike Perkins and Jasper Roe, translated into 12+ languages
- **Critic, Creator, Consumer**: A Venn diagram of three roles people play with GenAI, with the most interesting work at intersections
- **Digital Plastic metaphor**: Compares GenAI outputs to microplastics — cheap, malleable, ubiquitous, persistent — published in *Pedagogies* (September 2025)

---

## Area 2: World-class scrollytelling — patterns, examples, and techniques

### The foundational examples and what makes each exceptional

**NYT "Snow Fall" (December 2012)** at `nytimes.com/projects/2012/snow-fall/` birthed modern scrollytelling. A 15,000-word, six-chapter avalanche story built by **16 people over 6 months** using scroll-triggered multimedia, parallax scrolling, video loops as hero images, and integrated audio/animations. Won the Pulitzer, Peabody, and Webby. It coined the verb "to snowfall." Key lesson: every multimedia element was chosen to **enhance rather than distract** from narrative. Criticism centered on requiring NYT-level resources and scroll-jacking that hasn't aged well.

**Bloomberg's graphics team** (~20 people) produces technically sophisticated data journalism. Their standout pattern is **progressive network diagrams** — step-by-step scroll sections introduce nodes and connections, then make the full visualization interactive. They use **HTML5 Canvas** (not SVG) for performance with large datasets, plus D3.js and custom JavaScript. Their "2024: Year in Graphics" retrospective and AI bias investigations demonstrate scroll-driven data revelation at its finest.

**The Pudding** (`pudding.cool`) creates "visual essays" explaining culturally debated ideas with data. Their signature pattern: **sticky graphics with scrolling text annotations** where each text block triggers a state change in the visualization. Built with D3.js, custom JavaScript, Python/R for data analysis. Design philosophy: "Question-driven, visual-first." Every project includes a transparent Method section. Funded through their studio arm Polygraph.

**Stripe.com** sets web design trends with its scroll animations. Technical highlights include: a **WebGL gradient mesh** background ("miniGL"), a **morphing navigation dropdown** using CSS `transform: scaleX() scaleY() translateX()` for GPU-accelerated resizing, Intersection Observer for viewport-triggered reveals, custom cubic-bezier timing curves (never default easing), and `requestAnimationFrame` for 60fps. Stripe respects `prefers-reduced-motion` and uses only compositor-friendly properties (transform, opacity).

**Apple product pages** (e.g., MacBook Pro, AirPods Pro) pioneered **scroll-driven image sequence animation**: 150–300 pre-rendered JPEG frames drawn to a `<canvas>` element via `requestAnimationFrame`, with frame index calculated as `Math.floor(scrollFraction * totalFrames)`. Sticky sections hold the canvas while text overlays fade in/out with scroll progress. Creates a "premium unwrapping" feel where the user controls pacing. Some newer pages sync `<video>` `currentTime` to scroll position instead.

**Linear.app** spawned an entire design trend — dark mode as philosophy, not preference. Key characteristics: near-black backgrounds, gradient orb logo, glassmorphism, **light pulse animations** along interface edges, star field particle effects, bold Inter typography, and a near-monochrome palette using **LCH color space** for perceptually uniform contrast. Their website took **4 months** of dedicated design work.

**Bartosz Ciechanowski** (`ciechanow.ski`) creates extraordinarily deep interactive articles with dozens of custom-built simulations per piece. Topics include Moon physics, cameras and lenses, GPS, gears, color spaces. His approach: **progressive complexity** (start simple, add layers), **draggable simulations** with linked parameter sliders, **multiple simultaneous viewpoints**, ghost trails and force annotations, and mathematics presented alongside visual demonstrations. All custom WebGL/Canvas — no framework dependencies. Described as "everything Bartosz Ciechanowski makes is gold."

**Nicky Case** (`ncase.me`) creates "explorable explanations" teaching through play. Key works: *The Evolution of Trust* (game theory), *Parable of the Polygons* (segregation simulation with Vi Hart), *To Build A Better Ballot*. Design patterns documented by Case: **"start concrete, then abstract"**; embed "homework" (content gating — withhold next section until user completes interaction); **plot twist structure** (chain counter-intuitive ideas with "BUT" connectors); **sandbox at the end** after building up piece by piece. Open source, built with 11ty and custom JavaScript.

**Neal Agarwal** (`neal.fun`) creates ~35 interactive experiences blending education with entertainment, reaching **100+ million visitors**. *The Deep Sea* makes you **feel** ocean depth through sheer scroll distance. *Infinite Craft* uses LLaMA 2 for AI-powered element combination. *Spend Bill Gates' Money* puts billions into tangible perspective. Design principle: "You don't read that the ocean is deep — you feel it." One clear lesson per project, no dark patterns, no sign-ups.

### Award-winning work 2023–2025

The **2024 Webby Awards** recognized Apple Vision Pro's product page (3D scroll animations), Shopify's Winter '24 Edition (product updates as interactive magazine), NBC News interactive segregation maps (scrollytelling spanning 1930–2019), and National Geographic's Hawaii sustainability piece. The **2025 Webbys** added categories for AI Experiences and Immersive Storytelling. **Malofiej Awards** have been paused since 2021. **SND Best of Digital** (SND46, April 2025) remains the premier visual journalism award.

### The eight essential scrollytelling techniques

**Parallax scrolling** moves background and foreground layers at different speeds. Implementation: CSS `background-attachment: fixed` for simple, or GSAP ScrollSmoother with `data-speed` attributes. Best at subtle 0.5x–1.5x speed differences.

**Scroll-triggered animations** fire when elements enter the viewport. Three implementation tiers: Intersection Observer API (native, efficient), GSAP ScrollTrigger (full-featured: pinning, scrubbing, snapping), and CSS `animation-timeline: scroll()` (compositor-thread, GPU-accelerated, but limited browser support).

**Progressive reveal** controls information pacing. The dominant data journalism pattern: **sticky visualization on one side, scrolling text annotations on the other**, where text triggers state changes. Used by Bloomberg, The Pudding, and most newsrooms.

**Scroll-linked video/frame playback** ties playback to scroll position. Apple's method: image sequences on `<canvas>`. Alternative: `video.currentTime` sync (lighter but worse backward scrubbing). GSAP ScrollTrigger supports video scrubbing natively.

**Chapter-based navigation** divides content into discrete sections with progress indicators (dots, bars, chapter titles). Combined with `scroll-snap-type: y mandatory` for snapping. Always provide jump-to-chapter capability.

**Sticky sections with animated content** pin elements (`position: sticky`) while scrolling content within them changes. GSAP: `ScrollTrigger` with `pin: true` and `scrub: 1`. The **most common scrollytelling pattern in professional data journalism**.

**Horizontal scroll sections** convert vertical scrolling to horizontal movement within a pinned container. GSAP approach: pin container, animate `x` property of inner wrapper with `scrub`. Requires visual cues signaling the mode shift.

**Morphing transitions** smoothly transform elements between states. Stripe's approach: scale background container separately from content using CSS transforms. SVG path morphing interpolates between keyframes. The new CSS View Transitions API handles DOM state changes.

### Cross-cutting insight

The universal pattern across all world-class examples is **progressive disclosure** — from Ciechanowski's physics simulations to Bloomberg's network diagrams to Apple's product reveals. Scroll gives users agency over pacing, making content feel discovered rather than delivered. Performance is non-negotiable: every major site uses GPU-accelerated transforms, Intersection Observer (not scroll listeners), and respects `prefers-reduced-motion`.

---

## Area 3: How to explain GenAI to non-technical audiences

### The proven explanation sequence

The most effective explainers follow a consistent pedagogical arc: start with the **black box** (input goes in, output comes out), then progressively open it. The single most important concept for non-technical audiences is **next-token prediction** — the revelation that ChatGPT builds text one word at a time, like "the world's most sophisticated autocomplete." Multiple educators note this is the biggest "aha moment" for learners.

### Core concepts and their best analogies

**Tokenization:** Text is broken into "tokens" — words, word-parts, or characters, like Scrabble tiles. Andrej Karpathy's dedicated tokenizer video demonstrates that "a lot of weird behaviors and problems of LLMs actually trace back to tokenization." The token is the fundamental unit the model works with.

**Embeddings:** Tokens become numerical vectors — essentially **GPS coordinates in "meaning space"** where similar concepts cluster together. 3Blue1Brown explains geometrically: directions in high-dimensional space encode semantic relationships. The classic example: king − man + woman ≈ queen. Embeddings are learned during training, not hand-coded.

**Attention mechanism:** The "Attention Is All You Need" concept explained through Jay Alammar's signature example: *"The animal didn't cross the street because it was too tired"* — what does "it" refer to? Self-attention lets each word look at every other word to resolve this. 3Blue1Brown's "nouns asking questions" metaphor makes it visceral: *"Imagine each noun asking: 'Hey, are there any adjectives sitting in front of me?'"* The Query/Key/Value system works like a database lookup: Query = what I'm seeking, Key = what's available, Value = the actual information. The **"mole" disambiguation** example (American shrew mole / one mole of CO₂ / biopsy of the mole) shows why context-sensitive embeddings require attention.

**Next-token prediction:** The phone autocomplete analogy is universal. Luis Serrano spells it out: Command → "Write a story." Response → "Once." Command → "Write a story. Once" → "upon." And so on, word by word. As Serrano writes: *"The first time I found out that transformers build text one word at a time, I couldn't believe it."*

**Diffusion models (image generation):** The **ink-in-water analogy** — imagine ink diffusing in a glass until uniformly mixed. Diffusion models learn the reverse: starting from pure noise and gradually "un-mixing" into a coherent image. Training involves progressively adding noise to real images, then training a neural network to reverse each step. Text prompts guide the process via cross-attention — the text encoder (like CLIP) converts words to vectors that steer what image emerges from the noise.

**Multimodal AI:** The human senses analogy (McKinsey): when you wake up, you orient yourself through hearing, sight, touch simultaneously. Multimodal AI combines text, images, audio using a three-stage process: encode each modality separately → fuse representations via cross-attention → decode/generate output.

**Training vs. inference:** The education-to-career analogy: *"Training is like awarding a high school diploma. Fine-tuning is like making them a college graduate. Inference is where they apply all they've learned into their career."* Training is expensive (days/weeks on thousands of GPUs, happens once). Inference is fast (every time you send a prompt, ongoing).

### The standout visual explainers and what to learn from each

**Jay Alammar's "The Illustrated Transformer"** (`jalammar.github.io/illustrated-transformer/`) is featured in courses at Stanford, Harvard, MIT, Princeton, and CMU. His method: **progressive black-box opening** — starts with transformer as a single box, reveals encoder/decoder stacks, individual layers, then attention mechanisms. Uses color-coded vector diagrams, step-by-step calculation walkthroughs with actual numbers, and heat-map-style attention visualizations. Each diagram is self-contained and builds on the previous one. Now expanded into the book *Hands-On Large Language Models*.

**3Blue1Brown (Grant Sanderson)** published Chapters 5–7 on transformers (April 2024). Uses his custom animation library **manim** for precise mathematical visualizations. Embeddings shown as points/arrows in projected 3D space. The "mole" disambiguation drives the entire attention explanation. Described as *"by far the clearest explanation of attention"* (Simon Willison). Over **6 million YouTube subscribers**. Always builds from "what behavior do we want?" before "how the math achieves it."

**Andrej Karpathy's** "Let's build GPT: from scratch, in code, spelled out" (January 2023, **5.3M+ views**) implements a GPT from a bigram model upward. His **"build it to understand it" philosophy** makes every step executable code. Uses Tiny Shakespeare dataset for relatable output. His 2026 **microGPT** fits a complete transformer in 243 lines of pure Python. His tokenizer video uniquely explains how "weird behaviors and problems of LLMs trace back to tokenization."

**Google Teachable Machine** (`teachablemachine.withgoogle.com`, **182,000+ users in 201 countries**) teaches ML through immediate hands-on experience: gather examples via webcam → click Train → test instantly. All processing happens in-browser via TensorFlow.js transfer learning. Shows prediction **confidence as a spectrum, not binary** — teaching that ML operates on probabilities. Users physically showing objects to their webcam creates visceral understanding of training data and its limitations.

**TensorFlow Playground** (`playground.tensorflow.org`) lets users configure neural network architecture (1–6 layers, 1–8 neurons), adjust hyperparameters, and watch training in real-time. Blue/orange lines represent positive/negative weights; background color shows decision boundaries. The **spiral dataset** is a powerful "aha moment" — it demonstrates why depth matters.

**Georgia Tech's Transformer Explainer** (`poloclub.github.io/transformer-explainer/`, IEEE VIS 2024) runs a **live GPT-2 (124M params) in-browser** via ONNX Runtime. Users input text and watch the complete pipeline: tokenization → embedding → attention → MLP → next-token prediction. A **temperature slider** shows deterministic vs. creative outputs in real-time. Multi-level abstraction with expandable detail.

**Brendan Bycroft's LLM Visualization** (`bbycroft.net/llm`) provides a **stunning 3D visualization** of a GPT-style network performing inference. Every matrix multiplication, attention head, and layer is visible with animated data flow. Uses a tiny model from Karpathy's minGPT that sorts letters A, B, C. Described as "an extraordinary window into the inner workings of the technology powering ChatGPT."

### Common misconceptions good explanations must address

The biggest misconception is **"AI thinks/understands like humans."** The next-token prediction revelation is the single most powerful corrective. Other critical misconceptions: AI is one monolithic thing (reality: different architectures for different tasks); AI is always accurate and objective (reality: biased data → biased outputs); AI is a black box that can't be understood (visual explainers directly combat this); AI creates with genuine creativity (reality: sophisticated statistical prediction). The journal *Science* notes that AI terminology itself is anthropomorphic — "learns," "thinks," "understands" are what researchers call "wishful mnemonics." Best practice: use multiple complementary analogies and explicitly acknowledge their limitations.

---

## Area 4: Technical implementation for Claude Code

### Recommended stack: Astro + GSAP ScrollTrigger + inline SVG + Cloudflare Pages

This stack is optimal for autonomous AI agent development because it has **only two npm dependencies** (`astro` and `gsap`), generates all visuals programmatically, uses clear well-documented APIs, and deploys with a single command.

### Why Astro is the right framework

Astro ships **zero JavaScript by default** — only interactive components ("islands") hydrate where needed. Its `.astro` files are a superset of HTML, the simplest mental model for AI code generation. The `client:visible` directive loads component JavaScript only when scrolled into view — perfect for scroll sections. Astro pre-renders everything at build time (static output), ideal for CDN deployment. It's framework-agnostic, meaning Svelte or React components can be mixed in if needed. No SSR adapter is needed for a static site.

**Why not React + Framer Motion:** React adds ~87KB+ JavaScript overhead even for a blank page, requires a virtual DOM, and is heavier for a single-page content site. Framer Motion's `useScroll` and `useTransform` hooks provide scroll-linked animations, but GSAP offers more comprehensive scrollytelling features (pinning, snapping, timeline scrubbing).

**Why not Svelte:** Svelte compiles to vanilla JS (smaller bundle) and has excellent reactive animations via `svelte-motion`. But for a single-page site, Astro with vanilla JS + GSAP is simpler with fewer compilation concerns.

### GSAP ScrollTrigger — capabilities and patterns

GSAP became **completely free** (including commercial use) after Webflow's 2024 acquisition. Key capabilities for scrollytelling:

**Scrubbing** links animation progress directly to scroll position. `scrub: true` gives 1:1 mapping; `scrub: 1` adds 1-second catch-up smoothing. **Pinning** keeps elements fixed while scrolling through sections (`pin: true`). **Snapping** auto-snaps to section boundaries (`snap: 1/5` for five sections). **Batch processing** efficiently animates multiple elements (`ScrollTrigger.batch()`). **Timeline integration** sequences complex multi-step animations linked to a single scroll range.

The classic scrollytelling pattern in code:

```javascript
// Pin sticky visualization, trigger step changes
ScrollTrigger.create({
  trigger: "#scroll-container",
  start: "top top",
  end: "bottom bottom",
  pin: ".sticky-graphic",
});

gsap.utils.toArray('.step').forEach((step, i) => {
  ScrollTrigger.create({
    trigger: step,
    start: "top center",
    end: "bottom center",
    onEnter: () => updateVisualization(step.dataset.step),
    onEnterBack: () => updateVisualization(step.dataset.step),
  });
});
```

GSAP handles accessibility natively via `gsap.matchMedia()`:

```javascript
let mm = gsap.matchMedia();
mm.add("(prefers-reduced-motion: no-preference)", () => {
  // Full animations with scrubbing and pinning
});
mm.add("(prefers-reduced-motion: reduce)", () => {
  // Simplified fade-only transitions
});
mm.add("(max-width: 767px)", () => {
  // Simpler mobile animations
});
```

### CSS scroll-driven animations as progressive enhancement

The W3C `scroll-timeline` spec offers `animation-timeline: scroll()` and `animation-timeline: view()` for compositor-thread, GPU-accelerated scroll animations. Browser support as of February 2026: Chrome 115+ (stable), Firefox (behind flag), Safari (no support). Use as progressive enhancement with GSAP as fallback. The key advantage is running entirely off the main thread for silky-smooth performance.

### Generating all visuals programmatically

**Inline SVG is the primary visual approach.** SVG elements an AI agent can generate: neural network diagrams (circles for nodes, lines for connections, animated gradients for data flow), iceberg layered diagrams (paths with bezier curves), token visualizations (text + rect elements), attention heatmaps, and flowcharts. GSAP can animate any SVG property — `strokeDashoffset` for drawing paths, `opacity` for reveals, `transform` for movement.

**CSS art** supplements SVG: `conic-gradient` and `radial-gradient` for visual elements, `clip-path` for complex shapes, `box-shadow` stacking for detailed illustrations, and `@keyframes` for autonomous animations.

**HTML5 Canvas** handles generative backgrounds: particle effects for data flow visualization, ambient animated backgrounds. Lightweight and dependency-free. Skip Three.js unless 3D is essential — it adds ~150KB+ and is overkill for 2D scrollytelling. **Skip Lottie** — the JSON schema is too complex for AI agent generation without visual tooling; GSAP + SVG is far more controllable programmatically.

### Deployment to Cloudflare Pages

**Git integration method (recommended):** Push to GitHub → Cloudflare auto-detects Astro preset → build command `npm run build` → output directory `dist` → automatic deploy. Every push to `main` triggers rebuild. Preview deployments for pull requests. Free tier includes unlimited bandwidth, 500 builds/month, automatic SSL, global CDN.

**CLI method for AI agent:**
```bash
npx astro build
npx wrangler pages deploy dist --project-name=ai-explainer
```

**GitHub Actions CI/CD:**
```yaml
name: Deploy
on: { push: { branches: ['main'] } }
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with: { node-version: 20 }
      - run: npm ci && npm run build
      - run: npx wrangler pages deploy dist --project-name=ai-explainer
        env:
          CLOUDFLARE_API_TOKEN: ${{ secrets.CLOUDFLARE_API_TOKEN }}
```

### Performance optimization rules

**S-tier compositor properties (always use):** `transform` (translate, scale, rotate) and `opacity`. These never trigger layout or paint. **Never animate:** `width`, `height`, `top`, `left`, `margin`, `padding`, `box-shadow`, `border-radius` — these trigger expensive layout recalculations.

Apply `will-change: transform, opacity` sparingly to promote elements to compositor layers. Use `contain: layout style paint` on sections to limit layout impact. GSAP's `stagger` property sequences multiple element animations to avoid simultaneous GPU load. Lazy-load heavy components with Astro's `client:visible` directive and native `loading="lazy"` on images.

### Accessibility requirements

**Reduced motion:** Implement both CSS `@media (prefers-reduced-motion: reduce)` and GSAP `matchMedia()` to replace motion-heavy animations with simple fades. Provide an explicit UI motion toggle button with localStorage persistence.

**Screen readers:** Use semantic HTML (`<section>`, `<article>`, `<h1>`–`<h6>`). Add `aria-label` to animated sections. Apply `aria-hidden="true"` to purely decorative animations. Ensure all content is accessible without JavaScript (progressive enhancement — Astro pre-renders all HTML).

**Keyboard navigation:** Skip links (`<a href="#main-content">`), Tab/Enter navigation through scroll sections. Don't make critical information dependent on scroll position alone.

### Mobile responsiveness

Touch scroll events differ from mouse scroll — test `scrub` values on actual devices. Use `gsap.matchMedia()` to serve simpler animations on mobile. Avoid `vh` units in scroll calculations (mobile browsers resize viewport dynamically). Keep Canvas/WebGL minimal on mobile (GPU memory constraints). Target **60fps minimum** on low-powered devices.

### Recommended project structure

```
ai-explainer/
├── public/
│   └── favicon.svg
├── src/
│   ├── layouts/
│   │   └── Layout.astro          # Base HTML, meta, global styles
│   ├── components/
│   │   ├── IcebergSVG.astro      # Programmatic iceberg diagram
│   │   ├── NeuralNetworkSVG.astro # Neural network visualization
│   │   ├── TokenViz.astro        # Animated tokenization demo
│   │   ├── AttentionViz.astro    # Attention mechanism visualization
│   │   ├── EmbeddingViz.astro    # Vector space / embedding demo
│   │   ├── DiffusionViz.astro    # Image generation denoising
│   │   └── ParticleCanvas.astro  # Ambient background particles
│   ├── styles/
│   │   └── global.css            # All styles, animations, themes
│   └── pages/
│       └── index.astro           # Single scrollytelling page
├── astro.config.mjs
├── package.json                  # Only astro + gsap
└── CLAUDE.md                     # Build instructions
```

---

## Synthesis: how all four areas connect into a CLAUDE.MD strategy

The **narrative structure** should follow Furze's iceberg from top to bottom (or bottom to top) — starting with what users see (ChatGPT, the snowman/application layer), diving below the waterline to the LLM layer (where tokenization, embeddings, attention, and next-token prediction live), and plunging to the training data ocean floor. This mirrors the **progressive disclosure** pattern used by every world-class scrollytelling example.

Each concept should be explained using the **best proven analogies**: phone autocomplete for next-token prediction, GPS coordinates in meaning space for embeddings, the pronoun resolution example for attention, ink-in-water for diffusion. Address misconceptions directly — "it doesn't understand, it predicts" — following the pattern of Teachable Machine and TensorFlow Playground that make failures visible.

The **scrollytelling implementation** should use the dominant pattern from Bloomberg and The Pudding: sticky SVG visualizations that transform as scrolling text annotations trigger state changes via GSAP ScrollTrigger. Each "chapter" of the iceberg gets its own pinned section with scrubbed animations. Ciechanowski's approach of linked parameter controls and multiple viewpoints could enhance the attention mechanism section. Nicky Case's content-gating pattern (requiring user interaction before progressing) could make the tokenization section interactive.

The **technical execution** on Astro + GSAP + SVG + Cloudflare Pages gives Claude Code maximum autonomy: two dependencies, all-code visuals, pre-rendered HTML, and single-command deployment. Every animation respects `prefers-reduced-motion`, every section uses semantic HTML, and the mobile experience gracefully simplifies via `gsap.matchMedia()`. The site should feel like an Apple product page in craft, a Ciechanowski article in depth, and a Nicky Case explorable in interactivity — all organized around Furze's iceberg as the unifying visual metaphor that readers literally scroll through, descending from the snowman at the surface down through the hidden layers that make generative AI work.