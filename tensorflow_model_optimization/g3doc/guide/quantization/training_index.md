# Quantization-aware training

There are two forms of quantization: post-training quantization and
quantization-aware training. We recommend starting with [the first](index.md)
since it's easier to use, though the second is often better for model accuracy.

To jump right into the code, see the
[quantization-aware training with Keras tutorial](quantization_aware_training.ipynb).
For a more comprehensive guide on quantization during training for different use
cases, see the
[quantization-aware training guide](quantization_aware_training_guide.md).

### Overview

Quantization-aware training introduces TensorFlow operations and variables to
the model, to emulate inference and store information that downstream tools will
use to produce quantized models.

This technique brings improvements via model compression and latency reduction.
With the API defaults, the model size shrinks by 4x and we typically see between
2 - 4x improvements in CPU latency in the tested backends. Further latency
improvements can be seen on compatible machine learning accelerators, such
as the [EdgeTPU](https://coral.ai/docs/edgetpu/benchmarks/) and NNAPI.

The technique is used in production in speech, vision, text, and translate use
cases. The code currently supports vision use cases and will expand over time.

#### API Compatibility Matrix

Users can apply quantization with the following APIs:

*  Model building: `tf.keras` with only Sequential and Functional models.
*  TensorFlow versions: TF 2.x for tf-nightly
  *  `tf.compat.v1` with a TF 2.X package is not supported.
*  TensorFlow execution mode: eager execution

It is on our roadmap to add support in the following areas:

<!-- TODO: file Github issues. -->
*  Model building: clarify degree of support for Subclassed Models
*  Distributed training: `tf.distribute`

#### General Support Matrix

Support is available in the following areas:

*  Model coverage: Mobilenet v1 and v2

It is on our roadmap to add support in the following areas:

<!-- TODO: file Github issue. -->
*  Model coverage: extended coverage for vision and other use cases,
including concat support.

### Results

#### Image Classification via Tool

<!-- TODO: update Mobilenet v1 numbers if new and old experiments have varying
results -->

<figure>
  <table>
    <tr>
      <th>Model</th>
      <th>Non-quantized Top-1 Accuracy </th>
      <th>Quantized Accuracy </th>
    </tr>
    <tr>
      <td>MobilenetV1 224</td>
      <td>71.4%</td>
      <td>71.4%</td>
    </tr>
    <tr>
      <td>MobilenetV2 224</td>
      <td>71.9%</td>
      <td>71.1%</td>
    </tr>
 </table>
</figure>

The models were tested on Imagenet and evaluated in both TensorFlow and TFLite.

#### Image Classification for Technique

<figure>
  <table>
    <tr>
      <th>Model</th>
      <th>Non-quantized Top-1 Accuracy </th>
      <th>Quantized Accuracy </th>
    <tr>
      <td>Nasnet-Mobile</td>
      <td>74%</td>
      <td>73%</td>
    </tr>
    <tr>
      <td>Resnet-v1 50</td>
      <td>75.2%</td>
      <td>75%</td>
    </tr>
    <tr>
      <td>Resnet-v2 50</td>
      <td>75.6%</td>
      <td>75%</td>
    </tr>
 </table>
</figure>

The models were tested on Imagenet and evaluated in both TensorFlow and TFLite.

### Examples

In addition to the
[quantization-aware training with Keras tutorial](quantization_with_keras.ipynb),
see the following examples:

*   Train a CNN model on the MNIST handwritten digit classification task with
    quantization:
    [code](https://github.com/tensorflow/model-optimization/blob/master/tensorflow_model_optimization/python/examples/quantization/keras/mnist_cnn.py)

### Tips

1.  Start with a pre-trained model or weights.

No existing paper exactly reflects the current implementation. For background on
something similar, see *Quantization and Training of Neural Networks for
Efficient Integer-Arithmetic-Only Inference*
[[paper](https://arxiv.org/abs/1712.05877)].
