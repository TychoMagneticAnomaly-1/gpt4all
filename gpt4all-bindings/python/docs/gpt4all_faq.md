# GPT4All FAQ

## What models are supported by the GPT4All ecosystem?

Currently, there are five different model architectures that are supported:

1. GPT-J - Based off of the GPT-J architecture with examples found [here](https://huggingface.co/EleutherAI/gpt-j-6b)
2. LLaMA - Based off of the LLaMA architecture with examples found [here](https://huggingface.co/models?sort=downloads&search=llama)
3. MPT - Based off of Mosaic ML's MPT architecture with examples found [here](https://huggingface.co/mosaicml/mpt-7b)
4. Replit - Based off of Replit Inc.'s Replit architecture with examples found [here](https://huggingface.co/replit/replit-code-v1-3b)
5. Falcon - Based off of TII's Falcon architecture with examples found [here](https://huggingface.co/tiiuae/falcon-40b)

## Why so many different architectures? What differentiates them?

One of the major differences is license. Currently, the LLAMA based models are subject to a non-commercial license, whereas the GPTJ and MPT base models allow commercial usage. In the early advent of the recent explosion of activity in open source local models, the llama models have generally been seen as performing better, but that is changing quickly. Every week - even every day! - new models are released with some of the GPTJ and MPT models competitive in performance/quality with LLAMA. What's more, there are some very nice architectural innovations with the MPT models that could lead to new performance/quality gains.

## How does GPT4All make these models available for CPU inference?

By leveraging the ggml library written by Georgi Gerganov and a growing community of developers. There are currently multiple different versions of this library. The original github repo can be found [here](https://github.com/ggerganov/ggml), but the developer of the library has also created a LLAMA based version [here](https://github.com/ggerganov/llama.cpp). Currently, this backend is using the latter as a submodule.

## Does that mean GPT4All is compatible with all llama.cpp models and vice versa?

Yes!

The upstream [llama.cpp](https://github.com/ggerganov/llama.cpp) project has introduced several [compatibility breaking](https://github.com/ggerganov/llama.cpp/commit/b9fd7eee57df101d4a3e3eabc9fd6c2cb13c9ca1) quantization methods recently. This is a breaking change that renders all previous models (including the ones that GPT4All uses) inoperative with newer versions of llama.cpp since that change.

Fortunately, we have engineered a submoduling system allowing us to dynamically load different versions of the underlying library so that
GPT4All just works.

## What are the system requirements?

Your CPU needs to support [AVX or AVX2 instructions](https://en.wikipedia.org/wiki/Advanced_Vector_Extensions) and you need enough RAM to load a model into memory.

## What about GPU inference?

In newer versions of llama.cpp, there has been some added support for NVIDIA GPU's for inference. We're investigating how to incorporate this into our downloadable installers.

## Ok, so bottom line... how do I make my model on huggingface compatible with GPT4All ecosystem right now?

1. Check to make sure the huggingface model is available in one of our three supported architectures
2. If it is, then you can use the conversion script inside of our pinned llama.cpp submodule for GPTJ and LLAMA based models
3. Or if your model is an MPT model you can use the conversion script located directly in this backend directory under the scripts subdirectory 
