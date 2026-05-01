# Microplastic Detection Dataset

[![DOI](https://img.shields.io/badge/DOI-10.1016%2Fj.hazadv.2025.100787-blue)](https://doi.org/10.1016/j.hazadv.2025.100787)
[![Journal](https://img.shields.io/badge/Journal-Hazardous%20Materials%20Advances-orange)](https://www.sciencedirect.com/journal/journal-of-hazardous-materials-advances)
[![License](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey)](https://creativecommons.org/licenses/by/4.0/)
[![Open Access](https://img.shields.io/badge/Open-Access-green)](https://doi.org/10.1016/j.hazadv.2025.100787)

## About

This repository contains the labeled image dataset used in the development of a **low-cost portable microplastic detection system** that integrates Nile Red fluorescence staining with **YOLOv8-based deep learning**. The dataset comprises fluorescence images of six common microplastic polymer types together with corresponding YOLO-format annotations for object detection model training and validation.

## Associated Publication

> **Rermborirak, K., Nanuan, P., Komonpan, P., & Sukpancharoen, S.** (2025). Low-cost portable microplastic detection system integrating nile red fluorescence staining with YOLOv8-based deep learning. *Journal of Hazardous Materials Advances*, *19*, 100787. https://doi.org/10.1016/j.hazadv.2025.100787

**Open Access** under Creative Commons license — freely available at [ScienceDirect](https://doi.org/10.1016/j.hazadv.2025.100787).

## Microplastic Types

The dataset includes fluorescence images of six common microplastic polymers, each stained with Nile Red dye and captured under controlled imaging conditions:

| Polymer | Full Name | Common Sources |
|---------|-----------|----------------|
| **ABS** | Acrylonitrile Butadiene Styrene | Electronics housings, automotive parts, toys (LEGO) |
| **Nylon** | Polyamide | Textiles, fishing nets, ropes, packaging films |
| **PE** | Polyethylene | Plastic bags, bottles, food packaging |
| **PET** | Polyethylene terephthalate | Beverage bottles, food containers, textiles |
| **PS** | Polystyrene | Disposable cutlery, foam packaging, insulation |
| **PVC** | Polyvinyl chloride | Pipes, cables, flooring, medical tubing |

## Repository Structure

```
dataset_microplastic/
├── ABS.zip                                      # ABS image batch
├── Nylon.zip, Nylon (2).zip ... Nylon (8).zip   # Nylon image batches (8 sets)
├── PE.zip, PE (2).zip ... PE (6).zip            # PE image batches (6 sets)
├── PET.zip, PET (2).zip, PET (3).zip            # PET image batches (3 sets)
├── PS.zip, PS (2).zip                           # PS image batches (2 sets)
├── PVC.zip, PVC (2).zip ... PVC (6).zip         # PVC image batches (6 sets)
├── Alldataset_annotation.zip                    # YOLO-format annotations (combined)
├── Annotation folder.PNG                        # Reference: annotation folder structure
├── Dataset folder.PNG                           # Reference: dataset folder structure
└── README.md                                    # This file
```

Each `.zip` archive contains a batch of fluorescence images of the corresponding polymer type. Multiple zip files per polymer reflect data collection across different sampling sessions, particle sizes, and/or imaging conditions to ensure dataset diversity for robust YOLOv8 model training.

The **Alldataset_annotation.zip** file contains the consolidated YOLO-format label files (`.txt`) corresponding to each image, with bounding box coordinates and class labels for all six polymer classes. The two **PNG screenshots** illustrate the expected folder organization to facilitate reproduction of the training pipeline.

## Usage

### Download

To download the entire dataset:

```bash
git clone https://github.com/sombsuk/dataset_microplastic.git
cd dataset_microplastic
```

Or download individual zip files directly from the GitHub web interface.

### Extract

```bash
# Extract all zip files at once (Linux/macOS)
for f in *.zip; do unzip "$f" -d "${f%.zip}"; done

# Or extract individually
unzip "PE.zip" -d PE/
unzip "Alldataset_annotation.zip" -d annotations/
```

### Recommended Workflow for YOLOv8 Training

1. Extract all polymer image archives into class-named folders (`ABS/`, `Nylon/`, `PE/`, `PET/`, `PS/`, `PVC/`).
2. Extract `Alldataset_annotation.zip` to obtain matching `.txt` annotation files in YOLO format.
3. Refer to `Dataset folder.PNG` and `Annotation folder.PNG` for the expected directory layout.
4. Configure your YOLOv8 `data.yaml` file with the six classes:
   ```yaml
   names:
     0: ABS
     1: Nylon
     2: PE
     3: PET
     4: PS
     5: PVC
   nc: 6
   ```
5. Train using the [Ultralytics YOLOv8](https://github.com/ultralytics/ultralytics) framework as described in the associated publication.

### Citation

If you use this dataset in your research, please cite the associated publication:

**BibTeX:**
```bibtex
@article{Rermborirak2025microplastic,
  title   = {Low-cost portable microplastic detection system integrating nile red fluorescence staining with YOLOv8-based deep learning},
  author  = {Rermborirak, Kittanon and Nanuan, Phutawan and Komonpan, Pattarapon and Sukpancharoen, Somboon},
  journal = {Journal of Hazardous Materials Advances},
  volume  = {19},
  pages   = {100787},
  year    = {2025},
  doi     = {10.1016/j.hazadv.2025.100787},
  url     = {https://doi.org/10.1016/j.hazadv.2025.100787}
}
```

## Acknowledgements

This work was conducted at the **Faculty of Engineering, Khon Kaen University**, Thailand, by:

- **Program of Automation Robotics and Intelligent System Engineering** (K. Rermborirak, P. Nanuan, P. Komonpan)
- **Department of Agricultural Engineering** (S. Sukpancharoen, corresponding author)

## License

This dataset is released under the **Creative Commons Attribution 4.0 International (CC BY 4.0)** license, consistent with the open-access publication. You are free to share and adapt the material for any purpose, provided appropriate attribution is given.

## Contact

For questions, collaborations, or technical inquiries regarding the dataset:

**Assoc. Prof. Somboon Sukpancharoen, Ph.D.**
Department of Agricultural Engineering, Faculty of Engineering
Khon Kaen University, Khon Kaen 40002, Thailand
📧 sombsuk@kku.ac.th
