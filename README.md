# Autocomplete with PyTorch and RNNs on Colaboratory

Despite the recent very impressive advances in deep learning such as [GPT-2](https://openai.com/blog/better-language-models/), [BERT](https://ai.googleblog.com/2018/11/open-sourcing-bert-state-of-art-pre.html) or [Nvidia's GAN-powered face generator](https://medium.com/syncedreview/gan-2-0-nvidias-hyperrealistic-face-generator-e3439d33ebaf), the most influential article about deep learning for me personally is Andrej Karpathy‘s blog entry on [the unreasonable effectiveness of recurrent neural networks](http://karpathy.github.io/2015/05/21/rnn-effectiveness/). When I first read the article almost four years ago, I was amazed of how easily these networks produce text passages which resemble the basic style patterns of e.g. a work by Shakespeare or Linux source code. However, when I tried to train my own recurrent neural networks (RNN), I quickly noticed that without a state-of-art GPU, my neural network sounded more like a toddler than like Shakespeare. 

While buying your own GPU might be too expensive to just play around with a few deep learning examples and setting up an [AWS](https://aws.amazon.com/) instance might be too much of a hassle, there is an easy-to-use alternative: [Google Colaboratory](https://colab.research.google.com), a hosted Python development environment that features free GPU (and [TPU](https://cloud.google.com/tpu/)) usage. This tutorial can be opened in Colaboratory by simply clicking on the following badge:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/christophmark/pytorch-autocomplete/blob/master/pytorch-autocomplete.ipynb)

This tutorial aims to cover the complete workflow of a deep learning application, using only Google's computing and data storage resources. The content of this tutorial is inspried by Andrej Karpathy's examples: we will devise a recurrent neural network based on the deep learning framework `PyTorch` that is trained on topic-specific Python source code (e.g. code examples of `tensorflow` or `PyTorch` models) and subsequently serves as a helpful auto-complete function for coding.

To implement this application, we will learn to...
- connect the Colaboratoy notebook to Google Drive for data storage
- scrape training data from Github using automated search queries
- define a stacked LSTM recurrent neural network using PyTorch
- write a GPU-accelerated training routine with a live progress visualization
- integrate the trained model with the notebook environment to employ the auto-complete feature

**Acknowledgements**

Parts of the code in this tutorial have been taken from or are inspired by existing [GitHub](https://github.com/) projects & [StackOverflow](https://stackoverflow.com) answers:
- [neural_complete](https://github.com/kootenpv/neural_complete) by [Pascal van Kooten](https://github.com/kootenpv): A very similar project, based on `keras`/`tensorflow`. The webscraping code in this tutorial is adapted from *neural_complete*.
- [pytorch-charRNN](https://github.com/mcleonard/pytorch-charRNN) by [Mat Leonard](https://github.com/mcleonard): A PyTorch implementation of a character-wise RNN that served as the basis for the stacked LSTM network in this tutorial.
- The integration of the custom auto-complete function would not have been possible without [this hack](https://stackoverflow.com/questions/48187554/extended-information-for-an-ipython-custom-completer) by [Tarun Lalwani](https://stackoverflow.com/users/2830850/tarun-lalwani).

**Disclaimer**

Feel free to use this work for your own projects, it is licensed under the [MIT License](https://opensource.org/licenses/MIT):

<small><em>
> Copyright 2019 Christoph Mark

> Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

> The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

> THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.</em></small>