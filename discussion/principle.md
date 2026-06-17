You are helping me rewrite my master thesis into the first draft of an IEEE TITS journal paper.

The target paper title is:

Vehicle-Cloud Collaborative Predictive Planning and Anti-Rollover Control for Autonomous Tank Trucks

The LaTeX project has already been initialized locally. The `main.tex` file already includes the following section files:

```latex
\input{sec/sec0_abstract}

\input{sec/sec1_introduction}

\input{sec/sec2_problem_formulation}

\input{sec/sec3_cloud_predictive_planning}

\input{sec/sec4_vehicle_planning_and_control}

\input{sec/sec5_validation}

\input{sec/sec6_conclusion}

\input{sec/sec7_appendix}
```

Please generate the first journal-paper draft by reorganizing and rewriting the thesis content, not by simply translating or shortening the thesis chapter by chapter.

The central writing logic should be:

Cloud-side long-horizon predictive planning anticipates interaction-induced rollover risks, vehicle-side local planning handles abrupt local hazards, and high-frequency vehicle-side anti-rollover control guarantees stable trajectory execution for autonomous tank trucks.

The paper should read as a coherent multi-time-scale vehicle-cloud collaborative safety framework, rather than a compressed version of the whole thesis.

General rewriting principles:

1. Keep the main technical story focused on predictive planning and anti-rollover control.
2. Remove most of the architecture-modeling chapter. Do not retain the full So-MBSoSE / CT2ROP architecture derivation in the main text.
3. Keep only one system framework figure near the end of the Introduction. Use it to show cloud-side predictive planning, vehicle-side emergency planning, and vehicle-side high-frequency anti-rollover control.
4. Move detailed architecture modeling, excessive system-engineering descriptions, long derivations, and secondary implementation details to the appendix or remove them.
5. Preserve the important technical modules:

   * Graphflow / graph-diffusion interactive prediction.
   * Reinforcement-learning-based long-horizon decision-making.
   * Rollover-aware reference trajectory generation.
   * Vehicle-side emergency obstacle-avoidance trajectory replanning.
   * Coupled tanker-truck dynamics and liquid sloshing model.
   * Multi-constraint MPC for trajectory tracking, sloshing suppression, and anti-rollover control.
   * Co-simulation and scaled model truck validation.
6. Avoid dissertation-style wording such as “this thesis”, “this chapter”, “the following chapter”, “本文首先/其次/再次”. Rewrite everything in IEEE journal style.
7. Use consistent terminology:

   * vehicle-cloud collaborative predictive planning
   * cloud-side predictive planning
   * vehicle-side emergency planning
   * high-frequency anti-rollover control
   * autonomous tank truck
   * rollover-aware trajectory
   * Graphflow-based interactive prediction
   * multi-constraint MPC
8. Use `autonomous tank truck` consistently in the title and abstract, but use `tanker truck` where the context emphasizes liquid cargo dynamics if needed.
9. Do not fabricate new experimental results. Only use results that exist in the thesis. If exact numbers are not available in the source text, write qualitative descriptions or leave a clear TODO comment.

Section-by-section rewriting plan:

## sec0_abstract

Rewrite the abstract around one unified problem:

Autonomous tank trucks are prone to rollover because of high center of gravity, liquid sloshing, and interaction-induced driving risks. Existing single-vehicle methods lack long-horizon risk anticipation, while pure cloud-side planning cannot guarantee real-time stability under local emergencies. This paper proposes a vehicle-cloud collaborative predictive planning and anti-rollover control framework.

The abstract should include:

* problem background;
* proposed vehicle-cloud collaborative framework;
* cloud-side Graphflow-based prediction and decision-making;
* vehicle-side emergency planning;
* vehicle-side high-frequency multi-constraint MPC;
* validation through traffic simulation, vehicle-liquid co-simulation, and scaled model experiments;
* main results and contributions.

Keep the abstract concise, preferably 180–230 words.

## sec1_introduction

The Introduction should be rewritten as a journal-paper introduction, not copied from the dissertation.

Suggested logic:

Paragraph 1:
Introduce why autonomous tank trucks need dedicated anti-rollover planning and control. Emphasize high center of gravity, liquid sloshing, severe accident consequences, and highway operation.

Paragraph 2:
Discuss limitations of existing anti-rollover control and trajectory planning methods. They usually focus on vehicle-side control or local planning, but they lack long-horizon prediction of traffic interactions and cannot prevent risky states before they occur.

Paragraph 3:
Introduce the motivation for vehicle-cloud collaboration. The cloud side can use wide-area traffic information and parallel computation for long-horizon risk prediction and decision-making, while the vehicle side provides fast local replanning and high-frequency closed-loop stability control.

Paragraph 4:
Summarize the proposed method. Present it as a multi-time-scale framework:

* cloud-side predictive planning;
* vehicle-side emergency planning;
* high-frequency anti-rollover control.

Paragraph 5:
Add the overall framework figure near the end of the Introduction. The figure should replace the long architecture chapter. It should show information flow from cloud prediction and decision-making to vehicle-side planning and control.

Contribution bullets:
Use 3 or 4 concise contributions:

1. A vehicle-cloud collaborative predictive planning and anti-rollover control framework is proposed for autonomous tank trucks, integrating long-horizon cloud-side risk anticipation and vehicle-side real-time stability protection.

2. A Graphflow-based cloud-side predictive planning module is developed to model long-horizon stochastic interactions among surrounding vehicles and generate rollover-aware reference trajectories.

3. A vehicle-side planning and high-frequency control strategy is formulated by combining emergency trajectory replanning, coupled liquid-vehicle dynamics, and multi-constraint MPC for trajectory tracking, sloshing suppression, and rollover prevention.

4. The proposed method is validated through traffic simulation, high-fidelity vehicle-liquid co-simulation, and scaled tank-truck experiments.

The fourth contribution may be retained if the validation section is strong enough.

## sec2_problem_formulation

This section should replace the dissertation’s full architecture chapter. It should define the system boundary, variables, time scales, and optimization problem.

Suggested subsections:

```latex
\section{Problem Formulation}

\subsection{Vehicle-Cloud Collaborative Anti-Rollover Workflow}
\subsection{Tank-Truck Rollover Risk Description}
\subsection{Hierarchical Planning and Control Problem}
```

Content requirements:

1. Describe the cloud-side, vehicle-side planning, and vehicle-side control layers.
2. Define their inputs and outputs:

   * cloud input: traffic graph, road topology, surrounding vehicle states, ego state;
   * cloud output: long-horizon driving decision and rollover-aware reference trajectory;
   * vehicle planning input: cloud trajectory, local perception, ego state;
   * vehicle planning output: locally feasible emergency trajectory;
   * control input: reference trajectory and vehicle states;
   * control output: steering, braking, or other control commands.
3. Define time-scale differences:

   * cloud-side long-horizon prediction and decision-making;
   * vehicle-side short-horizon emergency planning;
   * high-frequency control.
4. Introduce rollover-related constraints, such as LTR or equivalent rollover index.
5. Present the overall objective in a compact way:
   safety, rollover stability, tracking accuracy, smoothness, and efficiency.
6. Do not include the full So-MBSoSE / CT2ROP derivation here. If some architecture content is needed, move it to `sec7_appendix`.

## sec3_cloud_predictive_planning

This should be the main cloud-side method section.

Suggested subsections:

```latex
\section{Cloud-Side Predictive Planning}

\subsection{Traffic Graph Representation}
\subsection{Graphflow-Based Interactive Prediction}
\subsection{Long-Horizon Decision-Making}
\subsection{Rollover-Aware Reference Trajectory Generation}
```

Content mapping from thesis:

* Use the thesis content on traffic graph representation.
* Use the graph-diffusion / Graphflow prediction model.
* Use the reinforcement-learning-based long-horizon decision-making model.
* Use the rollover-aware lane-change trajectory generation.

Writing requirements:

1. Explain why graph representation is used instead of BEV raster representation for cloud-side highway traffic prediction.
2. Define the traffic graph compactly.
3. Describe Graphflow as a probabilistic or generative long-horizon interactive prediction model.
4. Do not over-expand network architecture details; keep only the core encoder, temporal representation, and prediction output.
5. For RL decision-making, explain:

   * state;
   * action;
   * reward;
   * policy output;
   * how the result becomes a driving decision.
6. Emphasize that the cloud does not directly control the vehicle. It generates a predictive and rollover-aware reference trajectory.
7. Avoid excessive training details in the main text. Move detailed hyperparameters to the appendix if necessary.

## sec4_vehicle_planning_and_control

This section should combine vehicle-side local planning and high-frequency anti-rollover control.

Suggested subsections:

```latex
\section{Vehicle-Side Planning and Anti-Rollover Control}

\subsection{Vehicle-Side Emergency Trajectory Replanning}
\subsection{Coupled Tank-Truck Dynamics for Control}
\subsection{Multi-Constraint Anti-Rollover MPC}
\subsection{Real-Time Implementation}
```

Content mapping from thesis:

* Use the vehicle-side emergency obstacle-avoidance planning part from Chapter 3, but compress it.
* Use the liquid sloshing and coupled vehicle dynamics from Chapter 4.
* Use the multi-constraint MPC from Chapter 4 as the core of this section.
* Keep scaled-model and simulation results for the validation section, not here.

Writing requirements:

1. Vehicle-side emergency planning should be treated as a local safety fallback, not as an independent main contribution competing with the cloud-side planner.
2. Keep the constrained iLQR or local replanning formulation compact.
3. Explain when vehicle-side replanning is activated:

   * sudden obstacle;
   * cloud trajectory infeasible;
   * local rollover risk increases;
   * communication uncertainty or delay.
4. In the dynamics subsection, keep only the model needed by the controller:

   * articulated tank-truck states;
   * liquid sloshing equivalent dynamics;
   * additional forces and moments;
   * relation to rollover risk.
5. Move long liquid model derivations, residual RL re-linearization details, and parameter tables to the appendix if they are too long.
6. The MPC subsection should be written more carefully and in more detail:

   * objective function;
   * tracking error;
   * sloshing suppression;
   * rollover index constraint;
   * actuator constraints;
   * road-boundary or lateral deviation constraints if used;
   * steering and differential braking inputs if used;
   * soft constraints and slack variables if used.
7. Explain that the controller is the final safety layer of the vehicle-cloud system.

## sec5_validation

Combine cloud simulation, vehicle-side simulation, and scaled experiments into one validation section.

Suggested subsections:

```latex
\section{Validation}

\subsection{Cloud-Side Predictive Planning Evaluation}
\subsection{Vehicle-Side Planning and Control Evaluation}
\subsection{Scaled Tank-Truck Experimental Validation}
\subsection{Ablation and Real-Time Analysis}
```

Content mapping from thesis:

* Use Chapter 3 cloud planning simulation results.
* Use Chapter 3 vehicle-side planning simulation results.
* Use Chapter 4 vehicle-liquid co-simulation results.
* Use Chapter 4 scaled model vehicle experiments.

Writing requirements:

1. Do not simply paste all thesis plots. Select only the most convincing figures and tables.
2. Validation should answer four questions:

   * Does Graphflow improve long-horizon interaction prediction?
   * Does cloud-side predictive planning reduce dangerous interaction-induced rollover risks?
   * Does vehicle-side planning and control maintain stability under emergency maneuvers?
   * Does the method meet real-time and experimental feasibility requirements?
3. For cloud-side validation, use metrics such as:

   * prediction error;
   * safety score;
   * collision or conflict rate;
   * risky lane-change frequency;
   * maximum lateral acceleration or predicted rollover risk;
   * computation time.
4. For vehicle-side control validation, use metrics such as:

   * tracking error;
   * maximum roll angle;
   * maximum LTR or equivalent rollover index;
   * maximum lateral acceleration;
   * sloshing amplitude;
   * braking/steering smoothness;
   * solver time.
5. Include ablation studies if the thesis contains enough data. Recommended ablations:

   * without cloud prediction;
   * without rollover-aware trajectory generation;
   * without vehicle-side emergency replanning;
   * without anti-rollover MPC;
   * full proposed method.
6. If full ablation data are not available, do not invent numbers. Add TODO comments indicating which ablation tables should be completed manually.
7. Keep the validation section focused on comparison and evidence, not on platform description.

## sec6_conclusion

Write a concise journal-style conclusion.

It should include:

1. one paragraph summarizing the proposed vehicle-cloud collaborative framework;
2. one paragraph summarizing the main validation findings;
3. one short paragraph on limitations and future work.

Mention limitations carefully:

* real vehicle deployment is still needed;
* communication delay and packet loss should be further studied;
* full-scale tanker validation remains future work;
* cloud-edge deployment efficiency may need further optimization.

Do not overstate results.

## sec7_appendix

Use the appendix for content that is useful but too long for the main TITS paper.

Recommended appendix content:

1. Details of the architecture model if retained.
2. Detailed Graphflow network architecture and training hyperparameters.
3. Detailed residual reinforcement-learning re-linearization method.
4. Detailed liquid sloshing model derivation.
5. Additional vehicle parameters.
6. Additional simulation scenarios.
7. Additional experimental platform details.
8. Extra ablation or sensitivity results.

Important writing restrictions:

* Do not write the paper as a thesis summary.
* Do not preserve the original chapter order mechanically.
* Do not keep the full architecture chapter in the main text.
* Do not introduce too many unrelated acronyms.
* Do not use Chinese-style enumeration such as “firstly, secondly, thirdly” excessively.
* Do not claim full-scale deployment or real-road validation unless the thesis actually includes it.
* Do not invent quantitative results.
* Do not delete equations that are necessary for reproducibility.
* Do not over-expand derivations that distract from the vehicle-cloud collaborative planning and control story.

Final target:

Produce a coherent first draft where the reader can clearly understand:

1. why autonomous tank trucks need vehicle-cloud collaborative anti-rollover safety;
2. how cloud-side Graphflow predictive planning anticipates risk;
3. how vehicle-side planning and MPC handle local emergencies and stability;
4. how the whole system is validated through simulation and scaled experiments.
