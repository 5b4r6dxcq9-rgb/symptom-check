# symptom-check
증상을 선택하면 가능성 있는 질병 범주를 안내하는 참고용 건강 정보 웹사이트
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>증상 기반 질병 예측 사이트</title>
  <meta name="description" content="증상을 선택하면 가능성 있는 질병 범주를 안내하는 참고용 건강 정보 사이트입니다.">
  <meta name="robots" content="index, follow">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f4f6f8;
      padding: 20px;
    }
    h1 { text-align: center; }
    .container {
      max-width: 700px;
      margin: auto;
      background: #fff;
      padding: 20px;
      border-radius: 10px;
    }
    .symptom { margin: 6px 0; }
    button {
      margin-top: 20px;
      padding: 10px 20px;
      font-size: 16px;
    }
    .result {
      margin-top: 20px;
      padding: 15px;
      background: #eef;
      border-radius: 8px;
    }
    .warning {
      color: red;
      font-weight: bold;
    }
  </style>
</head>

<body>

<h1>증상 기반 질병 예측 사이트</h1>

<div class="container">
  <h3>증상을 선택하세요</h3>

  <div class="symptom"><input type="checkbox" value="발열"> 37.5℃ 이상 발열</div>
  <div class="symptom"><input type="checkbox" value="기침"> 기침 또는 인후통</div>
  <div class="symptom"><input type="checkbox" value="근육통"> 근육통</div>
  <div class="symptom"><input type="checkbox" value="피로"> 심한 피로</div>
  <div class="symptom"><input type="checkbox" value="복통"> 복통</div>
  <div class="symptom"><input type="checkbox" value="설사"> 설사 또는 구토</div>
  <div class="symptom"><input type="checkbox" value="호흡곤란"> 호흡 곤란</div>
  <div class="symptom"><input type="checkbox" value="가슴통증"> 가슴 통증</div>
  <div class="symptom"><input type="checkbox" value="두통"> 두통 또는 어지러움</div>
  <div class="symptom"><input type="checkbox" value="발진"> 발진 또는 가려움</div>

  <button onclick="predict()">결과 확인</button>
  <div id="result" class="result"></div>
</div>

<script>
function predict() {
  const checked = [...document.querySelectorAll("input:checked")]
                  .map(c => c.value);

  let results = [];

  if (checked.includes("발열") && checked.includes("기침")) {
    results.push("감기 또는 독감 등 상기도 감염 가능성");
  }
  if (checked.includes("발열") && checked.includes("근육통") && checked.includes("피로")) {
    results.push("인플루엔자(독감) 의심");
  }
  if (checked.includes("복통") && checked.includes("설사")) {
    results.push("급성 위장염 가능성");
  }
  if (checked.includes("호흡곤란") && checked.includes("가슴통증")) {
    results.push("⚠ 의료기관 즉시 방문 권장");
  }

  if (checked.length <= 1) {
    results.push("일시적 증상일 수 있으며 경과 관찰이 필요할 수 있음");
  }
  if (checked.length >= 4) {
    results.push("여러 증상이 동반됨 → 의료 전문가 상담 권장");
  }
  if (results.length === 0) {
    results.push("선택된 증상만으로는 판단이 어려움");
  }

  document.getElementById("result").innerHTML =
    "<ul>" + results.map(r => `<li>${r}</
