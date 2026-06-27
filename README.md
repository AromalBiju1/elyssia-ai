# Elyssia-AI

> A biologically-grounded cognitive architecture researching Emergent Cognitive Intelligence (ECI)

Elyssia is not a chatbot wrapper. It's a ground-up attempt to build a mind — one where every module maps to real neuroscience, every connection has a reason, and the system maintains persistent internal state across time.

The LLM is the last step, not the system.

---

## Architecture

<img width="778" height="665" alt="Screenshot_20260627_230904" src="https://github.com/user-attachments/assets/9947eb27-1719-40fd-abcc-eeeda51b5b22" />


*80+ biologically-grounded modules — 316 wired edges — across cortical, subcortical, and brainstem layers*

---

## How a single turn works

Every response runs through a **6-round recurrent execution loop** before the generator fires.

**Round 0 — Global modulators**
LC-NE sets arousal gain. HPC flags processing depth. Thalamus gates the prompt. Monoamine systems (ACh, 5-HT, DA) prime the network. HeartBrainBridge computes vagal tone and bond state. Moral intuitions fire fast via Haidt's social intuitionist model.

**Round 1 — Core affect**
Amygdala computes raw emotion via GoEmotions ONNX inference. Allostasis constructs an integrated emotional state from interoceptive prediction, reappraisal, somatic markers, and social baseline (Coan & Sbarra's Social Baseline Theory). ASAN spreads associative priming. BIS/BAS, attachment/grief, vitality, and boredom modules run in parallel.

**Round 1.5 — Metacognition & attention**
Higher-Order Thought monitors for metacognitive conflicts. Salience Map computes signal competition. Global Workspace Ignition fires the winning coalition (Baars' Global Workspace Theory). Temporal Binding, Emotional Granularity, and Epistemic Curiosity modules read the integrated state.

**Round 2 — Context assembly**
Palace-structured LTM, STM episodic buffer, and segment memory load. Theory of Mind updates. Default Mode Network runs a session arc. Akrasia checks ego reserve. Conscience monitors for anticipatory moral violations. Context Assembly integrates everything through claustrum binding, temporal self-model (autobiographical continuity), phenomenal binding, and a token-budgeted CCO context registry across 18 channels. PFC reasoning runs single-fire before this round, outputs response guidance and a top-down regulation signal that can re-fire the amygdala if affect is high.

**Round 3 — Generation & evaluation**
Motor generator fires with fully assembled context. Metacognitive monitor reads output before Guardian. Guardian (four-stream DeBERTa framed on ACC/OFC/INSULA/PFC) scores it and can trigger a regeneration loop. Recursive Self-Corrector checks for character drift and sycophancy patterns. Self-Awareness Engine monitors identity coherence.

**Round 4 — Retrospective learning**
Counterfactual simulation. Self-Surprise Discovery. Hebbian synaptic encoding (BCM sliding threshold rule — Bienenstock, Cooper & Munro 1982). RSIE adapts connectivity edge weights for next turn.

**Post-turn (async)** — Memory consolidation, personality write.

---

## Key subsystems

**Activation graph** — 316 edges wired into a Rust/PyO3 FastDispatcher at startup. Per-module threshold, decay, and single-fire constraints. Python mailbox routing layered on top. RSIE-adapted weights reload at engine start.

**Hormonal system** — 11-hormone model (dopamine, serotonin, oxytocin, cortisol, adrenaline, norepinephrine, GABA, endorphins, testosterone, estrogen, progesterone). Homeostatic decay converges to a true fixed point. Six biological antagonisms modelled explicitly: HPA-mesolimbic suppression, oxytocin social buffering (Coan 2006), GABAergic HPA inhibition, endorphin-ACTH suppression, testosterone-cortisol seesaw, and serotonin-HPA sensitivity amplification. Dopamine refractory period modelled on Schultz (1997) reward prediction error.

**Personality engine v5** — Five biological mechanisms: polyvagal gating (Porges' Polyvagal Theory), emotional momentum via Hebbian sensitisation, BCM sliding threshold on all traits, always-on homeostatic restoration (synaptic scaling), and experience crystallisation (Late-LTP → setpoint shift after sustained patterns). Trait correlation web based on serotonin/oxytocin and dopamine/testosterone families. Diurnal overlays model circadian cortisol/serotonin rhythms.

**Memory** — Palace-structured LTM with wing/hall/room taxonomy, STM episodic buffer, and segment memory for dense retrieval. Hebbian reconsolidation updates importance scores per mood state. ASAN bias modulates retrieval at assembly time. Temporal self-model maintains autobiographical continuity across turns.

**Guardian v8** — Multi-label DeBERTa-v3-small. 14 violation types across four neurologically-framed streams. Blocks output or triggers correction loop.

**Multimodal** — Image input supported via vision payload in context assembly. Whisper STT and Kokoro TTS for voice.

**DMN** — Default Mode Network runs a session arc tracking mood trajectory, self-referential processing, and open thought threads (Zeigarnik effect).

**Recursive Self-Corrector** — Detects character drift, hot cognition trajectory, and sycophancy patterns across turns. Feeds correction signals before generation.

---

## Theoretical grounding

Key frameworks this architecture draws from:

- Baars (1988) — Global Workspace Theory
- Porges (1994) — Polyvagal Theory  
- Bienenstock, Cooper & Munro (1982) — BCM synaptic plasticity rule
- Schultz (1997) — Dopamine reward prediction error
- Coan & Sbarra (2015) — Social Baseline Theory
- Panksepp (1998) — Affective neuroscience / SEEKING system
- Fisher (2005) — Catecholamine theory of romantic attachment
- Haidt (2001) — Social intuitionist model of moral judgment
- Friston (2010) — Predictive processing / active inference
- Tulving (1985) — Episodic memory and autonoetic consciousness

Memory architecture inspired in part by [MemPalace](https://github.com/mempalace/mempalace) and segment memory concepts from [arxiv:2602.24281](https://arxiv.org/abs/2602.24281).

---

## Stack

- **Runtime**: CachyOS · RTX 4050 6GB · systemd daemon
- **Generator**: Qwen3.5 4B Q4_K_M (llama.cpp, GPU, port 8080)
- **Reasoner**: Gemma 4 E2B Q4_K (llama.cpp, CPU, port 8081)
- **Activation graph**: Rust/PyO3 FastDispatcher + Python fallback
- **ML**: PyTorch · ONNX · DeBERTa · GoEmotions · fastembed
- **Voice**: Whisper STT · Kokoro TTS (lazy-loaded)
- **Backend**: FastAPI · SQLite · Python 3.11
- **Frontend**: React.js
---

## Status

Active development. Core architecture stable at v4.5. Source is private.
