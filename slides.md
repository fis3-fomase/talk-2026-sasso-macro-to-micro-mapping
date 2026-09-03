---
# try also 'default' to start simple
theme: default
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
#background: /imgs/banner2026.png # https://cover.sli.dev
# some information about your slides (markdown enabled)
layout: cover
title: "Macro-to-micro behavioural mappings in distributed systems: a characterisation on event structures"
# info provides ..
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# apply UnoCSS classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable Comark Syntax: https://comark.dev/syntax/markdown
comark: true
# duration of the presentation
duration: 5min

---

<style>
#slidev-goto-dialog {
  display: none !important;
  visibility: hidden !important;
  pointer-events: none !important;
}
</style>

# Macro-to-micro behavioural mappings in distributed systems
## A characterisation on event structures

---
layout: image-right
image: public/imgs/collective.png
backgroundSize: 75% 80%
---

<div class="h-110 grid content-evenly"><div>

# Context

- Collective adaptive systems
- Programming paradigms

</div><div>

# Goal

- Common, unified framework
- Simpler share of ideas

</div></div>

---
layout: two-cols-header
---

# Examples

<div class="grid grid-cols-2 gap-8 my-6 pt-5">

<div class="min-w-0 w-full pr-3 overflow-auto space-y-0">

## Aggregate computing

```java
def distanceTo(s) {
  rep(∞) {
    (dist) => mux(s, 0, minHood(nbr{dist} + nbrRange()))
  }
}
```


- Program into common instructions
- Abstract concept of field

</div>

<div class="min-w-0 w-full pr-3 overflow-auto space-y-0">

## Choreography

```java

C = if p.c == x
    then (p → r[L]; p.c → r; 0)
    else (p → r[R]; r.c → p; 0)

```


- Program into device-specific instructions
- Explicit concept of message / interaction

</div>

</div>

<div class="text-center pt-3">

Two formalisms to express the behavior of collective systems that are not mutually intelligible.

</div>

---

# A unifying framework

<div class="h-100 flex flex-col justify-center">

To capture and describe:

- Expected scenarios --- _macro-input_
- Desired outcomes --- _macro-output_ and _effect_
- Deployment process --- _macro-program_ to device _policy_
- Adaptation process --- _policy_ evolution over time

</div>

<!--
1. Macro-input ✅
2. Macro-output ✅
5. Macro-programming goal ~

1. Macro-to-Micro localization process ✅
2. Time slice ❎
3. Compatibility conditions ✅
4. Local information space ❎ -->

---
layout: image-right
image: public/imgs/event_structure.png
backgroundSize: contain
---

# Event structure

<div class="h-100 w-100 flex flex-col justify-center">

- Captures the execution of a collective system
- Express execution in function of events (_sense_, _compute_, _(inter)act_)

</div>

---

# Expected scenarios --- _macro-input_

<div class="h-100 flex flex-col justify-center">

The initial conditions that affect the system dynamics:

- environmental state
- initial computation (i.e., events at $t_0$)
- network topology

</div>

---

# Desired outcomes --- _macro-output_ and _effect_

<div class="h-100 flex flex-col justify-center">

Macro-output: result of the collective computation --- $\;\epsilon \in E_{T_\mathit{end}}$

Macro-effect: changes on the environment caused by the system execution

</div>

---

# Macro-programming goal

<div class="h-100 flex flex-col justify-center">

- Compute the _macro-output_ or cause the _macro-effect_ starting from a _macro-input_
- Map different (space-time) situations to specific behavioral policies: $\Theta: X \times T \rightarrow \mathcal{M}$

</div>

---
layout: image-right
image: public/imgs/deployment.png
backgroundSize: 80% 60%
---

<div class="w-200">

# Localization process & compatibility condition

</div>

<div class="h-100 flex flex-col justify-center">

- Map devices to policies $\;\;\Phi: \Delta \to M$
- Depend on device capabilities and program requirements $\;\;\mathit{cap}(\delta) \models \mathit{req}(\mu)$
$\;\;\Longleftrightarrow\;\; \mathit{req}(\mu) \subseteq \mathit{cap}(\delta)$
</div>

---

# Characterization of macro-programs

<div class="h-100 flex flex-col justify-center">

<!-- - _static_: $\forall \delta \in \Delta, \enspace \forall\,t, t+1 \in T, \enspace \mu^\delta_t = \mu^\delta_{t+1} \enspace$
- _dynamic_: $\exists\, \delta \in \Delta \; \land \;\,t, t+1 \in T \enspace | \enspace \mu^\delta_t \not= \mu^\delta_{t+1}$
- _homogeneous_: $\forall\,\delta, \delta' \in \Delta, \enspace \mu^\delta = \mu^{\delta'}$
- _heterogeneous_: $\exists\,\delta, \delta' \in \Delta \enspace | \enspace \mu^\delta \not= \mu^{\delta'}$ -->

<!-- - sta-hom: $\forall\,\delta, \delta' \in \Delta \land \forall\,t,t' \in T, \; \mu^\delta_t = \mu^{\delta'}_{t'}$
- sta-het: $\forall\,t,t' \in T, \; \exists\,\delta, \delta' \in \Delta | \mu^\delta_t = \mu^{\delta}_{t'} \land  \mu^\delta_t \not= \mu^{\delta'}_{t}$
- dyn-hom: $\mu $
- dyn-het: $\mu $ -->

According to time:
- _static_: the policy of each device remains the same over time
- _dynamic_: the policy of at least one device changes during execution

According to the collective:
- _homogeneous_: all devices share, at any moment, the same policy
- _heterogeneous_: at least two devices employ, at any moment in time, different policies

</div>

---

# Results

<div class="grid grid-cols-2 gap-8 my-6 pt-5">

<div class="min-w-0 w-full pr-3 overflow-auto space-y-0">

## Aggregate computing

```java
def distanceTo(s) {
  rep(∞) {
    (dist) => mux(s, 0, minHood(nbr{dist} + nbrRange()))
  }
}
```


- _Homogeneous_ localization
- Empty requirement and capability sets<br/>&nbsp;
- Events capture field-based computation

</div>

<div class="min-w-0 w-full pr-3 overflow-auto space-y-0">

## Choreography

```java

C = if p.c == x
    then (p → r[L]; p.c → r; 0)
    else (p → r[R]; r.c → p; 0)

```


- _Heterogeneous_ localization
- Requirement and capability sets associated with device type / role
- Events capture message-based computation

</div>

</div>

---

# Results

<div class="h-100 w-full flex flex-col justify-center">

- Unified interpretation of different paradigms
- Possibility to propose approach-agnostic solutions
- Simplified sharing of ideas

</div>

---

# Future works

<div class="h-100 w-full flex flex-col justify-center">

- Further elaborate the mapping mechanism
- Further elaborate dynamic macro-programming and related techniques

</div>
