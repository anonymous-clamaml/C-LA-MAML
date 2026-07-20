
This repository contains the code to reproduce results in supplementary material for **COnstrainedLAMAML** (Constrained Language-adapted Model-Agnostic Meta-Learning).

## 1. Installation

Refer to the requirements.txt file to install dependencies.

---


## 2. Train Models

> **Note:** We do not provide any pre-trained models due to space constraints. In order to run the experiments, **explicit training is required for all the models** before running the evaluation scripts.

> **Note:** Due to variations in hardware configurations training models from scratch on different systems may produce different results

*(The commands below use the `PickupDist` environment as a specific example, but models can be trained on **any of the environments as mentioned in the paper** by changing the `--env` parameter and its parameters such as room-size, num-dists, num-constraints and others)*

**Train C-LA-MAML Model:**
```bash
python train_language.py --env PickupDist --room-size 8 --num-dists 2 --max-steps 500 --delta-g 0.5 --delta-c 0.3 --num-constraints 1
```

**Train CRL Policy:**
```bash
python train_crl.py --env PickupDist --room-size 8 --num-dists 2 --max-steps 500
```

---


## 3. Evaluate Models & Reproduce Results

Once all the respective models are completely trained, use the scripts below to evaluate them.

### 3.1 Main Evaluation

*(Note: The generated results will be logged and appended to `evaluation_results.xlsx`.)*

```bash
# Evaluate for PickupDist on any new configuration, say room-size=8, num-dists=2
python evaluate.py --env PickupDist --room-size 8 --num-dists 2 --max-steps 500 --delta-g 0.5 --delta-c 0.3
```

### 3.2 Ablation 1 (Analyze C-LA-MAML individual components comparison)

Evaluate the ablation using the following testing script.

*(Note: The generated results will be logged and appended to `ablation_results.xlsx`.)*

```bash
python ablation.py --env PickupDist --room-size 8 --num-dists 2 --max-steps 500
```

### 3.3 Ablation 2 (Compare C-LA-MAML vs. Neural Network based adaptation)

> **Note:** For this comparison script to work, a separate training is required for Neural Network method using:

**Train Neural Netowrk based Policy:**
```bash
python train_language_nn.py --env PickupDist --room-size 8 --num-dists 2 --max-steps 500
```

To compare the trained C-LA-MAML policy against the Neural Netowrk based adaptation, run the comparison script:

*(Note: The generated results will be logged and appended to `ablation_nn_results.xlsx`.)*

**Example Command:**
```bash
python evaluate_ablation_nn.py --env PickupDist --room-size 8 --num-dists 2 --max-steps 500 --delta-g 0.5 --delta-c 0.3
```
