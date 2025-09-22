
# Hardware-Aware Machine Learning for Power and Area Optimization in FIR Filters Using Booth Multiplication

This repository contains the "Verilog HDL designs, Python/Colab notebooks, and machine-learning workflow" developed for our research on energy-efficient Finite Impulse Response (FIR) filters.
The work combines "approximate computing" and "machine learning–based optimization" to reduce power and area in digital signal processing hardware.

# Overview

FIR filters are critical blocks in DSP applications such as image enhancement, audio filtering, biomedical signal analysis, and communication systems.
However, implementing FIR filters efficiently on "FPGA" and "ASIC" platforms is challenging because of tight power and area constraints.
Multiplication dominates both metrics, making multiplier design optimization a key focus.

Our solution:

* Introduce exact and approximate radix-4 modified Booth multipliers.
* Integrate machine learning regression and Bayesian optimization to explore the hardware design space automatically.
* Deliver up to 56 % area reduction and 46 % power savings for error-tolerant DSP workloads.


## Key Contributions

1. Approximate Booth Multipliers:

   * Three novel designs—**ABM-M1, ABM-M2, ABM-M3**—simplify partial product generation and accumulation.
   * Significant improvements in hardware efficiency while maintaining acceptable computational error.

2. Hardware-Aware Machine Learning:

   * Synthetic dataset generation of thousands of multiplier configurations (bit-width, radix, approximation factor).
   * **Bayesian Ridge Regression** predicts power and area with near-perfect accuracy (R² ≈ 1.0).
   * **Gaussian Mixture Models** cluster designs to reveal accuracy/efficiency trade-off families.

3. End-to-End Verification:

   * Complete **Verilog/SystemVerilog RTL** implementation.
   * Automated testbenches check functional correctness and quantify approximation error.
   * Results verified on **Intel Quartus Prime Lite** for FPGA targets.


##  Repository Structure

```
├─ notebooks/
│   └─ hardware_aware_ml_fir.ipynb   # Google Colab notebook with ML pipeline
├─ verilog/
│   ├─ ApproxBoothMultiplier.v       # Top module
│   ├─ BoothEncoder.v
│   ├─ ExactPPG.v / ApproxPPG.v
│   ├─ DaddaTree.v
│   └─ testbench.sv
├─ data/
│   └─ synthetic_dataset.csv         # Generated hardware metrics
├─ docs/
│   └─ ml_research_paper.pdf         # Full research paper
└─ README.md
```

## Methodology

* Synthetic Data Generation: Python scripts create multiplier configurations varying bit-width (8/16/32), radix (2/4/8), and approximation factor.
* Analytical Hardware Models: Formulas estimate LUTs, Flip-Flops, DSP usage, power, and area.
* Machine Learning:
  1) Supervised: Bayesian Ridge Regression and Random Forests for area/power prediction.
  2) Unsupervised: Gaussian Mixture Model + PCA for design clustering.
* Hardware Verification: Verilog/SystemVerilog RTL simulation validates accuracy vs. exact multiplication.

## How to Reproduce:

1. Clone the Repo
   ```
   git clone https://github.com/PranathiBobbireddi/fir-power-area-optimization.git
   
   
2. Run the Colab Notebook
   
    Open `notebooks/hardware_aware_ml_fir.ipynb` in [Google Colab](https://colab.research.google.com/) to regenerate the dataset and ML results.
   
4. Synthesize Verilog
   * Tool: Intel Quartus Prime Lite
   * Target: FPGA (Cyclone series or similar).
   * Compile the `ApproxBoothMultiplier.v` and run the provided testbench.

## Results

* Area Reduction: Up to 56 % vs. exact Booth multiplier.
* Power Savings: Up to 46 %.
* ML Prediction Accuracy: MAE ≈ 2.5 × 10⁻¹⁵, R² ≈ 1.0.
* Clustering: Three well-separated design families with distinct accuracy/efficiency trade-offs.

## Future Work

* Runtime-configurable dynamic approximation.
* Multi-objective optimization including timing and reliability.
* Higher-radix (≥ 8) Booth multipliers.
* Cross-platform extension to ASIC flows.

##  Citation

If you use this work, please cite:

```
@article{bobbireddi2025hardwareaware,
  title   = {Hardware-Aware Machine Learning for Power and Area Optimization in FIR Filters Using Booth Multiplication},
  author  = {Pranathi Bobbireddi and Kavya Priya Bollabathini },
  year    = {2025},
  journal = {Unpublished Research Paper}
}
```

License
This project is licensed under the MIT License. Use freely with attribution.


This README gives a **clear start-to-finish explanation** of your project so that developers, researchers, or recruiters can immediately understand your goals, methodology, and how to run the code.
