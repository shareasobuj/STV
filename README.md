# STV 
<html lang="bn">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>EduTV - শিক্ষামূলক ভিডিও</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f4;
      margin: 0;
      padding: 0;
    }
    header {
      background-color: #333;
      color: white;
      text-align: center;
      padding: 10px 0;
    }
    nav {
      background-color: #444;
      overflow: hidden;
    }
    nav a {
      float: left;
      display: block;
      color: white;
      text-align: center;
      padding: 14px 20px;
      text-decoration: none;
    }
    nav a:hover {
      background-color: #ddd;
      color: black;
    }
    .video-container {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-around;
      padding: 20px;
    }
    .video-card {
      background-color: white;
      border-radius: 8px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
      margin: 10px;
      width: 300px;
      text-align: center;
    }
    .video-card video {
      width: 100%;
      border-radius: 8px;
    }
    .video-card h3 {
      margin: 10px 0;
      font-size: 18px;
    }
  </style>
</head>
<body>

<header>
  <h1>🎓 EduTV - শিক্ষামূলক ভিডিও</h1>
</header>

<nav>
  <a href="#">হোম</a>
  <a href="#">লগইন</a>
  <a href="#">সাইন আপ</a>
  <a href="#">অ্যাডমিন</a>
</nav>

<div class="video-container" id="videoContainer">
  <!-- ভিডিও কার্ড এখানে প্রদর্শিত হবে -->
</div>

<script>
  const videos = [
    { title: "ভিডিও ১", url: "https://www.learningcontainer.com/wp-content/uploads/2020/05/sample-mp4-file.mp4" },
    { title: "ভিডিও ২", url: "https://www.learningcontainer.com/wp-content/uploads/2020/05/sample-mp4-file.mp4" },
    { title: "ভিডিও ৩", url: "https://www.learningcontainer.com/wp-content/uploads/2020/05/sample-mp4-file.mp4" },
    { title: "ভিডিও ৪", url: "https://www.learningcontainer.com/wp-content/uploads/2020/05/sample-mp4-file.mp4" },
    { title: "ভিডিও ৫", url: "https://www.learningcontainer.com/wp-content/uploads/2020/05/sample-mp4-file.mp4" },
    { title: "ভিডিও ৬", url: "https://www.learningcontainer.com/wp-content/uploads/2020/05/sample-mp4-file.mp4" },
    { title: "ভিডিও ৭", url: "https://www.learningcontainer.com/wp-content/uploads/2020/05/sample-mp4-file.mp4" },
    { title: "ভিডিও ৮", url: "https://www.learningcontainer.com/wp-content/uploads/2020/05/sample-mp4-file.mp4" },
    { title: "ভিডিও ৯", url: "https://www.learningcontainer.com/wp-content/uploads/2020/05/sample-mp4-file.mp4" },
    { title: "ভিডিও ১০", url: "https://www.learningcontainer.com/wp-content/uploads/2020/05/sample-mp4-file.mp4" },
    { title: "ভিডিও ১১", url: "https://www.learningcontainer.com/wp-content/uploads/2020/05/sample-mp4-file.mp4" },
    { title: "ভিডিও ১২", url: "https://www.learningcontainer.com/wp-content/uploads/2020/05/sample-mp4-file.mp4" },
    { title: "ভিডিও ১৩", url: "https://www.learningcontainer.com/wp-content/uploads/2020/05/sample-mp4-file.mp4" },
    { title: "ভিডিও ১৪", url: "https://www.learningcontainer.com/wp-content/uploads/2020/05/sample-mp4-file.mp4" },
    { title: "ভিডিও ১৫", url: "https://www.learningcontainer.com/wp-content/uploads/2020/05/sample-mp4-file.mp4" },
    { title: "ভিডিও ১৬", url: "https://www.learningcontainer.com/wp-content/uploads/2020/05/sample-mp4-file.mp4" },
    { title: "ভিডিও ১৭", url: "https://www.learningcontainer.com/wp-content/uploads/2020/05/sample-mp4-file.mp4" },
    { title: "ভিডিও ১৮", url: "https://www.learningcontainer.com/wp-content/uploads/2020/05/sample-mp4-file.mp4" },
    { title: "ভিডিও ১৯", url: "https://www.learningcontainer.com/wp-content/uploads/2020/05/sample-mp4-file.mp4" },
    { title: "ভিডিও ২০", url: "https://www.learningcontainer.com/wp-content/uploads/2020/05/sample-mp4-file.mp4" }
  ];

  const videoContainer = document.getElementById('videoContainer');

  videos.forEach(video => {
    const videoCard = document.createElement('div');
    videoCard.classList.add('video-card');
    videoCard.innerHTML = `
      <video controls>
        <source src="${video.url}" type="video/mp4">
        আপনার ব্রাউজার ভিডিও ট্যাগ সমর্থন করে না।
      </video>
      <h3>${video.title}</h3>
    `;
    videoContainer.appendChild(videoCard);
  });
</script>
