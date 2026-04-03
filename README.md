[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/delauf/Pharmacokinetics-Python/blob/main/Pharmakokinetics%20(1).ipynb)
# Pharmacokinetics: Drug Concentration Modeling
A computational simulation of how drugs move through the body over time, built in Python and Google Colab.


## Overview
This project models the four core processes that govern drug behavior in the body — absorption, distribution, metabolism, and elimination (ADME) — using systems of ordinary differential equations solved numerically in Python.

The models build progressively in complexity, starting from a simple single-compartment baseline and ending in an interactive dashboard where you can select real medications and explore how their chemical and physiological properties shape their concentration-time profiles.

The metabolism component connects directly to enzyme kinetics — the same Michaelis-Menten saturation behavior that governs enzyme reactions in a test tube governs drug clearance at the whole-body level. This project extends that molecular-scale model into a full systems pharmacology framework.

---

## Models

**Model 1 — One-Compartment IV**
The simplest case. Drug is injected directly into the bloodstream and the body is treated as a single well-mixed compartment. Concentration decays exponentially. Visualized on both linear and log scale — on the log scale, first-order elimination appears as a straight line, which serves as a mathematical sanity check.

**Model 2 — One-Compartment Oral**
Adds an absorption phase. Drug must first move from the gut into the bloodstream, producing the characteristic rise-and-fall curve seen on drug packaging inserts. Identifies Cmax (peak concentration) and Tmax (time to peak), and shows how bioavailability shifts the entire profile.

**Model 3 — Two-Compartment**
Splits the body into a central compartment (blood and highly perfused organs) and a peripheral compartment (muscle, fat, slower tissues). Drug distributes between them while being eliminated from the central compartment. Produces a biphasic decay — a fast distribution phase followed by a slower terminal elimination phase — visible as two distinct slopes on the log-scale plot.

**Model 4 — Michaelis-Menten Metabolism**
Replaces linear elimination with enzyme-saturable elimination. At low drug concentrations the enzymes keep up and clearance looks first-order. At high concentrations the enzymes saturate and the drug accumulates faster than the body can clear it. This is the pharmacological mechanism behind overdose toxicity and why some drugs have dangerously nonlinear dose-response relationships.

**Model 5 — Multiple Dosing & Accumulation**
Simulates repeated dosing over time. Each dose adds to the remaining drug from the previous dose, causing accumulation until a steady-state plateau is reached after approximately 4–5 half-lives. Compares different dosing intervals and shows how they affect the degree of accumulation.

---

## Features

**Therapeutic Window Visualization**
Every plot is overlaid with the drug's minimum effective concentration (MEC) and maximum tolerated concentration (MTC), shading the sub-therapeutic, therapeutic, and toxic zones. Each dosing regimen is scored by the percentage of time spent in each zone.

**Population Variability Simulation**
Runs the model across 150 simulated patients whose PK parameters (absorption rate, elimination rate, volume of distribution, bioavailability) are drawn from realistic log-normal distributions. Displays individual patient curves, percentile bands (5th–95th, 25th–75th), population mean, and a Cmax histogram colored by therapeutic zone. This reflects how the same dose produces different outcomes in different people.

**Interactive Drug Selector Dashboard**
A dropdown-driven dashboard populated with real-world PK parameters from pharmacology literature. Select a drug and the entire five-panel dashboard updates — main concentration-time curve, log-scale view, steady-state zoom, population simulation, and Cmax distribution. Includes a custom dose slider to explore what happens when the standard dose is increased or decreased.

Drugs included:

| Drug | Class | Notable PK property |
|------|-------|-------------------|
| Ibuprofen | NSAID | Rapid absorption, short half-life |
| Caffeine | Stimulant | Near-complete bioavailability (F ≈ 1.0) |
| Amoxicillin | Antibiotic | Time-dependent efficacy — must stay above MEC |
| Warfarin | Anticoagulant | Narrow therapeutic window, ~33 hr half-life |
| Morphine | Opioid | Low oral bioavailability (30%) due to first-pass metabolism |
| Metformin | Antidiabetic | Not metabolized — excreted unchanged by kidneys |
| Phenytoin | Antiepileptic | Michaelis-Menten elimination — nonlinear at therapeutic doses |
| Vancomycin | Antibiotic (IV) | Two-compartment, renally eliminated, biphasic decay |
