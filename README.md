# Multi-Teacher-Tree-Alignment

## Environment Setup
Two sets of environments are used, with one for basic merging methods and the other for our routing training/inference. We offer the packed environments here.
- merge_env
- mcts_tune

## System 2 Data Collection and Inference
Trace collection on train set:
```bash
python collect_trace.py
```

Cd the "DataScripts" directory and run:
```bash
python process_data.py
```

Test inference methods on test set:
```bash
python run_debate.py
```

## System 1 Tuning and Inference
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
