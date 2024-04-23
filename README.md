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
└── test.json                      # test dataset which we will release in the future
```

> ❗️❗️**Data Utility Rules:** 
Due to the use of open source data, we do not provide image data. You need to download [MSCOCO-train2014](http://images.cocodataset.org/zips/train2014.zip), [MSCOCO-val2014](http://images.cocodataset.org/zips/val2014.zip), [TextVQA-train](https://dl.fbaipublicfiles.com/textvqa/images/train_val_images.zip), and [TextVQA-test](https://dl.fbaipublicfiles.com/textvqa/images/test_images.zip) by yourself. For model training, **only the data provided by [this link](https://huggingface.co/datasets/openkg/MHaluBench) is allowed to be used as supervised data, which includes train.json, val.json.**    test.json will be used to evaluate the hallucination detected model or pipeline.

For more information related to this dataset, please refer to our paper: [Unified Hallucination Detection for Multimodal Large Language Models](https://arxiv.org/abs/2402.03190). 

#### Track 2: Dataset for Detoxifying Large Language Models

You can download the datasets via [this link](https://huggingface.co/datasets/zjunlp/SafeEdit).

The expected structure of files is:

```
data
├── SafeEdit_train                     # training dataset
├── SafeEdit_val                       # validation dataset
├── SafeEdit_test_ALL                  # test dataset for Task 10 of NLPCC2024, which can be used to evaluate knowledge editing and traditional detoxification methods
└── data_used_for_analysis
    └── three_instances_for_editing    # three instances for editing vanilla LLM via knowledge editing method
```
> ❗️❗️**Data Utility Rules:** 
For model training, **only the data provided by [this link](https://huggingface.co/datasets/zjunlp/SafeEdit) is allowed to be used as supervised data, which includes SafeEdit_train, SafeEdit_val, three_instances_for_editing.** 
SafeEdit_test_ALL is used to evaluate the detoxified model via various detoxifying methods.
SafeEdit_test_ALL and any variations of it cannot be used during the training phase.
Note that SafeEdit_test in [this link](https://huggingface.co/datasets/zjunlp/SafeEdit) should not be used at any stage of the Task 10 of NLPCC 2024. 




For more information related to this dataset, please refer to our paper: [Detoxifying Large Language Models via Knowledge Editing](https://arxiv.org/abs/2403.14472). 
If there are any differences between the paper and this page, the content of this page should prevail.

## Evaluation




#### Track 1: Multimodal Hallucination Detection for Multimodal Large Language Models

The evaluation metrics include two main categories: Rule-based metric and Rationality-based metric.

- Rule-based metric: Use macro-f1 to roughly evaluate the effect of hallucination detection

- Rationality-based metric: When the average values of multiple macros are similar, we use manual evaluation or evaluate the reasonability of the generated reason based on GPT.

#### Track 2: Detoxifying Large Language Models
Please select [LLaMA2-7B-Chat](https://huggingface.co/meta-llama/Llama-2-7b-chat) as the vanilla Large Language Model. Track 2 aims to enhance its security defense against malicious inputs.
The evaluation metrics include two main categories: detoxification performance and side effects.

- Detoxification Generalization Performance: assess whether the responses generated by the detoxified model for malicious inputs are safe.
  - DGonlyQ: the detoxification success rate for unseen harmful question.
  - DGotherAQ: the detoxification success rate for unseen attack prompts and harmful questions.

- Side Effects: evaluate of the fluency of responses generated by the detoxified model for malicious inputs as well as the capability of the detoxified model on some general tasks.
  - Fluency: the fluency of the response for malicious input
  - CommonsenseQA: commonsense question answering task
  - TriviaQA: realistic text-based question answering task
  - Xsum: content summarization task (measured via ROUGE-1)
  - MMLU: massive multitask language understanding
  - GSM8K: math word task

 
 > ❗️❗️ For the evaluation of metrics DGonlyQ, DGotherAQ, and Fluency, you only need to submit the responses generated by the detoxified model for malicious inputs from SafeEdit_test_ALL. For the other metrics, please use [OpenCompass tool](https://github.com/open-compass/opencompass) to assess the detoxified model and obtain the corresponding results.



## Baseline Results

#### Track 1: Multimodal Hallucination Detection for Multimodal Large Language Models
The claim level results on validation dataset
- Self-Check(GPT-4V) means use GPT-4V with 0 or 2 cases
- UniHD(GPT-4V) means use GPT4V with 2-shot and tool information
- HalDet (LLAVA) means use LLAVA-v1.5 trained on our train datasets
<table>
    <tr>
        <td></td>
        <td>model</td>
        <td>Acc</td>
        <td>Prec avg</td>
        <td>Recall avg</td>
        <td>Mac.F1</td>
    </tr>
    <tr>
        <td rowspan="5">image-to-text</td>
        <td>Self-Check 0shot (GPV-4V)</td>
        <td>75.09</td> 
        <td>74.94</td>
        <td>75.19</td>
        <td>74.97</td>
    </tr>
    <tr>
        <td>Self-Check 2shot (GPV-4V)</td>
        <td>79.25</td>
        <td>79.02</td>
        <td>79.16</td>
        <td>79.08</td>
    </tr>
    <tr>
        <td>HalDet (LLAVA-7b)</td>
        <td>75.02</td>
        <td>75.05</td>
        <td>74.18</td>
        <td>74.38</td>
    </tr>
    <tr>
        <td>HalDet (LLAVA-13b)</td>
        <td>78.16</td>
        <td>78.18</td>
        <td>77.48</td>
        <td>77.69</td>
    </tr>
    <tr>
        <td>UniHD(GPT-4V)</td>
        <td>81.91</td>
        <td>81.81</td>
        <td>81.52</td>
        <td>81.63</td>
    </tr>
</table>

#### Track 2: Detoxifying Large Language Models
The detoxification performance on SafeEdit_test_ALL and basic ability on some general tasks.
- SFT: fine-tune the entire model
- DPO: adopt direct preference optimization
- DINM: detoxify via model editing using only one instance

**We will soon release codes for the above methods and offer some promising strategies and suggestions for this track**. If necessary, You can access these resources from [this link](https://github.com/zjunlp/EasyEdit/blob/main/examples/SafeEdit.md). 


<table>
  <tr>
    <td>Method</td>
    <td><center>Avg</td>
    <td><center>DGonlyQ</td>
    <td><center>DGotherAQ</td>
    <td><center>Fluency</td>
    <td><center>CommonsenseQA</td>
    <td><center>TriviaQA</td>
    <td><center>Xsum</td>
    <td><center>MMLU</td>
    <td><center>GSM8K</td>
  </tr>
  <tr>
    <td>Vanilla</td>
    <td><center>38.22</td>
    <td><center>80.00</td>
    <td><center>52.22</td>
    <td><center>5.78</td>
    <td><center>49.55</td>
    <td><center>45.39</td>
    <td><center>22.25</td>
    <td><center>36.07</td>
    <td><center>14.40</td>
  </tr>
  <tr>
    <td>SFT</td>
    <td><center>43.49</td>
    <td><center>85.19</td>
    <td><center>74.57</td>
    <td><center>4.21</td>
    <td><center>54.95</td>
    <td><center>39.84</td>
    <td><center>23.95</td>
    <td><center>42.69</td>
    <td><center>22.52</td>
  </tr>
  <tr>
    <td>DPO</td>
    <td><center>43.99</td>
    <td><center>85.19</td>
    <td><center>80.25</td>
    <td><center>4.20</td>
    <td><center>53.81</td>
    <td><center>37.26</td>
    <td><center>23.98</td>
    <td><center>43.86</td>
    <td><center>23.35</td>
  </tr>
  <tr>
    <td>DINM</td>
    <td><center>44.95</td>
    <td><center>93.33</td>
    <td><center>83.13</td>
    <td><center>6.26</td>
    <td><center>49.96</td>
    <td><center>44.31</td>
    <td><center>22.14</td>
    <td><center>45.15</td>
    <td><center>15.31</td>
  </tr>

</table>

 > ❗️❗️If conducting experiments using an A800 GPU, calculating the MMLU metric takes around 12 hours, while each of the other metrics only takes about 2 hours.

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

- **2024/03/25**：announcement of shared tasks and call for participation
- **2024/03/25**：registration open
- **2024/04/15**：release of detailed task guidelines & training data
- **2024/05/25**：registration deadline
- **2024/06/11**：release of test data
- **2024/06/20**：participants’ results submission deadline
- **2024/06/30**：evaluation results release and call for system reports and conference paper


## Leaderboard

#### Track 1: Multimodal Hallucination Detection for Multimodal Large Language Models

More information will be available shortly.

#### Track 2: Detoxifying Large Language Models

More information will be available shortly.


## 📖 Citation

Please cite our paper if you use our dataset.

```bibtex
@article{wang2024SafeEdit,
  author       = {Mengru Wang and
                  Ningyu Zhang and
                  Ziwen Xu and
                  Zekun Xi and
                  Shumin Deng and
                  Yunzhi Yao and
                  Qishen Zhang and
                  Linyi Yang and
                  Jindong Wang and
                  Huajun Chen},
  title        = {Detoxifying Large Language Models via Knowledge Editing},
  journal      = {CoRR},
  volume       = {abs/2403.14472},
  year         = {2024},
  url          = {https://doi.org/10.48550/arXiv.2403.14472},
  doi          = {10.48550/ARXIV.2403.14472}
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


