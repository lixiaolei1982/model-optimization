# TensorFlow Model Optimization Consistent User Experience

Status        | Pending
:------------ | :------------------------------------------------------
**RFC #**     | [257](https://github.com/tensorflow/model-optimization/pull/257)
**Author(s)** | Alan Chiao (alanchiao@google.com)
**Sponsor**   | TODO
**Updated**   | 2020-02-20

## Objective
Improve the usability of the Model Optimization Toolkit, by making the user
experience consistent across techniques whenever it is sensible. “User” refers
to the end user of the technique. Other types of users are out of scope.

## Design Proposal

At a high-level, achieving this requires the following:

1. Similar documentation across techniques, so that users can easily determine what
techniques they want to try and then try them.

2. Clear expectations on the degree of functionality and support they should expect
from the technique and its OWNERS. We achieve this via TODO: link to Ownership
RFC. The [technique contribution guide](https://github.com/tensorflow/model-optimization/blob/master/CONTRIBUTING_TECHNIQUE.md)
helps the technique contributor achieve this, though the user should never have to read the contribution guide to learn about
the expectations.

3. Similar public APIs when sensible. We achieve this as a part of the technique
contribution RFC process (TODO: link when complete).
   * An API built on tf.keras will be different from an API built on core TensorFlow.
  However, Keras APIs for techniques with shared properties should be as similar
  as possible in API structure and style, without compromising on the needs of the
  users of the technique itself.


The rest of this document focuses on 1.

Each technique will have three documentation pages, to serve three different
needs of users.

1. Overview page: users determine whether they want to try the technique. Once they’ve decided to try the technique, the page guides them to other pages to try the technique.
  * Given the purpose, the page should be as non-technical as possible. Ultimately, a user wants to optimize their models for deployment for their specific use case and environment.

2. Tutorial page in Colab: users see the end-to-end experience of the most critical usage pattern, up until the tutorial demonstrates the benefits of the technique (“critical” with respect to achieving the goal of easily deploying more efficient models).
  * The tutorial can reference back to the overview page to link some of the code to its benefits.

3. Comprehensive guide in Colab: users want to quickly find the API calls needed for their use case.
  * The guide should be concise. One of the disadvantages of an end-to-end tutorial is that it is difficult to find the exact few lines of code specific to the technique, amongst boilerplate code. This guide addresses that disadvantage. Realistically, there cannot be end-to-end tutorials for every use case either.
  * There should be headers for major use cases, which can be divided into smaller use cases. For an example, users of quantization may want to either deploy with quantization or experiment with quantization. There should be one header for each of these use cases and then further divisions for varying deployment or experimentation needs.
  * The guide should not reference any of the benefits of technique. Users have already decided to try the technique.

