---
theme: default
title: Toward Contextual Adaptation and Knowledge Grounding in Large Language Models
info: |
  Dissertation defense deck for Yufei Tao.
class: cover-slide
drawings:
  persist: false
transition: fade
mdc: true
---

<div class="cover-field">
  <div class="cover-scan" aria-hidden="true"></div>
  <svg class="cover-routes" viewBox="0 0 520 420" preserveAspectRatio="none" aria-hidden="true">
    <path class="route social" d="M134 100 C155 126 197 142 260 150" />
    <path class="route informational" d="M386 101 C365 126 323 142 260 150" />
    <path class="route outcome" d="M260 262 C260 300 260 330 260 359" />
    <circle class="route-anchor social" cx="134" cy="100" r="2.4" />
    <circle class="route-anchor informational" cx="386" cy="101" r="2.4" />
    <circle class="route-anchor node" cx="260" cy="150" r="2.6" />
    <circle class="route-anchor node" cx="260" cy="262" r="2.6" />
    <circle class="route-anchor outcome" cx="260" cy="359" r="2.4" />
  </svg>
  <div class="cover-stream social">
    <div class="cover-label">social context</div>
    <div class="cover-sub">roles / expectations<br>intentions / norms</div>
  </div>
  <div class="cover-stream informational">
    <div class="cover-label">informational context</div>
    <div class="cover-sub">passages / facts<br>language-specific cues</div>
  </div>
  <div class="cover-vellum" aria-hidden="true"></div>
  <div class="cover-node">
    <div>contextual adaptation</div>
    <div>knowledge grounding</div>
  </div>
  <div class="cover-outcome">adaptive / faithful / grounded</div>
  <div class="cover-ticks" aria-hidden="true">
    <span></span><span></span><span></span><span></span><span></span>
  </div>
</div>

<div class="cover-copy">
<div class="kicker">Dissertation Defense</div>

# Toward Contextual<br>Adaptation and<br>Knowledge Grounding in<br>Large Language Models

<div class="subtitle mt-5">
LLMs are expected to adapt to context in ways that are both socially appropriate and informationally faithful.
</div>

<div class="byline mt-7">
Yufei Tao<br>
Doctor of Philosophy in Computer Science<br>
Portland State University, 2026
</div>
</div>

---

<div class="kicker">Motivation</div>

# As LLMs move from research benchmarks into real-world applications, the demands on them change

<div class="grid-2 mt-7">
<div class="tile green">
<h3>Faithful to the material it was given</h3>
<p>A model that summarizes a legal document, assists a medical professional, or answers questions in a retrieval-augmented pipeline is expected to stay faithful to the material it was given.</p>
</div>
<div class="tile blue">
<h3>Fits the social situation</h3>
<p>A chatbot helping a language learner practice a difficult conversation is expected to respond in a way that fits the social situation.</p>
</div>
</div>

<div class="takeaway mt-7">
What matters is not just fluency but whether the model lets the relevant context shape what it says.
</div>

---

<div class="kicker">Two Meanings of Context</div>

# Context has two complementary meanings

<div class="grid-2 mt-7">
<div class="tile blue">
<h3>Social context</h3>
<p>Roles, expectations, intentions, and norms that shape an interaction.</p>
</div>
<div class="tile green">
<h3>Informational context</h3>
<p>Passages, facts, and language-specific cues that should ground a response at inference time.</p>
</div>
</div>

<div class="grid-2 mt-6">
<div class="tile blue">
<h3>Contextual adaptation</h3>
<p>Adjusting behavior to fit the social situation of an interaction such as its roles, tone, and interactional expectations.</p>
</div>
<div class="tile green">
<h3>Knowledge grounding</h3>
<p>Anchoring factual claims in provided evidence rather than defaulting to parametric memory.</p>
</div>
</div>

<div class="takeaway mt-6">
The central claim is that reliable LLM behavior depends on both.
</div>

---
class: pop-slide
---

<div class="kicker">Central Claim</div>

# Large language models are context-sensitive but not fully context-governed

<div class="grid-2 wide-right mt-7">
<div class="tile blue" v-click>
<h3>They respond to context</h3>
<p>Current LLMs respond to role cues, supplied evidence, prompt structure, and decode-time controls.</p>
</div>
<div class="tile amber" v-click>
<h3>They do so incompletely and unevenly</h3>
<p>Context acts less like a hard boundary on behavior than like a competing signal.</p>
</div>
</div>

<div class="takeaway mt-7" v-click>
Together, the four studies move from diagnosing failures of contextual adaptation to proposing a concrete intervention for more dependable grounded generation.
</div>

---
class: pop-slide
---

<div class="kicker">Roadmap</div>

# From diagnosis to intervention

<div class="storyline compact rowed mt-5">
<div class="story-row" v-click><div><span class="tag blue">1</span></div><div><strong>Role-play interaction</strong></div><div>Social adaptation</div></div>
<div class="story-row" v-click><div><span class="tag green">2</span></div><div><strong>Contextual vs. parametric knowledge</strong></div><div>Baseline grounding</div></div>
<div class="story-row" v-click><div><span class="tag amber">3</span></div><div><strong>Lost-in-the-Later</strong></div><div>Multilingual and positional grounding</div></div>
<div class="story-row focus" v-click><div><span class="tag red">4</span></div><div><strong>No-Worse Context-Aware Decoding</strong></div><div>Decode-time control</div></div>
<div class="story-row" v-click><div><span class="tag violet">5</span></div><div><strong>Synthesis</strong></div><div>Context as a control problem</div></div>
</div>

<div class="grid-3 mt-5">
<div class="tile blue" v-click><h3>RQ1</h3><p>How do LLMs adapt to context, and where does that adaptation fall short?</p></div>
<div class="tile amber" v-click><h3>RQ2</h3><p>How stable is knowledge grounding when the conditions become harder?</p></div>
<div class="tile red" v-click><h3>RQ3</h3><p>Can inference-time intervention improve knowledge grounding without degrading outputs that were already correct?</p></div>
</div>

<div class="fine mt-5" v-click>Together, the four studies move from diagnosing failures of contextual adaptation to proposing a concrete intervention for more dependable grounded generation.</div>

---
class: section-slide
---

<div class="section-number">Study 1 | Social Context</div>

# Conversational adaptability and response efficiency in role-play interactions

<div class="subtitle mt-6">
Characterizing conversational adaptability in role-play interactions.
</div>

---

<div class="kicker">CRD Dataset</div>

# Data collection at conversational scale

<div class="grid-4 mt-7">
<div class="metric"><div class="value">57</div><div class="label">participants</div></div>
<div class="metric green"><div class="value">85</div><div class="label">unique conversations</div></div>
<div class="metric amber"><div class="value">1,742</div><div class="label">utterances</div></div>
<div class="metric violet"><div class="value">15</div><div class="label">self-reported first-language labels</div></div>
</div>

<div class="grid-3 mt-8">
<div class="tile blue"><h3>Vanilla</h3><p>Open interaction with ChatGPT "as is" for 5-10 minutes.</p></div>
<div class="tile amber"><h3>Boss</h3><p>High imposition and unequal power distance.</p></div>
<div class="tile green"><h3>Classmate</h3><p>More peer-like, reciprocal, and open-ended.</p></div>
</div>

<div class="fine mt-5">Scope: ChatGPT-3.5 interactions collected in March-April 2023. The contribution is the interaction dataset and behavioral measurement lens.</div>

---

<div class="kicker">Result 1</div>

# Role-play changes the interactional rhythm

<table class="table-lite mt-5">
<thead>
<tr><th>Measure</th><th class="num">Vanilla</th><th class="num">Boss</th><th class="num">Classmate</th></tr>
</thead>
<tbody>
<tr><td>Average conversation length, turns</td><td class="num"><strong>29.59</strong></td><td class="num">14.57</td><td class="num">17.11</td></tr>
<tr><td>Average human utterance length</td><td class="num">12.18</td><td class="num"><strong>20.58</strong></td><td class="num">19.06</td></tr>
<tr><td>Average ChatGPT utterance length</td><td class="num"><strong>77.66</strong></td><td class="num">35.78</td><td class="num">46.10</td></tr>
<tr><td>Human questions as percent of conversation</td><td class="num"><strong>26.34</strong></td><td class="num">21.32</td><td class="num">21.29</td></tr>
<tr><td>ChatGPT questions as percent of conversation</td><td class="num">14.69</td><td class="num">20.34</td><td class="num"><strong>32.57</strong></td></tr>
</tbody>
</table>

<div class="takeaway mt-5">
Users in role-play produce longer turns; ChatGPT changes too, but remains systematically more verbose than human turns.
</div>

---

<div class="kicker">Result 2</div>

# Role-play shifts motives and naturalness

<div class="grid-2 mt-5">
<div class="media-rail"><img src="/assets/user-motives.png" class="media short"></div>
<div class="media-rail"><img src="/assets/model-naturalness.png" class="media short"></div>
</div>

<div class="grid-3 mt-5">
<div class="tile blue"><h3>Vanilla</h3><p>Natural model responses remain rare: 5.6% overall.</p></div>
<div class="tile green"><h3>Boss</h3><p>ChatGPT was annotated as natural about half of the time: 52%.</p></div>
<div class="tile amber"><h3>Classmate</h3><p>ChatGPT was annotated as natural about half of the time: 47%.</p></div>
</div>

---

<div class="kicker">Study 1 Takeaway</div>

# Social context influences behavior, but does not fully govern it

<div class="grid-3 mt-8">
<div class="tile blue"><h3>Context works</h3><p>Role-play reorganizes user and model behavior.</p></div>
<div class="tile amber"><h3>Adaptation is incomplete</h3><p>AI self-framing, too much information, and excessive helpfulness persist.</p></div>
<div class="tile green"><h3>Next objective</h3><p>Explaining contextual versus parametric knowledge behavior.</p></div>
</div>

---
class: section-slide
---

<div class="section-number">Study 2 | Informational Context</div>

# When Context Leads but Parametric Memory Follows

<div class="subtitle mt-6">
Contextual vs. parametric knowledge in LLM outputs.
</div>

---

<div class="kicker">Study 2 Framing</div>

# The task is open-ended question answering in a knowledge-consistent setting

<div class="grid-2 mt-7">
<div class="tile green">
<h3>Test item</h3>
<ul class="test-list">
<li><strong>Topic</strong>: the title of the Wikipedia article.</li>
<li><strong>Context</strong>: k atomic sentences provided in a prompt.</li>
<li><strong>Question</strong>: "With this information, tell me about {Topic}".</li>
<li><strong>Response</strong>: the model response is then atomized.</li>
</ul>
</div>
<div class="tile green">
<h3>Non-conflict setting</h3>
<p>Wikipedia is used as a knowledge-consistent benchmark because older articles are plausibly represented in the pretraining corpora of widely used LLMs.</p>
</div>
</div>

---

<div class="kicker">WikiAtomic Construction</div>

# WikiAtomic controls context length with atomic sentences

<div class="grid-4 mt-6">
<div class="metric blue"><div class="value">200</div><div class="label">Wikipedia articles</div></div>
<div class="metric green"><div class="value">50</div><div class="label">atomic sentences per article</div></div>
<div class="metric amber"><div class="value">10,000</div><div class="label">atomic sentences</div></div>
<div class="metric red"><div class="value">4,000</div><div class="label">topic-context instances</div></div>
</div>

<div class="grid-2 mt-7">
<div class="tile blue" v-click><h3>Articles</h3><p>High-quality Wikipedia articles, each over 1000 words, covering diverse topics from science and technology to history, culture, and prominent figures.</p></div>
<div class="tile green" v-click><h3>Context sizes</h3><p>For each topic, contexts use increments of 2 sentences from 2 to 30, followed by increments of 5 sentences until 50.</p></div>
</div>

---

<div class="kicker">Atomic Sentence Extraction</div>

# Each unit presents a single, unambiguous piece of information

<div class="grid-2 wide-right mt-5">
<div>
<div class="tile blue"><h3>Extraction</h3><p>GPT-4o extracts atomic sentences by using the definition of atomic facts and multiple passes over an article.</p></div>
<div class="tile green mt-4"><h3>Response atomization</h3><p>The same process is applied to break down responses from each model into atomic sentences.</p></div>
<div class="tile amber mt-4"><h3>Validation</h3><p>1,000 atomic sentences were manually verified; only 12 were insufficiently atomic or had their meaning changed.</p></div>
</div>
<div class="media-rail"><img src="/assets/ckpk-response-atomization.png" class="media tall"></div>
</div>

---

<div class="kicker">WikiAtomic Pipeline</div>

# Building a controlled setting for CK/PK analysis

<div class="media-rail mt-4">
<img src="/assets/ckpk-pipeline.png" class="media tall">
</div>

---

<div class="kicker">Example</div>

# Atomic responses are mapped to contextual and parametric knowledge

<div class="media-rail mt-4">
<img src="/assets/ckpk-real-example.png" class="media tall">
</div>

<div class="caption">An example of context, question, model response, and the list of atomic responses mapped to contextual knowledge and parametric knowledge.</div>

---

<div class="kicker">Evaluation Setup</div>

# The evaluation compares atomic contexts with atomic responses

<div class="grid-2 mt-6">
<div>
<div class="tile green"><h3>CK/PK detection</h3><p>Using the atomic contexts as a reference, atomic responses are categorized as contextual or parametric knowledge with INFUSE.</p></div>
<div class="tile amber mt-4"><h3>Threshold calibration</h3><p>The threshold is set at 0.5; three annotators reviewed ambiguously scored sentences.</p></div>
<div class="tile red mt-4"><h3>Hallucination detection</h3><p>Sentences classified as parametric knowledge are further assessed using FActScore.</p></div>
</div>
<div class="tile blue">
<h3>Models</h3>
<ul class="model-list">
<li>GPT-4o</li>
<li>Claude 3 Opus, Sonnet, Haiku</li>
<li>Llama 3 70B and 8B</li>
<li>Mixtral 8x22B</li>
<li>Mistral 7B</li>
<li>Phi-3</li>
</ul>
<p class="fine mt-4">Knowledge-consistency is checked with SBERT by comparing the k=0 response and the longest input context.</p>
</div>
</div>

---

<div class="kicker">Definitions</div>

# Two sources inside one response

<div class="grid-2 mt-8">
<div class="tile green">
<h3>Contextual knowledge (CK)</h3>
<p>Atomic response content entailed by the supplied context.</p>
</div>
<div class="tile amber">
<h3>Parametric knowledge proxy (PK)</h3>
<p>Atomic response content not entailed by the supplied context; factuality is checked separately.</p>
</div>
</div>

<div class="takeaway mt-8">
LLMs do not simply reproduce the provided evidence: they mix grounded content with parametric supplementation, fail to use all available context, and reduce hallucination only gradually as contextual evidence increases.
</div>

---

<div class="kicker">CK/PK Composition</div>

# Models rely on a mix of contextual and parametric knowledge

<div class="figure-pair mt-4">
<div class="media-rail"><img src="/assets/ckpk-gpt4o.png" class="media short"></div>
<div class="media-rail"><img src="/assets/ckpk-phi.png" class="media short"></div>
</div>

<div class="grid-3 evidence-strip mt-4">
<div class="tile green"><h3>Contextual knowledge</h3><p>Larger contexts generally increase the model's reliance on contextual knowledge.</p></div>
<div class="tile amber"><h3>Parametric knowledge</h3><p>The average proportion remains similar for k = 30, 40, and 50.</p></div>
<div class="tile red"><h3>Model difference</h3><p>All models except Phi-3 show consistently similar patterns.</p></div>
</div>

---

<div class="kicker">Position Bias</div>

# Context use becomes positionally uneven

<div class="grid-2 wide-right mt-5">
<div>
<div class="tile green"><h3>Small k</h3><p>Models use different parts of context more evenly.</p></div>
<div class="tile amber mt-4"><h3>Larger k</h3><p>The first quartile receives increasing emphasis.</p></div>
<div class="tile red mt-4"><h3>Failure shape</h3><p>The model struggles more with the bottom half than with the middle alone.</p></div>
</div>
<div class="media-rail"><img src="/assets/context-position-gpt4o.png" class="media tall"></div>
</div>

---

<div class="kicker">Position Mapping</div>

# Context quartiles map most closely to corresponding response quartiles

<div class="grid-2 wide-right mt-5">
<div>
<div class="tile blue"><h3>Method</h3><p>Contexts and responses are divided into four quartiles and compared using cosine similarity of SBERT embeddings.</p></div>
<div class="tile green mt-4"><h3>Pattern</h3><p>The first context quartile maps most closely to the first, and to a lesser extent, the adjacent response quartile.</p></div>
<div class="tile amber mt-4"><h3>Interpretation</h3><p>The model prefers to match the positions of data.</p></div>
</div>
<div class="media-rail"><img src="/assets/context-where-went-gpt4o.png" class="media fit-wide"></div>
</div>

---

<div class="kicker">Similarity Analysis</div>

# Responses tend to include similar contextual knowledge but supplemental parametric knowledge

<div class="similarity-grid mt-4">
<div class="media-rail"><img src="/assets/sim-local-local-gpt4o.png" class="media sim"><div class="caption">Local vs. local</div></div>
<div class="media-rail"><img src="/assets/sim-global-global-gpt4o.png" class="media sim"><div class="caption">Global vs. global</div></div>
<div class="media-rail"><img src="/assets/sim-local-global-combined.png" class="media sim-wide"><div class="caption">Local vs. global</div></div>
</div>

<div class="grid-3 evidence-strip mt-4">
<div class="tile blue"><h3>Contextual knowledge</h3><p>Becomes increasingly similar with larger contexts.</p></div>
<div class="tile amber"><h3>Parametric knowledge</h3><p>Comes from a small pool of knowledge, though not as uniformly homogeneous.</p></div>
<div class="tile green"><h3>CK/PK similarity</h3><p>Rises to around 0.6, suggesting supplemental rather than unrelated parametric knowledge.</p></div>
</div>

---

<div class="kicker">Faithfulness</div>

# Hallucination drops early, then unsupported content plateaus

<div class="grid-2 wide-left mt-5">
<div class="media-rail"><img src="/assets/factscore.png" class="media tall"></div>
<div>
<div class="claim small">Context improves faithfulness.</div>
<p class="mt-4">Much of the improvement appears early; residual unsupported content remains.</p>
<div class="takeaway mt-6">
Supplied evidence changes model outputs in the expected direction, but not deterministically.
</div>
</div>
</div>

---

<div class="kicker">Study 2 Takeaway</div>

# Models exhibit a stable mixed-grounding pattern

<div class="grid-3 mt-8">
<div class="tile green"><h3>Evidence matters</h3><p>Models move toward contextual knowledge as evidence increases.</p></div>
<div class="tile amber"><h3>Memory persists</h3><p>Responses continue to include residual parametric content.</p></div>
<div class="tile red"><h3>Position matters</h3><p>Evidence is not used uniformly across the prompt.</p></div>
</div>

<div class="takeaway mt-8">
The next chapter extends contextual grounding to multilingual and later-context settings.
</div>

---
class: section-slide
---

<div class="section-number">Study 3 | Harder Grounding Conditions</div>

# Lost-in-the-Later: multilingual contextual grounding

<div class="subtitle mt-6">
The third study tests whether grounding remains stable when evidence appears later and must be tracked across languages.
</div>

---

<div class="kicker">Study 3 Framing</div>

# Extending contextual grounding to multilingual and later-context settings

<div class="grid-2 mt-8">
<div>
- Context is divided into quartiles.
- Response atoms are classified as CK or PK.
- CK atoms are mapped back to the source quartile.
- The setup extends the CK/PK question to English, Spanish, and Danish.
</div>
<div class="tile amber">
<h3>Grounding criterion</h3>
<p>Having relevant evidence available does not guarantee that a model will use it reliably.</p>
</div>
</div>

---

<div class="kicker">MultiWikiAtomic + CoPE</div>

# Measuring grounding and recall together

<div class="media-rail mt-4">
<img src="/assets/lostlater-pipeline.png" class="media tall">
</div>

<div class="caption">CoPE computes contextual knowledge score and context recall distribution.</div>

<div class="fine mt-3">Scoring calibration: Study 2 uses English INFUSE scoring at threshold 0.5; Study 3 uses multilingual NLI scoring at a calibrated 0.7 entailment threshold.</div>

---

<div class="kicker">Scale</div>

# A multilingual behavioral probe

<div class="grid-4 mt-7">
<div class="metric"><div class="value">6</div><div class="label">models</div></div>
<div class="metric green"><div class="value">3</div><div class="label">languages</div></div>
<div class="metric amber"><div class="value">10,800</div><div class="label">question-response pairs</div></div>
<div class="metric red"><div class="value">0.7</div><div class="label">calibrated entailment threshold</div></div>
</div>

<div class="grid-3 mt-8">
<div class="tile blue"><h3>Large models</h3><p>GPT-4o and Gemini 1.5 Pro.</p></div>
<div class="tile green"><h3>Open-weights LLMs</h3><p>Llama 3.2 90B and Llama 3.2 3B.</p></div>
<div class="tile amber"><h3>Reasoning models</h3><p>GPT-o3 and Qwen 3 235B.</p></div>
</div>

---

<div class="kicker">CK Across Languages</div>

# More context helps, but language changes the operating point

<div class="grid-3 mt-5">
<div class="media-rail"><img src="/assets/lostlater-ck-english.png" class="media short"></div>
<div class="media-rail"><img src="/assets/lostlater-ck-spanish.png" class="media short"></div>
<div class="media-rail"><img src="/assets/lostlater-ck-danish.png" class="media short"></div>
</div>

<div class="takeaway mt-5">
Most models reach around 70-75 CK in English and Spanish, while Danish is more challenging. Reasoning models remain lower, around 55 CK even with more context.
</div>

---

<div class="kicker">Context Recall</div>

# The last quartile is recalled least reliably

<div class="grid-2 wide-left mt-5">
<div class="media-rail"><img src="/assets/lostlater-recall-en.png" class="media tall"></div>
<div>
<div class="tile amber"><h3>Pattern</h3><p>The first context quartile receives the most recall; the final quartile contributes least.</p></div>
<div class="tile green mt-4"><h3>Context length</h3><p>The imbalance becomes stronger as context length increases.</p></div>
<div class="tile red mt-4"><h3>Language</h3><p>The pattern persists across languages and is harder in Danish.</p></div>
</div>
</div>

---

<div class="kicker">Randomization Check</div>

# Shuffling does not remove the later-context gap

<div class="grid-2 mt-5">
<div>
<table class="table-lite">
<thead><tr><th>Language</th><th class="num">Q1 exceeds Q4 at 50 contexts</th></tr></thead>
<tbody>
<tr><td>English</td><td class="num">14.63-26.11 pp</td></tr>
<tr><td>Spanish</td><td class="num">12.63-25.81 pp</td></tr>
<tr><td>Danish</td><td class="num">8.91-19.10 pp</td></tr>
</tbody>
</table>
</div>
<div>
<div class="tile amber"><h3>Randomized trials</h3><p>450 representative questions across three languages and six models produced 8,100 randomized trials.</p></div>
<div class="tile red mt-4"><h3>Interpretation</h3><p>Lost-in-the-later is not just natural article order. It persists when order is disrupted.</p></div>
</div>
</div>

---

<div class="kicker">Prompt-Level Intervention</div>

# A CK prompt improves grounding more than reasoning alone

<table class="table-lite mt-5">
<thead><tr><th>Prompt</th><th class="num">English</th><th class="num">Spanish</th><th class="num">Danish</th></tr></thead>
<tbody>
<tr><td>Original</td><td class="num">70.45</td><td class="num">70.22</td><td class="num">69.33</td></tr>
<tr><td>Strict</td><td class="num">75.86</td><td class="num">75.86</td><td class="num">76.67</td></tr>
<tr><td>Balanced</td><td class="num">61.54</td><td class="num">70.21</td><td class="num">64.00</td></tr>
<tr><td><strong>CK Prompt</strong></td><td class="num"><strong>78.72</strong></td><td class="num"><strong>78.95</strong></td><td class="num"><strong>77.50</strong></td></tr>
<tr><td>CoT</td><td class="num">73.10</td><td class="num">74.05</td><td class="num">75.22</td></tr>
<tr><td>CoT + CK Prompt</td><td class="num">75.10</td><td class="num">78.28</td><td class="num">76.91</td></tr>
</tbody>
</table>

<div class="takeaway mt-5">
The CK prompt improves CK by +8.4 percentage points absolute, about 12% relative over the original prompt.
</div>

---

<div class="kicker">Study 3 Takeaway</div>

# Grounding is unstable under position, language, and reasoning variation

<div class="grid-3 mt-8">
<div class="tile amber"><h3>Lost-in-the-later</h3><p>Later evidence is recalled less reliably even when relevant.</p></div>
<div class="tile green"><h3>Multilingual stress</h3><p>English patterns generalize, but Danish is harder in this evaluation.</p></div>
<div class="tile red"><h3>Reasoning and grounding</h3><p>Reasoning-model outputs do not automatically imply better grounding.</p></div>
</div>

<div class="takeaway mt-8">
This motivates the final study: a decode-time intervention that preserves correct answers under weak or distracting context while still allowing genuinely helpful evidence to matter.
</div>

---
class: section-slide
---

<div class="section-number">Study 4 | Decode-Time Intervention</div>

# No-Worse Context-Aware Decoding

<div class="subtitle mt-6">
NWCAD treats context use as a routing problem: reduce context-induced regressions when added context is neutral or distracting, yet still use context when it is genuinely corrective.
</div>

---

<div class="kicker">Neutral Regression</div>

# Context can help, but it can also cause neutral regression

<div class="grid-2 mt-8">
<div class="tile green">
<h3>Helpful context</h3>
<p>Provides evidence that corrects a wrong no-context answer.</p>
</div>
<div class="tile red">
<h3>Neutral or distracting context</h3>
<p>Does not license changing an already-correct no-context answer.</p>
</div>
</div>

<div class="takeaway red mt-8">
The goal is to reduce do-no-harm failures on questions that are already answered correctly without context.
</div>

---

<div class="kicker">Trade-off</div>

# Separating do-no-harm from context utilization clarifies the decoder choice

<div class="tradeoff-plane mt-5">
<div class="axis-y">Preservation</div>
<div class="axis-x">Context utilization</div>
<div class="trade-zone preserve">Preserve baseline-correct answers</div>
<div class="trade-zone use">Use genuinely corrective context</div>
<div class="trade-point noctx">No-context</div>
<div class="trade-point ctx">With-context</div>
<div class="trade-point cad">CAD-style shift</div>
<div class="trade-point nwcad">NWCAD target</div>
</div>

<div class="grid-2 mt-4">
<div class="tile blue">
<h3>Do-no-harm preservation</h3>
<p>Questions that are already answered correctly without context.</p>
</div>
<div class="tile green">
<h3>Context utilization</h3>
<p>Questions where the context can correct the answer.</p>
</div>
</div>

---

<div class="kicker">Controlled Benchmark</div>

# The benchmark separates two objectives

<div class="grid-3 mt-7">
<div class="tile blue"><h3>Restated</h3><p>Neutral context restates or aligns with the answer.</p></div>
<div class="tile red"><h3>Distractor</h3><p>Incorrect but non-entailing pressure.</p></div>
<div class="tile green"><h3>Helpful</h3><p>Context provides evidence that the baseline lacks.</p></div>
</div>

<div class="flow mt-8">
<div class="step" v-click>Preserve neutral</div>
<div class="arrow" v-after>+</div>
<div class="step" v-after>Use helpful</div>
<div class="arrow" v-after>-></div>
<div class="step" v-after>No-worse decoding</div>
</div>

---

<div class="kicker">Two-Stream Setup</div>

# Compare generation with and without context at every token

<div class="grid-2 mt-7">
<div class="equation">
No-context stream:<br>
<strong>z<sub>0</sub><sup>t</sup></strong> -> p<sub>0</sub><sup>t</sup>
</div>
<div class="equation">
With-context stream:<br>
<strong>z<sub>c</sub><sup>t</sup></strong> -> p<sub>c</sub><sup>t</sup>
</div>
</div>

<div class="grid-2 mt-7">
<div class="tile blue"><h3>Context pressure</h3><p>Jensen-Shannon divergence between p<sub>c</sub><sup>t</sup> and p<sub>0</sub><sup>t</sup>.</p></div>
<div class="tile green"><h3>Confidence</h3><p>Top-1 margin: how decisive each stream is about the next token.</p></div>
</div>

<div class="fine mt-5">Evaluation setting: logit access, greedy decoding, and thresholds tuned on Llama-3.1-8B then transferred.</div>

---

<div class="kicker">NWCAD Gate</div>

# A three-way decision at each token

<div class="media-rail mt-4">
<img src="/assets/nwcad-pipeline.png" class="media tall">
</div>

---

<div class="kicker">NWCAD Logic</div>

# Preserve when neutral; use context when confident

<div class="grid-3 mt-7">
<div class="tile blue">
<h3>Stage 1</h3>
<p>If context pressure is low and no-context is confident, copy the no-context logits exactly.</p>
</div>
<div class="tile green">
<h3>Stage 2</h3>
<p>If context is confident, use the context stream.</p>
</div>
<div class="tile amber">
<h3>Fallback</h3>
<p>If neither stream is decisive, use a CAD-style fallback decoder.</p>
</div>
</div>

<div class="takeaway mt-8">
This turns context-aware decoding from continuous tilting into regime selection.
</div>

---

<div class="kicker">Neutral Regression Evidence</div>

# Adding context often hurts baseline-correct neutral cases

<div class="grid-2 wide-right mt-5">
<div>
<div class="tile red"><h3>Controlled filter</h3><p>Baseline-correct filtering makes no-context accuracy 100% by construction.</p></div>
<div class="tile amber mt-4"><h3>Regression signal</h3><p>In this evaluation slice, any with-context drop is a context-induced regression.</p></div>
</div>
<div class="media-rail"><img src="/assets/nwcad-neutral-regression.png" class="media tall"></div>
</div>

---

<div class="kicker">Controlled Evaluation</div>

# NWCAD moves up and to the right

<div class="media-rail mt-4">
<img src="/assets/nwcad-tradeoff.png" class="media tall">
</div>

<div class="caption">Higher y means better neutral preservation; higher x means better helpful-context accuracy.</div>

---

<div class="kicker">Full-Slice Evaluation</div>

# On evaluated slices, NWCAD reduces do-no-harm regressions while maintaining helpful-context accuracy

<div class="media-rail full-figure mt-4">
<img src="/assets/nwcad-fullslice.png" class="media tall">
</div>

<div class="grid-3 evidence-strip mt-4">
<div class="tile blue"><h3>Regression reduction</h3><p>Reduced failures under distractor contexts in the evaluated settings.</p></div>
<div class="tile green"><h3>Helpful context</h3><p>Helpful-context gains are largely preserved across the evaluated slices.</p></div>
<div class="tile amber"><h3>Scope</h3><p>Logit access, greedy decoding, and transferred thresholds.</p></div>
</div>

---

<div class="kicker">Qualitative Example</div>

# NWCAD preserves baseline-correct answers on neutral contexts while still using helpful context when it should

<table class="table-lite mt-5">
<thead><tr><th>Slice</th><th>Question</th><th>Bad behavior</th><th>NWCAD behavior</th></tr></thead>
<tbody>
<tr><td>Restated</td><td>Dumbledore actor after the first one died</td><td>Contrastive decoders flip to Richard Harris</td><td>Preserves Michael Gambon</td></tr>
<tr><td>Distractor</td><td>When did the US normalize relations with China?</td><td>Distractor pulls answer toward 1978</td><td>Preserves January 1, 1979</td></tr>
<tr><td>Helpful</td><td>Voice of the T. rex in The Good Dinosaur</td><td>Baseline gives wrong answer</td><td>Uses context: Sam Elliott</td></tr>
</tbody>
</table>

<div class="takeaway mt-6">
When the context is non-informative, a decoder should preserve the no-context output; when it is informative, it should shift toward context to correct the answer.
</div>

---

<div class="kicker">Adapter Analysis</div>

# NWCAD improves existing two-stream decoders

<div class="grid-2 wide-left mt-5">
<div class="media-rail"><img src="/assets/nwcad-adapter.png" class="media tall"></div>
<div>
<div class="tile green"><h3>Plug-in adapter</h3><p>NWCAD can wrap CAD, AdaCAD, or CoCoA by changing the fallback decoder.</p></div>
<div class="tile amber mt-4"><h3>Where gains come from</h3><p>Largest improvements appear in distractor-heavy settings, with competitive or modest gains elsewhere.</p></div>
<div class="tile blue mt-4"><h3>Stage 2 matters</h3><p>Full NWCAD improves over the Stage-1-only version by 5.2 percentage points on average.</p></div>
</div>
</div>

---

<div class="kicker">Routing Statistics</div>

# Most tokens do not need contrastive mixing

<table class="table-lite mt-5">
<thead><tr><th>Slice</th><th class="num">No-ctx token %</th><th class="num">Ctx token %</th><th class="num">Fallback token %</th><th class="num">Any fallback ex. %</th></tr></thead>
<tbody>
<tr><td>Restated (mixed subset)</td><td class="num">75.14</td><td class="num">23.65</td><td class="num">1.21</td><td class="num">5.68</td></tr>
<tr><td>Distractor (mixed subset)</td><td class="num">73.70</td><td class="num">24.35</td><td class="num">1.95</td><td class="num">8.65</td></tr>
<tr><td>Helpful</td><td class="num">63.06</td><td class="num">35.06</td><td class="num">1.88</td><td class="num">10.68</td></tr>
<tr><td>NQ-SYNTH</td><td class="num">49.57</td><td class="num">48.66</td><td class="num">1.78</td><td class="num">6.70</td></tr>
<tr><td>NQ-SWAP</td><td class="num">37.88</td><td class="num">60.26</td><td class="num">1.86</td><td class="num">7.10</td></tr>
<tr><td>HotpotQA-distractor</td><td class="num">60.53</td><td class="num">38.39</td><td class="num">1.08</td><td class="num">4.70</td></tr>
</tbody>
</table>

<div class="takeaway mt-5">
Token routing uses fallback rarely; "any fallback" reports the fraction of examples where at least one fallback step occurs.
</div>

---

<div class="kicker">Limitations</div>

# What NWCAD does and does not solve

<div class="grid-2 mt-8">
<div class="tile green">
<h3>What it solves</h3>
<p>Reduces a particular downstream consequence of weak grounding: added context making outputs worse when that context is neutral, distracting, or otherwise unhelpful.</p>
</div>
<div class="tile red">
<h3>What remains</h3>
<p>Does not guarantee full uptake of later evidence, remove multilingual asymmetries, or work directly for black-box APIs without logits.</p>
</div>
</div>

---
class: section-slide
---

<div class="section-number">Synthesis</div>

# The same failure pattern appears across the dissertation

<div class="subtitle mt-6">
The model responds to context, but context remains a competing signal rather than a hard boundary on behavior.
</div>

---

<div class="kicker">Unified Pattern</div>

# Context remains a competing signal

<div class="storyline mt-7">
<div><span class="tag blue">Social</span></div><div>Role-play changes behavior</div><div>Generic assistant habits persist</div>
<div><span class="tag green">CK/PK</span></div><div>Evidence changes composition</div><div>Residual PK persists</div>
<div><span class="tag amber">Position</span></div><div>Later evidence is available</div><div>Earlier evidence dominates recall</div>
<div><span class="tag red">Decoding</span></div><div>Control can shift behavior</div><div>It does not erase deeper instability</div>
</div>

---

<div class="kicker">Implications</div>

# Trustworthy behavior should be evaluated less by fluent output alone and more by situational obedience

<div class="grid-2 mt-8">
<div class="claim small">Not just: "Is the output fluent?"</div>
<div class="claim small">But: "Did the right context govern the output?"</div>
</div>

<div class="takeaway mt-8">
This reframes role-play, hallucination, multilingual recall, long-context behavior, and decoding control as connected symptoms of one context-use problem.
</div>

---

<div class="kicker">Contributions</div>

# Dissertation contributions

<div class="grid-2 mt-7">
<div class="tile blue"><h3>Social adaptation</h3><p>CRD shows role-play changes both user behavior and model behavior while exposing persistent assistant defaults.</p></div>
<div class="tile green"><h3>Knowledge composition</h3><p>WikiAtomic CK/PK analysis shows evidence and memory coexist even in knowledge-consistent settings.</p></div>
<div class="tile amber"><h3>Multilingual positional grounding</h3><p>CoPE identifies lost-in-the-later as a stable failure mode across language and prompt variations.</p></div>
<div class="tile red"><h3>Decode-time control</h3><p>NWCAD reduces neutral regression while preserving context utilization.</p></div>
</div>

---

<div class="kicker">Final Discussion</div>

# Across the four studies, context works but remains a competing signal

<div class="grid-2 mt-7">
<div class="tile blue"><h3>Social context</h3><p>Role-play reorganizes user and model behavior, while generic assistant habits persist.</p></div>
<div class="tile green"><h3>Informational context</h3><p>Evidence changes the composition of responses, but residual parametric knowledge remains.</p></div>
<div class="tile amber"><h3>Longer context</h3><p>Later evidence is available, but earlier evidence dominates recall in multilingual settings.</p></div>
<div class="tile red"><h3>Decode-time control</h3><p>Control can shift behavior, but it does not guarantee full uptake of relevant context.</p></div>
</div>

---

<div class="kicker">Conclusion</div>

# Contextual adaptation requires measuring whether the right context governs the output

<div class="grid-3 mt-8">
<div class="tile blue"><h3>Diagnose</h3><p>Measure where context changes behavior and where defaults persist.</p></div>
<div class="tile green"><h3>Ground</h3><p>Separate contextual knowledge from parametric knowledge in generated responses.</p></div>
<div class="tile red"><h3>Control</h3><p>Reduce context-induced regressions while preserving helpful-context gains.</p></div>
</div>

<div class="takeaway mt-8">
The dissertation frames role-play, hallucination, multilingual recall, long-context behavior, and decoding control as connected symptoms of one context-use problem.
</div>

---
class: section-slide
---

<div class="kicker">Future Work</div>

# Context becomes an evolving workspace in agentic systems

<div class="subtitle mt-6">
Context is no longer only the text that conditions one response. It becomes the evolving workspace through which a system must navigate.
</div>

---

<div class="kicker">Future Work</div>

# Multi-agent knowledge systems

<div class="grid-2 wide-right future-work-grid">
<div>
<div class="claim small">Different agents may retrieve evidence, propose interpretations, summarize findings, critique one another, and update shared state over time.</div>
<div class="research-target blue mt-5">Evaluation target: whether agents maintain a grounded account of what is known, uncertain, superseded, and evidence-backed.</div>
<div class="takeaway mt-6">Failures should not enter working knowledge and shape subsequent retrieval, coordination, or synthesis as if already verified.</div>
</div>
<div class="future-map blue">
<div class="future-map-title">shared knowledge state</div>
<div class="future-row"><span>known</span><p>claims held by the system</p></div>
<div class="future-row"><span>uncertain</span><p>claims needing retrieval or critique</p></div>
<div class="future-row"><span>superseded</span><p>claims revised by later evidence</p></div>
<div class="future-row"><span>evidence-backed</span><p>claims linked to provenance</p></div>
</div>
</div>

---

<div class="kicker">Future Work</div>

# Context navigation

<div class="grid-2 wide-left future-work-grid">
<div class="future-map green">
<div class="future-map-title">context path</div>
<div class="future-row"><span>retrieve</span><p>recover the relevant source</p></div>
<div class="future-row"><span>locate</span><p>identify the source evidence for the next step</p></div>
<div class="future-row"><span>revise</span><p>use later evidence to overturn earlier interpretation</p></div>
<div class="future-row"><span>govern</span><p>apply it to the next decision</p></div>
</div>
<div>
<div class="claim small">Having relevant evidence available does not guarantee that a model will use it reliably.</div>
<div class="research-target green mt-5">Evaluation target: how often the relevant source is used, when later evidence overturns earlier interpretation, and how quickly context use decays.</div>
<div class="takeaway green mt-6">The practical challenge is not only whether a model can ingest more context, but whether it can move through context well enough to recover, compare, and revise the information needed for the next decision.</div>
</div>
</div>

---

<div class="kicker">Future Work</div>

# Context focus and control

<div class="grid-2 wide-right future-work-grid">
<div>
<div class="claim small">Context is reordered by retrieval, compressed by summarization, filtered by tool selection, and transformed into intermediate state.</div>
<div class="research-target amber mt-5">Evaluation target: grounded uptake, revision from new evidence, and preservation of correct baseline behavior under neutral or misleading context.</div>
<div class="takeaway amber mt-6">Each step can either preserve or weaken grounding; contextual reliability is a pipeline-level problem.</div>
</div>
<div class="future-map amber">
<div class="future-map-title">control surface</div>
<div class="future-row"><span>retrieval</span><p>increase grounded uptake</p></div>
<div class="future-row"><span>memory</span><p>support revision from new evidence</p></div>
<div class="future-row"><span>prompting</span><p>focus the context to be used</p></div>
<div class="future-row"><span>decoding</span><p>preserve correct baseline behavior</p></div>
</div>
</div>

---

<div class="kicker">Future Work</div>

# Systems with memory,<br>retrieval, tools, and action

<div class="grid-2 wide-left future-work-grid">
<div class="future-map red">
<div class="future-map-title">extended trajectory</div>
<div class="future-row"><span>memory</span><p>maintain state over time</p></div>
<div class="future-row"><span>retrieval</span><p>navigate changing context</p></div>
<div class="future-row"><span>tools</span><p>coordinate tool use with evidence</p></div>
<div class="future-row"><span>action</span><p>remain grounded while acting</p></div>
</div>
<div>
<div class="claim small">Context is the operating environment within which the system searches, writes, revises, delegates, and acts.</div>
<div class="research-target red mt-5">Evaluation target: whether context governs the construction and use of working knowledge across extended trajectories.</div>
<div class="takeaway red mt-6">Judge systems not only by task completion or output quality, but by whether they remain grounded while navigating changing context over time.</div>
</div>
</div>

---

<div class="thanks">
<div class="kicker">Closing</div>

<div class="quote-large">
LLMs become more reliable when context moves from being an input that influences generation to a constraint that governs it.
</div>

<div class="byline mt-12">Thank you.</div>
</div>
