# readmefiles---
inference: false
language:
- code
license: llama2
model_creator: Meta
model_link: https://huggingface.co/codellama/CodeLlama-13b-Instruct-hf
model_name: CodeLlama 13B Instruct
model_type: llama
pipeline_tag: text-generation
quantized_by: TheBloke
tags:
- llama-2
---
<!-- header start -->
<!-- 200823 -->
<div style="width: auto; margin-left: auto; margin-right: auto">
<img src="https://i.imgur.com/EBdldam.jpg" alt="TheBlokeAI" style="width: 100%; min-width: 400px; display: block; margin: auto;">
</div>
<div style="display: flex; justify-content: space-between; width: 100%;">
    <div style="display: flex; flex-direction: column; align-items: flex-start;">
        <p style="margin-top: 0.5em; margin-bottom: 0em;"><a href="https://discord.gg/theblokeai">Chat & support: TheBloke's Discord server</a></p>
    </div>
    <div style="display: flex; flex-direction: column; align-items: flex-end;">
        <p style="margin-top: 0.5em; margin-bottom: 0em;"><a href="https://www.patreon.com/TheBlokeAI">Want to contribute? TheBloke's Patreon page</a></p>
    </div>
</div>
<div style="text-align:center; margin-top: 0em; margin-bottom: 0em"><p style="margin-top: 0.25em; margin-bottom: 0em;">TheBloke's LLM work is generously supported by a grant from <a href="https://a16z.com">andreessen horowitz (a16z)</a></p></div>
<hr style="margin-top: 1.0em; margin-bottom: 1.0em;">
<!-- header end -->
# CodeLlama 13B Instruct - GGUF
- Model creator: [Meta](https://huggingface.co/meta-llama)
- Original model: [CodeLlama 13B Instruct](https://huggingface.co/codellama/CodeLlama-13b-Instruct-hf)

## Description

This repo contains GGUF format model files for [Meta's CodeLlama 13B Instruct](https://huggingface.co/codellama/CodeLlama-13b-Instruct-hf).

<!-- README_GGUF.md-about-gguf start -->
### About GGUF
GGUF is a new format introduced by the llama.cpp team on August 21st 2023. It is a replacement for GGML, which is no longer supported by llama.cpp.
The key benefit of GGUF is that it is a extensible, future-proof format which stores more information about the model as metadata. It also includes significantly improved tokenization code, including for the first time full support for special tokens. This should improve performance, especially with models that use new special tokens and implement custom prompt templates.
As of August 25th, here is a list of clients and libraries that are known to support GGUF:
* [llama.cpp](https://github.com/ggerganov/llama.cpp)
* [text-generation-webui](https://github.com/oobabooga/text-generation-webui), the most widely used web UI. Supports GGUF with GPU acceleration via the ctransformers backend - llama-cpp-python backend should work soon too.
* [KoboldCpp](https://github.com/LostRuins/koboldcpp), now supports GGUF as of release 1.41! A powerful GGML web UI, with full GPU accel. Especially good for story telling.
* [LoLLMS Web UI](https://github.com/ParisNeo/lollms-webui), should now work, choose the `c_transformers` backend. A great web UI with many interesting features. Supports CUDA GPU acceleration.
* [ctransformers](https://github.com/marella/ctransformers), now supports GGUF as of version 0.2.24! A Python library with GPU accel, LangChain support, and OpenAI-compatible AI server.
* [llama-cpp-python](https://github.com/abetlen/llama-cpp-python), supports GGUF as of version 0.1.79. A Python library with GPU accel, LangChain support, and OpenAI-compatible API server.
* [candle](https://github.com/huggingface/candle), added GGUF support on August 22nd. Candle is a Rust ML framework with a focus on performance, including GPU support, and ease of use.

The clients and libraries below are expecting to add GGUF support shortly:
* [LM Studio](https://lmstudio.ai/), should be updated by end August 25th.
<!-- README_GGUF.md-about-gguf end -->
<!-- repositories-available start -->
## Repositories available
* [GPTQ models for GPU inference, with multiple quantisation parameter options.](https://huggingface.co/TheBloke/CodeLlama-13B-Instruct-GPTQ)
* [2, 3, 4, 5, 6 and 8-bit GGUF models for CPU+GPU inference](https://huggingface.co/TheBloke/CodeLlama-13B-Instruct-GGUF)
* [2, 3, 4, 5, 6 and 8-bit GGML models for CPU+GPU inference (deprecated)](https://huggingface.co/TheBloke/CodeLlama-13B-Instruct-GGML)
* [Meta's original unquantised fp16 model in pytorch format, for GPU inference and for further conversions](https://huggingface.co/codellama/CodeLlama-13b-Instruct-hf)
<!-- repositories-available end -->
<!-- prompt-template start -->
## Prompt template: CodeLlama
```
[INST] Write code to solve the following coding problem that obeys the constraints and passes the example test cases. Please wrap your code answer using ```:
{prompt}
[/INST]
```
<!-- prompt-template end -->
<!-- compatibility_gguf start -->
## Compatibility

These quantised GGUF files are compatible with llama.cpp from August 21st 2023 onwards, as of commit [6381d4e110bd0ec02843a60bbeb8b6fc37a9ace9](https://github.com/ggerganov/llama.cpp/commit/6381d4e110bd0ec02843a60bbeb8b6fc37a9ace9)

As of August 24th 2023 they are now compatible with KoboldCpp, release 1.41 and later.

They are are not yet compatible with any other third-party UIS, libraries or utilities but this is expected to change very soon.

## Explanation of quantisation methods
<details>
  <summary>Click to see details</summary>

The new methods available are:
* GGML_TYPE_Q2_K - "type-1" 2-bit quantization in super-blocks containing 16 blocks, each block having 16 weight. Block scales and mins are quantized with 4 bits. This ends up effectively using 2.5625 bits per weight (bpw)
* GGML_TYPE_Q3_K - "type-0" 3-bit quantization in super-blocks containing 16 blocks, each block having 16 weights. Scales are quantized with 6 bits. This end up using 3.4375 bpw.
* GGML_TYPE_Q4_K - "type-1" 4-bit quantization in super-blocks containing 8 blocks, each block having 32 weights. Scales and mins are quantized with 6 bits. This ends up using 4.5 bpw.
* GGML_TYPE_Q5_K - "type-1" 5-bit quantization. Same super-block structure as GGML_TYPE_Q4_K resulting in 5.5 bpw
* GGML_TYPE_Q6_K - "type-0" 6-bit quantization. Super-blocks with 16 blocks, each block having 16 weights. Scales are quantized with 8 bits. This ends up using 6.5625 bpw

Refer to the Provided Files table below to see what files use which methods, and how.
</details>
<!-- compatibility_gguf end -->
<!-- README_GGUF.md-provided-files start -->
## Provided files

| Name | Quant method | Bits | Size | Max RAM required | Use case |
| ---- | ---- | ---- | ---- | ---- | ----- |
| [codellama-13b-instruct.Q2_K.gguf](https://huggingface.co/TheBloke/CodeLlama-13B-Instruct-GGUF/blob/main/codellama-13b-instruct.Q2_K.gguf) | Q2_K | 2 | 5.66 GB| 8.16 GB | smallest, significant quality loss - not recommended for most purposes |
| [codellama-13b-instruct.Q3_K_S.gguf](https://huggingface.co/TheBloke/CodeLlama-13B-Instruct-GGUF/blob/main/codellama-13b-instruct.Q3_K_S.gguf) | Q3_K_S | 3 | 5.87 GB| 8.37 GB | very small, high quality loss |
| [codellama-13b-instruct.Q3_K_M.gguf](https://huggingface.co/TheBloke/CodeLlama-13B-Instruct-GGUF/blob/main/codellama-13b-instruct.Q3_K_M.gguf) | Q3_K_M | 3 | 6.55 GB| 9.05 GB | very small, high quality loss |
| [codellama-13b-instruct.Q3_K_L.gguf](https://huggingface.co/TheBloke/CodeLlama-13B-Instruct-GGUF/blob/main/codellama-13b-instruct.Q3_K_L.gguf) | Q3_K_L | 3 | 7.14 GB| 9.64 GB | small, substantial quality loss |
| [codellama-13b-instruct.Q4_K_S.gguf](https://huggingface.co/TheBloke/CodeLlama-13B-Instruct-GGUF/blob/main/codellama-13b-instruct.Q4_K_S.gguf) | Q4_K_S | 4 | 7.61 GB| 10.11 GB | small, greater quality loss |
| [codellama-13b-instruct.Q4_K_M.gguf](https://huggingface.co/TheBloke/CodeLlama-13B-Instruct-GGUF/blob/main/codellama-13b-instruct.Q4_K_M.gguf) | Q4_K_M | 4 | 8.06 GB| 10.56 GB | medium, balanced quality - recommended |
| [codellama-13b-instruct.Q5_K_S.gguf](https://huggingface.co/TheBloke/CodeLlama-13B-Instruct-GGUF/blob/main/codellama-13b-instruct.Q5_K_S.gguf) | Q5_K_S | 5 | 9.15 GB| 11.65 GB | large, low quality loss - recommended |
| [codellama-13b-instruct.Q5_K_M.gguf](https://huggingface.co/TheBloke/CodeLlama-13B-Instruct-GGUF/blob/main/codellama-13b-instruct.Q5_K_M.gguf) | Q5_K_M | 5 | 9.40 GB| 11.90 GB | large, very low quality loss - recommended |
| [codellama-13b-instruct.Q6_K.gguf](https://huggingface.co/TheBloke/CodeLlama-13B-Instruct-GGUF/blob/main/codellama-13b-instruct.Q6_K.gguf) | Q6_K | 6 | 10.83 GB| 13.33 GB | very large, extremely low quality loss |
| [codellama-13b-instruct.Q8_0.gguf](https://huggingface.co/TheBloke/CodeLlama-13B-Instruct-GGUF/blob/main/codellama-13b-instruct.Q8_0.gguf) | Q8_0 | 8 | 13.83 GB| 16.33 GB | very large, extremely low quality loss - not recommended |
**Note**: the above RAM figures assume no GPU offloading. If layers are offloaded to the GPU, this will reduce RAM usage and use VRAM instead.
<!-- README_GGUF.md-provided-files end -->

<!-- README_GGUF.md-how-to-run start -->
## How to run in `llama.cpp`
Make sure you are using `llama.cpp` from commit [6381d4e110bd0ec02843a60bbeb8b6fc37a9ace9](https://github.com/ggerganov/llama.cpp/commit/6381d4e110bd0ec02843a60bbeb8b6fc37a9ace9) or later.
For compatibility with older versions of llama.cpp, or for use with third-party clients and libaries, please use GGML files instead.
```
./main -t 10 -ngl 32 -m codellama-13b-instruct.q4_K_M.gguf --color -c 4096 --temp 0.7 --repeat_penalty 1.1 -n -1 -p "### Instruction: Write a story about llamas\n### Response:"
```
Change `-t 10` to the number of physical CPU cores you have. For example if your system has 8 cores/16 threads, use `-t 8`.
Change `-ngl 32` to the number of layers to offload to GPU. Remove it if you don't have GPU acceleration.
Change `-c 4096` to the desired sequence length for this model. For extended sequence models - eg 8K, 16K, 32K - the necessary RoPE scaling parameters are read from the GGUF file and set by llama.cpp automatically.
If you want to have a chat-style conversation, replace the `-p <PROMPT>` argument with `-i -ins`
For other parameters and how to use them, please refer to [the llama.cpp documentation](https://github.com/ggerganov/llama.cpp/blob/master/examples/main/README.md)
## How to run in `text-generation-webui`
Further instructions here: [text-generation-webui/docs/llama.cpp.md](https://github.com/oobabooga/text-generation-webui/blob/main/docs/llama.cpp.md).
<!-- README_GGUF.md-how-to-run end -->
<!-- footer start -->
<!-- 200823 -->
## Discord
For further support, and discussions on these models and AI in general, join us at:
[TheBloke AI's Discord server](https://discord.gg/theblokeai)
## Thanks, and how to contribute.
Thanks to the [chirper.ai](https://chirper.ai) team!
I've had a lot of people ask if they can contribute. I enjoy providing models and helping people, and would love to be able to spend even more time doing it, as well as expanding into new projects like fine tuning/training.
If you're able and willing to contribute it will be most gratefully received and will help me to keep providing more models, and to start work on new AI projects.
Donaters will get priority support on any and all AI/LLM/model questions and requests, access to a private Discord room, plus other benefits.
* Patreon: https://patreon.com/TheBlokeAI
* Ko-Fi: https://ko-fi.com/TheBlokeAI
**Special thanks to**: Aemon Algiz.
**Patreon special mentions**: Kacper Wikieł, knownsqashed, Leonard Tan, Asp the Wyvern, Daniel P. Andersen, Luke Pendergrass, Stanislav Ovsiannikov, RoA, Dave, Ai Maven, Kalila, Will Dee, Imad Khwaja, Nitin Borwankar, Joseph William Delisle, Tony Hughes, Cory Kujawski, Rishabh Srivastava, Russ Johnson, Stephen Murray, Lone Striker, Johann-Peter Hartmann, Elle, J, Deep Realms, SuperWojo, Raven Klaugh, Sebastain Graf, ReadyPlayerEmma, Alps Aficionado, Mano Prime, Derek Yates, Gabriel Puliatti, Mesiah Bishop, Magnesian, Sean Connelly, biorpg, Iucharbius, Olakabola, Fen Risland, Space Cruiser, theTransient, Illia Dulskyi, Thomas Belote, Spencer Kim, Pieter, John Detwiler, Fred von Graf, Michael Davis, Swaroop Kallakuri, subjectnull, Clay Pascal, Subspace Studios, Chris Smitley, Enrico Ros, usrbinkat, Steven Wood, alfie_i, David Ziegler, Willem Michiel, Matthew Berman, Andrey, Pyrater, Jeffrey Morgan, vamX, LangChain4j, Luke @flexchar, Trenton Dambrowitz, Pierre Kircher, Alex, Sam, James Bentley, Edmond Seymore, Eugene Pentland, Pedro Madruga, Rainer Wilmers, Dan Guido, Nathan LeClaire, Spiking Neurons AB, Talal Aujan, zynix, Artur Olbinski, Michael Levine, 阿明, K, John Villwock, Nikolai Manek, Femi Adebogun, senxiiz, Deo Leter, NimbleBox.ai, Viktor Bowallius, Geoffrey Montalvo, Mandus, Ajan Kanaga, ya boyyy, Jonathan Leane, webtim, Brandon Frisco, danny, Alexandros Triantafyllidis, Gabriel Tamborski, Randy H, terasurfer, Vadim, Junyu Yang, Vitor Caleffi, Chadd, transmissions 11
Thank you to all my generous patrons and donaters!
And thank you again to a16z for their generous grant.
<!-- footer end -->
<!-- original-model-card start -->
# Original model card: Meta's CodeLlama 13B Instruct
# **Code Llama**
Code Llama is a collection of pretrained and fine-tuned generative text models ranging in scale from 7 billion to 34 billion parameters. This is the repository for the 13 instruct-tuned version in the Hugging Face Transformers format. This model is designed for general code synthesis and understanding. Links to other models can be found in the index at the bottom.
|     | Base Model                                                                    | Python                                                                                      | Instruct                                                                                        |
| --- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| 7B  | [codellama/CodeLlama-7b-hf](https://huggingface.co/codellama/CodeLlama-7b-hf) | [codellama/CodeLlama-7b-Python-hf](https://huggingface.co/codellama/CodeLlama-7b-Python-hf) | [codellama/CodeLlama-7b-Instruct-hf](https://huggingface.co/codellama/CodeLlama-7b-Instruct-hf) |
| 13B  | [codellama/CodeLlama-13b-hf](https://huggingface.co/codellama/CodeLlama-13b-hf) | [codellama/CodeLlama-13b-Python-hf](https://huggingface.co/codellama/CodeLlama-13b-Python-hf) | [codellama/CodeLlama-13b-Instruct-hf](https://huggingface.co/codellama/CodeLlama-13b-Instruct-hf) |
| 34B  | [codellama/CodeLlama-34b-hf](https://huggingface.co/codellama/CodeLlama-34b-hf) | [codellama/CodeLlama-34b-Python-hf](https://huggingface.co/codellama/CodeLlama-34b-Python-hf) | [codellama/CodeLlama-34b-Instruct-hf](https://huggingface.co/codellama/CodeLlama-34b-Instruct-hf) |
## Model Use
To use this model, please make sure to install transformers from `main` until the next version is released:
```bash
pip install git+https://github.com/huggingface/transformers.git@main accelerate
```
Model capabilities:
- [x] Code completion.
- [x] Infilling.
- [x] Instructions / chat.
- [ ] Python specialist.
## Model Details
*Note: Use of this model is governed by the Meta license. Meta developed and publicly released the Code Llama family of large language models (LLMs).
**Model Developers** Meta
**Variations** Code Llama comes in three model sizes, and three variants:
* Code Llama: base models designed for general code synthesis and understanding
* Code Llama - Python: designed specifically for Python
* Code Llama - Instruct: for instruction following and safer deployment
All variants are available in sizes of 7B, 13B and 34B parameters.
**This repository contains the Instruct version of the 13B parameters model.**
**Input** Models input text only.
**Output** Models generate text only.
**Model Architecture** Code Llama is an auto-regressive language model that uses an optimized transformer architecture.
**Model Dates** Code Llama and its variants have been trained between January 2023 and July 2023.
**Status** This is a static model trained on an offline dataset. Future versions of Code Llama - Instruct will be released as we improve model safety with community feedback.
**License** A custom commercial license is available at: [https://ai.meta.com/resources/models-and-libraries/llama-downloads/](https://ai.meta.com/resources/models-and-libraries/llama-downloads/)
**Research Paper** More information can be found in the paper "[Code Llama: Open Foundation Models for Code](https://ai.meta.com/research/publications/code-llama-open-foundation-models-for-code/)".
## Intended Use
**Intended Use Cases** Code Llama and its variants is intended for commercial and research use in English and relevant programming languages. The base model Code Llama can be adapted for a variety of code synthesis and understanding tasks, Code Llama - Python is designed specifically to handle the Python programming language, and Code Llama - Instruct is intended to be safer to use for code assistant and generation applications.
**Out-of-Scope Uses** Use in any manner that violates applicable laws or regulations (including trade compliance laws). Use in languages other than English. Use in any other way that is prohibited by the Acceptable Use Policy and Licensing Agreement for Code Llama and its variants.
## Hardware and Software
**Training Factors** We used custom training libraries. The training and fine-tuning of the released models have been performed Meta’s Research Super Cluster.
**Carbon Footprint** In aggregate, training all 9 Code Llama models required 400K GPU hours of computation on hardware of type A100-80GB (TDP of 350-400W). Estimated total emissions were 65.3 tCO2eq, 100% of which were offset by Meta’s sustainability program.
## Training Data
All experiments reported here and the released models have been trained and fine-tuned using the same data as Llama 2 with different weights (see Section 2 and Table 1 in the [research paper](https://ai.meta.com/research/publications/code-llama-open-foundation-models-for-code/) for details).
## Evaluation Results
See evaluations for the main models and detailed ablations in Section 3 and safety evaluations in Section 4 of the research paper.
## Ethical Considerations and Limitations
Code Llama and its variants are a new technology that carries risks with use. Testing conducted to date has been in English, and has not covered, nor could it cover all scenarios. For these reasons, as with all LLMs, Code Llama’s potential outputs cannot be predicted in advance, and the model may in some instances produce inaccurate or objectionable responses to user prompts. Therefore, before deploying any applications of Code Llama, developers should perform safety testing and tuning tailored to their specific applications of the model.
Please see the Responsible Use Guide available available at [https://ai.meta.com/llama/responsible-user-guide](https://ai.meta.com/llama/responsible-user-guide).
<!-- original-model-card end -->
