<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>역곡중 나무위키</title>
  <style>
    body {
      font-family: sans-serif;
      background-color: #f2f2f2;
      margin: 0;
      padding: 20px;
    }

    h1 {
      text-align: center;
      color: #2c3e50;
    }

    .plus-button {
      position: fixed;
      bottom: 20px;
      right: 20px;
      font-size: 30px;
      background-color: #27ae60;
      color: white;
      border: none;
      border-radius: 50%;
      width: 60px;
      height: 60px;
      cursor: pointer;
    }

    .form-container, .card {
      background-color: white;
      padding: 15px;
      margin: 15px auto;
      border-radius: 10px;
      max-width: 400px;
      box-shadow: 0 2px 6px rgba(0,0,0,0.2);
    }

    input, textarea, select {
      width: 100%;
      margin-bottom: 10px;
      padding: 8px;
      border-radius: 5px;
      border: 1px solid #ccc;
    }

    .upload-button {
      background-color: #3498db;
      color: white;
      padding: 10px;
      width: 100%;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    img {
      max-width: 100%;
      border-radius: 10px;
      margin-top: 10px;
    }

    .card h3 {
      margin-top: 0;
      color: #2c3e50;
    }
  </style>
</head>
<body>

<h1>역곡중 나무위키</h1>

<div id="container"></div>

<button class="plus-button" onclick="addForm()">+</button>

<script>
  function addForm() {
    const form = document.createElement('div');
    form.className = 'form-container';
    form.innerHTML = `
      <input type="file" accept="image/*" class="photo">
      <input type="text" placeholder="이름" class="name">
      <input type="text" placeholder="성격" class="personality">
      <input type="text" placeholder="닮은 사람" class="lookalike">
      <input type="text" placeholder="특징" class="features">
      <select class="boyfriend">
        <option value="">남친 유무</option>
        <option value="있음">있음</option>
        <option value="없음">없음</option>
      </select>
      <input type="text" placeholder="몇반인지" class="class">
      <textarea placeholder="업적" class="achievements"></textarea>
      <button class="upload-button" onclick="upload(this)">업로드</button>
    `;
    document.getElementById('container').prepend(form);
  }

  function upload(button) {
    const form = button.parentElement;
    const photoInput = form.querySelector('.photo');
    const name = form.querySelector('.name').value;
    const personality = form.querySelector('.personality').value;
    const lookalike = form.querySelector('.lookalike').value;
    const features = form.querySelector('.features').value;
    const boyfriend = form.querySelector('.boyfriend').value;
    const classNum = form.querySelector('.class').value;
    const achievements = form.querySelector('.achievements').value;

    const reader = new FileReader();
    reader.onload = function(event) {
      const card = document.createElement('div');
      card.className = 'card';
      card.innerHTML = `
        <img src="${event.target.result}">
        <h3>${name}</h3>
        <p><strong>성격:</strong> ${personality}</p>
        <p><strong>닮은 사람:</strong> ${lookalike}</p>
        <p><strong>특징:</strong> ${features}</p>
        <p><strong>남친 유무:</strong> ${boyfriend}</p>
        <p><strong>반:</strong> ${classNum}</p>
        <p><strong>업적:</strong><br>${achievements.replace(/\n/g, "<br>")}</p>
      `;
      document.getElementById('container').appendChild(card);
      form.remove(); // 폼 제거
    };

    if (photoInput.files[0]) {
      reader.readAsDataURL(photoInput.files[0]);
    } else {
      alert("사진을 업로드하세요!");
    }
  }
</script>

</body>
</html>
