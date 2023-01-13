---
layout: model
title: Spanish DistilBertForQuestionAnswering Base Uncased model (from CenIA)
author: John Snow Labs
name: distilbert_qa_distillbert_base_uncased_finetuned_s_c
date: 2023-01-03
tags: [es, open_source, distilbert, question_answering, tensorflow]
task: Question Answering
language: es
edition: Spark NLP 4.3.0
spark_version: 3.0
supported: true
engine: tensorflow
article_header:
  type: cover
use_language_switcher: "Python-Scala-Java"
---

## Description

Pretrained DistilBertForQuestionAnswering model, adapted from Hugging Face and curated to provide scalability and production-readiness using Spark NLP. `distillbert-base-spanish-uncased-finetuned-qa-sqac` is a Spanish model originally trained by `CenIA`.

{:.btn-box}
<button class="button button-orange" disabled>Live Demo</button>
<button class="button button-orange" disabled>Open in Colab</button>
[Download](https://s3.amazonaws.com/auxdata.johnsnowlabs.com/public/models/distilbert_qa_distillbert_base_uncased_finetuned_s_c_es_4.3.0_3.0_1672774780047.zip){:.button.button-orange.button-orange-trans.arr.button-icon}

## How to use



<div class="tabs-box" markdown="1">
{% include programmingLanguageSelectScalaPythonNLU.html %}
```python
Document_Assembler = MultiDocumentAssembler()\
     .setInputCols(["question", "context"])\
     .setOutputCols(["document_question", "document_context"])

Question_Answering = DistilBertForQuestionAnswering.pretrained("distilbert_qa_distillbert_base_uncased_finetuned_s_c","es")\
     .setInputCols(["document_question", "document_context"])\
     .setOutputCol("answer")\
     .setCaseSensitive(True)
    
pipeline = Pipeline(stages=[Document_Assembler, Question_Answering])

data = spark.createDataFrame([["What's my name?","My name is Clara and I live in Berkeley."]]).toDF("question", "context")

result = pipeline.fit(data).transform(data)
```
```scala
val Document_Assembler = new MultiDocumentAssembler()
     .setInputCols(Array("question", "context"))
     .setOutputCols(Array("document_question", "document_context"))

val Question_Answering = DistilBertForQuestionAnswering.pretrained("distilbert_qa_distillbert_base_uncased_finetuned_s_c","es")
     .setInputCols(Array("document_question", "document_context"))
     .setOutputCol("answer")
     .setCaseSensitive(true)
    
val pipeline = new Pipeline().setStages(Array(Document_Assembler, Question_Answering))

val data = Seq("What's my name?","My name is Clara and I live in Berkeley.").toDS.toDF("question", "context")

val result = pipeline.fit(data).transform(data)
```
</div>

{:.model-param}
## Model Information

{:.table-model}
|---|---|
|Model Name:|distilbert_qa_distillbert_base_uncased_finetuned_s_c|
|Compatibility:|Spark NLP 4.3.0+|
|License:|Open Source|
|Edition:|Official|
|Input Labels:|[document_question, document_context]|
|Output Labels:|[answer]|
|Language:|es|
|Size:|250.6 MB|
|Case sensitive:|false|
|Max sentence length:|512|

## References

- https://huggingface.co/CenIA/distillbert-base-spanish-uncased-finetuned-qa-sqac