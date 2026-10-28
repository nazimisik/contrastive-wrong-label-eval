# Contrastive wrong-label evaluation of LLM bearing-fault explainers


The notebooks rebuild the data from the public Paderborn and CWRU recordings, train the explainer, generate its explanations and compute the reported metrics. No data, checkpoints or model outputs are included.

## Notebooks

Run them in this order in Google Colab. Every path is under `ROOT`, set in the configuration cell of each notebook (default `/content/drive/MyDrive/bearing_protocol`).

| Notebook | What it does |
|---|---|
| `1_paderborn_prepare` | Segments, audio and spectrogram files, measured quantities, bearing-level partition, level thresholds |
| `2_paderborn_train_generate` | Training set at a given contrastive ratio, LoRA adaptation, generation for the four conditions. Set `MODEL_CHOICE`, `CONTRASTIVE_RATIO` and `SEED` |
| `3_cwru_prepare_train_generate` | The same for CWRU, including the download of the recordings and the load-based partition. Set `CONTRASTIVE_RATIO` and `SEED` |
| `4_judge_reading` | Second reading of every run with Qwen2.5-32B-Instruct |
| `5_metrics` | Arbitration balanced accuracy, evidence accuracy per condition, condition-reciting nulls, margins, bootstrap intervals, reader agreement |

Each training run writes a record to `ROOT/runs/`. Notebooks 4 and 5 read every completed run from there. Tables are written to `ROOT/tables/`.

## Data

- Paderborn: KAt-DataCenter, Paderborn University, https://mb.uni-paderborn.de/kat/forschung/kat-datacenter/bearing-datacenter (CC BY-NC 4.0). Cite Lessmeier et al., PHM Society European Conference, 2016.
- CWRU: Case Western Reserve University Bearing Data Center, https://engineering.case.edu/bearingdatacenter/download-data-file (12k drive-end fault data and normal baseline data). Notebook 3 downloads the files it needs.

## Requirements

Training the 30B model and running the 32B judge need about 80 GB of GPU memory; we used one 96 GB NVIDIA RTX PRO 6000. The install cells pin the versions used: ms-swift 4.4.2, transformers 4.57.3 and datasets 3.6.0 (transformers 4.48.3 and peft 0.13.2 for Phi-4-multimodal). Models are loaded at their default hub revision.

## License

MIT for the code. The datasets keep their own licences.
