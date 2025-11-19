# baokhang.IT.web.com
Web của Khang
<!doctype html>
<html lang="vi">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Web của Khang ✨</title>
  <style>
    :root{
      --bg:#0f1724;
      --card:#111827;
      --accent:#7c3aed;
      --muted:#9ca3af;
      --glass: rgba(255,255,255,0.04);
      --radius:14px;
      font-family: Inter, ui-sans-serif, system-ui, -apple-system, "Segoe UI", Roboto;
    }
    *{box-sizing:border-box}
    body{
      margin:0;
      background: linear-gradient(180deg,#071028,#0f1724);
      color:#e6eef8;
      padding:24px;
      display:flex;
      justify-content:center;
      font-size:16px;
    }
    .wrap{
      width:100%;
      max-width:980px;
      display:grid;
      grid-template-columns:320px 1fr;
      gap:20px;
    }
    .card{
      background:rgba(255,255,255,0.03);
      border-radius:var(--radius);
      padding:18px;
      border:1px solid rgba(255,255,255,0.05);
    }
    .profile-pic{
      width:100%;
      aspect-ratio:1/1;
      border-radius:12px;
      object-fit:cover;
    }
    h1{font-size:20px;margin:12px 0 6px}
    p.muted{color:var(--muted);margin:0 0 12px;font-size:14px}
    .btn{
      display:inline-block;
      padding:8px 12px;
      border-radius:10px;
      background:var(--accent);
      color:white;
      font-weight:600;
      text-decoration:none;
      cursor:pointer;
      border:none;
    }
    textarea,input{
      width:100%;
      background:rgba(255,255,255,0.04);
      border:1px solid rgba(255,255,255,0.1);
      color:white;
      padding:10px;
      border-radius:10px;
      resize:none;
    }
    .posts{display:flex;flex-direction:column;gap:12px}
    .post{
      background:rgba(255,255,255,0.04);
      padding:12px;
      border-radius:12px;
    }
    .gallery{display:grid;grid-template-columns:repeat(auto-fill,minmax(120px,1fr));gap:8px}
    .gallery img{
      width:100%;height:100px;object-fit:cover;border-radius:10px;
    }
    @media(max-width:800px){.wrap{grid-template-columns:1fr}}
  </style>
</head>

<body>
<div class="wrap">

  <!-- LEFT SIDEBAR -->
  <aside class="card">
    <img id="profileImg" src="https://images.unsplash.com/photo-1535713875002-d1d0cf377fde?w=800&q=60" class="profile-pic">
    <h1 id="displayName">Khang</h1>
    <p class="muted" id="displayBio">Học sinh — web linh tinh, up ảnh, note, share cho bff ✌️</p>

    <hr style="margin:14px 0;opacity:0.2;">

    <h3 style="margin:0 0 6px">Gallery</h3>
    <div style="display:flex;gap:6px;margin-bottom:8px">
      <input id="imgUrl" placeholder="Dán URL ảnh...">
      <button id="addImg" class="btn" style="padding:6px 10px;font-size:13px">Add</button>
    </div>
    <div class="gallery" id="gallery"></div>

    <hr style="margin:14px 0;opacity:0.2;">

    <p class="muted" style="font-size:12px">Share link web:  
      <br><code id="shareLink"></code>
    </p>
  </aside>

  <!-- RIGHT CONTENT -->
  <main class="card">
    <h3 style="margin-top:0">Wall của Khang</h3>
    <textarea id="postText" placeholder="Viết gì đó..."></textarea>
    <input id="postImg" placeholder="URL ảnh (tùy chọn)">
    <button id="postBtn" class="btn" style="margin-top:10px;width:100%">Đăng</button>

    <div class="posts" id="posts" style="margin-top:20px"></div>
  </main>

</div>

<script>
  // share link
  document.getElementById("shareLink").textContent = window.location.href;

  // load posts
  let posts = JSON.parse(localStorage.getItem("posts") || "[]");
  renderPosts();

  // post
  document.getElementById("postBtn").onclick = () => {
    let text = postText.value.trim();
    let img = postImg.value.trim();

    if(!text) return;

    posts.unshift({text, img, time: new Date().toLocaleString()});
    localStorage.setItem("posts", JSON.stringify(posts));

    postText.value = "";
    postImg.value = "";

    renderPosts();
  };

  function renderPosts(){
    const box = document.getElementById("posts");
    box.innerHTML = "";
    posts.forEach(p => {
      let div = document.createElement("div");
      div.className = "post";
      div.innerHTML = `
        <p style="margin:0 0 6px;white-space:pre-wrap">${p.text}</p>
        ${p.img ? `<img src="${p.img}" style="width:100%;border-radius:10px;margin-top:6px">`: ""}
        <div style="font-size:12px;color:#9ca3af;margin-top:6px">${p.time}</div>
      `;
      box.appendChild(div);
    });
  }

  // gallery
  document.getElementById("addImg").onclick = () => {
    let url = imgUrl.value.trim();
    if(!url) return;
    gallery.innerHTML += `<img src="${url}">`;
    imgUrl.value = "";
  };
</script>

</body>
</html>
