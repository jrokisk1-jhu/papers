## [Linguistic Nepotism: Trading-off Quality for Language Preference in Multilingual RAG](https://arxiv.org/abs/2509.13930)
* Khashabi & Duh authors
* Multilingual Retrieaval-Augmented Generation (MRAG)
* 8 languages, 6 open weight models
* **multi-lingual models favor english documents for english queries even when they are not the most relevant**
* they use machine translate to generate documents in multiple languages
* models favor documents in the same language as the query

## [Where does In-context Learning Happen in Large Language Models?](https://www.cs.jhu.edu/~kevinduh/papers/sia24where.pdf)
* Duh author
* **"we demonstrate evidence of a "task recognition" point where the task is encoded into the input representations and attention to context is no longer necessary"**
* potential to make model more efficient as you can ignore some of the input once the task has been identified
* "Models do not need to maintain attention over the task context past a certain layer to perform the task."
* **"Our central finding that models do not need to maintain attention over all of the context across every layer has direct implications for inference efficiency of transformers, with estimated up to 45% cost-savings for llama model with 5 examples (Section 5)."**

## [Google Translate’s Research Submission to WMT2025](https://aclanthology.org/2025.wmt-1.48.pdf)
* Started with Gemma 3 27B model. SFT on available datasets and high quality synthetic data. Also RL.
* Used Gemma Kauldron SFT tooling
* SMOL and GATITOS datasets used in SFT stage
* MetricX-24-XXL, CHRF, Comet22
* languages in dataset improved, those not in dataset got worse
* generic gemma instruction dataset was included to ensure that it did not forget how to perform those tasks
* token level and sequence level scores were used in the RL process

## [Error Span Annotation: A Balanced Approach for Human Evaluation of Machine Translation](https://arxiv.org/abs/2406.11580)
* Introduced a new user interface for scoring MT tasks. The idea being that it is more consistent than direct assessment (DA) and not as burdensome as MQM
* **"To this end, we propose, describe, and analyze Error Span Annotation (ESA), which builds on top of previous protocols to enable economic evaluation at scale. It works by asking the annotators to mark error spans, but with only the error severities and not types. In contrast to MQM, we also solicit final translation score. This is more reliable than DA+SQM, as the annotators are primed and informed about the translation errors to assess quality of longer documents"**

## [MetricX-24: The Google Submission to the WMT 2024 Metrics Shared Task](https://arxiv.org/abs/2410.03983)
* **"Our primary submission is a hybrid referencebased/-free metric, which can score a translation irrespective of whether it is given the source segment, the reference, or both. The metric is trained on previous WMT data in a two-stage fashion, first on the DA ratings only, then on a mixture of MQM and DA ratings."**
* "MetricX is a learned regression-based metric trained to predict a floating point score representing the quality of a translation"

## [CHRF: character n-gram F-score for automatic MT evaluation](https://aclanthology.org/W15-3049.pdf)
* **"We propose the use of character n-gram F-score for automatic evaluation of machine translation output."**

## [MADLAD-400: A Multilingual And Document-Level Large Audited Dataset](https://arxiv.org/pdf/2309.04662)
* **"We introduce MADLAD-400, a manually audited, general domain 3T token monolingual dataset based on CommonCrawl, spanning 419 languages. We discuss the limitations revealed by self-auditing MADLAD-400, and the role data auditing had in the dataset creation process"**
* very large MT dataset
* good discussion with how it was made and other datasets
* trained a model on the dataset and ran comparisons

## [BLEU: a Method for Automatic Evaluation of Machine Translation](https://aclanthology.org/P02-1040.pdf)
* defines the BLEU metric
* builds it up from first principles
* presents challenges to the metric and shows how they are addressed
* n-gram here uses tokens
* shown to be comparable to human translators but from 2002!

## [Experts, Errors, and Context: A Large-Scale Study of Human Evaluation for Machine Translation](https://arxiv.org/pdf/2104.14478)
* compares human crowdworker results to MQM. Low correlation between the two
* "the field still lacks a commonlyaccepted standard procedure"
* from 2021
* "Surprisingly, we also find that automatic metrics based on pre-trained embeddings can outperform human crowd workers."
* CLAUDE: "it is the proximate cause for the Metrics Shared Task"
* "Our study shows that crowd-worker human evaluations (as conducted by WMT) have low correlation with MQM, and the resulting systemlevel rankings are quite different. This finding questions previous conclusions made on the basis of crowd-worker human evaluation, especially for high-quality MT. We further come to the surprising finding that many automatic metrics, and in particular embedding-based ones, already outperform crowd-worker human evaluation"

## [Marco Large Translation Model at WMT2025: Transforming Translation Capability in LLMs via Quality-Aware Training and Decoding](https://aclanthology.org/2025.wmt-1.33.pdf)
* strong submission to WMt2025. first place in 6 categories, second in 4, third in 2
* outlines a training pipeline that goes:
  - filter dataset so its only high quality data using Comet XXL
  - perform SFT on high quality data
  - Use very large deepseek model to generate translations for the low quality data
  - perform SFT on the low quality data
  - Perform RL (CPO) on a mix of DeepSeek and SFT'd models output
  - Perform RL (multi reward optimization with self distillation) **NOTE: WHAT IS THIS?**
  - Use special decoding strategy
* The learning rate decreases across each stage of this pipeline. **Note: this is an interesting approach.**
* **QUESTION: need to investigate the RL approaches**
* **QUESTION: if the teacher model works so well, why not just use that?**

## [M2PO: Multi-Perspective Multi-Pair Preference Optimization for Machine Translation](https://aclanthology.org/2026.acl-long.469/)
* interesting combination of multiple current approaches
* goal is to identify "fine-grained" errors via preference optimization
* "QE models over prioritize surface level fluency"
* introduce **Coverage Score**: "quantifies the proportion of source semantic units preserved in translation."
* "Crucially, even when unfaithful translations appear linguistically fluent, the model’s internal probability distribution reveals underlying uncertainty (“lying with hesitation”). This empirical evidence confirms that the model’s internal belief can serve as a reliable regularizer against external reward blind spots, a key insight driving our M2PO framework."
* "This hierarchical coupling creates a gradient of difficulty, ranging from clear quality gaps to subtle “hard negatives” (e.g., Pair-2) that demand deeper discrimination." | I think the goal is to find clear tricky pairs. Pair best wiht worst (easy) and middle with middle (like tournament bracket).
* better than CPO is the claim 

## [Findings of the WMT 2026 Shared Task on Model Compression: No Free Lunch at Extreme Compression(https://aclanthology.org/2026.wmt-main.52/)
* post training quant is the winner
* constrained (gemma3-12b) vs unconstrained (no data limits <20b). Could be good for us to target
* aya expanse used. Look into!
* int-4 weight only and FP8 weight activation is the "dependable recipe"

## [Findings of the WMT26 Multilingual Instruction Shared Task: Small Models Are Not Yet Polyglots](https://aclanthology.org/2026.wmt-main.50/)
* small models (<10B) on three different tasks across languages with different levels of resources
* dominant approach is peft but different base models, training data, and inference
* "without explicit penalties for language drift, models frequently default to English leakage, fundamentally failing the cross-lingual objective"

## [Qingqiu-MT-9B: An Instruction-Following Multilingual Translation Model](https://aclanthology.org/2026.wmt-main.83.pdf)
* two stage sft: first stage lots of medium qualtiy data, second stage higher quality data
* stage 1 has 4 million examples, 500k for stage 2. 500k for RL
* RL stage after the SFT. uses GRPO.
* Learning rates decline after the first stage. 2e-5 -> 2e-6 for last two
* synthetic data is used
* 16 gpu training via ms-swift

## [Qwen-MT-Lumen at WMT2026: Instruction-Specialized Translation via Quality-Aware Training and On-Policy Distillation](https://arxiv.org/pdf/2610.19758)
* four stage pipeline: continued pre training and sft, m2po (online), on policy distlillation transfers, postprocessing error checking and formatting
* each pipeline stage gets its own section
* <20b parameters and competitive with larger models at wmt26
* focus on translation quality given specialized instructions (e.g., translate this in this specific voice or for this specific context)
* instruction data built with llm-assisted synthesis pipeline
* 14B parameter model
