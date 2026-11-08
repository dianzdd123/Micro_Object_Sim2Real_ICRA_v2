# Reusing Micro_Object_Sim2Real_ICRA_v2

Physics-informed microscopy rendering, translation and pose estimation.

**Current scope:** Multi-stage research workflow; external microscopy data and experiment-specific paths are required.

This repository is a fork of [Zongcai23/Micro_Object_Sim2Real_ICRA_v2](https://github.com/Zongcai23/Micro_Object_Sim2Real_ICRA_v2). Original authorship, citations and upstream notices are retained. Changes here apply to this fork.

## Environment

```bash
conda env create -f environment.yml
conda activate pytorch-CycleGAN-and-pix2pix
python scripts/check_repository.py
```

The environment file is the starting point for the supplied GAN code. The rendering notebook also uses a GPU-oriented numerical stack; inspect its imports and CUDA requirements separately. The paper's recorded hardware/software configuration and this environment file serve different purposes and should not be treated as an identical lockfile.

## Workflow and contracts

| Stage | Entry point | Inputs → outputs |
|---|---|---|
| Rendering | `rendering_imge_generate.ipynb` | CAD/depth information and microscope parameters → rendered image stack |
| Pairing | `Processing_image.ipynb` | Real/rendered sequences and kinematics → aligned paired images and pose subsets |
| Translation | `train.py`, `test.py` | Paired image dataset and model options → checkpoints and translated images |
| Pose baseline | `Pose_Model_Train.py` | Pose-labelled image folders → pitch/roll model results |
| Hybrid datasets | `create_hybrid_data.py` | Experimental/generated images → class-balanced mixture folders |
| Hybrid training | `Pose_model_Train_Hybrid.py` | Mixtures → pose model evaluation |

Run commands from the repository root. Replace `./xxx/`, `./Lan_Data/` and checkpoint paths before execution. Match the `Pxx_Ryy` label convention, image direction (`AtoB`/`BtoA`), colour channels and spatial resolution across preparation, translation and evaluation. Reuse the same label mapping when comparing pose models.

## Small first experiment

Prepare a small, separate paired dataset before running the README's full training commands. Reduce the batch size to fit your GPU. Inspect generated images and parsed pose labels before training the full dataset. `train.py --help` is useful only after its imports/dependencies are installed; the structural check is the dependency-free inspection route.

Keep outputs outside the raw-data folders. Record the sampled image IDs, split rules, rendering parameters, random seeds, GAN checkpoint and pose model together. Split related experimental sequences before augmentation to avoid evaluating on near-duplicates of training data.

## Limits

The repository contains two notebooks, code, figures and papers; it does not include the complete experimental dataset. Syntax and notebook JSON validation do not execute notebook cells, verify optics or reproduce reported metrics. External pix2pix/CycleGAN components retain their original attribution and terms.

## Attribution and reuse permissions

No repository-wide licence file is included in this checkout. Confirm reuse and redistribution permissions with the relevant rights holders; this maintenance update does not add a licence or relicense upstream code, data or assets.

## Contributing

See [CONTRIBUTING.md](../CONTRIBUTING.md) for the local workflow and what to include with a proposed change.
