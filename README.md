# DesignLab

<input type="text" id="searchInput" placeholder="Tìm theo tên hoặc tag...">
<div id="gallery"></div>

let imageData = []; // Nơi lưu trữ dữ liệu từ file json

// 1. Tải dữ liệu từ file json
fetch('data.json')
  .then(response => response.json())
  .then(data => {
    imageData = data;
    displayImages(imageData); // Hiển thị tất cả ảnh lúc đầu
  });

// 2. Hàm hiển thị ảnh ra màn hình
function displayImages(images) {
  const gallery = document.getElementById('gallery');
  gallery.innerHTML = images.map(img => `
    <div class="image-card">
      <img src="${img.imageUrl}" alt="${img.name}" style="width:200px">
      <p>${img.name}</p>
      <span>${img.tags.join(', ')}</span>
    </div>
  `).join('');
}

// 3. Xử lý sự kiện tìm kiếm
document.getElementById('searchInput').addEventListener('input', (e) => {
  const keyword = e.target.value.toLowerCase();
  const filtered = imageData.filter(img => 
    img.name.toLowerCase().includes(keyword) || 
    img.tags.some(tag => tag.toLowerCase().includes(keyword))
  );
  displayImages(filtered);
});
