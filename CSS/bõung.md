## Thanh điều hướng
```
ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
  overflow: hidden;
  background-color: #333;
}

li {
  float: left;
}

li a {
  display: block;
  color: white;
  text-align: center;
  padding: 14px 16px;
  text-decoration: none;
}

li a:hover:not(.active) {
  background-color: #111;
}

.active {
  background-color: #4CAF50;
}
```
- thanh điều hướng này ta dùng thẻ `<ul>` và `<li>` có thuộc tính `display: block` tạo thành các khối 
- `.active` dùng tạo lớp đang hoạt động khi di chuyển trỏ chuột
- `li a:hover:not(.active)` thay đổi màu khi chuyển chuột
## Trình thả xuống
```
<!DOCTYPE html>
<html>
<head>
<style>
.dropbtn {
  background-color: #4CAF50;
  color: white;
  padding: 16px;
  font-size: 16px;
  border: none;
  cursor: pointer;
}

.dropdown {
  position: relative;
  display: inline-block;
}

.dropdown-content {
  display: none;
  position: absolute;
  background-color: #f9f9f9;
  min-width: 160px;
  box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
  z-index: 1;
}

.dropdown-content a {
  color: black;
  padding: 12px 16px;
  text-decoration: none;
  display: block;
}

.dropdown-content a:hover {background-color: #f1f1f1}

.dropdown:hover .dropdown-content {
  display: block;
}

.dropdown:hover .dropbtn {
  background-color: #3e8e41;
}
</style>
</head>
<body>

<h2>Dropdown Menu</h2>
<p>Move the mouse over the button to open the dropdown menu.</p>

<div class="dropdown">
  <button class="dropbtn">Dropdown</button>
  <div class="dropdown-content">
  <a href="#">Link 1</a>
  <a href="#">Link 2</a>
  <a href="#">Link 3</a>
  </div>
</div>

<p><strong>Note:</strong> We use href="#" for test links. In a real web site this would be URLs.</p>

</body>
</html>
```
- `.dropbtn` :tạo kiểu thả xuống
- `.dropdown `: thiết đặt định vị nội dung thả xuống
- `.dropdown-content `:nội dung thả xuống được ẩn
- `.dropdown-content a`:Link liên kết trong trình thả đơn
- `.dropdown:hover .dropdown-content` :hiển thị menu thả xuống khi di chuyển chuột đến
-