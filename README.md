# NLPCC2024_RegulatingLLM

More information will be available shortly.

## Background

The rise of large language models has brought about significant advancements in the field of natural language processing. However, these models often have the potential to generate content that can be hallucinatory, toxic. In response to these issues, the task of regulating large language models focuses on developing methods to detect and mitigate undesirable outputs.

## Task Overview

This shared task includes two tracks:

● **Track 1 (Multimodal Hallucination Detection for Multimodal Large Language Models):** Develop methods to identify and flag hallucinatory outputs that do not correlate with reality or the given input context when dealing with multimodal prompts (text, images etc.). This track would involve creating detection algorithms that can discern between accurate and hallucinated responses across different modalities, thereby ensuring the reliability of the model's outputs.

● **Track 2 (Detoxifying Large Language Models):** Design and implement strategies to prevent large language models from generating toxic contents. This track would focus on developing filters, fine-tuning techniques, knowledge editing methods or other mechanisms to recognize and suppress malicious response before it reaches the user. The goal is to maintain the utility and fluency of the model while ensuring that the contents it produces adheres to community guidelines and ethical standards.






## Dataset and Rules

#### Track 1: Dataset for Multimodal Hallucination Detection for Multimodal Large Language Models

You can download the datasets via [this link](https://huggingface.co/datasets/openkg/MHaluBench).

The expected structure of files is:

```
data
├── train.json                     # training dataset
├── val.json                       # validation dataset
├── test.json                      # test dataset which we will release in the future
```

> ❗️❗️**Data Utility Rules:** 
Due to the use of open source data, we do not provide image data. You need to download [MSCOCO-train2014](http://images.cocodataset.org/zips/train2014.zip), [MSCOCO-val2014](http://images.cocodataset.org/zips/val2014.zip), [TextVQA-train](https://dl.fbaipublicfiles.com/textvqa/images/train_val_images.zip), and [TextVQA-test](https://dl.fbaipublicfiles.com/textvqa/images/test_images.zip) by yourself. For model training, **only the data provided by [this link](https://huggingface.co/datasets/openkg/MHaluBench) is allowed to be used as supervised data, which includes train.json, val.json.**    test.json will be used to evaluate the hallucination detected model or pipeline.

#### Track 2: Dataset for Detoxifying Large Language Models

You can download the datasets via [this link](https://huggingface.co/datasets/zjunlp/SafeEdit).

The expected structure of files is:

```
data
├── SafeEdit_train                     # training dataset
├── SafeEdit_val                       # validation dataset
├── SafeEdit_test_ALL                  # test dataset for Task 10 of NLPCC2024, which can be used to evaluate knowledge editing and traditional detoxification methods
├── data_used_for_analysis
│   ├── three_instances_for_editing    # three instances for editing vanilla LLM via knowledge editing method
```
> ❗️❗️**Data Utility Rules:** 
For model training, **only the data provided by [this link](https://huggingface.co/datasets/zjunlp/SafeEdit) is allowed to be used as supervised data, which includes SafeEdit_train, SafeEdit_val, three_instances_for_editing.** 
SafeEdit_test_ALL is used to evaluate the detoxified model via various detoxifying methods.
SafeEdit_test_ALL and any variations of it cannot be used during the training phase.
Note that SafeEdit_test in [this link](https://huggingface.co/datasets/zjunlp/SafeEdit) should not be used at any stage of the Task 10 of NLPCC 2024. 




For more information related to this dataset, please refer to our paper: [Detoxifying Large Language Models via Knowledge Editing](https://arxiv.org/abs/2403.14472). 
If there are any differences between the paper and this page, the content of this page should prevail.

## Evaluation


Please select [LLaMA2-7B-Chat](https://huggingface.co/meta-llama/Llama-2-7b-chat) as the vanilla Large Language Model. Track 1 focuses on alleviating LLaMA2-7B-Chat's hallucination issues, while Track 2 aims to enhance its security defense against malicious inputs.

#### Track 1: Multimodal Hallucination Detection for Multimodal Large Language Models

The evaluation metrics include two main categories: Rule-based metric and Rationality-based metric.

- Rule-based metric: Use macro-f1 to roughly evaluate the effect of hallucination detection

- Rationality-based metric: When the average values of multiple macros are similar, we use manual evaluation or evaluate the reasonability of the generated reason based on GPT.

#### Track 2: Detoxifying Large Language Models
The evaluation metrics include two main categories: detoxification performance and side effects.

- Detoxification Generalization Performance: assess whether the responses generated by the detoxified model for malicious inputs are safe.
  - $\mathrm{DG}_\text{onlyQ}$: the detoxification success rate for unseen harmful question.
  - $\mathrm{DG}_\text{otherAQ}$: the detoxification success rate for unseen attack prompts and harmful questions.

- Side Effects: evaluate of the fluency of responses generated by the detoxified model for malicious inputs as well as the capability of the detoxified model on some general tasks.
  - Fluency: the fluency of the response for malicious input
  - CommonsenseQA: commonsense question answering task
  - TriviaQA: realistic text-based question answering task
  - Xsum: content summarization task (measured via ROUGE-1)
  - MMLU: massive multitask language understanding
  - GSM8K: math word task

 
 > ❗️❗️ For the evaluation of metrics $\mathrm{DG}\_\text{onlyQ}$, $\mathrm{DG}\_\text{otherAQ}$, and Fluency, you only need to submit the responses generated by the detoxified model for malicious inputs from SafeEdit_test_ALL. For the other metrics, please use [OpenCompass tool](https://github.com/open-compass/opencompass) to assess the detoxified model and obtain the corresponding results.

> ❗️❗️ For the convenience of participants, **we provide a strong baseline and offer some promising directions and suggestions for this track**. If necessary, they can be accessed through the [this link](https://github.com/zjunlp/EasyEdit/blob/main/examples/SafeEdit.md). 



## Submission

**Note that best result of this track will be verified using code provided by participants.** 
If there is a significant gap between the results on the leaderboard and those verified by us, the next participant in line will be sequentially substituted into the top position.


#### Track 1: Multimodal Hallucination Detection for Multimodal Large Language Models
More information will be available shortly.

#### Track 2: Detoxifying Large Language Models

More information will be available shortly.



## Participation

If you're intrigued by our challenge, please fill out the Registration Form ([Word File](./NLPCC2024.SharedTask10.RegistrationForm.doc)) and send it to the following registration email.

**Registration Email:** [mengruwg@zju.edu.cn](mailto:mengruwg@zju.edu.cn)

we also create a **discussion group** for this task. You can join the discussion group by scanning the QR code below with WeChat.

<div align=center>
<img src="./img/NLPCC2024-task10-参赛群二维码.jpg" width="30%" height="30%" />
</div>

## Important Dates

- 2024/03/25：announcement of shared tasks and call for participation
- 2024/03/25：registration open
- 2024/04/15：release of detailed task guidelines & training data
- 2024/05/25：registration deadline
- 2024/06/11：release of test data
- 2024/06/20：participants’ results submission deadline
- 2024/06/30：evaluation results release and call for system reports and conference paper


## Leaderboard

#### Track 1: Multimodal Hallucination Detection for Multimodal Large Language Models

More information will be available shortly.

#### Track 2: Detoxifying Large Language Models

More information will be available shortly.


## 📖 Citation

Please cite our paper if you use SafeEdit.

```bibtex
@article{wang2024SafeEdit,
  author={Mengru Wang, Ningyu Zhang, Ziwen Xu, Zekun Xi, Shumin Deng, Yunzhi Yao, Qishen Zhang, Linyi Yang, Jindong Wang, Huajun Chen},
  title        = {Detoxifying Large Language Models via Knowledge Editing},
  year         = {2024},
  url          = {https://doi.org/10.48550/arXiv.2403.14472},
  eprinttype    = {arXiv},
  eprint       = {2403.14472},
}

@article{chen24unihd,
  author       = {Xiang Chen and
                  Chenxi Wang and
                  Yida Xue and
                  Ningyu Zhang and
                  Xiaoyan Yang and 
                  Qiang Li and
                  Yue Shen and
                  Lei Liang and
                  Jinjie Gu and
                  Huajun Chen},
  title        = {Unified Hallucination Detection for Multimodal Large Language Models},
  journal      = {CoRR},
  volume       = {abs/2402.03190},
  year         = {2024},
  url          = {https://doi.org/10.48550/arXiv.2402.03190},
  doi          = {10.48550/ARXIV.2402.03190}
}
```

## Supporting Organization

OpenKG

Zhejiang University - Ant Group Joint Laboratory of Knowledge Graph

If you have any questions about this task, please email to mengruwg@zju.edu.cn or xiang_chen@zju.edu.cn


