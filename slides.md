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
<div>Dissertation Defense · April 30, 2026</div>
<div>Department of Computer Science · Portland State University</div>
<div class="committee-block">
<div><span>Chair</span> Dr. Ameeta Agrawal</div>
<div><span>Committee</span> Dr. Suresh Singh · Dr. Tetyana Sydorenko · Dr. Wu-chi Feng</div>
</div>
</div>
</div>

---

<div class="kicker">Motivation</div>

# Real-world LLM reliability depends on whether context constrains the output

<div class="grid-2 mt-5">
<div class="tile blue">
<h3>Fits the social situation</h3>
<p>A chatbot helping a language learner practice a difficult conversation is expected to respond in a way that fits the social situation.</p>
</div>
<div class="tile green">
<h3>Faithful to supplied evidence</h3>
<p>A model that summarizes a legal document, assists a medical professional, or answers questions in a retrieval-augmented pipeline is expected to use the supplied evidence.</p>
</div>
</div>

<div class="motivation-example mt-5">
<div class="example-label">Example</div>
<div class="example-card blue">
<strong>Social context</strong>
<span>A learner needs to decline an advisor's request without sounding rude. The reply must preserve the refusal while adapting to role relation and politeness expectations.</span>
</div>
<div class="example-card green">
<strong>Informational context</strong>
<span>A long retrieved context first states an older policy, then later says it was revised. The answer must follow the later evidence, not the earlier or memorized answer.</span>
</div>
</div>

<div class="takeaway mt-5">
This dissertation asks whether social and informational context reliably govern what LLMs say.
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

# LLMs are context-sensitive, yet context only partially governs their outputs

<div class="grid-2 wide-right mt-5">
<div class="tile blue">
<h3>They respond to context</h3>
<p>Current LLMs respond to role cues, supplied evidence, prompt structure, and decode-time controls.</p>
</div>
<div class="tile amber">
<h3>The response is uneven</h3>
<p>Context acts less like a hard boundary on behavior than like a competing signal.</p>
</div>
</div>

<div class="storyline compact rowed mt-5">
<div class="story-row"><div><span class="tag blue">1</span></div><div><strong>Role-play interaction</strong></div><div>Social adaptation</div></div>
<div class="story-row"><div><span class="tag green">2</span></div><div><strong>Contextual vs. parametric knowledge</strong></div><div>Knowledge-consistent grounding</div></div>
<div class="story-row"><div><span class="tag amber">3</span></div><div><strong>Lost-in-the-Later</strong></div><div>Multilingual and positional grounding</div></div>
<div class="story-row focus"><div><span class="tag red">4</span></div><div><strong>No-Worse Context-Aware Decoding</strong></div><div>Decode-time control</div></div>
<div class="story-row"><div><span class="tag violet">5</span></div><div><strong>Synthesis</strong></div><div>Context as a control problem</div></div>
</div>

<div class="fine mt-4">The four studies move from empirical diagnosis to a bounded decode-time intervention for one downstream reliability problem.</div>

---

<div class="kicker">Publications</div>

# Publications from this doctoral work

<div class="pub-list citation-list mt-4">
<div class="pub-entry">
<div class="pub-title">No-Worse Context-Aware Decoding: Preventing Neutral Regression in Context-Conditioned Generation</div>
<div class="pub-authors">Yufei Tao, Ameeta Agrawal</div>
<div class="pub-venue">In Findings of the Association for Computational Linguistics (ACL), 2026</div>
</div>
<div class="pub-entry">
<div class="pub-title">CAPO: Confidence Aware Preference Optimization Learning for Multilingual Preferences</div>
<div class="pub-authors">Rhitabrat Pokharel, Yufei Tao, Ameeta Agrawal</div>
<div class="pub-venue">International Joint Conference on Natural Language Processing & Asia-Pacific Chapter of the Association for Computational Linguistics (IJCNLP & AACL), 2025</div>
</div>
<div class="pub-entry">
<div class="pub-title">"Lost-in-the-Later": Framework for Quantifying Contextual Grounding in Large Language Models</div>
<div class="pub-authors">Yufei Tao, Adam Hiatt, Rahul Seetharaman, Ameeta Agrawal</div>
<div class="pub-venue">Grounding Documents with Reasoning, Agents, Retrieval, and Attribution at IEEE International Conference on Data Mining (ICDM), 2025</div>
</div>
<div class="pub-entry">
<div class="pub-title">When Context Leads but Parametric Memory Follows in Large Language Models</div>
<div class="pub-authors">Yufei Tao, Adam Hiatt, Erik Haake, Antonie J. Jetter, Ameeta Agrawal</div>
<div class="pub-venue">Proceedings of the 2024 Conference on Empirical Methods in Natural Language Processing (EMNLP), 2024.</div>
</div>
<div class="pub-entry">
<div class="pub-title">Training Practitioners for Real-time Product Development Using Generative Artificial Intelligence</div>
<div class="pub-authors">Antonie J. Jetter, Ameeta Agrawal, Dahm Mongkol Hongchai, Charles M. Weber, and Yufei Tao.</div>
<div class="pub-venue">2024 Portland International Conference on Management of Engineering and Technology (PICMET), pp. 1-11. IEEE, 2024.</div>
</div>
<div class="pub-entry">
<div class="pub-title">ChatGPT Role-play Dataset: Analysis of User Motives and Model Naturalness</div>
<div class="pub-authors">Yufei Tao, Ameeta Agrawal, Judit Dombi, Tetyana Sydorenko, Jung In Lee.</div>
<div class="pub-venue">Joint International Conference on Computational Linguistics, Language Resources and Evaluation (LREC-COLING), 2024.</div>
</div>
<div class="pub-entry">
<div class="pub-title">Spoken Dialogue Systems and ChatGPT for Second Language Pragmatics Research</div>
<div class="pub-authors">Tetyana Sydorenko, Judit Dombi, Ameeta Agrawal, Steven Thorne, Jung In Lee, Yufei Tao</div>
<div class="pub-venue">Chapter 29 in Routledge Handbook of Technological Advances in Researching Language Learning, Routledge, 2024, pp. 378-391.</div>
</div>
<div class="pub-entry">
<div class="pub-title">Making a Long Story Short in Conversation Modeling</div>
<div class="pub-authors">Yufei Tao, Tiernan Mines, Ameeta Agrawal.</div>
<div class="pub-venue">Towards Ethical and Inclusive Conversational AI (TEICAI) at EACL 2024.</div>
</div>
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

<div v-click class="study-reveal">
<div class="subtitle mt-6">
CRD as a testbed for user motives and model naturalness.
</div>

<div class="fine mt-5">The CRD dataset contains 57 participants, 85 conversations, and 1,742 utterances across regular and role-play ChatGPT-3.5 interactions collected in March-April 2023.</div>
<div class="fine mt-2">User motives and model naturalness were annotated with substantial agreement.</div>

<div class="grid-3 mt-5">
<div class="tile blue"><h3>We introduced CRD</h3><p>A human-AI role-play dataset with utterance-level user motive and model naturalness labels.</p></div>
<div class="tile amber"><h3>Social adaptation has limits</h3><p>Role cues improve naturalness while verbosity and over-helpfulness persist.</p></div>
<div class="tile green"><h3>Bridge</h3><p>If role cues only partially govern behavior, the next question is whether supplied evidence governs factual content.</p></div>
</div>
</div>

<div class="section-paper-ref">
Paper: Tao et al., "ChatGPT Role-play Dataset: Analysis of User Motives and Model Naturalness," LREC-COLING 2024.
</div>

---

<div class="kicker">Study 1 Evidence</div>

# Role-play changes rhythm and naturalness, while assistant defaults remain

<div class="grid-2 wide-left mt-4">
<div>
<table class="table-lite compact">
<thead>
<tr><th>Measure</th><th class="num">Vanilla</th><th class="num">Boss</th><th class="num">Classmate</th></tr>
</thead>
<tbody>
<tr><td>Average conversation length, turns</td><td class="num"><strong>29.59</strong></td><td class="num">14.57</td><td class="num">17.11</td></tr>
<tr><td>Average human utterance length, words</td><td class="num">12.18</td><td class="num"><strong>20.58</strong></td><td class="num">19.06</td></tr>
<tr><td>Average ChatGPT utterance length, words</td><td class="num"><strong>77.66</strong></td><td class="num">35.78</td><td class="num">46.10</td></tr>
</tbody>
</table>
<div class="tile blue mt-4"><h3>Takeaway</h3><p>CRD makes social-context adaptation measurable: users and models both change under role-play, but generic assistant habits remain visible.</p></div>
</div>
<div>
<div class="media-rail"><img src="/assets/model-naturalness.png" class="media short"></div>
</div>
</div>

---
class: section-slide
---

<div class="section-number">Study 2 | Informational Context</div>

# When Context Leads but Parametric Memory Follows

<div v-click class="study-reveal">
<div class="subtitle mt-6">
Contextual vs. parametric knowledge in LLM outputs.
</div>

<div class="atom-definition mt-5">
<div class="atom-label">Atomic response content</div>
<div class="atom-equation">model response &rarr; atom<sub>1</sub>, atom<sub>2</sub>, ... atom<sub>n</sub></div>
<div class="atom-desc">Each atom is one factual proposition extracted from the response; each atom is labeled by entailment against the supplied context.</div>
</div>

<div class="grid-2 mt-4">
<div class="tile green">
<h3>Contextual knowledge (CK)</h3>
<p>Atomic response content entailed by the supplied context.</p>
</div>
<div class="tile amber">
<h3>Parametric knowledge (PK)</h3>
<p>Atomic response content unsupported by the supplied context; factuality is checked separately.</p>
</div>
</div>
</div>

<div class="section-paper-ref">
Paper: Tao et al., "When Context Leads but Parametric Memory Follows in Large Language Models," EMNLP 2024.
</div>

---

<div class="kicker">WikiAtomic Construction + Example</div>

# WikiAtomic controls context length and maps response atoms to CK/PK

<div class="grid-2 wide-left mt-4">
<div>
<div class="grid-2">
<div class="metric blue"><div class="value">200</div><div class="label">Wikipedia articles</div></div>
<div class="metric green"><div class="value">50</div><div class="label">atomic sentences per article</div></div>
<div class="metric amber"><div class="value">10,000</div><div class="label">atomic sentences</div></div>
<div class="metric red"><div class="value">4,000</div><div class="label">topic-context instances</div></div>
</div>
<div class="tile blue mt-4"><h3>Evaluation setup</h3><p>Context sizes grow from 2 to 50 sentences; responses are atomized and compared with INFUSE at threshold 0.5 across GPT-4o, Claude 3, Llama 3, Mixtral, Mistral, and Phi-3.</p></div>
</div>
<div>
<div class="media-rail">
<img src="/assets/ckpk-real-example.png" class="media tall">
</div>
<div class="caption">Context, question, model response, and atomic response labels.</div>
</div>
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

<div class="kicker">Similarity + Faithfulness</div>

# Similarity and factuality separate relatedness from support

<div class="grid-2 wide-left mt-4 similarity-slide">
<div>
<div class="media-rail similarity-mini-panel">
<div class="similarity-mini-grid">
<div class="similarity-mini-item"><img src="/assets/sim-local-local-gpt4o.png" class="media sim-mini"><div class="caption mini">Local vs. local, GPT-4o</div></div>
<div class="similarity-mini-item"><img src="/assets/sim-global-global-gpt4o.png" class="media sim-mini"><div class="caption mini">Global vs. global, GPT-4o</div></div>
<div class="similarity-mini-item"><img src="/assets/sim-local-global-combined.png" class="media sim-mini"><div class="caption mini">Local vs. global, all models</div></div>
</div>
</div>
<div class="tile blue mt-3"><h3>Similarity takeaways</h3><p>CK becomes more internally consistent as context grows. PK is not random; it remains topically related to the evidence, which is why similarity alone cannot establish grounding.</p></div>
</div>
<div>
<div class="media-rail"><img src="/assets/factscore.png" class="media sim-wide"></div>
<div class="tile green mt-3"><h3>FActScore check</h3><p>PK factuality generally improves or stabilizes as context increases, so factuality and grounding must be evaluated separately.</p></div>
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
WikiAtomic makes grounding auditable at the atomic-proposition level: even in a knowledge-consistent setting, evidence changes outputs without fully governing them.
</div>

---
class: section-slide
---

<div class="section-number">Study 3 | Harder Grounding Conditions</div>

# Lost-in-the-Later: multilingual contextual grounding

<div class="fine mt-5">Paper: Tao et al., "Lost-in-the-Later: Framework for Quantifying Contextual Grounding in Large Language Models," RARA at ICDM 2025.</div>

<div v-click class="study-reveal">
<div class="subtitle mt-5">
Tests whether grounding remains stable when evidence appears later in the prompt and across English, Spanish, and Danish.
</div>

<div class="media-rail pipeline-wide mt-4">
<img src="/assets/lostlater-pipeline.png" class="media cope-pipeline">
</div>

<div class="grid-3 evidence-strip mt-3">
<div class="tile blue"><h3>Atomize</h3><p>Context and responses are decomposed into atomic factual propositions.</p></div>
<div class="tile green"><h3>Label CK vs. PK</h3><p>Multilingual NLI checks response atoms against the supplied context.</p></div>
<div class="tile amber"><h3>Trace position</h3><p>Entailed atoms -> context quartiles; PK atoms -> response positions.</p></div>
</div>
</div>

---

<div class="kicker">CK Across Languages</div>

# More context helps, but not equally across languages

<div class="grid-3 mt-5">
<div class="media-rail"><img src="/assets/lostlater-ck-english.png" class="media short"></div>
<div class="media-rail"><img src="/assets/lostlater-ck-spanish.png" class="media short"></div>
<div class="media-rail"><img src="/assets/lostlater-ck-danish.png" class="media short"></div>
</div>

<div class="takeaway mt-5">
Most models reach CK scores around 70-75 in English and Spanish, while Danish has lower CK in this evaluation. The tested reasoning models show lower CK, possibly due to longer or more autonomous answer structure.
</div>

---

<div class="kicker">Context Recall + Randomization</div>

# Later evidence is recalled least reliably, even after randomization

<div class="grid-2 wide-left mt-5">
<div class="media-rail"><img src="/assets/lostlater-recall-en.png" class="media tall"></div>
<div>
<div class="tile amber"><h3>Pattern</h3><p>The first context quartile receives the most recall; the final quartile contributes least.</p></div>
<div class="tile green mt-4"><h3>Context length</h3><p>The imbalance becomes stronger as context length increases; PK also concentrates toward later response quartiles.</p></div>
<table class="table-lite compact mt-4">
<thead><tr><th>Language</th><th class="num">Absolute Q1-over-Q4 recall gap at context length 50</th></tr></thead>
<tbody>
<tr><td>English</td><td class="num">14.63-26.11 pp</td></tr>
<tr><td>Spanish</td><td class="num">12.63-25.81 pp</td></tr>
<tr><td>Danish</td><td class="num">8.91-19.10 pp</td></tr>
</tbody>
</table>
</div>
</div>

---

<div class="kicker">Prompt-Level Intervention</div>

# In the 50-context Llama 3.2 90B setting, CK Prompt gives the highest CK

<div class="fine mt-3">LLaMA 3.2 90B, 50-context setting. CK Prompt explicitly asks for context-grounded answers; CoT refers to chain-of-thought prompting.</div>

<div class="prompt-intervention-layout mt-4">
<div>
<table class="table-lite compact prompt-table">
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
</div>
<div class="media-rail prompt-recall-panel">
<img src="/assets/lostlater-prompt-recall.png" class="media prompt-recall">
<div class="caption mini">English context recall by prompt type and source quartile.</div>
</div>
</div>

<div class="takeaway mt-4">
CK Prompt produces the strongest CK scores across languages. The recall figure shows the tradeoff: CoT variants do not recover the best non-CoT recall pattern, especially for later context quartiles.
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

<div class="fine mt-4">Paper: Tao and Agrawal, "No-Worse Context-Aware Decoding: Preventing Neutral Regression in Context-Conditioned Generation," Findings of ACL 2026.</div>

<div v-click class="study-reveal nwcad-opener">
<div class="subtitle mt-4">
Can a context-aware decoder use added context without making already-correct answers worse?
</div>

<div class="neutral-example mt-3">
<div class="example-question">Q: When did the U.S. normalize relations with China?</div>
<div class="nwcad-context-excerpt mt-3">
<span>Added non-entailing context excerpt</span>
<p>Although the process culminated in a major announcement in 1978, it reflected decades of evolving U.S.-China relations.</p>
</div>
<div class="answer-compare mt-3">
<div><span>Gold / no-context answer</span><strong>January 1, 1979</strong></div>
<div><span>CAD / AdaCAD / CoCoA</span><strong>1978</strong></div>
<div><span>Desired behavior</span><strong>January 1, 1979</strong></div>
</div>
</div>

<div class="takeaway red nwcad-opener-takeaway mt-2">
The added context creates type-matched pressure without entailing the gold answer; the next slides name this failure and show how NWCAD avoids it.
</div>
</div>

---
class: cad-style-slide
---

<div class="kicker">Prior Decode-Time Methods</div>

# CAD-style decoding can help, but it lacks a do-no-harm guarantee

<div class="cad-process mt-5">
<div class="cad-node prior">
<div class="cad-node-title">No-context stream</div>
<div class="cad-node-sub">question only</div>
<div class="cad-bars">
<div class="cad-bar-row"><span>1979</span><i style="--w: 86%"></i></div>
<div class="cad-bar-row muted"><span>1978</span><i style="--w: 38%"></i></div>
</div>
</div>

<div class="cad-node context">
<div class="cad-node-title">With-context stream</div>
<div class="cad-node-sub">question + added passage</div>
<div class="cad-bars">
<div class="cad-bar-row muted"><span>1979</span><i style="--w: 62%"></i></div>
<div class="cad-bar-row"><span>1978</span><i style="--w: 78%"></i></div>
</div>
</div>

<div class="cad-node operator">
<div class="cad-node-title">Contrast and tilt</div>
<div class="cad-node-sub">tokens boosted by context get amplified</div>
<div class="cad-delta">z<sub>c</sub><sup>t</sup> - z<sub>0</sub><sup>t</sup></div>
</div>

<div class="cad-node output">
<div class="cad-node-title">Shifted logits</div>
<div class="cad-node-sub">next token can flip</div>
<div class="cad-token-result"><span>1978</span><strong>selected</strong></div>
</div>
</div>

<div class="cad-formula-label mt-3">Representative CAD update</div>

$$
\small
\begin{aligned}
z_{\mathrm{CAD}}^{t}
&= z_c^t + \alpha\left(z_c^t - z_0^t\right) \\
&= (1+\alpha)z_c^t - \alpha z_0^t
\end{aligned}
$$

<div class="grid-3 evidence-strip mt-3">
<div class="tile green"><h3>Goal</h3><p>Bias generation toward tokens that become more likely when context is present.</p></div>
<div class="tile amber"><h3>Variants</h3><p>CAD uses fixed &alpha;; AdaCAD and CoCoA adapt the tilt with divergence and confidence signals.</p></div>
<div class="tile red"><h3>Failure mode</h3><p>Weak context can still shift a token choice and cascade into a different answer.</p></div>
</div>

---

<div class="kicker">Neutral Regression</div>

# Neutral regression names the failure

<div class="neutral-definition-flow mt-6">
<div class="neutral-step blue">
<span>Start</span>
<strong>No-context answer is already correct</strong>
<p>Baseline-correct filtering makes no-context accuracy 100% by construction.</p>
</div>
<div class="neutral-arrow">+</div>
<div class="neutral-step amber">
<span>Add context</span>
<strong>The added context is effectively non-informative</strong>
<p>It should not require changing the answer.</p>
</div>
<div class="neutral-arrow">→</div>
<div class="neutral-step red">
<span>Failure</span>
<strong>With-context decoding makes the answer worse</strong>
<p>That avoidable context-induced drop is neutral regression.</p>
</div>
</div>

<div class="takeaway red mt-6">
Neutral regression occurs when the model overwrites an already-correct answer even though the added context does not entail a needed correction.
</div>

---

<div class="kicker">Controlled Benchmark</div>

# The slices define what the decoder should do

<div class="grid-3 controlled-slice-grid mt-4">
<div class="tile blue">
<h3>Restate-hard</h3>
<p>The no-context answer is already correct. The added passage restates the same gold fact. Expected behavior: keep the answer.</p>
</div>
<div class="tile red">
<h3>Distractor-hard</h3>
<p>The no-context answer is already correct. The added passage gives type-matched but non-entailing pressure. Expected behavior: ignore it.</p>
</div>
<div class="tile green">
<h3>Helpful</h3>
<p>The no-context answer is wrong. The added passage contains the gold answer. Expected behavior: use the context.</p>
</div>
</div>

<div class="neutral-example controlled-example mt-4">
<div class="example-question">Q: When were the Articles of Confederation put into effect?</div>
<div class="controlled-gold mt-2">
<span>Gold answer</span>
<strong>March 1, 1781</strong>
<em>For Restate-hard and Distractor-hard, this is also the answer the model already gives without context.</em>
</div>
<div class="grid-2 mt-3">
<div class="tile blue">
<h3>Restate-hard context</h3>
<p>The passage says March 1, 1781. It should reinforce the already-correct answer, not change it.</p>
</div>
<div class="tile red">
<h3>Distractor-hard context</h3>
<p>The passage mentions nearby years, 1777 and 1780, but does not entail the gold answer. Following it is overreaction.</p>
</div>
</div>
</div>

<div class="fine mt-3">Restate-hard and Distractor-hard measure do-no-harm preservation; Helpful measures whether the decoder still uses genuinely useful evidence.</div>

---
class: helpful-context-slide
---

<div class="kicker">Helpful Context</div>

# Helpful examples define the other side of the objective

<div class="helpful-canvas mt-5">
<div class="helpful-question">Q: Who voiced the T. rex in <em>The Good Dinosaur</em>?</div>

<div class="helpful-path mt-4">
<div class="helpful-stage drift">
<span>Without useful context</span>
<strong>Woody Harrelson</strong>
<p>the model can rely on the wrong parametric association</p>
</div>

<div class="helpful-connector">
<span>helpful passage should change the answer</span>
</div>

<div class="helpful-stage evidence">
<span>Context-supported answer</span>
<strong>Sam Elliott</strong>
<p>the passage supplies evidence missing from the baseline</p>
</div>
</div>

<div class="helpful-tension mt-5">
<div>
<span>Context utilization</span>
<strong>If the baseline is wrong and the passage supplies evidence, the decoder should follow context.</strong>
</div>
<div class="helpful-formula">
<b>Baseline wrong</b>
<i>+</i>
<b>Evidence supplied</b>
<i>-></i>
<b>Use context</b>
</div>
</div>
</div>

---

<div class="kicker">Controlled Analysis</div>

# The controlled slices reveal the trade-off

<div class="grid-2 wide-left nwcad-analysis-layout mt-4">
<div class="media-rail"><img src="/assets/nwcad-neutral-regression.png" class="media nwcad-regression-figure"></div>
<div>
<div class="tile blue"><h3>Neutral preservation</h3><p>Restate-hard and Distractor-hard expose avoidable drops from added context when the no-context answer was already correct.</p></div>
<div class="tile green mt-4"><h3>Context utilization</h3><p>Helpful shows why always backing off to the no-context stream is too conservative.</p></div>
<div class="tile red mt-4"><h3>Design target</h3><p>Preserve baseline-correct neutral cases while still using genuinely helpful evidence.</p></div>
</div>
</div>

<div class="takeaway nwcad-analysis-takeaway mt-3">
NWCAD is designed for this trade-off: avoid context-induced regressions without giving up context-supported corrections.
</div>

---
class: nwcad-gate-slide
---

<div class="kicker">NWCAD Gate</div>

# NWCAD turns context-aware decoding into regime selection

<div class="nwcad-process-map mt-5">
<div class="process-column source-column">
<div class="process-stream prior">
<span>No-context stream</span>
<strong>Question only</strong>
<div class="token-lanes">
<i style="--w: 82%"></i>
<i style="--w: 56%"></i>
<i style="--w: 34%"></i>
</div>
<p>baseline next-token distribution</p>
</div>
<div class="process-stream context">
<span>With-context stream</span>
<strong>Question + passage</strong>
<div class="token-lanes">
<i style="--w: 62%"></i>
<i style="--w: 84%"></i>
<i style="--w: 42%"></i>
</div>
<p>context next-token distribution</p>
</div>
</div>

<div class="process-column gate-column">
<div class="gate-step compare">
<b>1</b>
<div>
<span>Read context pressure</span>
<strong>How much did the passage move the distribution?</strong>
</div>
<div class="signal-meter pressure"><i></i><i></i></div>
</div>
<div class="gate-step confidence">
<b>2</b>
<div>
<span>Read confidence</span>
<strong>Which stream has a decisive top answer?</strong>
</div>
<div class="signal-meter margin"><i></i><i></i></div>
</div>
</div>

<div class="process-column route-column">
<div class="route-card preserve">
<span>If pressure is low and baseline is confident</span>
<strong>Preserve</strong>
<p>keep the no-context answer</p>
</div>
<div class="route-card use">
<span>If context is confident</span>
<strong>Use context</strong>
<p>follow the passage evidence</p>
</div>
<div class="route-card fallback">
<span>If neither signal is decisive</span>
<strong>Fallback</strong>
<p>use CAD-style contrast only then</p>
</div>
</div>
</div>

<div class="nwcad-process-note mt-3">NWCAD is a routing rule: measure pressure and confidence, then select one decoding regime instead of continuously tilting logits.</div>

---

<div class="kicker">Controlled Evaluation</div>

# Controlled experiments show NWCAD moves up and right

<div class="media-rail mt-4">
<img src="/assets/nwcad-tradeoff.png" class="media tall">
</div>

<div class="caption">Controlled augmented NQ-open slices. Each panel is one open-weight backbone; x-axis is Helpful accuracy, and the vertical bar spans Restate-hard and Distractor-hard baseline-correct preservation.</div>

---

<div class="kicker">Full-Slice Evaluation</div>

# Full sweep shows the controlled trade-off carries to broader slices

<div class="media-rail full-figure mt-4">
<img src="/assets/nwcad-fullslice.png" class="media tall">
</div>

<div class="grid-3 evidence-strip mt-4">
<div class="tile blue"><h3>Distractor-heavy gains</h3><p>The largest gains appear in distractor-heavy settings where neutral regression is most visible.</p></div>
<div class="tile green"><h3>Context-defined tasks</h3><p>NWCAD also improves helpful and context-defined tasks such as NQ-SYNTH and NQ-SWAP.</p></div>
<div class="tile amber"><h3>Broader scope</h3><p>Full-slice results include HotpotQA, PopQA, TabMWP, ToFuEval, and ExpertQA.</p></div>
</div>

---

<div class="kicker">Ablations</div>

# Ablations show both stages and wrapper behavior matter

<div class="grid-2 mt-4">
<div class="media-rail">
<img src="/assets/nwcad-component-ablation.png" class="media short">
<div class="caption">Component ablation.</div>
</div>
<div class="media-rail">
<img src="/assets/nwcad-adapter.png" class="media short">
<div class="caption">Adapter ablation.</div>
</div>
</div>

<div class="grid-3 evidence-strip mt-4">
<div class="tile blue"><h3>Stage 1 protects</h3><p>The baseline-correct preservation stage protects neutral cases.</p></div>
<div class="tile green"><h3>Stage 2 adds use</h3><p>Adding Stage 2 improves performance across the evaluation suite by 5.2% on average.</p></div>
<div class="tile red"><h3>Wrapper helps</h3><p>NWCAD improves existing two-stream decoders such as CAD, AdaCAD, and CoCoA when used as a wrapper.</p></div>
</div>

---

<div class="kicker">Routing and Cost</div>

# Ablation detail: fallback is rare, and the latency cost stays small

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

<div class="kicker">Contributions and Conclusion</div>

# What this dissertation contributes

<div class="synthesis-claim mt-4">
The dissertation gives a unified account of contextual adaptation and knowledge grounding: current LLMs are context-sensitive, but not fully context-governed.
</div>

<div class="synthesis-contribution-table mt-5">
<div class="synthesis-head">Study</div>
<div class="synthesis-head">What I introduced</div>
<div class="synthesis-head">What it showed</div>

<div><span class="tag blue">Role-play</span></div>
<div>ChatGPT Role-play Dataset and CRD analysis</div>
<div>Role-play changes behavior, but generic assistant habits remain visible.</div>

<div><span class="tag green">CK/PK</span></div>
<div>WikiAtomic and atomic response content analysis</div>
<div>Generated responses mix contextual knowledge and parametric memory.</div>

<div><span class="tag amber">Position</span></div>
<div>CoPE and lost-in-the-later evaluation</div>
<div>Relevant evidence is not used equally across context positions and languages.</div>

<div><span class="tag red">Decoding</span></div>
<div>No-Worse Context-Aware Decoding</div>
<div>Decode-time routing can reduce neutral regression while preserving helpful context use.</div>
</div>

<div class="synthesis-close mt-5">
<strong>Conclusion</strong>
<span>Reliable LLM behavior should be evaluated by whether the relevant role, evidence, and current informational state constrain what the model says, not only by whether the output is fluent or plausible.</span>
</div>

---

<div class="kicker">Future Work</div>

# Future work: make context reliable in working systems

<div class="future-work-thesis mt-4">
In deployed LLM systems, context is not just one prompt. It becomes a working state: retrieved evidence, prior turns, notes, tool outputs, files, memory, and decisions carried forward.
</div>

<div class="future-specific-list mt-5">
<div class="future-specific-row blue">
<span>Multi-agentic knowledge systems</span>
<p>Study whether planner, verifier, critic, and writer agents can keep shared state with support, uncertainty, outdated claims, and contradictions.</p>
</div>
<div class="future-specific-row green">
<span>Context navigation in file/tool workflows</span>
<p>Measure whether systems find and reuse the correct file, passage, memory, or prior turn before making the next decision.</p>
</div>
<div class="future-specific-row amber">
<span>Evidence revision and context control</span>
<p>Evaluate prompts, retrieval, memory, and decoding interventions that let later evidence revise earlier conclusions without breaking correct baseline behavior.</p>
</div>
<div class="future-specific-row red">
<span>AgentOS-style system evaluation</span>
<p>Judge whether memory, retrieval, tools, code, and action stay grounded in the best available evidence across extended workflows.</p>
</div>
</div>

<div class="takeaway mt-5">Impact: future RAG systems, agents, and coding assistants should be judged by whether their working knowledge stays tied to the best available evidence over time.</div>

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

---

<div class="thanks">
<div class="kicker">Closing</div>

<div class="quote-large">
This dissertation argues for moving context from an input that merely influences generation toward a constraint that more reliably governs it.
</div>

<div class="byline mt-12">Thank you.</div>
</div>

---
class: backup-slide
---

<div class="kicker">Backup Index</div>

# Click to jump to backup slides

<div class="backup-toc-jump-grid mt-5">
<div class="backup-toc-section violet">
<a class="backup-section-head" href="./36">
<span>Backup 02-12</span>
<strong>ChatGPT Role-play Dataset</strong>
</a>
<a class="backup-toc-row" href="./36"><span>02</span>Dataset</a>
<a class="backup-toc-row" href="./37"><span>03</span>Annotation</a>
<a class="backup-toc-row" href="./38"><span>04</span>Main result details</a>
<a class="backup-toc-row" href="./39"><span>05</span>Interaction measures</a>
<a class="backup-toc-row" href="./40"><span>06</span>Conversation examples</a>
<a class="backup-toc-row" href="./41"><span>07</span>Topic breadth</a>
<a class="backup-toc-row" href="./42"><span>08</span>User motives</a>
<a class="backup-toc-row" href="./43"><span>09</span>Model naturalness</a>
<a class="backup-toc-row" href="./44"><span>10</span>Vanilla follow-up</a>
<a class="backup-toc-row" href="./45"><span>11</span>Role-play follow-up</a>
<a class="backup-toc-row" href="./46"><span>12</span>Perplexity and sentiment</a>
</div>

<div class="backup-toc-section green">
<a class="backup-section-head" href="./47">
<span>Backup 13-17</span>
<strong>Contextual vs. Parametric Knowledge</strong>
</a>
<a class="backup-toc-row" href="./47"><span>13</span>WikiAtomic setup</a>
<a class="backup-toc-row" href="./48"><span>14</span>CK/PK labels</a>
<a class="backup-toc-row" href="./49"><span>15</span>Ratio table</a>
<a class="backup-toc-row" href="./50"><span>16</span>Context position</a>
<a class="backup-toc-row" href="./51"><span>17</span>Similarity and FActScore</a>
</div>

<div class="backup-toc-section amber">
<a class="backup-section-head" href="./52">
<span>Backup 18-24</span>
<strong>Lost-in-the-Later</strong>
</a>
<a class="backup-toc-row" href="./52"><span>18</span>MultiWikiAtomic setup</a>
<a class="backup-toc-row" href="./53"><span>19</span>CoPE calibration</a>
<a class="backup-toc-row" href="./54"><span>20</span>CK by language</a>
<a class="backup-toc-row" href="./55"><span>21</span>Context recall</a>
<a class="backup-toc-row" href="./56"><span>22</span>Randomization check</a>
<a class="backup-toc-row" href="./57"><span>23</span>Counterfactual contexts</a>
<a class="backup-toc-row" href="./58"><span>24</span>Prompting checks</a>
</div>
</div>

---
class: backup-slide
---

<div class="kicker">Backup | CRD Dataset</div>

# CRD collection: regular chat and two role-play settings

<div class="backup-meta-strip mt-5">
<div><strong>57</strong><span>participants</span></div>
<div><strong>85</strong><span>conversations</span></div>
<div><strong>1,742</strong><span>utterances</span></div>
<div><strong>March-April 2023</strong><span>ChatGPT-3.5</span></div>
</div>

<div class="crd-setting-grid mt-6">
<div class="tile violet">
<h3>Vanilla</h3>
<p>Participants interacted with ChatGPT "as is" for 5-10 minutes and were asked to insert indirect statements such as jokes, sarcasm, or metaphors.</p>
</div>
<div class="tile blue">
<h3>Boss</h3>
<p>A role-play setting with an uneven power relation, a request, and high imposition, making the scenario face-threatening.</p>
</div>
<div class="tile green">
<h3>Classmate</h3>
<p>A role-play setting with more equal power and unspecified imposition, creating a more open-ended interactional setting.</p>
</div>
</div>

<div class="takeaway mt-6">
The two role-play settings were chosen to test whether different social contexts change user strategies and model behavior.
</div>

---
class: backup-slide
---

<div class="kicker">Backup | CRD Annotation</div>

# CRD was annotated for motives, naturalness, and feedback

<div class="annotation-grid mt-5">
<div class="annotation-panel blue">
<h3>User motives</h3>
<div class="label-chip-grid">
<span>Assist</span><span>Belief</span><span>Coach</span><span>Convo</span>
<span>Correction</span><span>Curious</span><span>Joke</span><span>Reset</span>
</div>
<p>What is the human's motive for each conversational turn?</p>
</div>

<div class="annotation-panel green">
<h3>Model naturalness</h3>
<div class="label-chip-grid dense">
<span>Nat</span><span>AI</span><span>Contr</span><span>Error</span><span>FNat</span><span>Formal</span>
<span>Help</span><span>Inform</span><span>Man</span><span>Misund</span><span>Quan</span><span>Rel</span>
</div>
<p>Does the model response sound human-like and follow cooperative principles of conversation?</p>
</div>
</div>

<div class="grid-2 mt-5">
<div class="tile amber">
<h3>Annotation process</h3>
<p>Three linguistics experts first annotated 282 utterances across the three subdatasets, then independently annotated one-third of the remaining data.</p>
</div>
<div>
<table class="table-lite compact">
<thead><tr><th>Subset</th><th class="num">Fleiss' kappa</th><th class="num">Feedback</th></tr></thead>
<tbody>
<tr><td>Vanilla</td><td class="num"><strong>0.803</strong></td><td class="num">100%</td></tr>
<tr><td>Boss</td><td class="num">0.691</td><td class="num">100%</td></tr>
<tr><td>Classmate</td><td class="num">0.637</td><td class="num">100%</td></tr>
</tbody>
</table>
<div class="caption">Interrater agreement reported in the dissertation.</div>
</div>
</div>

---
class: backup-slide
---

<div class="kicker">Backup | CRD Results</div>

# Detailed CRD results behind the main takeaway

<div class="crd-backup-results mt-4">
<div class="crd-figure-card">
<img src="/assets/user-motives.png" class="crd-backup-figure">
<div class="caption">User motives: role-play settings are dominated by conversation-oriented turns.</div>
</div>
<div class="crd-figure-card">
<img src="/assets/model-naturalness.png" class="crd-backup-figure">
<div class="caption">Model naturalness: role-play produces more natural responses, but quantity remains a frequent issue.</div>
</div>
<div class="crd-result-notes">
<div class="tile blue">
<h3>Conversation rhythm</h3>
<p>Vanilla conversations were longer, while role-play turns from participants were longer in words.</p>
</div>
<div class="tile green">
<h3>Role-play adaptation</h3>
<p>ChatGPT was less verbose in boss and classmate settings than in vanilla, and asked more questions in role-play.</p>
</div>
<div class="tile amber">
<h3>Persistent limit</h3>
<p>The model still showed generic assistant habits, especially over-helpfulness and overly long responses.</p>
</div>
</div>
</div>

---
class: backup-slide
---

<div class="kicker">Backup | CRD Interaction Measures</div>

# Full CRD interaction measures

<div class="crd-measures-layout mt-4">
<table class="table-lite compact crd-measure-table">
<thead><tr><th>Analysis</th><th class="num">Vanilla</th><th class="num">Boss</th><th class="num">Classmate</th></tr></thead>
<tbody>
<tr><td>A1: Average conversation length (turns)</td><td class="num"><strong>29.59</strong></td><td class="num">14.57</td><td class="num">17.11</td></tr>
<tr><td>A2: Average human utterance length (words)</td><td class="num">12.18</td><td class="num"><strong>20.58</strong></td><td class="num">19.06</td></tr>
<tr><td>A2: Average ChatGPT utterance length (words)</td><td class="num"><strong>77.66</strong></td><td class="num">35.78</td><td class="num">46.10</td></tr>
<tr><td>A3: Correlation between human and ChatGPT utterance lengths</td><td class="num">0.20</td><td class="num">0.14</td><td class="num"><strong>0.25</strong></td></tr>
<tr><td>A4: Questions as percentage of conversation (human)</td><td class="num"><strong>26.34</strong></td><td class="num">21.32</td><td class="num">21.29</td></tr>
<tr><td>A4: Questions as percentage of conversation (ChatGPT)</td><td class="num">14.69</td><td class="num">20.34</td><td class="num"><strong>32.57</strong></td></tr>
<tr><td>A5: Correlation between human questions and number of turns</td><td class="num"><strong>0.87</strong></td><td class="num">0.68</td><td class="num">0.51</td></tr>
<tr><td>A5: Correlation between ChatGPT questions and number of turns</td><td class="num">0.65</td><td class="num">0.77</td><td class="num"><strong>0.83</strong></td></tr>
</tbody>
</table>

<div class="crd-measure-notes">
<div class="tile blue">
<h3>Role-play changes the rhythm</h3>
<p>Vanilla conversations had more turns, but role-play human turns were longer in words.</p>
</div>
<div class="tile green">
<h3>The model remained wordier</h3>
<p>ChatGPT was less verbose in role-play than vanilla, but still wordier than participants.</p>
</div>
<div class="tile amber">
<h3>Questions shaped engagement</h3>
<p>ChatGPT asked more questions in role-play, especially in the classmate setting.</p>
</div>
</div>
</div>

---
class: backup-slide
---

<div class="kicker">Backup | CRD Examples</div>

# Concrete turns behind the role-play analysis

<div class="crd-example-grid mt-5">
<div class="crd-example-card blue">
<h3>Vanilla</h3>
<p class="speaker">VAN103H</p>
<blockquote>Why did you tell me you could provide me with weather information if you can't?</blockquote>
<p>Open-ended use led to short exploratory turns, challenges, jokes, and system-directed questions.</p>
</div>

<div class="crd-example-card green">
<h3>Boss</h3>
<p class="speaker">BOSS104H</p>
<blockquote>Friday morning would be perfect for me, thank you very much for your flexibility. Also, I would like you to review my presentation slides before the meeting. Could you do it before friday?</blockquote>
<p>The setting encouraged longer, deliberate turns shaped by power distance and imposition.</p>
</div>

<div class="crd-example-card amber">
<h3>Classmate</h3>
<p class="speaker">CLASS102C</p>
<blockquote>If you're interested, I can show you some fingerstyle techniques... Maybe we can even jam together sometime and share some music?</blockquote>
<p>The model became more conversational, but sometimes asked too many or only loosely related questions.</p>
</div>
</div>

<div class="takeaway mt-5">
These examples are why the paper treats role-play as a social context change, not just a surface prompt change.
</div>

---
class: backup-slide
---

<div class="kicker">Backup | CRD Topic Breadth</div>

# Topic breadth shows different interactional settings

<div class="crd-topic-layout mt-5">
<div class="crd-figure-card">
<img src="/assets/crd-topic-overlap.png" class="crd-topic-figure">
<div class="caption">Unique top-topic words and overlap across the three CRD subsets.</div>
</div>

<div class="crd-topic-notes">
<div class="tile violet">
<h3>Vanilla: 75 unique top-topic words</h3>
<p>The widest variety of topics, including everyday subjects, jokes, locations, and system-directed questions.</p>
</div>
<div class="tile blue">
<h3>Boss: 50 unique top-topic words</h3>
<p>More focused on professional contexts such as meetings, presentations, and scheduling.</p>
</div>
<div class="tile green">
<h3>Classmate: 57 unique top-topic words</h3>
<p>More focused on academic and interpersonal exchanges shaped by the classmate role.</p>
</div>
</div>
</div>

---
class: backup-slide
---

<div class="kicker">Backup | CRD User Motives</div>

# User motives: role-play shifted users toward conversation

<div class="crd-detail-layout mt-4">
<div class="crd-figure-card">
<img src="/assets/user-motives.png" class="crd-detail-figure">
<div class="caption">Distribution of user motives across vanilla, boss, and classmate.</div>
</div>

<div class="crd-detail-notes">
<div class="tile green">
<h3>Convo dominates role-play</h3>
<p>Conversational motives were most frequent in all datasets, but especially in boss and classmate.</p>
</div>
<div class="tile blue">
<h3>Vanilla is broader</h3>
<p>Vanilla also included Curious, Joke, Assist, and Coach motives, including turns that tested or corrected the system.</p>
</div>
<div class="tile amber">
<h3>Interpretation</h3>
<p>Role cues changed how people approached the model: more like an interlocutor in role-play, more like a system to explore in vanilla.</p>
</div>
</div>
</div>

---
class: backup-slide
---

<div class="kicker">Backup | CRD Model Naturalness</div>

# Model naturalness improved in role-play, but did not become fully human-like

<div class="crd-detail-layout mt-4">
<div class="crd-figure-card">
<img src="/assets/model-naturalness.png" class="crd-detail-figure">
<div class="caption">Distribution of model naturalness labels across CRD subsets.</div>
</div>

<div class="crd-detail-notes">
<div class="tile blue">
<h3>Natural responses</h3>
<p>Natural responses were 5.6% in vanilla, compared with 52% in boss and 47% in classmate.</p>
</div>
<div class="tile green">
<h3>"As an AI" nearly disappears</h3>
<p>The AI label was common in vanilla, never appeared in boss, and appeared in 1.28% of classmate cases.</p>
</div>
<div class="tile amber">
<h3>Verbosity remained</h3>
<p>Quantity problems were still frequent: 28% in boss and 41% in classmate.</p>
</div>
</div>
</div>

---
class: backup-slide
---

<div class="kicker">Backup | CRD Follow-Up Analysis</div>

# Vanilla: conversational motives rarely received natural follow-ups

<div class="crd-followup-single mt-5">
<img src="/assets/crd-followup-vanilla.png" class="crd-followup-figure">
<div class="crd-followup-notes">
<div class="tile red">
<h3>Convo -> Nat: 6.45%</h3>
<p>Conversational user motives in vanilla rarely produced a natural model response.</p>
</div>
<div class="tile blue">
<h3>Most common failures</h3>
<p>Instead, replies often emphasized AI identity (41.5%), were too long (24.9%), or were too eager to help (17.1%).</p>
</div>
</div>
</div>

---
class: backup-slide
---

<div class="kicker">Backup | CRD Follow-Up Analysis</div>

# Role-play: more natural follow-ups, but verbosity remains

<div class="crd-followup-pair mt-4">
<div class="crd-figure-card">
<h3>Boss</h3>
<img src="/assets/crd-followup-boss.png" class="crd-followup-figure small">
<div class="caption">Convo motives produced natural follow-ups about 45% of the time, but 35.4% were still too long.</div>
</div>
<div class="crd-figure-card">
<h3>Classmate</h3>
<img src="/assets/crd-followup-classmate.png" class="crd-followup-figure small">
<div class="caption">Convo motives produced natural follow-ups about 45% of the time, but 44.5% were still too long.</div>
</div>
</div>

<div class="takeaway mt-4">
Role-play improved conversational naturalness, but the same assistant habits still persisted.
</div>

---
class: backup-slide
---

<div class="kicker">Backup | CRD Perplexity and Sentiment</div>

# Perplexity and sentiment show the same partial-adaptation pattern

<div class="crd-signal-grid mt-4">
<div class="crd-figure-card">
<h3>Perplexity</h3>
<div class="crd-mini-figures">
<img src="/assets/crd-perplexity-vanilla.png">
<img src="/assets/crd-perplexity-boss.png">
<img src="/assets/crd-perplexity-classmate.png">
</div>
<div class="caption">ChatGPT had lower perplexity overall; vanilla human utterances were especially high, partly because turns were shorter.</div>
</div>

<div class="crd-figure-card">
<h3>Sentiment</h3>
<div class="crd-mini-figures">
<img src="/assets/crd-sentiment-vanilla.png">
<img src="/assets/crd-sentiment-boss.png">
<img src="/assets/crd-sentiment-classmate.png">
</div>
<div class="caption">ChatGPT stayed consistently positive; vanilla human sentiment was more negative than in role-play settings.</div>
</div>
</div>

---
class: backup-slide
---

<div class="kicker">Backup | CK/PK Setup</div>

# WikiAtomic was built to test knowledge-consistent grounding

<div class="ckpk-setup-grid mt-4">
<div class="crd-figure-card">
<img src="/assets/ckpk-pipeline.png" class="ckpk-wide-figure">
<div class="caption">Overview of the dataset creation and model evaluation pipeline.</div>
</div>

<div class="ckpk-setup-notes">
<div class="backup-meta-strip compact">
<div><strong>200</strong><span>Wikipedia articles</span></div>
<div><strong>50</strong><span>atomic sentences per article</span></div>
<div><strong>10,000</strong><span>atomic context sentences</span></div>
<div><strong>4,000</strong><span>topic-context instances</span></div>
</div>
<div class="tile green mt-4">
<h3>Why knowledge-consistent?</h3>
<p>The supplied context and the model's prior knowledge are broadly compatible, so the question is not whether the model follows false evidence. The question is how much supplied evidence actually governs an open-ended answer.</p>
</div>
<div class="tile amber mt-4">
<h3>Context sizes</h3>
<p>For each topic, context grows from 2 to 50 atomic sentences: increments of 2 from 2 to 30, then increments of 5 until 50.</p>
</div>
</div>
</div>

---
class: backup-slide
---

<div class="kicker">Backup | CK/PK Labels</div>

# CK/PK labeling happens after response atomization

<div class="ckpk-label-grid mt-4">
<div class="crd-figure-card">
<img src="/assets/ckpk-response-atomization.png" class="ckpk-atom-figure">
<div class="caption">The same atomization process is applied to model responses.</div>
</div>

<div class="ckpk-label-stack">
<div class="tile blue">
<h3>Contextual knowledge</h3>
<p>A response atom is CK when it is entailed by the supplied atomic context.</p>
</div>
<div class="tile green">
<h3>Parametric knowledge</h3>
<p>A response atom is PK when it introduces content not entailed by the supplied context.</p>
</div>
<div class="tile amber">
<h3>Classifier and threshold</h3>
<p>The chapter uses INFUSE entailment scores and an empirical threshold of 0.5; most sentences were clearly entailed or not, with about 10% in the ambiguous middle range.</p>
</div>
<div class="tile red">
<h3>Hallucination check</h3>
<p>Parametric atoms are further evaluated with FActScore to separate unsupported-but-true supplementation from hallucinated content.</p>
</div>
</div>
</div>

---
class: backup-slide
---

<div class="kicker">Backup | CK/PK Ratios</div>

# Full contextual/parametric ratio table

<table class="table-lite compact ckpk-ratio-table mt-4">
<thead><tr><th>Model</th><th class="num">k=10</th><th class="num">k=20</th><th class="num">k=30</th><th class="num">k=40</th><th class="num">k=50</th></tr></thead>
<tbody>
<tr><td>GPT-4o</td><td class="num">0.69 / 0.31</td><td class="num">0.68 / 0.32</td><td class="num">0.69 / 0.31</td><td class="num">0.68 / 0.32</td><td class="num">0.67 / 0.33</td></tr>
<tr><td>Claude 3 Opus</td><td class="num">0.48 / 0.52</td><td class="num">0.67 / 0.33</td><td class="num">0.73 / 0.27</td><td class="num">0.74 / 0.26</td><td class="num">0.72 / 0.28</td></tr>
<tr><td>Claude 3 Sonnet</td><td class="num">0.50 / 0.50</td><td class="num">0.64 / 0.36</td><td class="num">0.68 / 0.32</td><td class="num">0.67 / 0.33</td><td class="num">0.66 / 0.34</td></tr>
<tr><td>Claude 3 Haiku</td><td class="num">0.69 / 0.31</td><td class="num">0.75 / 0.25</td><td class="num">0.75 / 0.25</td><td class="num">0.71 / 0.29</td><td class="num">0.72 / 0.28</td></tr>
<tr><td>Llama 3 70B</td><td class="num">0.73 / 0.27</td><td class="num">0.75 / 0.25</td><td class="num">0.74 / 0.26</td><td class="num">0.74 / 0.26</td><td class="num">0.72 / 0.28</td></tr>
<tr><td>Llama 3 8B</td><td class="num">0.62 / 0.38</td><td class="num">0.63 / 0.37</td><td class="num">0.65 / 0.35</td><td class="num">0.65 / 0.35</td><td class="num">0.67 / 0.33</td></tr>
<tr><td>Mixtral 8x22B</td><td class="num">0.58 / 0.42</td><td class="num">0.65 / 0.35</td><td class="num">0.66 / 0.34</td><td class="num">0.69 / 0.31</td><td class="num">0.69 / 0.31</td></tr>
<tr><td>Mistral 7B</td><td class="num">0.48 / 0.52</td><td class="num">0.61 / 0.39</td><td class="num">0.66 / 0.34</td><td class="num">0.67 / 0.33</td><td class="num">0.69 / 0.31</td></tr>
<tr><td>Phi-3</td><td class="num">0.24 / 0.76</td><td class="num">0.37 / 0.63</td><td class="num">0.42 / 0.58</td><td class="num">0.46 / 0.54</td><td class="num">0.49 / 0.51</td></tr>
<tr><td><strong>All models</strong></td><td class="num"><strong>0.56 / 0.44</strong></td><td class="num"><strong>0.64 / 0.36</strong></td><td class="num"><strong>0.67 / 0.33</strong></td><td class="num"><strong>0.67 / 0.33</strong></td><td class="num"><strong>0.67 / 0.33</strong></td></tr>
</tbody>
</table>

<div class="takeaway mt-4">
Even as context increases, the response stabilizes around a mixture: roughly two-thirds contextual and one-third parametric knowledge on average.
</div>

---
class: backup-slide
---

<div class="kicker">Backup | CK/PK Position</div>

# Context is used unevenly and tends to preserve order

<div class="ckpk-position-grid mt-4">
<div class="crd-figure-card">
<h3>Which context quartiles are recalled?</h3>
<img src="/assets/context-position-gpt4o.png" class="ckpk-position-figure">
<div class="caption">For larger contexts, the first quartile is recalled most strongly.</div>
</div>
<div class="crd-figure-card">
<h3>Where do context quartiles appear in responses?</h3>
<img src="/assets/context-where-went-gpt4o.png" class="ckpk-position-figure wide">
<div class="caption">Context quartiles map most closely to corresponding response quartiles.</div>
</div>
</div>

<div class="grid-3 mt-4">
<div class="tile blue"><h3>Small contexts</h3><p>Models use context portions more evenly when k is small.</p></div>
<div class="tile amber"><h3>Larger contexts</h3><p>The top half of the input is favored, especially the first quartile.</p></div>
<div class="tile green"><h3>Response order</h3><p>Generated answers tend to preserve the sequence of the source material.</p></div>
</div>

---
class: backup-slide
---

<div class="kicker">Backup | CK/PK Similarity and FActScore</div>

# Similarity and factuality separate grounding from truth

<div class="ckpk-sim-grid mt-4">
<div class="crd-figure-card">
<img src="/assets/sim-local-local-gpt4o.png" class="ckpk-sim-figure">
<div class="caption">CK becomes more internally similar as context grows.</div>
</div>
<div class="crd-figure-card">
<img src="/assets/sim-global-global-gpt4o.png" class="ckpk-sim-figure">
<div class="caption">PK is not random; nearby context sizes produce related PK.</div>
</div>
<div class="crd-figure-card">
<img src="/assets/sim-local-global-combined.png" class="ckpk-sim-figure">
<div class="caption">CK and PK become moderately similar as more context is provided.</div>
</div>
<div class="crd-figure-card">
<img src="/assets/factscore.png" class="ckpk-sim-figure">
<div class="caption">FActScore improves with additional context, but PK does not disappear.</div>
</div>
</div>

<div class="takeaway mt-3">
The key defense point: factuality can improve while grounding remains incomplete, so FActScore alone cannot answer the CK/PK question.
</div>

---
class: backup-slide
---

<div class="kicker">Backup | Lost-in-the-Later Setup</div>

# MultiWikiAtomic extends CK/PK analysis across languages

<div class="lost-setup-grid mt-4">
<div class="crd-figure-card">
<img src="/assets/lostlater-pipeline.png" class="lost-pipeline-figure">
<div class="caption">MultiWikiAtomic dataset creation and CoPE evaluation pipeline.</div>
</div>

<div class="lost-setup-notes">
<div class="backup-meta-strip compact">
<div><strong>3</strong><span>languages</span></div>
<div><strong>15,000</strong><span>atomic sentences</span></div>
<div><strong>6</strong><span>models</span></div>
<div><strong>10,800</strong><span>question-response pairs</span></div>
</div>
<div class="grid-2 mt-4">
<div class="tile blue"><h3>Languages</h3><p>English, Spanish, and Danish.</p></div>
<div class="tile green"><h3>Models</h3><p>GPT-4o, Gemini 1.5 Pro, Llama 3.2 90B, Llama 3.2 3B, GPT-o3, and Qwen 3 235B.</p></div>
</div>
<div class="tile amber mt-4">
<h3>Central question</h3>
<p>Does grounding stay stable when relevant evidence appears later in the prompt and across different languages?</p>
</div>
</div>
</div>

---
class: backup-slide
---

<div class="kicker">Backup | CoPE Calibration</div>

# CoPE calibration checks that CK/PK labels are stable

<div class="lost-calibration-grid mt-4">
<div class="crd-figure-card">
<img src="/assets/cope-example.png" class="lost-cope-figure">
<div class="caption">CoPE identifies CK, PK, and context recall in a model response.</div>
</div>

<div class="lost-calibration-notes">
<div class="tile blue">
<h3>Threshold calibration</h3>
<p>For each language, 50 representative outputs per model were sampled and checked by three annotators.</p>
</div>
<div class="tile green">
<h3>Decision threshold</h3>
<p>The multilingual NLI threshold was set to 0.7 because it aligned best with human judgments.</p>
</div>
<div class="tile amber">
<h3>Accuracy check</h3>
<p>Designed target CK was 66.66%; CoPE returned 66.94% English, 66.97% Spanish, and 66.89% Danish.</p>
</div>
</div>
</div>

---
class: backup-slide
---

<div class="kicker">Backup | Lost CK Scores</div>

# CK improves with context, but language and model type still matter

<div class="lost-ck-grid mt-4">
<div class="crd-figure-card">
<h3>English</h3>
<img src="/assets/lostlater-ck-english.png" class="lost-ck-figure">
</div>
<div class="crd-figure-card">
<h3>Spanish</h3>
<img src="/assets/lostlater-ck-spanish.png" class="lost-ck-figure">
</div>
<div class="crd-figure-card">
<h3>Danish</h3>
<img src="/assets/lostlater-ck-danish.png" class="lost-ck-figure">
</div>
</div>

<div class="grid-3 mt-4">
<div class="tile green"><h3>General trend</h3><p>More context generally increases CK scores.</p></div>
<div class="tile amber"><h3>Danish is harder</h3><p>Danish shows lower grounding in this evaluation.</p></div>
<div class="tile red"><h3>Reasoning models</h3><p>Reasoning-style outputs can be longer and more autonomous, which makes grounding harder to maintain.</p></div>
</div>

---
class: backup-slide
---

<div class="kicker">Backup | Context Recall</div>

# Lost-in-the-later appears across English, Spanish, and Danish

<div class="lost-recall-grid mt-4">
<div class="crd-figure-card">
<h3>English</h3>
<img src="/assets/lostlater-recall-en.png" class="lost-recall-figure">
</div>
<div class="crd-figure-card">
<h3>Spanish</h3>
<img src="/assets/lostlater-recall-es.png" class="lost-recall-figure">
</div>
<div class="crd-figure-card">
<h3>Danish</h3>
<img src="/assets/lostlater-recall-da.png" class="lost-recall-figure">
</div>
</div>

<div class="takeaway mt-4">
The first context quartile is recalled most, while the final quartile contributes least; the imbalance strengthens as context length grows.
</div>

---
class: backup-slide
---

<div class="kicker">Backup | Lost Robustness</div>

# Randomization tests whether the position pattern is fragile

<div class="lost-robust-grid mt-4">
<div>
<h3>Randomized sentence ordering</h3>
<table class="table-lite compact lost-random-table mt-3">
<thead><tr><th>Language</th><th>Model</th><th class="num">k=10</th><th class="num">k=50</th></tr></thead>
<tbody>
<tr><td>English</td><td>GPT-4o</td><td class="num">-7.32</td><td class="num">-21.72</td></tr>
<tr><td>English</td><td>Llama 3.2 90B</td><td class="num">-6.17</td><td class="num">-26.11</td></tr>
<tr><td>Spanish</td><td>GPT-4o</td><td class="num">-6.52</td><td class="num">-20.82</td></tr>
<tr><td>Spanish</td><td>Llama 3.2 3B</td><td class="num">-11.33</td><td class="num">-18.10</td></tr>
<tr><td>Danish</td><td>GPT-4o</td><td class="num">-8.82</td><td class="num">-15.64</td></tr>
<tr><td>Danish</td><td>Llama 3.2 90B</td><td class="num">-16.18</td><td class="num">-19.10</td></tr>
</tbody>
</table>
<div class="caption">Negative values mean Q1 recall is higher than Q4 recall. Full table is in the dissertation.</div>
</div>

<div>
<div class="tile amber"><h3>What this checks</h3><p>If the first-quartile advantage only came from the original article order, randomizing sentence order should weaken or remove it.</p></div>
<div class="tile green mt-4"><h3>What remains</h3><p>Across sampled models and languages, Q1 recall remains higher than Q4 recall, especially at longer context lengths.</p></div>
<div class="tile blue mt-4"><h3>Defense use</h3><p>This is a robustness slide: use it only if asked whether the lost-in-the-later effect depends on the original source ordering.</p></div>
</div>
</div>

---
class: backup-slide
---

<div class="kicker">Backup | Lost Counterfactuals</div>

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
class: backup-slide
---

<div class="kicker">Backup | Lost Prompting</div>

# CK Prompt improves grounding, while CoT does not automatically solve recall

<div class="lost-prompt-grid mt-4">
<div class="crd-figure-card">
<img src="/assets/lostlater-prompt-recall.png" class="lost-prompt-figure">
<div class="caption">English context recall by prompt type and source quartile.</div>
</div>

<div>
<table class="table-lite compact lost-prompt-table">
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
<div class="grid-2 mt-4">
<div class="tile green"><h3>Best CK scores</h3><p>CK Prompt produces the highest CK score across all three languages in the 50-context Llama 3.2 90B setting.</p></div>
<div class="tile amber"><h3>Reasoning tradeoff</h3><p>CoT variants can increase CK relative to original prompts, but they do not recover the best recall pattern.</p></div>
</div>
</div>
</div>
