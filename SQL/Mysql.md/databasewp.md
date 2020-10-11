# Cấu trúc database của wordpress
 database cơ bản của wordpress thì gồm 12 table lưu trữ dữ liệu
- wp_postmeta
- wp_posts
- wp_terms
- wp_users
- wp_links
- wp_usermeta
- wp_commentmeta
- wp_termmeta
- wp_comments
- wp_term_taxonomy
- wp_term_relationships
- wp_options
## wp_commentmeta
![alt](/images/Screenshot_20.png)

Bảng này là bảng lưu trữ các dữ liệu liên quan đến các comment như :id,id comment, từ khóa ,biến
## wp_comments
![alt](/images/Screenshot_21.png)

Bảng này chứa các bình luận trong wordpresss như:id_comment,nội dung,ngày tháng,tác giả,...
## wp_links
![alt](/images/Screenshot_22.png)

Bảng này chứa các thông tin liên quan đến link khi sử dụng tính năng link của wordpress như: url,...

## wp_options 
![alt](/images/Screenshot_23.png)

Phần này chứa các thông tin về cấu hình của wordpress
## wp_postmeta
![alt](/images/Screenshot_24.png)

 Mỗi bài viết có một thông tin duy nhất gọi là metadata, thông tin này sẽ được lưu bảng này.

 ## wp_post
  ![alt](/images/Screenshot_25.png)

  Các bài viết của bạn đều được lưu trữ .Bảng này lưu thông tin này, Pages và Menu điều hướng cũng được lưu tại đây
## wp_termmeta 
  ![alt](/images/Screenshot_26.png)

   Mỗi term có thông tin duy nhất gọi là metadata, thông tin đó sẽ được lưu trong phần này.
   ## wp_term 
  ![alt](/images/Screenshot_27.png)

  Categories cho bài viết, links và tags được lưu tại đây.
  ## wp_term_relationships 
  ![alt](/images/Screenshot_28.png)

  Categories và tag từ trong bảng wp_terms sẽ lưu các mối liên hệ của nó tại bảng này.
  ## wp_term_taxonomy
 
![alt](/images/Screenshot_29.png)

Bảng này mô tả taxonomy (category, link, và tag) cho các dữ liệu trong bảng wp_terms.
## wp_usermeta
![alt](/images/Screenshot_30.png)

 Mỗi người dùng có thông tin duy nhất gọi là metadata, thông tin này được lưut ại bảng wp usermeta này.
## wp_users
![alt](/images/Screenshot_31.png)

Người dùng được lưu trong bảng này.