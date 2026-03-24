## 📄 Paper Review

### DSEG-LIME: Explaining Image Segmentation Models Using Local Interpretable Model-Agnostic Explanations

---

## 1. Background

### LIME

LIME(Local Interpretable Model-agnostic Explanations)은  
모델의 예측 결과를 **국소적(local) 관점에서 설명**하는 대표적인 XAI 기법이다.

#### 🔹 핵심 아이디어
- 입력 데이터를 일부 변형(perturbation)하여 모델 출력 변화 관찰
- 이를 기반으로 단순한 선형 모델로 근사하여 설명 생성

#### 🔹 기존 적용 방식
- 주로 **이미지 분류(classification)** 문제에 사용
- superpixel 단위로 입력을 분할 후 중요도 분석

---

## 2. Problem

기존 LIME은 **이미지 분할(Segmentation) 모델**에 그대로 적용하기 어려움

### ❗ 주요 문제점

1. **픽셀 단위 출력 문제**
   - segmentation은 픽셀 단위 예측 → LIME과 구조 불일치

2. **Superpixel 한계**
   - segmentation 결과와 superpixel 경계가 일치하지 않음

3. **설명 왜곡**
   - 중요한 영역이 정확히 반영되지 않을 수 있음

4. **계산 비용 증가**
   - 픽셀 단위 perturbation은 비효율적

---

## 3. Proposed Method: DSEG-LIME

DSEG-LIME은 segmentation 모델을 설명하기 위해  
**LIME을 segmentation 구조에 맞게 확장한 방법**

---

## 4. Method

### 4.1 Segmentation-aware Perturbation

- 기존 superpixel 대신  
  **segmentation 결과 기반 영역 단위 perturbation 적용**

👉 효과:
- 모델 출력 구조와 일치
- 의미 있는 영역 단위 설명 가능

---

### 4.2 Pixel-level Explanation Aggregation

- 픽셀 단위 예측을 그룹화하여  
  **설명 가능한 단위로 재구성**

👉 효과:
- 해석 가능성 증가
- noise 감소

---

### 4.3 Local Surrogate Model

- perturbation된 데이터로  
  **local surrogate model 학습**

👉 핵심:
- 특정 이미지/영역에 대한 **국소적 설명 생성**

---

### 4.4 Importance Score Mapping

- 각 영역에 대해 중요도 점수 계산
- heatmap 형태로 시각화

👉 효과:
- 모델이 어떤 영역을 기반으로 판단했는지 직관적으로 확인 가능

---

## 5. Key Idea Summary

### ✔ 기존 LIME 한계
- segmentation과 구조 불일치
- superpixel 기반 설명의 부정확성

### ✔ DSEG-LIME 개선
- segmentation-aware perturbation
- pixel-level → region-level 설명 변환
- local surrogate 기반 설명 유지

---

## 6. Result

- segmentation 모델에 대한 **해석 가능성 향상**
- 기존 LIME 대비 더 정확한 중요 영역 추출
- 시각적으로 일관된 explanation 제공

👉 핵심 성과:
- segmentation 모델에도 적용 가능한 XAI 방법 제안
- 모델의 decision boundary를 직관적으로 해석 가능

---

## 7. Conclusion

DSEG-LIME은 기존 LIME의 한계를 보완하여  
**segmentation 모델에 적합한 설명 방법을 제안한 연구**

특히,
- 모델 구조에 맞춘 perturbation 설계
- 해석 가능성과 정확도를 동시에 개선

---

## 8. My Insight

- XAI는 단순히 “설명”이 아니라  
  **모델 구조에 맞게 재설계되어야 함**
- segmentation과 classification은  
  설명 방식 자체가 달라야 함을 확인

👉 extension:
- 의료 데이터를 적용하여 실험 해봄 (추후 보완이 더 필요함)
