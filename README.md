# baokhang.IT.web.com
<!doctype html>
<html lang="vi">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Web của Khang ✨</title>
  
  <!-- Nhạc nền -->
  <audio id="bgm" autoplay loop>
    <source src="https://files.catbox.moe/4p0m7p.mp3" type="audio/mpeg">
  </audio>
  
  <style>
    :root{
      --bg:#1d0b33;
      --card:#2a0e4a;
      --accent:#b26bff;
      --muted:#c7b7e8;
      --glass: rgba(255,255,255,0.06);
      --radius:16px;
      font-family: Inter, ui-sans-serif, system-ui;
    }
    *{box-sizing:border-box;transition:0.25s ease}
    body{
      margin:0;
      background:linear-gradient(180deg,#160628,#1d0b33);
      color:#f5eaff;
      padding:24px;
      display:flex;
      justify-content:center;
      animation:fadeIn 0.8s ease forwards;
      opacity:0;
    }
    @keyframes fadeIn{
      from{opacity:0;transform:translateY(10px);} to{opacity:1;transform:none;}
    }
    .wrap{
      width:100%;max-width:980px;
      display:grid;grid-template-columns:320px 1fr;
      gap:20px;
      animation:fadeIn 1s ease;
    }
    .card{
      background:var(--glass);
      border-radius:var(--radius);
      padding:18px;
      border:1px solid rgba(255,255,255,0.1);
      backdrop-filter:blur(12px);
    }
    .profile-pic{
      width:100%;aspect-ratio:1/1;border-radius:14px;object-fit:cover;
      box-shadow:0 0 20px rgba(178,107,255,0.3);
    }
    h1{font-size:22px;margin:12px 0 6px}
    p.muted{color:var(--muted);margin:0 0 12px;font-size:14px}
    .btn{
      padding:8px 12px;border-radius:12px;background:var(--accent);
      color:white;border:none;font-weight:600;cursor:pointer;
      box-shadow:0 4px 14px rgba(178,107,255,0.3);
    }
    textarea,input{
      width:100%;background:rgba(255,255,255,0.05);
      border:1px solid rgba(255,255,255,0.1);
      color:#f5eaff;padding:10px;border-radius:12px;
    }
    .posts{display:flex;flex-direction:column;gap:12px}
    .post{
      background:rgba(255,255,255,0.07);
      padding:12px;border-radius:12px;
      animation:fadeIn 0.4s ease;
    }
    .gallery{display:grid;grid-template-columns:repeat(auto-fill,minmax(120px,1fr));gap:10px}
    .gallery img{
      width:100%;height:100px;object-fit:cover;border-radius:12px;
      filter:brightness(0.9);
    }
    @media(max-width:800px){.wrap{grid-template-columns:1fr}}
  </style>
</head>

<body>
<div class="wrap">

  <!-- LEFT -->
  <aside class="card">
    <img id="profileImg" src="https://i.imgur.com/rJr6xTD.jpeg" class="profile-pic">
    <h1 id="displayName">Khang</h1>
    <p class="muted">Học sinh — web linh tinh, chill chill ✌️</p>

    <hr style="opacity:0.25;margin:14px 0;">

    <h3 style="margin:0 0 6px">Gallery</h3>
    <div style="display:flex;gap:6px;margin-bottom:8px">
      <input id="imgUrl" placeholder="Dán URL ảnh...">
      <button id="addImg" class="btn" style="padding:6px 10px;font-size:13px">Add</button>
    </div>
    <div class="gallery" id="gallery"></div>

    <hr style="opacity:0.25;margin:14px 0;">

    <p class="muted" style="font-size:12px">Share web: <br><code id="shareLink"></code></p>
  </aside>

  <!-- RIGHT -->
  <main class="card">
    <h3 style="margin-top:0">Wall của Khang</h3>
    <textarea id="postText" placeholder="Viết gì đó..."></textarea>
    <input id="postImg" placeholder="URL ảnh (tuỳ chọn)">
    <button id="postBtn" class="btn" style="margin-top:10px;width:100%">Đăng</button>
    <div class="posts" id="posts" style="margin-top:20px"></div>
  </main>
</div>

<script>
  document.getElementById("shareLink").textContent = location.href;

  let posts = JSON.parse(localStorage.getItem("posts") || "[]");
  renderPosts();

  postBtn.onclick = () => {
    let text = postText.value.trim();
    let img = postImg.value.trim();
    if(!text) return;
    posts.unshift({text, img, time: new Date().toLocaleString()});
    localStorage.setItem("posts", JSON.stringify(posts));
    postText.value = ""; postImg.value = "";
    renderPosts();
  };

  function renderPosts(){
    postsDiv = document.getElementById("posts");
    postsDiv.innerHTML = "";
    posts.forEach(p => {
      let div = document.createElement("div");
      div.className = "post";
      div.innerHTML = `
        <p style="margin:0 0 6px;white-space:pre-wrap">${p.text}</p>
        ${p.img ? `<img src="${p.img}" style="width:100%;border-radius:12px;margin-top:6px">`: ""}
        <div style="font-size:12px;color:#c7b7e8;margin-top:6px">${p.time}</div>
      `;
      postsDiv.appendChild(div);
    });
  }

  addImg.onclick = () => {
    let url = imgUrl.value.trim(); if(!url) return;
    gallery.innerHTML += `<img src="${url}">`;
    imgUrl.value = "";
  };
</script>

</body>
</html>

