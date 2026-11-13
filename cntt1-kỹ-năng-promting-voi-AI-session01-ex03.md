


# Phần 1 :
1. Giải thích cơ chế cắt từ của BPE đối với ký tự tiếng Việt có dấu. 
 - Cơ chế cắt từ của BPE với tiếng Việt ( có dấu ) 
 > BPE được hiểu là cách đếm token được phân cách bởi nhiều kiểu được hiển thị bởi các màu khác nhau  
 > **ví dụ**: nguyễn văn an 
 >     => mỗi chữ cái có 1 màu 1 kí tự khác nhau trong tiếng việt được là đính với 1 token như  sau: `n` ;`ễ`; `g` ;.....đều là 1 token mỗi chữ cái có 1 màu định dạng riêng 

2. Bóc tách lý do khiến Mẫu B (viết bằng tiếng Việt) tốn gấp 2.4 lần Token của Mẫu A (viết bằng tiếng Anh ) 
> BPE được tối ưu trong môi trường bảng chữ cái  Latinh ( tiếng Anh ) Tiếng Việt có dấu thanh và ít xuất hiện trong tập dữ liệu Pre-training nên bị thuật toán BPE cắt thành nhiều mảnh byte nhỏ.

ví dụ :
tôi có 1 cái bút 
=> có tận 12 kí tự token 
I have one pen 
=> có 4 kí tự token 
**Nên khi viết bằng tiếng Việt cần nhiều token hơn khi viết bằng tiếng Anh gấp 2,4 lần**
# Phần  2 : Phương pháp Promoting tối ưu 
-   Tất cả thuật ngữ kỹ thuật, tên file, đoạn code, định dạng đầu ra **giữ nguyên tiếng Anh**: `DPF`, `Markdown`, `Python`,…
-   Chỉ phần **bối cảnh và yêu cầu** viết bằng tiếng Việt **có dấu**
- Xóa bỏ các lời chào dư thừa không cần thiết cho vấn đề cần hỏi 
- Có thể rút gọn thành **Vai trò , Bối cảnh , Yêu cầu , Mẫu sẵn , Định dạng đầu ra**.
=> Giảm các câu xã giao ,các câu không mang nội dung tập chung vào vấn đề chính 

