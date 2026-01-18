# Tree Detection with Faster R-CNN on SelvaBox Dataset

This project experiments with Faster R-CNN models for tree detection using the [SelvaBox dataset](https://huggingface.co/datasets/CanopyRS/SelvaBox) from HuggingFace. The project explores different training strategies including baseline models, larger input sizes, and multi-resolution augmentation techniques.

## 📊 Dataset

The [SelvaBox dataset](https://huggingface.co/datasets/CanopyRS/SelvaBox) contains high-resolution aerial imagery for tree detection. The dataset is particularly challenging due to:
- Very high resolution images
- Dense tree coverage
- Varying tree sizes (small, medium, large)
- Complex forest canopy structures

## 🎯 Project Overview

This project consists of 6 Jupyter notebooks that progressively explore different approaches:

1. **`01_download_data.ipynb`** - Downloads the SelvaBox dataset from HuggingFace and saves it to disk
2. **`02_explore_the_data.ipynb`** - Loads and explores the dataset with visualizations and statistics
3. **`03_faster_r_cnn_baseline.ipynb`** - Vanilla Faster R-CNN implementation with custom PyTorch dataset (baseline)
4. **`04_faster_r_cnn_larger_input_size.ipynb`** - Faster R-CNN with larger input size to capture more context from high-resolution images
5. **`05_faster_r_cnn_with_multi_res.ipynb`** - Advanced multi-resolution data augmentation pipeline (see [augmentation diagram](figures/))
6. **`06_deepforest_pretrained.ipynb`** - DeepForest pre-trained model for tree detection (inference only)

All notebooks are self-contained and include "Open in Colab" buttons for easy execution.

## 🚀 Getting Started

### Option 1: Google Colab (Recommended for Training)

1. Open any notebook and click the "Open in Colab" button
2. Select GPU runtime (A100 recommended for faster training)
3. For faster data loading, download the dataset once using `01_download_data.ipynb` and save to Google Drive
4. Run the notebook cells sequentially

### Option 2: Local Environment with UV

Install dependencies using [uv](https://github.com/astral-sh/uv) package manager:

```bash
# Install uv (if not already installed)
curl -LsSf https://astral.sh/uv/install.sh | sh

# Create virtual environment and install dependencies
uv sync

# Activate the environment
source .venv/bin/activate  # On Linux/Mac
.venv\Scripts\activate     # On Windows

# Run Jupyter
jupyter notebook
```

**Note:** Local training will be significantly slower on consumer GPUs (e.g., RTX 3070) compared to Google Colab's A100.

## 📦 Dependencies

Key dependencies include:
- **PyTorch** (with CUDA 12.8 support)
- **torchvision** - For Faster R-CNN implementation
- **torchmetrics** - For evaluation metrics
- **datasets** - HuggingFace datasets library
- **deepforest** - Pre-trained tree detection model
- **wandb** - Experiment tracking
- **plotly** - Interactive visualizations

See [pyproject.toml](pyproject.toml) for the complete list.

## 📈 Results

[![W&B Report](https://img.shields.io/badge/W%26B-Report-yellow)](https://api.wandb.ai/links/warwick-team/luj6fg44)

📊 **[View Interactive W&B Report](https://api.wandb.ai/links/warwick-team/luj6fg44)** for detailed training metrics, visualizations, and experiment comparisons.

### Model Performance Comparison

| Metric                  | Vanilla Faster R-CNN | Larger Input Size | Multi-Resolution | DeepForest Pretrained | Best Model        |
|-------------------------|---------------------|-------------------|------------------|-----------------------|-------------------|
| mAP (IoU=0.50:0.95)     | 0.0962              | 0.1353            | **0.1494**       | 0.0431                | Multi-Resolution  |
| mAP (IoU=0.50)          | 0.2206              | 0.2786            | **0.4084**       | 0.1472                | Multi-Resolution  |
| mAP (IoU=0.75)          | 0.0700              | 0.1203            | **0.1265**       | 0.0104                | Multi-Resolution  |
| mAP (large)             | 0.1347              | 0.1778            | **0.2378**       | 0.0657                | Multi-Resolution  |
| mAP (medium)            | 0.0318              | 0.0642            | **0.0808**       | 0.0093                | Multi-Resolution  |
| mAP (small)             | **0.0040**          | 0.0002            | 0.0011           | 0.0000                | Vanilla           |
| mAP (per class)         | 0.0962              | 0.1353            | **0.1494**       | 0.0431                | Multi-Resolution  |
| MAR@1                   | 0.0054              | **0.0061**        | 0.0060           | 0.0032                | Larger Input Size |
| MAR@100                 | 0.1613              | 0.2051            | **0.2199**       | 0.0837                | Multi-Resolution  |
| MAR@100 (per class)     | 0.1613              | 0.2051            | -                | 0.0837                | Larger Input Size |
| MAR@400                 | -                   | -                 | **0.3031**       | -                     | Multi-Resolution  |
| MAR@400 (per class)     | -                   | -                 | **0.3031**       | -                     | Multi-Resolution  |
| MAR (large)             | 0.2008              | 0.2458            | **0.3831**       | 0.1256                | Multi-Resolution  |
| MAR (medium)            | 0.1042              | 0.1483            | **0.1848**       | 0.0181                | Multi-Resolution  |
| MAR (small)             | 0.0016              | 0.0041            | **0.0216**       | 0.0000                | Multi-Resolution  |

### Training Details

| Model | Epochs | Input Size | Training Time | Best Val mAP |
|-------|--------|------------|---------------|--------------|
| **Vanilla Faster R-CNN** | 8 | Default (800x1333) | 30.2 min | 0.0969 |
| **Larger Input Size** | 20 | 1024x2000 | 72.7 min | 0.1399 |
| **Multi-Resolution** | 11 | 1024x2000 | 121.5 min | 0.1472 |
| **DeepForest Pretrained** | - | - | 8.2 min | - |

*Training performed on Google Colab Pro with NVIDIA A100 GPU*

### Key Findings

- ✅ **Multi-Resolution model achieves the best performance** across most metrics
- ✅ Larger input sizes (1024x2000) significantly improve detection quality for high-resolution imagery
- ✅ Advanced data augmentation (multi-resolution) provides substantial gains
- ⚠️ DeepForest pre-trained model underperforms on this dataset, likely due to domain differences
- 📊 The dataset is challenging, with lower performance on small objects

## 🏗️ Project Structure

```
selva-box-tree-detection/
├── notebooks/
│   ├── 01_download_data.ipynb
│   ├── 02_explore_the_data.ipynb
│   ├── 03_faster_r_cnn_baseline.ipynb
│   ├── 04_faster_r_cnn_larger_input_size.ipynb
│   ├── 05_faster_r_cnn_with_multi_res.ipynb
│   └── 06_deepforest_pretrained.ipynb
├── data/
│   └── selvabox/              # Downloaded dataset (train/val/test splits)
├── figures/                   # Augmentation pipeline diagrams
├── models/                    # Saved model checkpoints
├── pyproject.toml            # Project dependencies
├── uv.lock                   # Locked dependencies
└── README.md                 # This file
```

## 🔬 Methodology

### Baseline (Notebook 3)
- Standard Faster R-CNN with ResNet-50-FPN backbone
- Default torchvision transforms
- Basic training configuration

### Larger Input Size (Notebook 4)
- Increased input size: `min_size=1024`, `max_size=2000`
- Helps preserve details in high-resolution images
- Better detection of small and medium-sized objects

### Multi-Resolution Augmentation (Notebook 5)
- Advanced augmentation pipeline inspired by the SelvaBox paper
- Multiple resolution scales during training
- Improved generalization and detection performance
- See [figures/](figures/) for visualization

### DeepForest Baseline (Notebook 6)
- Pre-trained model specifically designed for tree detection
- Inference-only evaluation for comparison
- Shows domain adaptation challenges

## 📝 Citation

If you use the SelvaBox dataset, please cite:

```bibtex
@dataset{selvabox,
  title={SelvaBox: A Dataset for Tree Detection in High-Resolution Aerial Imagery},
  author={CanopyRS},
  year={2024},
  url={https://huggingface.co/datasets/CanopyRS/SelvaBox}
}
```

## 🤝 Contributing

Contributions are welcome! Feel free to:
- Report bugs or issues
- Suggest improvements
- Add new experiments or models
- Improve documentation

## 📄 License

This project is provided as-is for educational and research purposes.

## 🙏 Acknowledgments

- SelvaBox dataset creators (CanopyRS team)
- HuggingFace for hosting the dataset
- Google Colab for providing GPU resources
- PyTorch and torchvision teams