# CRDAC: Cyber-Resilient Distributed Adaptive Control for Cooperative Vehicular Platoons

This repository provides the **self-contained reference implementation and numerical evaluation** of the **Cyber-Resilient Distributed Adaptive Control (CRDAC)** framework for cooperative vehicular platoons operating in heterogeneous traffic environments.

## Overview

CRDAC is designed to maintain tracking performance and resilience in the presence of communication delays, packet dropouts, and cyberattacks. The framework integrates:

- Delay-aware compensation
- Disturbance estimation
- Cyberattack filtering/detection
- Adaptive control-gain tuning
- Lyapunov-based stability verification

The implementation compares CRDAC with **ACC, CACC, PID, and RLCC** controllers.

## Experimental Setup

The notebook evaluates **100 heterogeneous urban traffic scenarios** with:

| Parameter | Configuration |
|---|---|
| Scenarios | 100 |
| Platoon size | 5–20 vehicles |
| Vehicle types | CAVs, HDVs, Buses, Trucks |
| Traffic density | Low / Medium / High |
| V2V standard | IEEE 802.11p |
| Communication delay | 10–250 ms |
| Mean delay | 41.51 ms |
| Packet loss | 1–20% |
| Mean PDR | 85.06% |
| Cyberattacks | DoS, Sybil, Replay, Jamming |

## Repository Contents

```text
crdac_platoon_control/
├── CRDAC_Framework_Evaluation.ipynb   # Main experimental notebook
├── CRDAC_Results_Complete.xlsx        # Generated experimental results
├── build_excel.py                     # Excel-results generation script
├── generate_notebook.py               # Notebook-generation script
└── README.md
```

## Requirements

Recommended: **Python 3.10+**

Install the main dependencies:

```bash
pip install numpy pandas matplotlib seaborn scipy openpyxl jupyter
```

## Run the Experiments

```bash
jupyter notebook CRDAC_Framework_Evaluation.ipynb
```

Execute the notebook cells sequentially. It contains the mathematical formulation, controller implementations, scenario generation, comparative evaluation, dynamic simulation, Lyapunov analysis, statistical validation, ablation study, and results export.

## Controllers

| Controller | Description |
|---|---|
| **CRDAC** | Proposed cyber-resilient distributed adaptive control |
| **ACC** | Adaptive Cruise Control |
| **CACC** | Cooperative Adaptive Cruise Control |
| **PID** | Proportional-Integral-Derivative control |
| **RLCC** | Reinforcement Learning-Based Control baseline |

## Key Results

Under the reported common network conditions (**PDR = 85.06%**, **communication delay = 41.51 ms**), CRDAC achieved:

| Metric | CRDAC |
|---|---:|
| MAE | **9.04 m** |
| RMSE | **15.84 m** |
| Maximum spacing error | **65.41 m** |
| Safety margin | **97.58%** |
| Resilience score | **0.8162** |
| Attack detection accuracy | **73.01%** |
| Energy consumption | **113.29 L** |
| Negative Lyapunov derivative | **86.40% of timesteps** |

The notebook also performs **One-Way ANOVA**, pairwise t-tests, confidence-interval analysis, Lyapunov/ISS verification, and component-level ablation analysis.

## Ablation Study

The contribution of the following CRDAC components is evaluated:

- Full CRDAC
- Without Delay Compensation
- Without Disturbance Estimation
- Without Adaptive Gain Tuning
- Without Attack Detection
- Without Lyapunov Adaptation

## Mathematical Model

Vehicle dynamics are modeled as:

$$\dot{x}_i(t)=v_i(t), \qquad \dot{v}_i(t)=u_i(t)+d_i(t)$$

The proposed control law is:

$$u_i(t)=-k_i e_i(t)-c_i(v_i(t)-v_{i-1}(t))+\hat d_i(t)$$

The Lyapunov candidate is:

$$V(e)=\frac{1}{2}\sum_{i=1}^{N}e_i^2(t)$$

The notebook evaluates the Lyapunov derivative and practical Input-to-State Stability (ISS) under bounded communication delay and packet-drop disturbances.

## Reproducibility

The implementation uses a fixed NumPy random seed (`42`) for reproducible stochastic experiments. Changing the seed may change individual simulation trajectories and scenario-level results.

## Results File

`CRDAC_Results_Complete.xlsx` contains the generated experimental results and scenario-level data used for analysis.

## Citation

If you use this implementation, please cite the associated research publication:

```bibtex
@article{more_crdac,
  title   = {A Cyber-Resilient Distributed Adaptive Control (CRDAC) Framework for Cooperative Vehicular Platoons in Heterogeneous Traffic Environments},
  author  = {More, Jyoti Sunil and Chandran, Priya and Chaudhari, Chaitrali},
  year    = {2026}
}
```

> Replace the provisional BibTeX entry with the final publication metadata after publication.

## Authors

**Jyoti Sunil More** — Department of Computer Engineering, Fr. C. Rodrigues Institute of Technology, Vashi, Navi Mumbai, India  
**Priya Chandran** — Bharati Vidyapeeth's Institute of Management and Information Technology, Navi Mumbai, India  
**Chaitrali Chaudhari** — Department of CSE AIML, Lokmanya Tilak College of Engineering, Navi Mumbai, India

## License

This repository is intended for academic and research use. Check the licensing conditions of third-party datasets and software before redistribution or commercial use.
