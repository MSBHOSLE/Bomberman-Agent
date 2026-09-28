# Bomberman RL — Full Model History & Checkpoints

This document provides a permanent record of all trained model checkpoints, their mathematical specifications, training stages, and benchmark results.

---

## ⚠️ The Golden Rule

> **Only one model file is actively loaded by the game:**  
> **`agent_code/hybrid_q_agent/model.pt`**  
> All other files are historical checkpoint snapshots preserved for reproducibility and academic evaluation.

---

## 1. Full Model History & Checkpoints Table

| Model File | Dimensions | Weight Norm | Trained / Created | Role & Performance Notes |
| :--- | :---: | :---: | :---: | :--- |
| **`model.pt`** *(Active)* | **(24,)** | **56.5841** | Sep 4, 19:05 | 🥇 **FINAL CHAMPION**: 671 pts / 71 kills in 100 rounds. |
| **`model_champion_24feat_663.pt`** | **(24,)** | **56.5841** | Sep 4, 19:05 | Permanent safety backup of the 24-feature champion. |
| **`model_18_backup.pt`** | (18,) | 52.0622 | Sep 2, 18:08 | Backup of the previous 18-feature model. |
| **`model_clean_1200_504.pt`** | (18,) | 52.0622 | Sep 2, 18:08 | Model checkpoint at the 1,200-round curriculum horizon. |
| **`model_champion_610.pt`** | (18,) | 51.1906 | Sep 2, 17:05 | Best 18-feature model (scored 610 pts in 100 rounds). |
| **`model_champion_610_clean_baseline.pt`** | (18,) | 51.1906 | Sep 2, 17:38 | Clean baseline freeze of the 610-point model. |
| **`model_best_559.pt`** | (18,) | 51.1906 | Sep 2, 14:35 | Early high-performing checkpoint (559 pts). |
| **`model_stable_607.pt`** | (18,) | 51.1906 | Sep 2, 19:25 | Stabilized checkpoint from exploration tuning. |
| **`model_crate_boost.pt`** | (18,) | 53.2429 | Sep 2, 18:10 | Checkpoint after testing boosted crate-clearing rewards. |
| **`model_test_safe.pt`** | (18,) | 56.9687 | Sep 2, 17:42 | Checkpoint from escape safety testing. |
| **`model_after_bad_curriculum.pt`** | (18,) | 55.6427 | Sep 2, 17:02 | Experimental run where overtraining hurt coin navigation. |
| **`model_learned_379.pt`** | (18,) | 7.6907 | Sep 2, 16:17 | Intermediate checkpoint early in reinforcement learning. |
| **`model_before_curriculum.pt`** | (18,) | 7.6907 | Sep 2, 16:15 | Pure imitation baseline (Ridge regression before RL). |
| **`model_old_hardcoded.pt`** | (18,) | 50.3655 | Sep 2, 15:45 | Initial prototype weights before curriculum optimization. |
| **`tabular_q_agent/model.pt`** | Q-table | N/A | Sep 2, 00:11 | Baseline Tabular Q-agent (288 KB, state space explosion). |

---

## 2. Active Champion Verification & Checksums

- **File**: `agent_code/hybrid_q_agent/model.pt`
- **File Size**: 267 Bytes
- **Weight Vector**: $\mathbf{w} \in \mathbb{R}^{24}$
- **Weight L2 Norm**: $\|\mathbf{w}\|_2 = 56.5841$
- **MD5 Hash**: `1a313e195c416527c026e447c2bbae25`
- **Submission ZIP**: `final-project-agent-code.zip` (MD5: `9e79b07f4d3abbb098bbb6b58887ba2f`)

---

## 3. Official Tournament Benchmark Performance

### 100-Round Official Arena Benchmark (`scoreboard.py 100`)
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

### 200-Round Endurance Arena Benchmark (`scoreboard.py 200`)
```
==========================================================================================
  🏆 FINAL TOURNAMENT SCOREBOARD (200 Rounds Classic)
==========================================================================================
Rank  | Agent                  |   Score | Avg/Rnd |  Coins |  Kills |  Suicides |  Crates
------------------------------------------------------------------------------------------
🥇 1   | hybrid_q_agent         |    1324 |    6.62 |    712 |    132 |        58 |    8401
🥈 2   | rule_based_agent       |    1117 |    5.58 |    690 |     95 |        82 |    8610
🥉 3   | coin_collector_agent   |     640 |    3.20 |    340 |     60 |       180 |    7480
   4  | peaceful_agent         |       0 |    0.00 |      0 |      0 |         0 |       0
==========================================================================================
```

---

## 4. How to Restore Any Checkpoint (If Needed)

To activate any of the historical checkpoints for testing, simply copy it over `model.pt`:

```bash
# Example: Restore the best 18-feature model (610 pts)
cp agent_code/hybrid_q_agent/model_champion_610.pt agent_code/hybrid_q_agent/model.pt

# Restore the 24-feature champion (671 pts)
cp agent_code/hybrid_q_agent/model_champion_24feat_663.pt agent_code/hybrid_q_agent/model.pt
```
