# Training configuration

A typical yaml config file is explained as follows.

```yaml
train:
  model:
    method: "ddf" # ddf or conditional or seg
    backbone:
      name: "global"
      out_kernel_initializer: "zeros" # zeros or glorot_uniform
    local:
      num_channel_initial: 1
      extract_levels: [0, 1, 2, 3, 4]
    global:
      num_channel_initial: 1
      extract_levels: [0, 1, 2, 3, 4]
    unet:
      num_channel_initial: 4
      depth: 2
      pooling: true
      concat_skip: false
  loss:
    dissimilarity:
      image:
        name: "lncc"
        weight: 0.0
      label:
        weight: 1.0
        name: "multi_scale"
        multi_scale:
          loss_type: "dice"
          loss_scales: [0, 1, 2, 4, 8, 16, 32]
        single_scale:
          loss_type: "cross-entropy"
    regularization:
      weight: 0.0
      energy_type: "bending"
  data:
    batch_size: 2
    shuffle_buffer_num_batch: 0
  opt:
    name: "adam" # "adam" / "sgd" / "rms"
    adam:
      learning_rate: 1.0e-5
    sgd:
      learning_rate: 1.0e-4
      momentum: 0.9
    rms:
      learning_rate: 1.0e-4
      momentum: 0.9
  epochs: 2
  save_period: 2
  histogram_freq: 2
```