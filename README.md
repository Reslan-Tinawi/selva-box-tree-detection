## Faster R-CNN Model Evaluation Metrics

| Metric                  | Vanilla Faster R-CNN | Larger Input Size | Multi-Resolution | Best Model        |
|-------------------------|---------------------|-------------------|------------------|-------------------|
| mAP (IoU=0.50:0.95)     | 0.0928              | 0.1348            | **0.1493**       | Multi-Resolution  |
| mAP (IoU=0.50)          | 0.2107              | 0.2778            | **0.4105**       | Multi-Resolution  |
| mAP (IoU=0.75)          | 0.0680              | 0.1199            | **0.1251**       | Multi-Resolution  |
| mAP (large)             | 0.1295              | 0.1779            | **0.2368**       | Multi-Resolution  |
| mAP (medium)            | 0.0334              | 0.0628            | **0.0807**       | Multi-Resolution  |
| mAP (small)             | **0.0035**          | 0.0001            | 0.0020           | Vanilla           |
| mAP (per class)         | 0.0928              | 0.1348            | **0.1493**       | Multi-Resolution  |
| MAR@1                   | 0.0054              | **0.0061**        | **0.0061**       | Larger/Multi-Res  |
| MAR@10                  | 0.0416              | **0.0495**        | -                | Larger Input Size |
| MAR@100                 | 0.1565              | 0.2049            | **0.2204**       | Multi-Resolution  |
| MAR@100 (per class)     | 0.1565              | 0.2049            | -                | Larger Input Size |
| MAR@400                 | -                   | -                 | **0.3030**       | Multi-Resolution  |
| MAR@400 (per class)     | -                   | -                 | **0.3030**       | Multi-Resolution  |
| MAR (large)             | 0.1894              | 0.2457            | **0.3815**       | Multi-Resolution  |
| MAR (medium)            | 0.1101              | 0.1481            | **0.1872**       | Multi-Resolution  |
| MAR (small)             | 0.0024              | 0.0044            | **0.0224**       | Multi-Resolution  |

**Classes:** 1 (`torch.int32`)

**Note:** Best results for each metric are **bolded**. For metrics not reported by all models, the best available value is highlighted.
