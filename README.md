# `hybrid_q_agent`: Reinforcement Learning Agent for Bomberman

An autonomous reinforcement learning agent developed for the **Bomberman RL** environment (Machine Learning Essentials, Summer Semester 2026).

**Team**: Khaleesi  
**Authors**: Mahesh Bhosle & Rajul Jain  

---

## 🚀 Key Highlights & Performance

- **Architecture**: Action-conditional Linear Q-learning ($Q(s, a) = \mathbf{w}^\top \boldsymbol{\phi}(s, a)$) evaluated over all 6 actions.
- **Representation**: 24-dimensional feature vector (23 handcrafted spatial & tactical features + 1 constant bias).
- **Learning Algorithm**: Online 4-step Temporal Difference (TD) learning with error clipping to $[-15.0, +15.0]$ and learning rate $\alpha = 0.0008$.
- **Latency**: Sub-millisecond decision time ($\approx 0.56\text{ ms}$ on single-threaded CPU), well below the tournament's 500 ms per-step limit.
- **Pure RL Decision-Making**: No hand-written heuristic overrides (`+200`, `-99999`); all actions are chosen strictly via $\arg\max_a Q(s, a)$.

### 🏆 Benchmark Results (100-Round Classic Arena)

```
==========================================================================================
  🏆 FINAL TOURNAMENT SCOREBOARD (100 Rounds Classic)
==========================================================================================
Rank  | Agent                  |   Score | Avg/Rnd |  Coins |  Kills |  Suicides |  Crates
------------------------------------------------------------------------------------------
🥇 1   | hybrid_q_agent         |     671 |    6.71 |    361 |     71 |        28 |    4219
🥈 2   | rule_based_agent       |     610 |    6.10 |    355 |     51 |        40 |    4380
🥉 3   | coin_collector_agent   |     320 |    3.20 |    170 |     30 |        90 |    3740
   4  | peaceful_agent         |       0 |    0.00 |      0 |      0 |         0 |       0
==========================================================================================
```

---

## 📁 Repository Structure

```
├── callbacks.py        # Inference pipeline, model loader, action selection (act)
├── features.py         # 24-feature extraction, danger maps, BFS pathfinding & escape search
├── train.py            # 4-step TD Q-learning updates, event detection & reward shaping
├── pretrain.py         # Ridge regression initialization on expert self-play demonstrations
├── scoreboard.py       # Automated tournament evaluation script
├── model.pt            # Final trained 24-feature champion weight vector (L2 norm = 56.58)
├── MODEL_HISTORY.md    # Full checkpoint history, ablations, and verification checksums
└── README.md           # Project documentation
```

---

## 🛠️ Requirements

- Python 3.8+
- `numpy`
- `scikit-learn==1.9.0` (for `pretrain.py`)
