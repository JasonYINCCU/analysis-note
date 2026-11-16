# AGENTS.md — 학부 해석학(Real Analysis) 강의 노트 프로젝트 지침서

## 1. 프로젝트 목적
본 프로젝트는 대학교 수학과 및 이공계 학부생을 위한 **해석학(Real Analysis) 온라인 강의 노트**입니다.
모든 강의 페이지는 수학 전공 서적(LaTeX `amsthm` 스타일)과 같은 일관된 시각적 구조와 엄밀한 논리 흐름(정의 → 정리 → 증명 → 예제)을 유지해야 합니다.

---

## 2. 디렉토리 구조 및 파일 명명 규칙
AI가 파일을 생성하거나 수정할 때는 반드시 아래 구조를 따릅니다.

- `index.html`: 메인 랜딩 페이지 및 전체 강의 목차(Syllabus)
- `assets/style.css`: 전역 스타일시트 (임의로 인라인 스타일을 남발하지 말 것)
- `lectures/NN-topic-slug.html`: 개별 강의 노트 페이지
  - `NN`: 두 자리 숫자의 강의 번호 (예: `01`, `02`, `03`...)
  - `topic-slug`: 영문 소문자와 하이픈(`-`)으로 구성된 핵심 주제명 (예: `01-completeness.html`, `02-sequences.html`, `03-continuity.html`)

---

## 3. 수식 렌더링 규칙 (KaTeX)
모든 수학 기호와 수식은 **KaTeX**를 사용하여 렌더링합니다.
- 모든 강의 HTML의 `<head>`에는 반드시 `index.html`과 동일한 KaTeX CDN 스크립트를 포함해야 합니다.
- **인라인 수식**: `$ ... $` 사용 (예: `$\varepsilon > 0$`, `$x \in \mathbb{R}$`)
- **블록 수식**: `$$ ... $$` 사용 (중요한 식이나 여러 줄의 부등식 전개 시 사용)
- 자주 쓰는 표준 기호 표기법을 통일합니다:
  - 집합: `\mathbb{N}`, `\mathbb{Z}`, `\mathbb{Q}`, `\mathbb{R}`
  - 엡실론-델타: `\varepsilon` (`\epsilon` 대신 사용), `\delta`
  - 상한/하한: `\sup`, `\inf`

---

## 4. 콘텐츠 블록 및 디자인 규칙
강의 본문은 개념의 성격에 따라 반드시 `assets/style.css`에 정의된 전용 클래스를 사용해야 합니다.

1. **정의 (`<div class="math-box definition">`)**
   - 새로운 수학적 개념이나 용어를 도입할 때 사용합니다.
   - 내부 제목 형식: `<div class="box-title">정의 1.1 (상계와 상한)</div>`
2. **정리 / 보조정리 (`<div class="math-box theorem">`)**
   - 증명이 필요한 핵심 명제나 정리를 서술할 때 사용합니다.
   - 내부 제목 형식: `<div class="box-title">정리 1.2 (상한의 $\varepsilon$-특성화)</div>`
3. **증명 (`<div class="proof-box">`)**
   - 정리 바로 아래에 배치하며, 증명 끝에는 자동으로 우측 하단에 사각형 기호($\blacksquare$)가 표시됩니다.
   - 내부 시작 형식: `<span class="proof-label">증명.</span>`
4. **예제 (`<div class="math-box example">`)**
   - 정의나 정리의 직관적 이해를 돕는 구체적인 계산·반례를 제시할 때 사용합니다.
   - 내부 제목 형식: `<div class="box-title">예제 1.3</div>`

---

## 5. 새 강의 페이지 추가 시 AI 필수 체크리스트
사용자가 새로운 강의(예: "제2강 수열의 극한 페이지 추가해 줘")를 요청하면 AI는 다음 **4단계**를 빠짐없이 수행해야 합니다.

1. **강의 파일 생성**: `lectures/NN-topic-slug.html` 경로에 아래 표준 HTML 템플릿을 기반으로 새 파일을 생성합니다.
2. **목차 업데이트 (`index.html`)**: `index.html`의 `<ul class="lecture-list">` 내부에 새 강의로 연결되는 카드(`<li>`)를 순서에 맞게 추가합니다.
3. **이전/다음 강 네비게이션 연결**: 새 강의 페이지 하단의 `.lecture-nav`에 이전 강 링크를 연결하고, 직전 강의 파일의 `.lecture-nav`에도 새로 추가된 다음 강 링크를 업데이트합니다.
4. **단원 번호 일관성 유지**: 제 $N$강의 모든 정의·정리·예제 번호는 `N.1`, `N.2`, `N.3` 순서대로 매깁니다.

---

## 6. 새 강의 페이지 표준 템플릿
```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>제N강. 강의 제목 | 학부 해석학 강의 노트</title>
  <link rel="stylesheet" href="../assets/style.css">
  <link rel="stylesheet" href="[https://cdn.jsdelivr.net/npm/katex@0.16.11/dist/katex.min.css](https://cdn.jsdelivr.net/npm/katex@0.16.11/dist/katex.min.css)">
  <script defer src="[https://cdn.jsdelivr.net/npm/katex@0.16.11/dist/katex.min.js](https://cdn.jsdelivr.net/npm/katex@0.16.11/dist/katex.min.js)"></script>
  <script defer src="[https://cdn.jsdelivr.net/npm/katex@0.16.11/dist/contrib/auto-render.min.js](https://cdn.jsdelivr.net/npm/katex@0.16.11/dist/contrib/auto-render.min.js)"
    onload="renderMathInElement(document.body, {
      delimiters: [
        {left: '$$', right: '$$', display: true},
        {left: '$', right: '$', display: false}
      ]
    });"></script>
</head>
<body>
  <header class="site-header">
    <div class="container">
      <a href="../index.html" class="brand">Real Analysis Notes</a>
      <nav><a href="../index.html">전체 목차</a></nav>
    </div>
  </header>

  <main class="container lecture-content">
    <div class="lecture-meta">Chapter N · 핵심 키워드</div>
    <h1>제N강. 강의 제목</h1>
    <p class="lecture-summary">이번 강의의 학습 목표와 핵심 개념 요약</p>
    <hr>

    <!-- 여기에 .math-box (definition, theorem, example) 및 .proof-box 작성 -->

    <div class="lecture-nav">
      <a href="이전강의.html">← 이전 강</a>
      <a href="../index.html">목차로 돌아가기</a>
      <span class="disabled">다음 강 →</span>
    </div>
  </main>

  <footer class="site-footer">
    <div class="container">Undergraduate Real Analysis Lecture Notes</div>
  </footer>
</body>
</html>

