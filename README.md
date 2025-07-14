# Algorithm Reporting Standard 
This repository contains a Reporting Standard for Algorithms. It consists out of a System Card which contains Model Cards and Assessment Cards.

## Introduction

Inspired by [Model Cards for Model Reporting](https://arxiv.org/abs/1810.03993) and
[Papers with Code Model Index](https://github.com/paperswithcode/model-index) this standard almost[^1] [^2] [^3] [^4]
extends the
[Hugging Face model card metadata specification](https://github.com/huggingface/hub-docs/blob/main/modelcard.md?plain=1)
to allow for:

1. More fine-grained information on performance metrics, by extending the `metrics_field` from the Hugging
   Face metadata specification.
2. Capturing additional *measurements* on fairness and bias, which can be partitioned into bar plot like
   measurements (such as mean absolute SHAP values) and graph plot like measurements (such as partial dependence). This
   is achieved by defining a new field `measurements`.
3. Capturing *assessments* (such as
   [IAMA](https://www.rijksoverheid.nl/documenten/rapporten/2021/02/25/impact-assessment-mensenrechten-en-algoritmes)
   and [ALTAI](https://digital-strategy.ec.europa.eu/en/library/assessment-list-trustworthy-artificial-intelligence-altai-self-assessment)).
   This is achieved by defining a new field `assessments`.

Following Hugging Face, this proposed standard will be written in YAML.

This standard does not contain all fields present in the Hugging Face metadata specification. The fields that are
optional in the Hugging Face specification and are specific to the Hugging Face interface are omitted.

Another difference is that we divide our implementation into three separate parts.

1. `system_card`, containing information about a group of ML-models which accomplish a specific task.
2. `model_card`, containing information about a specific data science model.
3. `assessment_card`, containing information about a regulatory assessment.

!!! note "Include statements"

    These `model_card`s and  `assessment_card`s  can be included verbatim into a `system_card`, or referenced with an
    `!include` statement, allowing for minimal cards to be compact in a single file. Extensive cards can be split up for
    readability and maintainability. Our standard allows for the `!include` to be used anywhere.

## Specification of the standard

The standard will be written in YAML. Example YAML files are given in the next section. The standard defines three
cards: a `system_card`, a `model_card` and an `assessment_card`. A `system_card` contains information about an
algorithmic system. It can have multiple models and each of these models should have a `model_card`. Regulatory
assessments can be processed in an `assessment_card`. Note that `model_card`'s and `assessment_card`'s can be included
directly into the `system_card` or can be included as separate YAML files with help of a YAML-include mechanism. For
clarity the latter is preferred and is also used in the examples in the next section.
