


# Bối cảnh và vấn đề 

> Bối cảnh: Nhân viên CSKH MartX tư vấn khách hàng trên 1 phiên ChatGPT duy nhất qua 45 lượt liên tục. Đến lượt 42, AI gọi sai tên ("chị Mai" thay vì "anh Trần Văn B") và yêu cầu cung cấp lại mã đơn hàng #MTX-9988 — dù khách đã khai từ lượt 1.

----------

## Phần 1  Giải thích 

### 1.1 Dàn cảnh ẩn dụ

Khái niệm kỹ thuật

Tương ứng trong ẩn dụ

Context Window (cửa sổ ngữ cảnh / "RAM" của AI)

**Chiếc cốc nước** có dung tích cố định (ví dụ 128.000 token ≈ 1 lít)

Mỗi lượt chat (câu hỏi + câu trả lời)

**Một góc nước** đổ vào cốc

Câu trả lời của AI dài dòng (32.000 token)

**Một góc nước TO, đổ ồ ạt**

Token cũ nhất bị đẩy ra (truncation)

**Nước cũ tràn ra khỏi miệng cốc**

Thông tin lượt 1 (tên + mã đơn)

**Gốc nước đáy cốc — bị tràn ra đầu tiên**

### 1.2 Diễn biến 45 lượt chat theo "cốc nước"

1.  **Lượt 1 — Cốc gần như trống (95% trống):** Khách khai tên "Trần Văn B" + mã đơn #MTX-9988. Góc nước này đổ vào **đáy cốc**. AI "nhìn thấy" rõ, chào đúng tên anh B.

2.  **Lượt 2 → 41 — Đổ nước liên tục 40 lượt:** Mỗi lượt tư vấn rau củ là một góc nước. Vì AI trả lời **dông dài**, mỗi góc lại to gấp 3–4 lần bình thường → cốc đầy nhanh. Tích lũy đến **32.000 token**, cốc đã gần đầy.

3.  **Lượt 42 — Cốc đầy 100%, nước tràn:** Khách hỏi "Đơn hàng có được miễn phí hoàn tiền không?" — đây là góc nước mới nhất. Khi đổ vào, cốc không chứa thêm → **nước ở đáy cốc (lượt 1) bị đẩy văng ra ngoài** theo cơ chế FIFO (vào trước, ra trước).

4.  **Kết quả:** AI chỉ "nhìn thấy" phần nước còn lại trong cốc (lượt 5 → 42). Phần lượt 1 (tên + mã đơn) **không còn trong cốc** nên AI không hề biết → gọi nhầm thành "chị Mai" (suy đoán mò) và bắt khách khai lại mã đơn.

### 1.3 Kết luận cho nhân viên CSKH

> AI **không bị mất trí nhớ ngắn hạn do lỗi** — mà **cốc của nó có đáy, và nước cũ luôn bị đẩy ra khi cốc đầy**.
> 
> Quy luật bất biến: **Dung tích cốc cố định × Mỗi lượt chat đều chiếm dung tích × Lượt cũ nhất = lượt bị quên đầu tiên.**
> 
> Nên càng tư vấn dài, AI càng dễ quên những thông tin khai báo từ đầu phiên — đây không phải lỗi của nhân viên, mà là giới hạn kỹ thuật cần được quản lý chủ động.

----------

## Phần 2 — Phương án quản lý "RAM bộ nhớ" để không bị tràn cốc

### Phương án A — Thao tác của người dùng (nhân viên CSKH) — áp dụng ngay, không cần kỹ thuật

**Mục tiêu:** Giảm lượng nước đổ vào cốc và giữ "gốc nước quan trọng" luôn trong cốc.

|#|Hành động cụ thể|Cơ chế chống tràn|
|-|-|-|
|1|Ghim thông tin cố định ở đầu mỗi phiên: Tạo một "thẻ thông tin khách" (tên, mã đơn, cửa hàng, vấn đề chính)|Gốc nước quan trọng được **đổ lại liên tục** |
|2|**Yêu cầu AI trả lời ngắn gọn:** Thêm vào system prompt / câu hỏi: "Trả lời ngắn gọn, dưới 150 từ, không lặp lại."|Mỗi góc nước nhỏ hơn  cốc đầy chậm lại 2–3 lần.|
|3|**Tách phiên khi đổi chủ đề:** Sau khi tư vấn xong rau củ (lượt 40), **mở phiên chat mới** .|Đổ cốc cũ đi,dùng cốc mới  không còn nguy cơ tràn.|


### Phương án B : Thiết kế hệ thống ( giải pháp bền vững)

**Mục tiêu:** Xây "ngăn đá" và "bể chứa bên ngoài" cho chiếc cốc, để cốc luôn chứa thứ quan trọng nhất.
**Xây dựng hệ thống lâu dài — tóm tắt 4 lớp, theo thứ tự ưu tiên:**

1.  **Không để bị tràn (chống mất gốc):** Cố định thông tin khách (tên, mã đơn, vấn đề) vào không bị đẩy ra khỏi context.
2.  **Nén cho đỡ đầy (tự động):** **khi context >70%, hệ thống tự gọi AI tóm tắt phần cũ thành đoạn ngắn. 
3.  **Cất ngoài, lấy khi cần (RAG):** Lưu lịch sử chat vào `database`; không nhét toàn bộ lịch sử vào cốc.
4.  **Cảnh báo sớm:** Theo dõi % dung tích theo thời gian thực,



## Tóm tắt nhanh cho nhân viên CSKH

-   **Tại sao quên?** lý do quên là có nhiều vấn đề cần giải quyết 1 lúc => quá tải thông tin 

-   **Làm gì ngay?** yêu cầu AI trả lời ngắn, tóm tắt định kỳ.

-   **Làm gì về lâu dài?** Đội kỹ thuật tích hợp  tra cứu lịch sử.
