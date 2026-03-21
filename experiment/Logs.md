## Experiment Setup

| Config | `UNFREEZE_LAST_N_LAYERS` | `BATCH_SIZE` | `GRAD_ACCUM_STEPS` | Expected |
|---|---|---|---|---|
| **Baseline** | 0 | 180 | 1 | Reference |
| **Exp-A** | 2 | 96 | 2 | +3–5% VQA Acc |
| **Exp-B** | 4 | 64 | 3 | +5–8% VQA Acc |

# Kết quả

## Thí nghiệm 1
IMAGE_SIZE   = 224
MAX_SEQUENCE = 77
HIDDEN_DIM   = 512
MAX_EPOCH    = 36
BATCH_SIZE   = 180   # ⚠️  Giảm xuống 64 nếu UNFREEZE_LAST_N_LAYERS >= 3
NUM_LAYER    = 1     # Số LSTM layers trong Decoder
DROPOUT      = 0.42
UNFREEZE_LAST_N_LAYERS = 0    # 🔬 Thay đổi: 0 (baseline), 2, 3, 4 để thí nghiệm
UNFREEZE_PARAM = False        # Legacy flag — không dùng trực tiếp trong v2

Seed set to 42

🚀 Training: VisualQuestionAnswering
   unfreeze=0 layers | batch=180 | accum=1 | epochs=36
🔒 ViT fully frozen — Baseline config
GPU available: True (mps), used: True
TPU available: False, using: 0 TPU cores
💡 Tip: For seamless cloud logging and experiment tracking, try installing [litlogger](https://pypi.org/project/litlogger/) to enable LitLogger, which logs metrics and artifacts automatically to the Lightning Experiments platform.

  | Name            | Type              | Params | Mode  | FLOPs
----------------------------------------------------------------------
0 | image_extractor | VisionTransformer | 87.8 M | train | 0    
1 | token_embedding | Embedding         | 25.3 M | train | 0    
2 | transformer     | Transformer       | 37.8 M | train | 0    
3 | ln_final        | LayerNorm         | 1.0 K  | train | 0    
4 | decoder         | Decoder           | 53.3 M | train | 0    
5 | test_squad      | SQuAD             | 0      | train | 0    
6 | test_bleu       | SacreBLEUScore    | 0      | train | 0    
  | other params    | n/a               | 301 K  | n/a   | n/a  
----------------------------------------------------------------------
53.3 M    Trainable params
151 M     Non-trainable params
204 M     Total params
818.186   Total estimated model params size (MB)
233       Modules in train mode
0         Modules in eval mode
0         Total Flops

Epoch 0, global step 103: 'val_loss' reached 2.98560 (best 2.98560), saving model to '/Users/tieunui/Data science/HUST-MDS-Study/projects/advanced-deep-learning/notebooks/experiment/model/VisualQuestionAnswering_best.ckpt' as top 1
Epoch 1, global step 206: 'val_loss' reached 2.81993 (best 2.81993), saving model to '/Users/tieunui/Data science/HUST-MDS-Study/projects/advanced-deep-learning/notebooks/experiment/model/VisualQuestionAnswering_best.ckpt' as top 1
Epoch 2, global step 309: 'val_loss' reached 2.78288 (best 2.78288), saving model to '/Users/tieunui/Data science/HUST-MDS-Study/projects/advanced-deep-learning/notebooks/experiment/model/VisualQuestionAnswering_best.ckpt' as top 1
Epoch 3, global step 412: 'val_loss' reached 2.72172 (best 2.72172), saving model to '/Users/tieunui/Data science/HUST-MDS-Study/projects/advanced-deep-learning/notebooks/experiment/model/VisualQuestionAnswering_best.ckpt' as top 1
Epoch 4, global step 515: 'val_loss' reached 2.66996 (best 2.66996), saving model to '/Users/tieunui/Data science/HUST-MDS-Study/projects/advanced-deep-learning/notebooks/experiment/model/VisualQuestionAnswering_best.ckpt' as top 1
Epoch 5, global step 618: 'val_loss' was not in top 1
Epoch 6, global step 721: 'val_loss' was not in top 1
Epoch 7, global step 824: 'val_loss' was not in top 1
Epoch 8, global step 927: 'val_loss' was not in top 1
Epoch 9, global step 1030: 'val_loss' was not in top 1
Epoch 10, global step 1133: 'val_loss' was not in top 1


## Thí nghiệm 2
IMAGE_SIZE   = 224
MAX_SEQUENCE = 77
HIDDEN_DIM   = 512
MAX_EPOCH    = 36
BATCH_SIZE   = 96    # ⚠️  Giảm xuống 64 nếu UNFREEZE_LAST_N_LAYERS >= 3
NUM_LAYER    = 1     # Số LSTM layers trong Decoder
DROPOUT      = 0.42
UNFREEZE_LAST_N_LAYERS = 2    # 🔬 Thay đổi: 0 (baseline), 2, 3, 4 để thí nghiệm
UNFREEZE_PARAM = True         # Legacy flag — không dùng trực tiếp trong v2

INFO: Seed set to 42
INFO:lightning.fabric.utilities.seed:Seed set to 42

🚀 Training: VisualQuestionAnswering
   unfreeze=2 layers | batch=96 | accum=1 | epochs=36
🔓 Unfrozen last 2 ViT layers (14,570,496/87,849,216 params, 16.6%)
INFO: Using 16bit Automatic Mixed Precision (AMP)
INFO:lightning.pytorch.utilities.rank_zero:Using 16bit Automatic Mixed Precision (AMP)
INFO: GPU available: True (cuda), used: True
INFO:lightning.pytorch.utilities.rank_zero:GPU available: True (cuda), used: True
INFO: TPU available: False, using: 0 TPU cores
INFO:lightning.pytorch.utilities.rank_zero:TPU available: False, using: 0 TPU cores
INFO: 💡 Tip: For seamless cloud logging and experiment tracking, try installing [litlogger](https://pypi.org/project/litlogger/) to enable LitLogger, which logs metrics and artifacts automatically to the Lightning Experiments platform.
INFO:lightning.pytorch.utilities.rank_zero:💡 Tip: For seamless cloud logging and experiment tracking, try installing [litlogger](https://pypi.org/project/litlogger/) to enable LitLogger, which logs metrics and artifacts automatically to the Lightning Experiments platform.
INFO: Restoring states from the checkpoint path at experiment/model/VisualQuestionAnswering_best.ckpt
INFO:lightning.pytorch.utilities.rank_zero:Restoring states from the checkpoint path at experiment/model/VisualQuestionAnswering_best.ckpt
   Resuming from: experiment/model/VisualQuestionAnswering_best.ckpt
INFO: LOCAL_RANK: 0 - CUDA_VISIBLE_DEVICES: [0]
INFO:lightning.pytorch.accelerators.cuda:LOCAL_RANK: 0 - CUDA_VISIBLE_DEVICES: [0]
⚙️  clip_visual: 27 tensors @ lr=4.10e-04 | decoder: 9 tensors @ lr=4.10e-03
┏━━━┳━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━┳━━━━━━━━┳━━━━━━━┳━━━━━━━┓
┃   ┃ Name            ┃ Type              ┃ Params ┃ Mode  ┃ FLOPs ┃
┡━━━╇━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━╇━━━━━━━━╇━━━━━━━╇━━━━━━━┩
│ 0 │ image_extractor │ VisionTransformer │ 87.8 M │ train │     0 │
│ 1 │ token_embedding │ Embedding         │ 25.3 M │ train │     0 │
│ 2 │ transformer     │ Transformer       │ 37.8 M │ train │     0 │
│ 3 │ ln_final        │ LayerNorm         │  1.0 K │ train │     0 │
│ 4 │ decoder         │ Decoder           │ 53.3 M │ train │     0 │
│ 5 │ test_squad      │ SQuAD             │      0 │ train │     0 │
│ 6 │ test_bleu       │ SacreBLEUScore    │      0 │ train │     0 │
│   │ other params    │ n/a               │  301 K │ n/a   │   n/a │
└───┴─────────────────┴───────────────────┴────────┴───────┴───────┘
Trainable params: 67.8 M                                                                                           
Non-trainable params: 136 M                                                                                        
Total params: 204 M                                                                                                
Total estimated model params size (MB): 818                                                                        
Modules in train mode: 233                                                                                         
Modules in eval mode: 0                                                                                            
Total FLOPs: 0    

INFO: Restored all states from the checkpoint at experiment/model/VisualQuestionAnswering_best.ckpt
INFO:lightning.pytorch.utilities.rank_zero:Restored all states from the checkpoint at experiment/model/VisualQuestionAnswering_best.ckpt
Epoch 17/35 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 193/193 0:08:27 • 0:00:00 0.40it/s train_loss: 1.774 val_loss: 3.071
Validation  ━━━━━━━━━━━━━━━╺━━━━━━━━━━━━━━━━━━ 10/22   0:00:21 • 0:00:29 0.43it/s                                  
📉 LR changed → 4.10e-04 at epoch 1
INFO: Epoch 1, global step 296: 'val_loss' reached 2.92768 (best 2.92768), saving model to '/content/experiment/model/VisualQuestionAnswering_best.ckpt' as top 1
INFO:lightning.pytorch.utilities.rank_zero:Epoch 1, global step 296: 'val_loss' reached 2.92768 (best 2.92768), saving model to '/content/experiment/model/VisualQuestionAnswering_best.ckpt' as top 1
INFO: Epoch 2, global step 489: 'val_loss' reached 2.81889 (best 2.81889), saving model to '/content/experiment/model/VisualQuestionAnswering_best.ckpt' as top 1
INFO:lightning.pytorch.utilities.rank_zero:Epoch 2, global step 489: 'val_loss' reached 2.81889 (best 2.81889), saving model to '/content/experiment/model/VisualQuestionAnswering_best.ckpt' as top 1
INFO: Epoch 3, global step 682: 'val_loss' reached 2.79212 (best 2.79212), saving model to '/content/experiment/model/VisualQuestionAnswering_best.ckpt' as top 1
INFO:lightning.pytorch.utilities.rank_zero:Epoch 3, global step 682: 'val_loss' reached 2.79212 (best 2.79212), saving model to '/content/experiment/model/VisualQuestionAnswering_best.ckpt' as top 1
INFO: Epoch 4, global step 875: 'val_loss' reached 2.74648 (best 2.74648), saving model to '/content/experiment/model/VisualQuestionAnswering_best.ckpt' as top 1
INFO:lightning.pytorch.utilities.rank_zero:Epoch 4, global step 875: 'val_loss' reached 2.74648 (best 2.74648), saving model to '/content/experiment/model/VisualQuestionAnswering_best.ckpt' as top 1
INFO: Epoch 5, global step 1068: 'val_loss' was not in top 1
INFO:lightning.pytorch.utilities.rank_zero:Epoch 5, global step 1068: 'val_loss' was not in top 1
INFO: Epoch 6, global step 1261: 'val_loss' was not in top 1
INFO:lightning.pytorch.utilities.rank_zero:Epoch 6, global step 1261: 'val_loss' was not in top 1
INFO: Epoch 7, global step 1454: 'val_loss' was not in top 1
INFO:lightning.pytorch.utilities.rank_zero:Epoch 7, global step 1454: 'val_loss' was not in top 1
INFO: Epoch 8, global step 1647: 'val_loss' was not in top 1
INFO:lightning.pytorch.utilities.rank_zero:Epoch 8, global step 1647: 'val_loss' was not in top 1
INFO: Epoch 9, global step 1840: 'val_loss' was not in top 1
INFO:lightning.pytorch.utilities.rank_zero:Epoch 9, global step 1840: 'val_loss' was not in top 1
INFO: Epoch 10, global step 2033: 'val_loss' was not in top 1
INFO:lightning.pytorch.utilities.rank_zero:Epoch 10, global step 2033: 'val_loss' was not in top 1
INFO: Epoch 11, global step 2226: 'val_loss' was not in top 1
INFO:lightning.pytorch.utilities.rank_zero:Epoch 11, global step 2226: 'val_loss' was not in top 1
INFO: Epoch 12, global step 2419: 'val_loss' was not in top 1
INFO:lightning.pytorch.utilities.rank_zero:Epoch 12, global step 2419: 'val_loss' was not in top 1
INFO: Epoch 13, global step 2612: 'val_loss' was not in top 1
INFO:lightning.pytorch.utilities.rank_zero:Epoch 13, global step 2612: 'val_loss' was not in top 1
INFO: Epoch 14, global step 2805: 'val_loss' was not in top 1
INFO:lightning.pytorch.utilities.rank_zero:Epoch 14, global step 2805: 'val_loss' was not in top 1
INFO: Epoch 15, global step 2998: 'val_loss' was not in top 1
INFO:lightning.pytorch.utilities.rank_zero:Epoch 15, global step 2998: 'val_loss' was not in top 1
INFO: Epoch 16, global step 3191: 'val_loss' was not in top 1
INFO:lightning.pytorch.utilities.rank_zero:Epoch 16, global step 3191: 'val_loss' was not in top 1

## Thí nghiệm 3
IMAGE_SIZE   = 224
MAX_SEQUENCE = 77
HIDDEN_DIM   = 512
MAX_EPOCH    = 36
BATCH_SIZE   = 96    # ⚠️  Giảm xuống 64 nếu UNFREEZE_LAST_N_LAYERS >= 3
NUM_LAYER    = 1     # Số LSTM layers trong Decoder
DROPOUT      = 0.42
UNFREEZE_LAST_N_LAYERS = 0     # 🔬 Thay đổi: 0 (baseline), 2, 3, 4 để thí nghiệm
UNFREEZE_PARAM = False         # Legacy flag — không dùng trực tiếp trong v2

INFO: Seed set to 42
INFO:lightning.fabric.utilities.seed:Seed set to 42

📉 LR changed → 4.10e-04 at epoch 0
Metric val_loss improved. New best score: 2.954
Epoch 0, global step 193: 'val_loss' reached 2.95388 (best 2.95388), saving model to '/Users/tieunui/Data science/HUST-MDS-Study/projects/advanced-deep-learning/notebooks/experiment/model/VisualQuestionAnswering_best.ckpt' as top 1
Metric val_loss improved by 0.196 >= min_delta = 0.0. New best score: 2.758
Epoch 1, global step 386: 'val_loss' reached 2.75831 (best 2.75831), saving model to '/Users/tieunui/Data science/HUST-MDS-Study/projects/advanced-deep-learning/notebooks/experiment/model/VisualQuestionAnswering_best.ckpt' as top 1
Metric val_loss improved by 0.055 >= min_delta = 0.0. New best score: 2.703
Epoch 2, global step 579: 'val_loss' reached 2.70324 (best 2.70324), saving model to '/Users/tieunui/Data science/HUST-MDS-Study/projects/advanced-deep-learning/notebooks/experiment/model/VisualQuestionAnswering_best.ckpt' as top 1
Metric val_loss improved by 0.024 >= min_delta = 0.0. New best score: 2.680
Epoch 3, global step 772: 'val_loss' reached 2.67954 (best 2.67954), saving model to '/Users/tieunui/Data science/HUST-MDS-Study/projects/advanced-deep-learning/notebooks/experiment/model/VisualQuestionAnswering_best.ckpt' as top 1
Epoch 4, global step 965: 'val_loss' was not in top 1
Epoch 5, global step 1158: 'val_loss' was not in top 1
Epoch 6, global step 1351: 'val_loss' was not in top 1
Epoch 7, global step 1544: 'val_loss' was not in top 1

## Thí nghiệm 4

IMAGE_SIZE   = 224
MAX_SEQUENCE = 77
HIDDEN_DIM   = 512
MAX_EPOCH    = 36
BATCH_SIZE   = 96    # ⚠️  Giảm xuống 64 nếu UNFREEZE_LAST_N_LAYERS >= 3
NUM_LAYER    = 1     # Số LSTM layers trong Decoder
DROPOUT      = 0.42
UNFREEZE_LAST_N_LAYERS = 2     # 🔬 Thay đổi: 0 (baseline), 2, 3, 4 để thí nghiệm
UNFREEZE_PARAM = True          # Legacy flag — không dùng trực tiếp trong v2
GRAD_ACCUM_STEPS = 2 

📉 LR changed → 4.10e-04 at epoch 4
Epoch 4, global step 869: 'val_loss' was not in top 1
Epoch 5, global step 966: 'val_loss' was not in top 1
Epoch 6, global step 1063: 'val_loss' was not in top 1
Epoch 7, global step 1160: 'val_loss' was not in top 1
Epoch 8, global step 1257: 'val_loss' was not in top 1
Epoch 9, global step 1354: 'val_loss' was not in top 1

Detected KeyboardInterrupt, attempting graceful shutdown ...

────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
       Test metric             DataLoader 0
────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
       bleu_1gram           0.4397708773612976
    test_exact_match         43.57490158081055
         test_f1            44.188411712646484
    test_vqa_accuracy       0.5374701023101807
────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

## Thí nghiệm 5

IMAGE_SIZE   = 224
MAX_SEQUENCE = 77
HIDDEN_DIM   = 512
MAX_EPOCH    = 36
BATCH_SIZE   = 180    # ⚠️  Giảm xuống 64 nếu UNFREEZE_LAST_N_LAYERS >= 3
NUM_LAYER    = 1     # Số LSTM layers trong Decoder
DROPOUT      = 0.42
UNFREEZE_LAST_N_LAYERS = 0     # 🔬 Thay đổi: 0 (baseline), 2, 3, 4 để thí nghiệm
UNFREEZE_PARAM = False          # Legacy flag — không dùng trực tiếp trong v2
GRAD_ACCUM_STEPS = 1 

Testing ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 24/24 0:03:01 • 0:00:00 0.18it/s  
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃        Test metric        ┃       DataLoader 0        ┃
┡━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━━┩
│        bleu_1gram         │    0.48178842663764954    │
│     test_exact_match      │     47.18684768676758     │
│          test_f1          │    48.774017333984375     │
│     test_vqa_accuracy     │    0.5670293569564819     │
└───────────────────────────┴───────────────────────────┘

## Thí nghiệm 6

IMAGE_SIZE   = 224
MAX_SEQUENCE = 77
HIDDEN_DIM   = 512
MAX_EPOCH    = 36
BATCH_SIZE   = 96    # ⚠️  Giảm xuống 64 nếu UNFREEZE_LAST_N_LAYERS >= 3
NUM_LAYER    = 1     # Số LSTM layers trong Decoder
DROPOUT      = 0.42
UNFREEZE_LAST_N_LAYERS = 2     # 🔬 Thay đổi: 0 (baseline), 2, 3, 4 để thí nghiệm
UNFREEZE_PARAM = True          # Legacy flag — không dùng trực tiếp trong v2
GRAD_ACCUM_STEPS = 2 

WIP

---

# Ghi chú
### Pytorch, Chip M1 (Apple)
PyTorch trên M1 dùng backend MPS (Metal Performance Shaders) thay vì CUDA. Tuy nhiên MPS có một số đặc điểm khiến nó chậm hơn CUDA đáng kể trong bối cảnh này.

MPS chưa hỗ trợ tốt tất cả các operations của PyTorch — một số ops sẽ silently fallback về CPU, gây ra overhead khi data phải di chuyển qua lại giữa CPU và GPU.
Ngoài ra, **M1 Pro có 16-core GPU tích hợp, so với T4 trên Colab có 2560 CUDA cores** — về throughput thực tế cho deep learning, T4 nhanh hơn M1 Pro khoảng 5–8 lần.

### Ước tính thời gian
VizWiz train set có khoảng 20,000 ảnh, sau khi split 90/10 => có ~18,000 training samples. 
Với BATCH_SIZE=180, mỗi epoch có khoảng 100 batches.
Mỗi batch cần: 
- forward pass qua ViT-B/32 (87.8M params) để encode ảnh
- forward pass qua Text Transformer (37.8M) để encode câu hỏi
- forward + backward qua Decoder LSTM (53.3M), và gradient update.

Trên M1 Pro với MPS, mỗi batch training ước tính mất khoảng 8–15 giây (con số này phụ thuộc nhiều vào việc các ops của ViT có được MPS accelerate hoàn toàn không). 
=> mỗi epoch mất khoảng 15–25 phút, và với 36 epochs tổng thời gian training sẽ vào khoảng: 9–15 giờ cho toàn bộ quá trình.

### Điều chỉnh tham số thí nghiệm
- Môi trường Local không sử dụng được num_workers (=0), khi chạy trên Colab set lên num_workers = 2
- giảm BATCH_SIZE = 64 (đánh đổi học ít đặc trưng hơn)
- Chỉ chạy 30% dữ liệu mỗi epoch:

```python
trainer = Trainer(
    ...
    limit_train_batches=0.3,  # Chỉ dùng khi debug/validate pipeline
                               # Xóa dòng này khi train thật
)
```

Thực tế: TBD

### Tính khoảng khoảng cách train loss - val loss**

> |train loss - val loss| khá lớn (2.760 - 1.220 = 1.54). Đây là dấu hiệu của overfitting đang xảy ra: model đang học tốt trên training data nhưng không generalize tốt sang validation data.

Gap lớn giữa train loss và val loss sau 10 epoch là tín hiệu quan trọng. Với DROPOUT=0.42 đã khá cao, nguyên nhân có thể là val set quá nhỏ (chỉ 1,850 samples sau split 10%) nên val_loss noise cao, hoặc model thực sự đang overfit vào training set nhỏ của VizWiz.

Khi đó cần thực hiện early_stop

| Tham số chung | Giá trị cũ | Giá trị mới |
|---|---|---|
| **Train/Val split** | 90/10 | 85/15 |
| **MAX_EPOCH** | 36 | 20 |
| **Early stopping** | Không | patience = 4 |
| **DROPOUT** | 4 | 64 |