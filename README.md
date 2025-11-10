# BDC
This is the implementation for [Boost, Disentangle, and Customize: A Robust System2-to-System1 Pipeline for Code Generation](https://arxiv.org/pdf/2502.12492?).

## System 2 Data Collection and Inference (MC-Tree-Of-Agents)
<img width="215" height="293" alt="image" src="https://github.com/user-attachments/assets/9400857e-e55f-4d44-9366-17df430c8ff9" />
<img width="286" height="163" alt="image" src="https://github.com/user-attachments/assets/99ac5b1e-9a09-4918-a550-0b14c903e90b" />


Trace collection on train set (Sampled from all the data excluding the test set.):
```bash
python collect_trace.py
```

Cd the "DataScripts" directory and run:
```bash
python process_data.py
```

Test inference methods on test set (For APPS: intro (index 4000-4100), inter (index 0-100), comp (index 3000-3100)):
```bash
python run_debate.py
```

## System 1 Tuning and Inference
<img width="352" height="286" alt="image" src="https://github.com/user-attachments/assets/d6119dcb-f9d8-40e2-a61b-625ad083934b" />

1. Cluster data obtained.
```bash
python enc_and_clustering.py
```
2. Finetuning model on full data and data clusters for "full_adpater" and "adpater_cluser_i". 
```bash
sh train_with_clusters.sh
```
3. Test for their corresponding system 1 performances.
```bash
sh test_all_cluster.sh
```

4. Run different base merge methods on {adpater_cluser_i|i=1,2,..., #clusters} to obtain the merged model, including ties, twin, and dare.
```bash
sh run_all_mergs.sh
```

5. Test for their corresponding system 1 performances.
```bash
sh test_all_merged.sh
```

6. Train the hypernetwork for routing.
```bash
python train_router.py
```

7. Load the trained router net for System 1 inference.

```bash
python load_router_for_test.py
```

If you find this repo useful, please cite the correponding paper:
```bash
@inproceedings{
anonymous2025boost,
title={Boost, Disentangle, and Customize: A Robust System2-to-System1 Pipeline for Code Generation},
author={Anonymous},
booktitle={The 63rd Annual Meeting of the Association for Computational Linguistics},
year={2025},
url={https://openreview.net/forum?id=LvqKcMtgce}
}
```
