## Faster R-CNN Model Evaluation Metrics

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

**Training Details:**
- **Vanilla Faster R-CNN:** Epoch 8, Training time: 30.2 min, Best val mAP: 0.0969
- **Larger Input Size:** Epoch 20 (min_size=1024, max_size=2000), Training time: 72.7 min, Best val mAP: 0.1399
- **Multi-Resolution:** Epoch 11 (min_size=1024, max_size=2000), Training time: 121.5 min, Best val mAP: 0.1472
- **DeepForest Pretrained:** Training time: 8.2 min

**Note:** Best results for each metric are **bolded**. Multi-Resolution model achieves the best performance across most metrics.
