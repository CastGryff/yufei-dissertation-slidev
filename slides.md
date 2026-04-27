---
theme: default
title: Toward Contextual Adaptation and Knowledge Grounding in Large Language Models
info: |
  Dissertation defense deck for Yufei Tao.
addons:
  - slidev-component-progress
aspectRatio: 16/9
canvasWidth: 960
fonts:
  sans: Inter
  mono: Fira Code
  provider: none
class: cover-slide
drawings:
  persist: false
transition: fade
mdc: true
---

<div class="cover-field">
  <svg class="cover-routes" viewBox="0 0 520 420" preserveAspectRatio="none" aria-hidden="true">
    <defs>
      <path id="cover-social-path" d="M151 142 C177 190 218 215 250 228" />
      <path id="cover-info-path" d="M369 142 C343 190 302 215 270 228" />
      <path id="cover-outcome-path" d="M260 292 C260 306 260 318 260 326" />
    </defs>
    <path class="route social" d="M151 142 C177 190 218 215 250 228" />
    <path class="route informational" d="M369 142 C343 190 302 215 270 228" />
    <path class="route outcome" d="M260 292 C260 306 260 318 260 326" />
    <circle class="route-packet social" r="4.4">
      <animateMotion dur="3s" repeatCount="indefinite"><mpath href="#cover-social-path" /></animateMotion>
    </circle>
    <circle class="route-packet informational" r="4.4">
      <animateMotion dur="3.35s" begin=".45s" repeatCount="indefinite"><mpath href="#cover-info-path" /></animateMotion>
    </circle>
  </svg>
  <div class="cover-symbol social">
    <PublicAssetImg path="assets/flaticon/tinted/role-blue.png" />
  </div>
  <div class="cover-symbol informational">
    <PublicAssetImg path="assets/flaticon/tinted/evidence-green.png" />
  </div>
  <div class="cover-symbol-label social">ADAPTATION</div>
  <div class="cover-symbol-label informational">GROUNDING</div>
  <div class="cover-vellum" aria-hidden="true"></div>
  <div class="cover-node">
    <PublicAssetImg path="assets/flaticon/tinted/brain-white.png" />
  </div>
  <div class="cover-symbol-label control">CONTROL</div>
  <div class="cover-symbol outcome">
    <PublicAssetImg path="assets/flaticon/tinted/target-amber.png" />
  </div>
  <div class="cover-symbol-label outcome">RELIABILITY</div>
</div>

<div class="cover-copy">
<div class="kicker">Dissertation Defense</div>

# Toward Contextual<br>Adaptation and<br>Knowledge Grounding in<br>Large Language Models

<div class="byline mt-7">
<div class="presenter-name">Yufei Tao</div>
<div>Dissertation Defense · April 2026</div>
<div>Department of Computer Science · Portland State University</div>
<div class="committee-block">
<div><span>Chair</span> Dr. Ameeta Agrawal</div>
<div><span>Committee</span> Dr. Suresh Singh · Dr. Tetyana Sydorenko · Dr. Wu-chi Feng</div>
</div>
</div>
</div>

---

<div class="kicker">Motivation</div>

# As LLMs move from research benchmarks into real-world applications, the demands on them change

<div class="grid-2 mt-5">
<div class="tile green">
<h3>Faithful to the material it was given</h3>
<p>A model that summarizes a legal document, assists a medical professional, or answers questions in a retrieval-augmented pipeline is expected to use the supplied evidence.</p>
</div>
<div class="tile blue">
<h3>Fits the social situation</h3>
<p>A chatbot helping a language learner practice a difficult conversation is expected to respond in a way that fits the social situation.</p>
</div>
</div>

<div class="motivation-example mt-5">
<div class="example-label">Example</div>
<div class="example-card blue">
<strong>Role cue</strong>
<span>"Let's role-play that you are my boss Lisa. I need to ask for an extension."</span>
</div>
<div class="example-card green">
<strong>Evidence cue</strong>
<span>Passage: "The deadline moved to Friday." Question: "When is it due?"</span>
</div>
</div>

<div class="takeaway mt-5">
The same reliability question appears in both cases: does the relevant context constrain the output?
</div>

---

<div class="kicker">Two Meanings of Context</div>

# Context leads to two reliability targets

<div class="context-map mt-7">
<div class="context-path blue">
<div class="context-source">Social context</div>
<div class="context-terms">roles · expectations · intentions · norms</div>
<div class="context-arrow">leads to</div>
<div class="context-target">Contextual adaptation</div>
<div class="context-desc">behavior that fits the social situation</div>
</div>
<div class="context-path green">
<div class="context-source">Informational context</div>
<div class="context-terms">passages · facts · language-specific cues</div>
<div class="context-arrow">leads to</div>
<div class="context-target">Knowledge grounding</div>
<div class="context-desc">claims anchored in supplied evidence</div>
</div>
</div>

<div class="takeaway mt-6">
The dissertation treats both as complementary requirements for reliable LLM behavior.
</div>

---
class: pop-slide
---

<div class="kicker">Central Claim</div>

# Across the models and settings studied here, LLMs are context-sensitive, yet context only partially governs their outputs

<div class="grid-2 wide-right mt-7">
<div class="tile blue">
<h3>They respond to context</h3>
<p>Current LLMs respond to role cues, supplied evidence, prompt structure, and decode-time controls.</p>
</div>
<div class="tile amber">
<h3>The response is uneven</h3>
<p>Context acts less like a hard boundary on behavior than like a competing signal.</p>
</div>
</div>

<div class="takeaway mt-7">
Together, the four studies move from empirical diagnosis to a bounded decode-time intervention for one downstream reliability problem.
</div>

---
class: pop-slide
---

<div class="kicker">Roadmap</div>

# From diagnosis to intervention

<div class="storyline compact rowed mt-5">
<div class="story-row"><div><span class="tag blue">1</span></div><div><strong>Role-play interaction</strong></div><div>Social adaptation</div></div>
<div class="story-row"><div><span class="tag green">2</span></div><div><strong>Contextual vs. parametric knowledge</strong></div><div>Knowledge-consistent grounding</div></div>
<div class="story-row"><div><span class="tag amber">3</span></div><div><strong>Lost-in-the-Later</strong></div><div>Multilingual and positional grounding</div></div>
<div class="story-row focus"><div><span class="tag red">4</span></div><div><strong>No-Worse Context-Aware Decoding</strong></div><div>Decode-time control</div></div>
<div class="story-row"><div><span class="tag violet">5</span></div><div><strong>Synthesis</strong></div><div>Context as a control problem</div></div>
</div>

<div class="fine mt-5">The dissertation asks how LLMs adapt to context, how stable grounding is under harder conditions, and whether inference-time control can reduce one reliability failure.</div>

---

<div class="kicker">Publications</div>

# Publications from this doctoral work

<div class="pub-list mt-5">
<div class="pub-row"><span>2026</span><div><strong>Tao & Agrawal.</strong> No-Worse Context-Aware Decoding. Findings of ACL.</div></div>
<div class="pub-row"><span>2025</span><div><strong>Pokharel, Tao, & Agrawal.</strong> CAPO. IJCNLP-AACL Findings.</div></div>
<div class="pub-row"><span>2025</span><div><strong>Tao, Hiatt, Seetharaman, & Agrawal.</strong> Lost-in-the-Later. RARA at ICDM.</div></div>
<div class="pub-row"><span>2024</span><div><strong>Tao, Hiatt, Haake, Jetter, & Agrawal.</strong> When Context Leads but Parametric Memory Follows. EMNLP.</div></div>
<div class="pub-row"><span>2024</span><div><strong>Jetter, Agrawal, Hongchai, Weber, & Tao.</strong> Training Practitioners for Real-time Product Development Using Generative Artificial Intelligence. PICMET.</div></div>
<div class="pub-row"><span>2024</span><div><strong>Tao, Agrawal, Dombi, Sydorenko, & Lee.</strong> ChatGPT Role-play Dataset. LREC-COLING.</div></div>
<div class="pub-row"><span>2024</span><div><strong>Sydorenko, Dombi, Agrawal, Thorne, Lee, & Tao.</strong> Spoken Dialogue Systems and ChatGPT for Second Language Pragmatics Research. Routledge Handbook chapter.</div></div>
<div class="pub-row"><span>2024</span><div><strong>Tao, Mines, & Agrawal.</strong> Making a Long Story Short in Conversation Modeling. TEICAI at EACL.</div></div>
</div>

---

<div class="kicker">Related Work</div>

# How each study extends prior work

<div class="related-work mt-5">
<div class="rw-head"><div>Study</div><div>Prior work</div><div>This dissertation</div></div>
<div class="rw-row">
<div class="rw-paper blue">Role-play interaction</div>
<div>Dialogue systems, CASA, Gricean pragmatics, and accommodation theory study social expectations in interaction.</div>
<div>We introduced the CRD dataset and measured user motives and model naturalness across various roles.</div>
</div>
<div class="rw-row">
<div class="rw-paper green">Contextual vs. parametric knowledge</div>
<div>RAG, knowledge-conflict studies, and factuality metrics study grounding, memory, and claim-level support.</div>
<div>We introduced WikiAtomic and classified atomic response content as contextual or parametric in knowledge-consistent QA.</div>
</div>
<div class="rw-row">
<div class="rw-paper amber">Lost-in-the-Later</div>
<div>Long-context work such as Lost in the Middle shows that position changes retrieval and use.</div>
<div>We proposed CoPE and MultiWikiAtomic to measure multilingual, positional grounding.</div>
</div>
<div class="rw-row">
<div class="rw-paper red">No-Worse Context-Aware Decoding</div>
<div>CAD, AdaCAD, and CoCoA tilt decoding toward tokens boosted by context-conditioned generation.</div>
<div>We proposed NWCAD to separate preservation from context utilization at decode time.</div>
</div>
</div>

<div class="fine mt-4">Representative references include Weizenbaum; Nass and Moon; Grice; Giles et al.; Longpre et al.; Min et al.; Liu et al.; Shi et al.; Wang et al.; and Khandelwal et al.</div>

---
class: section-slide
---

<div class="section-number">Study 1 | Social Context</div>

# Conversational adaptability and response efficiency in role-play interactions

<div class="subtitle mt-6">
Characterizing social-context adaptability in CRD.
</div>

<div class="fine mt-5">The CRD dataset contains 57 participants, 85 conversations, and 1,742 utterances across regular and role-play ChatGPT-3.5 interactions collected in March-April 2023.</div>
<div class="fine mt-2">User motives and model naturalness were annotated with substantial agreement.</div>

<div class="section-paper-ref">
Paper: Tao et al., "ChatGPT Role-play Dataset: Analysis of User Motives and Model Naturalness," LREC-COLING 2024.
</div>

---

<div class="kicker">Result 1</div>

# Role-play changes conversation rhythm, while the verbosity gap remains

<table class="table-lite mt-5">
<thead>
<tr><th>Measure</th><th class="num">Vanilla</th><th class="num">Boss</th><th class="num">Classmate</th></tr>
</thead>
<tbody>
<tr><td>Average conversation length, turns</td><td class="num"><strong>29.59</strong></td><td class="num">14.57</td><td class="num">17.11</td></tr>
<tr><td>Average human utterance length, words</td><td class="num">12.18</td><td class="num"><strong>20.58</strong></td><td class="num">19.06</td></tr>
<tr><td>Average ChatGPT utterance length, words</td><td class="num"><strong>77.66</strong></td><td class="num">35.78</td><td class="num">46.10</td></tr>
<tr><td>Human questions as percent of conversation</td><td class="num"><strong>26.34</strong></td><td class="num">21.32</td><td class="num">21.29</td></tr>
<tr><td>ChatGPT questions as percent of conversation</td><td class="num">14.69</td><td class="num">20.34</td><td class="num"><strong>32.57</strong></td></tr>
</tbody>
</table>

<div class="takeaway mt-5">
Users in role-play produce longer turns; ChatGPT changes too, while remaining systematically more verbose than human turns.
</div>

---

<div class="kicker">Result 2</div>

# Role-play raises naturalness, but assistant defaults remain

<div class="grid-2 crd-naturalness-figures mt-4">
<div class="media-rail"><img src="/assets/user-motives.png" class="media short"></div>
<div class="media-rail"><img src="/assets/model-naturalness.png" class="media short"></div>
</div>

<div class="takeaway mt-4">
Role cues suppress "as an AI" behavior and increase naturalness; verbosity and over-helpfulness remain.
</div>

<div class="fine mt-3">Naturalness is a pragmatic annotation of conversational behavior, not a measure of task success or factual correctness.</div>

---

<div class="kicker">Study 1 Takeaway</div>

# CRD shows that social context changes LLM behavior unevenly

<div class="grid-3 mt-8">
<div class="tile blue"><h3>We introduced CRD</h3><p>A human-AI role-play dataset with utterance-level user motive and model naturalness labels.</p></div>
<div class="tile amber"><h3>Social adaptation has limits</h3><p>Role cues improve naturalness while verbosity, over-helpfulness, and partial misreading of user intent persist.</p></div>
<div class="tile green"><h3>From roles to evidence</h3><p>If role cues only partially govern behavior, the next question is whether supplied evidence governs factual content.</p></div>
</div>

---
class: section-slide
---

<div class="section-number">Study 2 | Informational Context</div>

# When Context Leads but Parametric Memory Follows

<div class="subtitle mt-6">
Contextual vs. parametric knowledge in LLM outputs.
</div>

<div class="section-paper-ref">
Paper: Tao et al., "When Context Leads but Parametric Memory Follows in Large Language Models," EMNLP 2024.
</div>

---

<div class="kicker">Operational Definitions</div>

# Contextual and parametric knowledge are labels over atomic response content

<div class="atom-definition mt-5">
<div class="atom-label">Atomic response content</div>
<div class="atom-equation">model response &rarr; atom<sub>1</sub>, atom<sub>2</sub>, ... atom<sub>n</sub></div>
<div class="atom-desc">Each atom is one factual proposition extracted from the response; each atom is labeled by entailment against the supplied context.</div>
</div>

<div class="grid-2 mt-5">
<div class="tile green">
<h3>Contextual knowledge (CK)</h3>
<p>Atomic response content entailed by the supplied context.</p>
</div>
<div class="tile amber">
<h3>Parametric knowledge (PK)</h3>
<p>Atomic response content unsupported by the supplied context; factuality is checked separately.</p>
</div>
</div>

<div class="grid-2 evidence-strip mt-5">
<div class="tile green"><h3>Test item</h3><p>Topic, a chosen number of atomic context sentences, open-ended question, and atomized model response.</p></div>
<div class="tile blue"><h3>Knowledge-consistent setting</h3><p>Older Wikipedia contexts test grounding while staying broadly compatible with model prior knowledge.</p></div>
</div>

<div class="takeaway mt-5">
The evaluation asks which generated claims are supported by the supplied context and which generated claims go beyond it.
</div>

---

<div class="kicker">WikiAtomic Construction</div>

# WikiAtomic controls context length and supports atomic CK/PK evaluation

<div class="grid-4 mt-6">
<div class="metric blue"><div class="value">200</div><div class="label">Wikipedia articles</div></div>
<div class="metric green"><div class="value">50</div><div class="label">atomic sentences per article</div></div>
<div class="metric amber"><div class="value">10,000</div><div class="label">atomic sentences</div></div>
<div class="metric red"><div class="value">4,000</div><div class="label">topic-context instances</div></div>
</div>

<div class="grid-3 evidence-strip mt-5">
<div class="tile blue" v-click><h3>Construction</h3><p>High-quality Wikipedia articles are decomposed into atomic sentences; context sizes grow from 2 to 50 sentences.</p></div>
<div class="tile green" v-click><h3>Scoring</h3><p>Model responses are atomized and compared against atomic contexts with the INFUSE entailment scorer at threshold 0.5.</p></div>
<div class="tile amber" v-click><h3>Models</h3><p>GPT-4o, Claude 3, Llama 3, Mixtral, Mistral, and Phi-3.</p></div>
</div>

<div class="fine mt-5">Validation: 1,000 atomic sentences were manually verified; only 12 were insufficiently atomic or had their meaning changed. Threshold calibration: three annotators reviewed ambiguous INFUSE scores.</div>

---

<div class="kicker">Example</div>

# Atomic responses are mapped to contextual and parametric knowledge

<div class="media-rail mt-4">
<img src="/assets/ckpk-real-example.png" class="media tall">
</div>

<div class="caption">An example of context, question, model response, and the list of atomic responses mapped to contextual knowledge and parametric knowledge.</div>

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
<div class="tile red"><h3>Model difference</h3><p>Most models show similar CK/PK trends; Phi-3 is the main exception in some settings.</p></div>
</div>

---

<div class="kicker">Position Bias</div>

# Context use becomes positionally uneven

<div class="grid-2 wide-right mt-5">
<div>
<div class="tile green"><h3>Small k</h3><p>Models use different parts of context more evenly.</p></div>
<div class="tile amber mt-4"><h3>Larger k</h3><p>The first quartile receives increasing emphasis.</p></div>
<div class="tile red mt-4"><h3>Failure shape</h3><p>Later evidence is recalled less reliably than earlier evidence, especially as k grows.</p></div>
</div>
<div class="media-rail"><img src="/assets/context-position-gpt4o.png" class="media tall"></div>
</div>

---

<div class="kicker">Similarity Analysis</div>

# Responses tend to include similar contextual knowledge and topically related parametric content

<div class="similarity-grid mt-4">
<div class="media-rail"><img src="/assets/sim-local-local-gpt4o.png" class="media sim"><div class="caption">Local vs. local</div></div>
<div class="media-rail"><img src="/assets/sim-global-global-gpt4o.png" class="media sim"><div class="caption">Global vs. global</div></div>
<div class="media-rail"><img src="/assets/sim-local-global-combined.png" class="media sim-wide"><div class="caption">Local vs. global</div></div>
</div>

<div class="grid-3 evidence-strip mt-4">
<div class="tile blue"><h3>Contextual knowledge</h3><p>Becomes increasingly similar with larger contexts.</p></div>
<div class="tile amber"><h3>Parametric knowledge</h3><p>Repeatedly draws on certain pieces of information, though less uniformly than contextual knowledge.</p></div>
<div class="tile green"><h3>CK/PK similarity</h3><p>Rises to around 0.6, suggesting related rather than unrelated parametric content.</p></div>
</div>

<div class="fine mt-4">SBERT sentence-embedding similarity supports topical relatedness, not usefulness or factual support.</div>

---

<div class="kicker">Faithfulness</div>

# FActScore factuality evaluation improves for PK-classified content as context increases

<div class="grid-2 wide-left mt-5">
<div class="media-rail"><img src="/assets/factscore.png" class="media tall"></div>
<div>
<div class="claim small">PK factuality scores improve.</div>
<p class="mt-4">Residual parametric knowledge remains at larger context sizes.</p>
<div class="takeaway mt-6">
FActScore factuality evaluation checks factuality separately from CK/PK grounding; supplied evidence changes model outputs in the expected direction, but not deterministically.
</div>
</div>
</div>

---

<div class="kicker">Study 2 Takeaway</div>

# Models exhibit a mixed-grounding pattern in the tested WikiAtomic setting

<div class="grid-3 mt-8">
<div class="tile green"><h3>Evidence matters</h3><p>Models move toward contextual knowledge as evidence increases.</p></div>
<div class="tile amber"><h3>Memory persists</h3><p>Responses continue to include residual parametric content.</p></div>
<div class="tile red"><h3>Position matters</h3><p>Evidence is not used uniformly across the prompt.</p></div>
</div>

<div class="takeaway mt-8">
Even in a knowledge-consistent setting, evidence changes outputs without fully governing them. The next chapter extends contextual grounding to multilingual and later-context settings.
</div>

---
class: section-slide
---

<div class="section-number">Study 3 | Harder Grounding Conditions</div>

# Lost-in-the-Later: multilingual contextual grounding

<div class="subtitle mt-6">
The third study tests whether grounding remains stable when evidence appears later in the prompt and when grounding is evaluated across English, Spanish, and Danish.
</div>

<div class="section-paper-ref">
Paper: Tao et al., "Lost-in-the-Later: Framework for Quantifying Contextual Grounding in Large Language Models," RARA at ICDM 2025.
</div>

---

<div class="kicker">MultiWikiAtomic + CoPE</div>

# CoPE measures whether later evidence is grounded across languages

<div class="media-rail pipeline-wide mt-4">
<img src="/assets/lostlater-pipeline.png" class="media cope-pipeline">
</div>

<div class="grid-3 evidence-strip mt-3">
<div class="tile blue"><h3>Atomize</h3><p>Input context and model responses are broken into atomic factual propositions.</p></div>
<div class="tile green"><h3>Label CK vs. PK</h3><p>Each response atom is checked against the supplied context with multilingual NLI.</p></div>
<div class="tile amber"><h3>Measure recall position</h3><p>Entailed response atoms are traced back to context segments to estimate early, middle, and later evidence use.</p></div>
</div>

<div class="fine mt-3">MultiWikiAtomic extends WikiAtomic to English, Spanish, and Danish. Scale: 6 models, 10,800 question-response pairs, calibrated entailment threshold 0.7. CoPE reports contextual knowledge score and context recall distribution.</div>

---

<div class="kicker">CK Across Languages</div>

# More context helps, but language changes the operating point

<div class="grid-3 mt-5">
<div class="media-rail"><img src="/assets/lostlater-ck-english.png" class="media short"></div>
<div class="media-rail"><img src="/assets/lostlater-ck-spanish.png" class="media short"></div>
<div class="media-rail"><img src="/assets/lostlater-ck-danish.png" class="media short"></div>
</div>

<div class="takeaway mt-5">
Most models reach CK scores around 70-75 in English and Spanish, while Danish has lower CK in this evaluation. The tested reasoning models show lower CK, possibly due to longer or more autonomous answer structure.
</div>

---

<div class="kicker">Context Recall</div>

# The last quartile is recalled least reliably

<div class="grid-2 wide-left mt-5">
<div class="media-rail"><img src="/assets/lostlater-recall-en.png" class="media tall"></div>
<div>
<div class="tile amber"><h3>Pattern</h3><p>The first context quartile receives the most recall; the final quartile contributes least.</p></div>
<div class="tile green mt-4"><h3>Context length</h3><p>The imbalance becomes stronger as context length increases.</p></div>
<div class="tile red mt-4"><h3>Language</h3><p>The pattern persists across languages; the Danish setting shows larger recall difficulty in this evaluation.</p></div>
</div>
</div>

---

<div class="kicker">Randomization Check</div>

# Later evidence is still underused after sentence-order randomization

<div class="grid-2 mt-5">
<div>
<table class="table-lite">
<thead><tr><th>Language</th><th class="num">Absolute Q1-over-Q4 recall gap at context length 50</th></tr></thead>
<tbody>
<tr><td>English</td><td class="num">14.63-26.11 pp</td></tr>
<tr><td>Spanish</td><td class="num">12.63-25.81 pp</td></tr>
<tr><td>Danish</td><td class="num">8.91-19.10 pp</td></tr>
</tbody>
</table>
</div>
<div>
<div class="tile red"><h3>Interpretation</h3><p>This is not just because Wikipedia articles put easier facts first; the later-context gap remains after order is randomized.</p></div>
<div class="tile amber mt-4"><h3>Randomized trials</h3><p>450 representative questions across three languages and six models produced 8,100 randomized trials.</p></div>
</div>
</div>

---

<div class="kicker">PK Position</div>

# Parametric content accumulates later in responses

<div class="grid-2 wide-left mt-5">
<div class="media-rail"><img src="/assets/lostlater-pk-position.png" class="media tall"></div>
<div>
<div class="tile amber"><h3>Pattern</h3><p>PK is increasingly concentrated toward later response quartiles.</p></div>
<div class="tile green mt-4"><h3>Interpretation</h3><p>Content not grounded in the supplied context can enter after the response has already established a grounded opening.</p></div>
<div class="tile red mt-4"><h3>Connection</h3><p>This strengthens the position-bias account: later prompt evidence is underused while later response content is more likely to draw on PK.</p></div>
</div>
</div>

---

<div class="kicker">Contradiction</div>

# Counterfactual contexts separate grounding from truth

<div class="grid-2 wide-left mt-5">
<div>
<table class="table-lite compact">
<thead><tr><th>Model</th><th class="num">Factual</th><th class="num">All CF</th><th class="num">True first</th><th class="num">False first</th></tr></thead>
<tbody>
<tr><td>GPT-4o</td><td class="num">72.11</td><td class="num">69.40</td><td class="num">71.22</td><td class="num">68.51</td></tr>
<tr><td>Gemini 1.5 Pro</td><td class="num">76.29</td><td class="num">64.97</td><td class="num">71.97</td><td class="num">67.28</td></tr>
<tr><td>Llama 3.2 90B</td><td class="num">76.32</td><td class="num">66.91</td><td class="num">74.44</td><td class="num">64.40</td></tr>
<tr><td>Llama 3.2 3B</td><td class="num">73.13</td><td class="num">68.27</td><td class="num">72.97</td><td class="num">68.48</td></tr>
<tr><td>GPT-o3</td><td class="num">49.58</td><td class="num">46.34</td><td class="num">55.75</td><td class="num">54.37</td></tr>
<tr><td>Qwen 3 235B</td><td class="num">55.30</td><td class="num">52.85</td><td class="num">58.02</td><td class="num">55.62</td></tr>
</tbody>
</table>
<div class="caption">CK scores in English under factual, counterfactual, true-first, and false-first contexts.</div>
</div>
<div>
<div class="tile red"><h3>All counterfactual</h3><p>All 20 context sentences are made non-factual by swapping named entities with plausible alternatives.</p></div>
<div class="tile amber mt-4"><h3>Mixed order</h3><p>True-first and false-first settings mix factual and counterfactual evidence to test order sensitivity.</p></div>
<div class="tile green mt-4"><h3>Interpretation</h3><p>All-counterfactual contexts lower CK relative to factual contexts; mixed settings expose order sensitivity. CK measures grounding to the input, not truth in the world.</p></div>
</div>
</div>

---

<div class="kicker">Prompt-Level Intervention</div>

# In the 50-context Llama 3.2 90B setting, CK Prompt gives the highest CK

<div class="fine mt-3">LLaMA 3.2 90B, 50-context setting. CK Prompt explicitly asks for context-grounded answers; CoT refers to chain-of-thought prompting.</div>

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
CoT alone does not match the CK Prompt and lowers context recall relative to the best non-CoT prompt variants; shorter CoT outputs may contribute to this drop.
</div>

---

<div class="kicker">Study 3 Takeaway</div>

# Grounding is unstable under the tested positions, languages, and models

<div class="grid-3 mt-8">
<div class="tile amber"><h3>Lost-in-the-later</h3><p>Later evidence is recalled less reliably even when relevant.</p></div>
<div class="tile green"><h3>Multilingual stress</h3><p>Similar patterns appear in Spanish and Danish, with lower CK and larger recall difficulty in Danish.</p></div>
<div class="tile red"><h3>Reasoning and grounding</h3><p>Reasoning-model outputs do not automatically imply better grounding.</p></div>
</div>

<div class="takeaway mt-8">
This motivates a related decode-time control problem: preserving correct answers under weak or distracting context while allowing genuinely helpful evidence to matter.
</div>

---
class: section-slide
---

<div class="section-number">Study 4 | Decode-Time Intervention</div>

# No-Worse Context-Aware Decoding

<div class="subtitle mt-6">
NWCAD treats context use as a routing problem: preserve already-correct answers when added context is neutral or distracting, yet still use context when it is genuinely corrective.
</div>

<div class="section-paper-ref">
Paper: Tao and Agrawal, "No-Worse Context-Aware Decoding: Preventing Neutral Regression in Context-Conditioned Generation," Findings of ACL 2026.
</div>

---

<div class="kicker">Neutral Regression</div>

# Neutral regression: weak context overwrites a correct answer

<div class="neutral-example mt-5">
<div class="example-question">Q: When did the U.S. normalize relations with China?</div>
<div class="grid-2 mt-3">
<div class="tile blue">
<h3>Gold / no-context answer</h3>
<p>January 1, 1979</p>
</div>
<div class="tile amber">
<h3>Distractor context excerpt</h3>
<p>Although the process culminated in a major announcement in 1978, it reflected decades of evolving U.S.-China relations.</p>
</div>
</div>
<div class="answer-compare mt-3">
<div><span>With-context / context-aware decoders</span><strong>1978</strong></div>
<div><span>NWCAD</span><strong>January 1, 1979</strong></div>
</div>
</div>

<div class="takeaway red mt-4">
The added context creates type-matched pressure, but it does not entail the gold answer. Changing the already-correct answer is neutral regression.
</div>

---

<div class="kicker">Controlled Benchmark</div>

# The benchmark separates two objectives

<div class="grid-3 mt-7">
<div class="tile blue"><h3>Restated</h3><p>Neutral context restates or aligns with the answer.</p></div>
<div class="tile red"><h3>Distractor</h3><p>Incorrect but non-entailing pressure.</p></div>
<div class="tile green"><h3>Helpful</h3><p>Context provides evidence that the baseline lacks.</p></div>
</div>

<div class="fine mt-5">Restated and distractor examples are baseline-correct neutral cases; helpful examples are baseline-wrong but context-correct cases.</div>
<div class="fine mt-2">The helpful slice isolates context utilization; it is not intended to estimate natural prevalence.</div>

<div class="flow mt-8">
<div class="step" v-click>Preserve neutral</div>
<div class="arrow" v-after>+</div>
<div class="step" v-after>Use helpful</div>
<div class="arrow" v-after>-></div>
<div class="step" v-after>No-worse decoding</div>
</div>

---

<div class="kicker">Neutral Regression Evidence</div>

# In the baseline-correct controlled slice, added context often induces regressions

<div class="grid-2 wide-right mt-5">
<div>
<div class="tile red"><h3>Controlled filter</h3><p>Baseline-correct filtering makes no-context accuracy 100% by construction.</p></div>
<div class="tile amber mt-4"><h3>Regression signal</h3><p>Within baseline-correct neutral cases, a with-context drop is a context-induced regression.</p></div>
</div>
<div class="media-rail"><img src="/assets/nwcad-neutral-regression.png" class="media tall"></div>
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
<div class="trade-point cad">Context-shifted decoder</div>
<div class="trade-point nwcad">NWCAD</div>
</div>

<div class="grid-2 mt-4">
<div class="tile blue">
<h3>Do-no-harm preservation</h3>
<p>Preserve baseline-correct answers when added context is neutral or distracting.</p>
</div>
<div class="tile green">
<h3>Context utilization</h3>
<p>Questions where the context can correct the answer.</p>
</div>
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

<div class="fine mt-5">Evaluation setting: logit access, greedy decoding, top-K union JS with K = 50, and thresholds tuned on Llama-3.1-8B then transferred.</div>

---

<div class="kicker">NWCAD Gate</div>

# A three-way decision at each token

<div class="grid-3 mt-6">
<div>
<div class="tile blue"><h3>No-context stream</h3><p>p<sub>0</sub><sup>t</sup> represents the model's next-token distribution without the added context.</p></div>
<div class="tile green mt-4"><h3>With-context stream</h3><p>p<sub>c</sub><sup>t</sup> represents the same prefix conditioned on the added context.</p></div>
</div>
<div class="tile amber">
<h3>Gate signals</h3>
<p>Jensen-Shannon divergence estimates context pressure; top-1 margins estimate stream confidence.</p>
<p class="fine mt-5">Low pressure plus confident no-context favors preservation. Confident context favors context use.</p>
</div>
<div>
<div class="tile blue"><h3>Preserve</h3><p>Copy no-context logits on low-pressure confident steps.</p></div>
<div class="tile green mt-4"><h3>Use context</h3><p>Use context logits when the context stream is confident.</p></div>
<div class="tile amber mt-4"><h3>Fallback</h3><p>Use a plug-in contrastive decoder only when neither gate is decisive.</p></div>
</div>
</div>

<div class="takeaway mt-5">
NWCAD treats context-aware decoding as regime selection rather than continuous logit tilting.
</div>

---

<div class="kicker">NWCAD Logic</div>

# Back off on neutral token steps; use context when confident

<div class="grid-3 mt-7">
<div class="tile blue">
<h3>Stage 1</h3>
<p>If context pressure is low and no-context is confident, copy the no-context logits exactly when Stage 1 applies under greedy decoding.</p>
</div>
<div class="tile green">
<h3>Stage 2</h3>
<p>If context is confident, use the context stream.</p>
</div>
<div class="tile amber">
<h3>Fallback</h3>
<p>Otherwise, fall back to a plug-in contrastive decoder when Stage 1 does not apply and the context stream is not sufficiently confident.</p>
</div>
</div>

<div class="takeaway mt-8">
This turns context-aware decoding from continuous tilting into regime selection.
</div>

---

<div class="kicker">Controlled Evaluation</div>

# NWCAD moves up and to the right

<div class="media-rail mt-4">
<img src="/assets/nwcad-tradeoff.png" class="media tall">
</div>

<div class="caption">Controlled augmented NQ-open slices. Each panel is one open-weight backbone; x-axis is Helpful accuracy, and the vertical bar spans Restated and Distractor baseline-correct preservation.</div>

---

<div class="kicker">Qualitative Example</div>

# Qualitative examples: reducing regressions while using helpful context

<table class="table-lite mt-5">
<thead><tr><th>Slice</th><th>Question</th><th>Bad behavior</th><th>NWCAD behavior</th></tr></thead>
<tbody>
<tr><td>Restated</td><td>Dumbledore actor after the first one died</td><td>Contrastive decoders flip to Richard Harris</td><td>Preserves Michael Gambon</td></tr>
<tr><td>Distractor</td><td>When did the US normalize relations with China?</td><td>Distractor pulls answer toward 1978</td><td>Preserves January 1, 1979</td></tr>
<tr><td>Helpful</td><td>Voice of the T. rex in The Good Dinosaur</td><td>Baseline gives wrong answer</td><td>Uses context: Sam Elliott</td></tr>
</tbody>
</table>

<div class="takeaway mt-6">
When the context is non-informative and the no-context answer is already correct, a decoder should preserve the no-context output; when context is informative, it should shift toward context to correct the answer.
</div>

---

<div class="kicker">Full-Slice Evaluation</div>

# NWCAD reduces neutral regressions across evaluated slices

<div class="media-rail full-figure mt-4">
<img src="/assets/nwcad-fullslice.png" class="media tall">
</div>

<div class="grid-3 evidence-strip mt-4">
<div class="tile blue"><h3>Regression reduction</h3><p>Reduced failures under distractor contexts in the evaluated settings.</p></div>
<div class="tile green"><h3>Helpful context</h3><p>Helpful-context gains are largely preserved across the evaluated slices.</p></div>
<div class="tile amber"><h3>Scope</h3><p>Logit access, greedy decoding, transferred thresholds; representative slices include NQ-SYNTH/SWAP, HotpotQA, PopQA, TabMWP, ToFuEval, and ExpertQA.</p></div>
</div>

---

<div class="kicker">Component Ablation</div>

# Full two-stage NWCAD improves over Stage 1 alone

<div class="grid-2 wide-left mt-5">
<div class="media-rail">
<img src="/assets/nwcad-component-ablation.png" class="media fit-wide">
</div>
<div>
<div class="tile blue"><h3>Stage 1 only</h3><p>The baseline-correct preservation stage protects baseline-correct neutral cases.</p></div>
<div class="tile green mt-4"><h3>Full method</h3><p>Stage 2 adds gains when the decoder should use the context rather than ignore it.</p></div>
<div class="tile amber mt-4"><h3>Takeaway</h3><p>Adding Stage 2 improves performance across the evaluation suite by 5.2% on average.</p></div>
</div>
</div>

---

<div class="kicker">Adapter Ablation</div>

# NWCAD improves existing two-stream decoders when used as a wrapper

<div class="grid-2 wide-left mt-5">
<div class="media-rail">
<img src="/assets/nwcad-adapter.png" class="media fit-wide">
</div>
<div>
<div class="tile red"><h3>Largest gains</h3><p>Wrapping existing contrastive decoders such as CAD and CoCoA gives large improvements because they are more exposed to neutral regression under distractor pressure.</p></div>
<div class="tile green mt-4"><h3>Fallback is plug-in</h3><p>NWCAD can use existing decoders such as CAD, AdaCAD, or CoCoA as the Stage-2 fallback.</p></div>
<div class="tile blue mt-4"><h3>Interpretation</h3><p>The result supports the adapter view: regime selection improves existing two-stream context-aware decoding methods.</p></div>
</div>
</div>

---

<div class="kicker">Routing and Cost</div>

# The fallback path is rare, and the latency cost stays small

<div class="grid-2 mt-5">
<div>
<table class="table-lite compact">
<thead><tr><th>Slice</th><th class="num">No-context</th><th class="num">Context</th><th class="num">Fallback</th></tr></thead>
<tbody>
<tr><td>Restated</td><td class="num">75.14</td><td class="num">23.65</td><td class="num"><strong>1.21</strong></td></tr>
<tr><td>Distractor</td><td class="num">73.70</td><td class="num">24.35</td><td class="num"><strong>1.95</strong></td></tr>
<tr><td>Helpful</td><td class="num">63.06</td><td class="num">35.06</td><td class="num"><strong>1.88</strong></td></tr>
<tr><td>NQ-SYNTH</td><td class="num">49.57</td><td class="num">48.66</td><td class="num"><strong>1.78</strong></td></tr>
<tr><td>NQ-SWAP</td><td class="num">37.88</td><td class="num">60.26</td><td class="num"><strong>1.86</strong></td></tr>
<tr><td>HotpotQA-distractor</td><td class="num">60.53</td><td class="num">38.39</td><td class="num"><strong>1.08</strong></td></tr>
</tbody>
</table>
<div class="caption">Routing frequencies (% of generated tokens).</div>
</div>
<div>
<table class="table-lite compact">
<thead><tr><th>Pair</th><th class="num">QA mean</th><th class="num">ToFuEval</th><th class="num">ExpertQA</th></tr></thead>
<tbody>
<tr><td>NWCAD<sub>CAD</sub> / CAD</td><td class="num">0.88</td><td class="num">1.01</td><td class="num">0.99</td></tr>
<tr><td>NWCAD<sub>AdaCAD</sub> / AdaCAD</td><td class="num">0.99</td><td class="num">1.01</td><td class="num">0.98</td></tr>
<tr><td>NWCAD<sub>CoCoA</sub> / CoCoA</td><td class="num">0.90</td><td class="num">0.98</td><td class="num">1.01</td></tr>
</tbody>
</table>
<div class="caption">Relative decoding latency; values below 1 are faster than the base decoder.</div>
</div>
</div>

<div class="takeaway mt-5">
NWCAD improves reliability mainly by selecting between the no-context and context streams, with contrastive fallback reserved for uncommon uncertain steps.
</div>

---

<div class="kicker">Limitations</div>

# What NWCAD reduces and what remains

<div class="grid-2 mt-8">
<div class="tile green">
<h3>What it reduces</h3>
<p>Reduces a particular downstream consequence of weak grounding: added context making outputs worse when that context is neutral, distracting, or otherwise unhelpful.</p>
</div>
<div class="tile red">
<h3>What remains</h3>
<p>Does not guarantee full uptake of later evidence, remove multilingual asymmetries, or work directly for black-box APIs without logits.</p>
</div>
</div>

---

<div class="kicker">Unified Pattern</div>

# Viewed together, context often behaves like a competing signal

<div class="storyline mt-7">
<div><span class="tag blue">Social</span></div><div>Role-play changes behavior</div><div>Generic assistant habits persist</div>
<div><span class="tag green">CK/PK</span></div><div>Evidence changes composition</div><div>Residual PK persists</div>
<div><span class="tag amber">Position</span></div><div>Later evidence is available</div><div>Earlier evidence dominates recall</div>
<div><span class="tag red">Decoding</span></div><div>Control can shift behavior</div><div>It does not erase deeper instability</div>
</div>

<div class="takeaway mt-5">
The evaluation target is not just fluent output, but whether the right context constrained the output.
</div>

---

<div class="kicker">Contributions</div>

# Dissertation contributions

<div class="grid-2 mt-7">
<div class="tile blue"><h3>Social adaptation</h3><p>CRD shows role-play changes both user behavior and model behavior while exposing persistent assistant defaults.</p></div>
<div class="tile green"><h3>Knowledge composition</h3><p>WikiAtomic CK/PK analysis shows evidence and memory coexist even in knowledge-consistent settings.</p></div>
<div class="tile amber"><h3>Multilingual positional grounding</h3><p>CoPE identifies lost-in-the-later across English, Spanish, Danish, and tested order/prompt variations.</p></div>
<div class="tile red"><h3>Decode-time control</h3><p>NWCAD reduces neutral regression while preserving context utilization.</p></div>
</div>

<div class="takeaway mt-5">
Together, these contributions support the central claim: context influences current LLMs, but it does not reliably govern them.
</div>

---

<div class="kicker">Conclusion</div>

# Reliable LLM behavior requires measuring whether the right context constrains the output

<div class="grid-3 mt-8">
<div class="tile blue"><h3>Diagnose</h3><p>Measure where context changes behavior and where defaults persist.</p></div>
<div class="tile green"><h3>Ground</h3><p>Separate contextual knowledge from parametric knowledge in generated responses.</p></div>
<div class="tile red"><h3>Control</h3><p>Reduce context-induced regressions while preserving helpful-context gains.</p></div>
</div>

<div class="takeaway mt-8">
The dissertation frames role-play, hallucination, multilingual recall, later-context behavior, and decoding control as connected symptoms of one context-use problem.
</div>

---

<div class="kicker">Future Work</div>

# Next directions for contextual grounding

<div class="takeaway mt-4">
Context becomes an evolving workspace of prior turns, files, tool outputs, memory, and evidence.
</div>

<div class="grid-2 mt-6">
<div class="tile blue"><h3>Multi-agent knowledge systems</h3><p>Evaluate whether agents maintain a grounded account of what is known, uncertain, superseded, and evidence-backed.</p></div>
<div class="tile green"><h3>Context navigation</h3><p>Measure whether systems can recover, compare, and revise the relevant evidence needed for the next decision.</p></div>
<div class="tile amber"><h3>Context focus and control</h3><p>Study how retrieval, memory, prompting, and decoding preserve or weaken grounding across a pipeline.</p></div>
<div class="tile red"><h3>Memory, retrieval, tools, and action</h3><p>Judge systems not only by task completion, but by whether they remain grounded while acting over extended trajectories.</p></div>
</div>

<div class="takeaway mt-6">
The next step is to evaluate whether context governs the construction and use of working knowledge, not only the final generated answer.
</div>

---

<div class="kicker">Acknowledgements</div>

# Thank you

<div class="grid-2 mt-7">
<div class="tile blue">
<h3>Committee</h3>
<p>Dr. Ameeta Agrawal, Dr. Suresh Singh, Dr. Tetyana Sydorenko, and Dr. Wu-chi Feng.</p>
</div>
<div class="tile green">
<h3>Collaborators</h3>
<p>Adam Hiatt, Rahul Seetharaman, Erik Haake, Antonie J. Jetter, Judit Dombi, Jung In Lee, Tiernan Mines, Rhitabrat Pokharel, and other coauthors across this work.</p>
</div>
</div>

<div class="grid-2 mt-5">
<div class="tile amber">
<h3>Research community</h3>
<p>PortNLP, Portland State University, annotators, study participants, and reviewers who shaped the studies.</p>
</div>
<div class="tile red">
<h3>Family and friends</h3>
<p>For support throughout the PhD and through the long path from drafts to dissertation.</p>
</div>
</div>

<div class="fine mt-6">Title icons made by Freepik from Flaticon.</div>

---

<div class="thanks">
<div class="kicker">Closing</div>

<div class="quote-large">
This dissertation argues for moving context from an input that merely influences generation toward a constraint that more reliably governs it.
</div>

<div class="byline mt-12">Thank you.</div>
</div>

---

<div class="kicker">Backup | Study 2 Robustness</div>

# CK/PK trends persist under evaluator and prompt checks

<div class="grid-2 mt-7">
<div class="tile green"><h3>Ambiguous-score filtering</h3><p>Removing sentences with INFUSE scores between 0.3 and 0.7 preserves the main CK/PK patterns.</p></div>
<div class="tile amber"><h3>Alternative metrics</h3><p>ROUGE, METEOR, and partial-match checks show similar broad patterns in preliminary comparisons.</p></div>
<div class="tile blue"><h3>Prompt sensitivity</h3><p>No-restrict and strict prompts change CK/PK ratios, confirming that the semi-restrict prompt is a controlled choice.</p></div>
<div class="tile red"><h3>Newer knowledge check</h3><p>A recent-event probe tests behavior when supplied context contains information less likely to be represented in pretraining.</p></div>
</div>

<div class="fine mt-5">Backup slide for committee questions about whether the CK/PK measurement depends on a single threshold, metric, or prompt form.</div>

---

<div class="kicker">Backup | CoPE Validation</div>

# CoPE calibration checks the multilingual grounding measure

<div class="grid-4 mt-7">
<div class="metric blue"><div class="value">50</div><div class="label">outputs per model / language</div></div>
<div class="metric green"><div class="value">0.7</div><div class="label">selected entailment threshold</div></div>
<div class="metric amber"><div class="value">66.66%</div><div class="label">synthetic CK target</div></div>
<div class="metric red"><div class="value">~66.9%</div><div class="label">observed CK estimate</div></div>
</div>

<div class="grid-3 mt-7">
<div class="tile blue"><h3>Human calibration</h3><p>Three annotators checked CK/PK labels across English, Spanish, and Danish.</p></div>
<div class="tile green"><h3>Synthetic check</h3><p>Constructed responses with 10 CK and 5 unrelated sentences recover the expected CK rate.</p></div>
<div class="tile amber"><h3>Threshold robustness</h3><p>Filtering ambiguous scores in p ∈ [0.4, 0.8] preserves the main trends.</p></div>
</div>

---

<div class="kicker">Backup | NWCAD Settings</div>

# Thresholds and JS approximation are checked directly

<div class="grid-4 mt-7">
<div class="metric blue"><div class="value">τ=.30</div><div class="label">neutrality threshold</div></div>
<div class="metric green"><div class="value">κ<sub>pri</sub>=.30</div><div class="label">no-context margin</div></div>
<div class="metric amber"><div class="value">κ<sub>ctx</sub>=.05</div><div class="label">context margin</div></div>
<div class="metric red"><div class="value">K=50</div><div class="label">top-K union JS</div></div>
</div>

<div class="grid-2 mt-7">
<div class="tile blue"><h3>Transfer</h3><p>Defaults are tuned once on Llama-3.1-8B controlled slices and reused for Llama-3.1-70B and Ministral-3-8B.</p></div>
<div class="tile green"><h3>Top-K sanity check</h3><p>On 150 controlled examples and 784 generated tokens, K = 50 matches full-vocabulary JS for neutrality and Stage-1 decisions with zero routing flips.</p></div>
</div>
