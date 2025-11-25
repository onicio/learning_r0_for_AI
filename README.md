# Learning R₀ for AI
prototype for a Learning R0 dashboard

Learning R₀ for AI: Network‑driven strategies to advance women upskilling in health workplaces

This repository contains a browser‑based prototype of the Learning Epidemiology Platform, a visual sandbox for modeling how AI skills diffuse through health and public health workplaces—especially among women in tribal, rural, and county settings.  ￼

The prototype treats AI upskilling like an epidemic: each worker is a node in a collaboration network, and “learning AI” spreads through that network according to SEIR‑style dynamics and equity‑sensitive rules.

The project is linked to work at the Mel & Enid Zuckerman College of Public Health (MEZCOPH), University of Arizona, on AI workforce development, digital epidemiology, and equity in Native, rural, and county health workplaces.

Core ideas
	•	AI as diffusion, not one‑off training
Instead of assuming AI skills spread evenly through org charts, the platform models diffusion across real‑world collaboration networks (who actually talks to whom, mentors whom, and shares knowledge with whom).
	•	Learning R₀ for AI
We borrow concepts from infectious disease epidemiology (e.g., R₀, SEIR models) to define and visualize how many additional staff a trained person tends to influence.
	•	Equity front and center
The prototype is designed with women in public health and healthcare workplaces in mind, especially Native American, rural, and county health workers who are often last to be trained and first to bear new burdens.
	•	Graph Neural Networks (GNNs) as “network microscopes”
A toy GNN layer illustrates how more advanced models can combine network structure and demographics to prioritize peer champions and identify high‑risk (left‑behind) workers.

What’s in the web app?

The prototype is a single‑page HTML app (pure HTML/CSS/JS) with four main views:

1. SEIR Model (Learning as an epidemic)
	•	Interactive sliders for β (exposure), σ (incubation), and γ (recovery).
	•	Conceptual Learning R₀ slider for communicating how many additional staff each “infectious learner” tends to influence.
	•	A Chart.js time series showing the number of workers in each SEIR state over simulation steps:
	•	S (Susceptible): not yet reached by AI training
	•	E (Exposed): aware of AI / signed up / curious
	•	I (Infected): actively learning and sharing AI practices
	•	R (Recovered): proficient / saturated / no longer spreading learning
	•	Summary metrics for:
	•	Counts of S, E, I, R
	•	Gender‑disaggregated proficiency (women vs men)
	•	Rural, tribal, and urban coverage

These metrics are derived directly from the network‑level simulation, not from a separate toy model.

⸻

2. Network Analysis (SNA + SEIR on a graph)
	•	A synthetic collaboration network of ~100 workers generated in‑browser.
	•	Nodes:
	•	Color = current SEIR learning state
	•	S = green, E = orange, I = red, R = blue
	•	Size = influence score
	•	Border + dashed outline = women
	•	Links represent collaboration/mentoring ties, laid out via D3 force‑directed layout.
	•	SEIR dynamics live on the network:
	•	Each simulation step updates node states based on neighbors and β/σ/γ.
	•	Play / Pause / Step controls drive the simulation through time.
	•	The SEIR chart and node colors stay in sync.
	•	Filters:
	•	Filter nodes by gender (all / female / male)
	•	Filter by location (all / urban / rural / tribal)
	•	Filter by state (S / E / I / R)
	•	Links are hidden if either endpoint is filtered out, making it easier to focus on (for example) rural women in Exposed or Infected states.
	•	Clickable nodes:
	•	Clicking a node opens an info box summarizing:
	•	Gender, location, role
	•	Current learning state (with interpretation)
	•	Degree / neighbors
	•	Synthetic centrality and influence scores
	•	The info box also highlights why certain nodes are strong peer champion candidates (e.g., women in rural/tribal settings with high influence).
	•	Network‑level metrics (currently synthetic placeholders for demonstration):
	•	Density
	•	Average clustering
	•	Average path length
	•	Top “key influencers” by influence score
	•	Counts of isolated nodes by gender and location

⸻

3. GNN Predictions (toy graph neural network layer)

This tab sketches how a graph neural network might be used in a full implementation:
	•	Layered explanation of a 4‑layer GNN:
	1.	Node feature encoding (gender, location, state, degree → embedding)
	2.	Graph convolution (neighbor aggregation)
	3.	Attention over relationship types (mentor vs peer vs supervisor)
	4.	Classification (predict S/E/I/R probabilities)
	•	A bar chart showing synthetic GNN performance vs actual transitions for:
	•	S→E, E→I, I→R, and “Stay”
	•	A list of “high‑risk” individuals (nodes with low centrality that remain Susceptible), useful for targeting outreach.

This is illustrative only: real training, validation, and fairness auditing would happen in a full backend pipeline, not in the browser.

⸻

4. Interventions (counterfactual scenarios)

A simple radar chart compares three synthetic intervention strategies:
	1.	Peer Champions: train high‑centrality women as AI champions.
	2.	Bridge Training: target structural bridges that connect otherwise separate clusters.
	3.	Micro‑Cohorts: small learning cohorts based on observed collaboration patterns.

Each intervention is summarized in terms of:
	•	Learning R₀
	•	Gender equity
	•	Rural and tribal reach
	•	Speed of diffusion
	•	Sustainability

Buttons pop up short interpretive summaries; in a full implementation these would trigger new simulations and update the network and SEIR views.

⸻

Tech stack

Everything runs entirely in the browser:
	•	HTML5 + CSS3 (no framework, single file)
	•	JavaScript (vanilla, no build step)
	•	Chart.js for charts
	•	D3.js for the network visualization and force layout

No backend, database, or build tools are required.
