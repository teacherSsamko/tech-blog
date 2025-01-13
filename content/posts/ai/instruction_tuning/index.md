---
title: "Instruction Tuning 이해하기"
date: 2025-01-13
draft: false
tags: ["ai", "instruction tuning"]
categories: ["ai"]
ShowToc: true
TocOpen: true
---



# Instruction Tuning 이해하기: AI 학습의 새로운 패러다임

이번 포스트에서는 AI 분야에서 매우 중요한 개념인 Instruction Tuning에 대해 알아보도록 하겠습니다.

## Instruction Tuning이란?

Instruction Tuning은 AI 모델이 사람의 자연어 명령어를 이해하고 그에 따라 적절한 응답을 생성할 수 있도록 학습시키는 방법입니다. 쉽게 말해서, AI에게 "이것을 해줘"라고 말했을 때 그것을 이해하고 수행할 수 있게 만드는 훈련 방법이라고 할 수 있죠.

## 왜 필요한가?

기존의 언어 모델은 다음 단어를 예측하는 방식(Next Word Prediction)으로 학습되었습니다. 예를 들어 "나는 학교에 ___"라는 문장이 있으면 "간다"라는 단어를 예측하는 식이죠. 하지만 이런 모델은 특정 작업을 수행하라는 명령을 이해하고 실행하는 데는 한계가 있었습니다.

Instruction Tuning은 이러한 한계를 극복하고, AI가 다음과 같은 일들을 할 수 있게 만듭니다:
- "이 텍스트를 한국어로 번역해줘"
- "이 수학 문제를 풀어줘"
- "이 글의 감정을 분석해줘"

## Instruction Tuning의 과정

Instruction Tuning의 과정은 크게 다음과 같습니다:

1. **기본 모델 준비**: 먼저 GPT-4처럼 대규모 텍스트 데이터로 사전 학습된 언어 모델을 준비합니다.

2. **명령어 데이터셋 구성**: 다양한 명령어와 그에 대한 적절한 응답 쌍을 수집합니다. 
   예시) 
   - 명령어: "이 문장을 긍정적으로 바꿔줘"
   - 입력: "오늘 날씨가 좋지 않다"
   - 응답: "내일은 더 좋은 날씨가 될 거야"
   ```json
   [
     {'inputData': "Question: 다음 문장을 한글로 번역해줘: hello, world! Answer: 안녕, 세계!", 'label': "Answer: 안녕, 세계!"},
     {'inputData': "Question: 1+1은 얼마입니까? Answer: 답은 2입니다.", 'label': "Answer: 답은 2입니다."},
     ...
   ]
   ```

3. **Fine-tuning**: 준비된 명령어-응답 쌍으로 모델을 추가 학습시킵니다.

## Instruction Tuning의 장점

1. **자연스러운 상호작용**: 사람이 일상적으로 사용하는 언어로 AI와 소통할 수 있습니다.

2. **다목적성**: 하나의 모델로 번역, 요약, 질문 답변 등 다양한 작업을 수행할 수 있습니다.

3. **적응성**: 새로운 유형의 작업에도 적절히 대응할 수 있는 능력이 생깁니다.

## 실제 응용 사례

- **ChatGPT**: OpenAI의 대화형 AI 모델
- **Claude**: Anthropic의 AI 어시스턴트
- **Bard**: Google의 대화형 AI 시스템

이러한 AI 시스템들은 모두 Instruction Tuning을 통해 사용자의 다양한 요구사항을 이해하고 처리할 수 있게 되었습니다.

## 앞으로의 발전 방향

Instruction Tuning은 계속해서 발전하고 있으며, 특히 다음과 같은 방향으로 연구가 진행되고 있습니다:

- 더 복잡한 작업의 수행 능력 향상
- 여러 단계가 필요한 작업의 처리 능력 개선
- 더 정확하고 안전한 응답 생성

## QnA

Q: 왜 InputData에 질문과 응답을 모두 넣어야 하나요? InputData에는 질문만 넣고, label에는 응답만 넣으면 안되나요?

A: 
### Question과 Answer를 모두 Input에 넣는 이유

1.	Context 유지
   - LLM은 기본적으로 문맥을 이해하고, 문맥을 기반으로 다음 토큰을 예측하는 방식으로 동작합니다.
   - Question과 Answer를 함께 Input으로 제공하면 모델이 문맥을 자연스럽게 파악하며, 질문에 따른 답변의 연관성을 학습할 수 있습니다.
   - 특히, Instruction-tuning의 목표는 “Instruction(질문)에 따라 올바른 Output(답변)을 생성하는 능력”을 강화하는 것이므로, 둘을 함께 학습하는 것이 중요합니다.
2.	답변의 구조와 형식을 학습
   - 모델이 질문에 맞는 답변의 형식과 톤을 학습하려면, 질문과 답변을 한 세트로 제공하는 것이 더 효과적입니다.
   - 예를 들어, 특정 질문이 “숫자” 형태의 답변을 요구하거나, “설명” 형태를 요구하는 것을 학습하려면, 질문과 답변의 쌍이 필요합니다.
3.	실제 사용 시 자연스러운 Generative Task를 반영
   - Instruction-tuning의 목적은 모델이 사용자의 질문에 대해 자연스럽게 답을 생성하게 하는 것입니다.
   - Question과 Answer를 Input으로 함께 학습하면, 모델은 질문을 보고 자연스럽게 답변을 이어서 생성하는 패턴을 학습하게 됩니다.

### Question만 Input에 넣고, Answer만 label에 넣는 방식

이 방식은 일반적인 supervised learning에서 사용되는 접근법이지만, Instruction-tuning에서는 적합하지 않을 수 있습니다. 이유는 다음과 같습니다:
1.	Generative Model의 특성
   - LLM은 분류(Classification)가 아닌 생성(Generation)에 초점이 맞춰져 있습니다.
   - Question만 Input에 넣고 Answer를 Label로 설정하면, 모델이 “다음 토큰을 예측”하는 대신 “질문 → 답변”의 전체적인 흐름을 학습하기 어렵습니다.
2.	문맥 정보의 단절
   - Question과 Answer가 분리되면 모델은 질문과 답변의 연결성을 충분히 이해하지 못할 가능성이 있습니다.
   - 예를 들어, “1+1은 얼마입니까?“라는 질문에 대해 “2”라는 답변만 학습한다면, “이 답변이 어떤 질문과 관련이 있는지”를 맥락적으로 학습하기 어렵습니다.
3.	미세 조정(Fine-tuning)의 제한
   - Instruction-tuning은 모델이 다양한 형태의 질문과 답변 쌍을 학습하도록 설계됩니다.
   - Answer를 Label로 설정하면, 정답이 고정된 문제에만 적합하며, 창의적이고 개방적인 답변을 학습하기 어려워집니다.

### 결론
- Question과 Answer를 함께 Input에 넣는 방식은 모델이 문맥과 답변의 연관성을 학습하고, 실제 사용 환경에서 자연스럽게 동작하도록 만드는 데 효과적입니다.
- Answer를 Label로 분리하면 정답이 고정된 문제(예: 분류)에서는 유용할 수 있으나, 생성 모델의 학습 목적과는 거리가 멀기 때문에 적합하지 않습니다.