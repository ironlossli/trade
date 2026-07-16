# UniMol Source-Conditioned Baseline Package

本仓库保存 UniMol source-conditioned one-step edit 对照实验的源码迁移包。

## 下载与解包

```bash
cd source_conditioned_baselines_20260716
cat source_conditioned_baselines_20260716.tar.gz.part-* > source_conditioned_baselines_20260716.tar.gz
sha256sum -c archive.SHA256SUMS
tar -xzf source_conditioned_baselines_20260716.tar.gz
cd source_conditioned_baselines_20260716
```

包内包含：

- UniMol one-step GINE edit model、数据接口和训练/推理代码；
- GINE-edit-lite、MEGAN-style、MoLeR-style、Omni-style、MECo-style 的协议适配器；
- Graph2Edits、MEGAN、MoLeR 的源码骨架和许可证；
- FG100 drug-like vocab、14-task 配置、环境文件和中文复现说明；
- 已完成 GINE/MEGAN/MoLeR 对照的 task-level 结果摘要。

包内不包含训练数据、checkpoint、日志、缓存或嵌套 Git 仓库。请在目标机器上单独准备数据和当前 full-model checkpoint。

## 统一训练入口

```bash
python scripts/run_source_conditioned_baselines.py \
  --train_csv data/one_step_5prop_scaffold_split/train.csv \
  --eval_csv data/one_step_5prop_scaffold_split/test.csv \
  --current_checkpoint /path/to/full_model.pt \
  --current_config experiments/rawbase_5prop_14task_editcap_balanced/h256_bs64_seed43_8ep_onestep_5prop_C_dual_decoder_fg100.yaml \
  --device cuda:0 --candidate_k 20 --gine_epochs 2 --sequence_epochs 2 --omni_epochs 2
```

完整协议和方法边界见包内 `README_ZH.md` 与 `docs/SOURCE_CONDITIONED_ONE_STEP_BASELINES_20260715_ZH.md`。

## 注意

Graph2Edits 的现有结果是 task-small 外部 control；MEGAN/MoLeR 是针对本项目 FG100 one-step 数据接口编写的 style adapter；Omni 和 MECo 的当前迁移包保存代码，但上一轮 Omni 完整候选评估尚未落盘，MECo 尚未完成本轮 test。
