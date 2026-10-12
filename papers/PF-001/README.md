# PF-001 — Beyond a Single Future

**Subtitle:** An AI-Augmented Actuarial Engineering Framework for Stochastic Risk and Decision-Making  
**Programme:** Actuarial Engineering — Parallel Futures Initiative  
**Research initiator:** Harsh Vikram Arora  
**Status:** Working-paper concept and research protocol — v0.1 (12 October 2026)  
**Discussion:** https://github.com/hvikramarora/actuarial-engineering-parallel-futures/discussions/2

> **Research integrity note:** This document defines a proposed study. No experimental results, performance improvements, or empirical conclusions are claimed. The phrase *parallel futures* means alternative simulated outcomes, not verified parallel physical universes.

## Abstract

Actuarial valuation and risk management rely on stochastic projections of uncertain economic, demographic and insurance outcomes. Advances in machine learning and artificial intelligence offer opportunities to augment scenario generation, accelerate computationally intensive valuation, and support risk-based decision-making. However, their additional complexity must be justified by measurable improvements over established actuarial techniques. This working paper proposes a modular **Parallel Futures Framework** that represents uncertain conditions as coherent stochastic scenarios, applies actuarial valuation models to each scenario, and evaluates management decisions across the resulting loss distributions. It defines testable comparisons between conventional models and selected AI-assisted components, with particular attention to tail-risk fidelity, computational efficiency, calibration, auditability and decision quality. An initial reproducible case study will use synthetic general-insurance portfolio data. The intended contribution is an evaluated engineering framework and transparent benchmark methodology, not a claim that multiverse physics has been demonstrated or that AI necessarily outperforms conventional actuarial methods.

## Central research question

**Under what conditions, if any, can AI-augmented components improve the efficiency or decision usefulness of stochastic actuarial risk modelling without unacceptable losses in calibration, tail-risk accuracy, robustness or auditability?**

## Scope of the inaugural study

The first case study is a stylised **one-year general-insurance portfolio**. We will model aggregate claims under interacting uncertainties in claim frequency, claim severity, claims inflation and a common shock factor. Management decisions will be compared using the same underlying set of scenarios. Other fields—including life insurance, pensions and relativistic valuation—are prospective follow-on applications, not claims to be tested in this inaugural experiment.

## Research questions

- **RQ1 — Scenario integrity:** How well do traditional and AI-assisted approaches reproduce the target loss distribution, dependence relationships and extreme outcomes?
- **RQ2 — Computation:** Can an AI surrogate estimate expensive actuarial outputs materially faster at a prespecified error tolerance?
- **RQ3 — Decision quality:** Do AI-assisted estimates change the ranking of plausible reinsurance or capital-management decisions, and are those changes supported by out-of-sample results?
- **RQ4 — Governance:** What information must be retained for results to be reproducible, explainable and independently auditable?

## Testable hypotheses

- **H1 (computational efficiency):** A trained surrogate can reduce valuation time relative to direct Monte Carlo at comparable target accuracy on held-out scenarios. This is a *hypothesis*, not an expected finding.
- **H2 (tail-risk fidelity):** AI-assisted outputs can meet prespecified tolerances for high-quantile VaR and TVaR/Expected Shortfall relative to a high-simulation reference benchmark. Failure to meet tolerances is a valid negative result.
- **H3 (decision stability):** Decisions selected with AI-assisted estimates achieve similar or better out-of-sample objective values compared with baseline-selected decisions, accounting for estimation uncertainty.

## Initial mathematical framework

Let $s$ index a simulated possible future and $a$ denote an admissible management decision. A basic aggregate-claims model is

$$
L_s = \sum_{i=1}^{N_s} X_{i,s} I_s + C_s,
$$

where $N_s$ is claim count, $X_{i,s}$ individual claim severity, $I_s$ a claims-inflation multiplier, and $C_s$ an aggregate common-shock loss. Model parameters and dependence structures must be specified and calibrated (or, in the initial synthetic experiment, transparently generated).

A decision can transform gross losses into net losses, written $L_s(a)$; for example, an excess-of-loss reinsurance contract modifies the retained loss while adding premium expense. We then compare decisions with a prespecified objective such as

$$
J(a)=\mathbb{E}[L(a)] + \lambda\,\operatorname{TVaR}_{\alpha}(L(a)) + c(a),
$$

where $c(a)$ represents additional decision costs and $\lambda$ represents an explicit tail-risk preference. Care is required to avoid double-counting expenses already included in $L(a)$; the implemented definition will document exactly which terms are included.

For loss variable $L$, define the upper-tail conditional risk measure at level $\alpha$ using the quantile-integral definition

$$
\operatorname{TVaR}_{\alpha}(L)=\frac{1}{1-\alpha}\int_{\alpha}^{1}\operatorname{VaR}_u(L)\,du,
$$

which also accommodates distributions with atoms. The experiment will assess, for example, $\alpha=0.99$ and $0.995$ subject to adequate simulation precision.

## What AI will and will not do

**Proposed first AI experiment:** Train a supervised surrogate model to predict selected actuarial outputs (e.g., expected net loss and tail measures) from scenario/model parameters and decision inputs. Compare the surrogate against direct simulation on held-out parameter combinations. The reference approach remains conventional simulation with sufficient draws and uncertainty estimates.

**Optional later experiment:** Compare learned scenario-generation methods to conventional parametric or copula-based generators. A convincing result must demonstrate realistic dependence and tail behaviour, not just visually plausible simulated data.

**Generative-language tools:** These may help draft code, summarize evidence or explain methodology, but all mathematics, code and sourced claims must be independently reviewed. Language-model output will not be treated as an empirical result.

## Evaluation protocol

1. **Define a transparent synthetic portfolio** and parameter ranges, with fixed reproducible random seeds.
2. **Implement a conventional baseline**, including clear assumptions and a high-precision reference simulation.
3. **Separate training, validation and test configurations**, ensuring test scenarios are not reused during AI model development.
4. **Evaluate accuracy**, including expected loss error, quantile error, TVaR error, dependence sensitivity and uncertainty intervals.
5. **Evaluate runtime and resources** in a reproducible environment, counting model training and inference costs separately.
6. **Evaluate decisions out of sample**, with sensitivity analyses, stress scenarios and explicit decision criteria.
7. **Publish code, methods and limitations**; report unsuccessful results as clearly as successful ones.

## Expected research outputs

- A versioned working-paper manuscript containing literature review, equations, implementation and results.
- A baseline open-source risk model with tests and documented synthetic input data.
- A separately identifiable AI-augmented component with benchmark results.
- An interactive application for inspecting scenarios and decision outcomes, linked to the reproducible computation.
- Public discussion threads recording key methodological challenges and changes.

## Collaboration and authorship

Researchers are invited to critique the scope, propose mathematical approaches, contribute implementations and participate in manuscript development. Participation in public discussions does **not** automatically establish authorship. Authorship decisions for PF-001 will reflect substantive intellectual contributions, manuscript engagement, final approval and accountability, subject to applicable journal rules and explicit agreement among contributors. Contributions may be tracked using CRediT roles.

Please participate in the [PF-001 research discussion](https://github.com/hvikramarora/actuarial-engineering-parallel-futures/discussions/2) and describe your proposed contribution before starting substantial work.

## Immediate milestone

**Approve the research scope and benchmark design before collecting results or claiming novelty.** The literature review must establish how the framework differs from established stochastic scenario generation, actuarial simulation, surrogate modelling and AI-based decision support.
