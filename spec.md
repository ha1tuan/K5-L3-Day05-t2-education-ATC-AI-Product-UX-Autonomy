
Bài nộp LAB5 — Track 2 - Education · Nhóm ATC

| Họ và Tên | Mã Học Viên | Việc đã làm |
|---|---|---|
| Vũ Hải Tuấn | 2A202603689 |  |
| Đặng Đức Cương | 2A202603680  |  |
| Phạm Quỳnh Anh | 2A202603671 |  |

## §1. Lát cắt & phạm vi
- Lát cắt (chép từ track).
Lát cắt (phát sẵn, không chọn lại). Trong trợ lý học bài của trang khoá học (kiểu ChatGPT Study mode), khi học viên đang hỏi bài lúc tối muộn, khi không còn ai để hỏi, AI giảng kèm trích tài liệu, hỏi lại cho rõ, gợi ý từng bước, hay nói thẳng "tài liệu không có, hỏi giảng viên", để học viên hiểu đúng bài mình đang học, không chép đáp án, không học sai mà không biết.

- 3 việc tính năng KHÔNG làm, mỗi việc một câu vì sao.

1. Không giải hộ, không đưa ra đáp số đúng hay sai. Vì bài đang mở tới 13/11 23:59 và gợi ý qua goi_y_bai_tap không thu hồi được: học viên đã chép là mất luôn mục tiêu “hiểu bài”. 
2. Không giảng nội dung buổi 4–10 (ví dụ p-value ở buổi 7), vì trang khoá học chỉ có tên buổi, không có tài liệu để trích mục, nên mọi lời giảng đều là bịa.
3. Không tự sửa hay khẳng định tài liệu khoá học là đúng (ví dụ câu sai ở §3.3), vì quyền sửa thuộc giảng viên, còn AI tự sửa rồi đăng qua dang_FAQ sẽ lan cái sai ra cả lớp trước khi ai kịp gỡ.

## §2. Kịch bản rủi ro  (chặng 2)

### 2.1 Bảng 8 kịch bản rủi ro
### Bảng 8 kịch bản lỗi phía hệ thống

| # | Kịch bản (hệ thống thiếu / sai gì) | Vì sao AI trả lời sai → hậu quả trong T2 | Lớp | Thiết kế chặn | Nhãn |
|---|---|---|---|---|---|
| 1 | **System prompt thiếu role và phạm vi.** Không nói AI là "trợ lý của khoá Nhập môn phân tích dữ liệu, chỉ dựa tài liệu buổi 1–3", cũng không nói người đang chat là học viên hay TA. | AI hành xử như chatbot chung: giảng p-value (buổi 7), hàm Excel, công thức không có trong tài liệu. Ai nhắn "mình là TA" thì AI tin luôn. | ① ③ | Ghi rõ vai trò, khoá, các buổi đã mở, nguồn sự thật duy nhất. Vai trò người dùng lấy từ phiên đăng nhập, không lấy từ tin nhắn. | Sửa được |
| 2 | **Tài liệu thiếu nội dung.** Không có công thức phương sai, không có ngưỡng ngoại lai, không có hàm Excel. | AI lấp chỗ trống bằng kiến thức ngoài nhưng vẫn gắn mã § như thể trích từ tài liệu; học viên tin đó là nội dung khoá. | ① | Tách rõ "trích tài liệu" và "ngoài tài liệu"; chỗ thiếu thì nói thẳng là thiếu và đề nghị `chuyen_TA`. | Sửa được |
| 3 | **Không có hướng dẫn khi không chắc.** | Tra "độ lệch" ra cả §3.2 và §3.3; AI tự chọn §3.3 rồi giảng, có thể sai khái niệm học viên đang hỏi. | ② | Quy tắc: nhiều đoạn khớp thì hỏi lại một câu; không đoạn nào khớp thì nói tài liệu không có. | Sửa được |
| 4 | **System prompt không nói tài liệu có thể sai.** | AI coi tài liệu là chân lý: dựng lời giải thích cho câu sai ở §3.3, hoặc bảo học viên đã tính đúng là "tính lại đi". Kèm mã § nên càng đáng tin; nếu lên FAQ thì cả lớp sai theo. | ④ ① | Luật: khi tài liệu mâu thuẫn với phép tính hoặc phản ví dụ thì gắn cờ "cần xem lại", chuyển TA, không đăng FAQ khi chưa có xác nhận. | Không chấp nhận được |
| 5 | **System prompt thiếu ngày giờ hiện tại.** | AI không biết bài 3 đang mở hay đã đóng, TA đang trực hay đã nghỉ → giải hộ bài đang mở, hoặc hứa "TA trả lời ngay" lúc 23h. | ④ | Chèn thời gian hiện tại vào mỗi lượt; trạng thái bài do hệ thống tính từ trang khoá học, không để model tự suy. | Không chấp nhận được |
| 6 | **Đề bài nằm chung kho với lý thuyết, không có nhãn.** §3.5 lẫn với §3.1–§3.4. | Tra "trung vị" ra cả §3.5; AI lấy dãy lương 9…45 làm ví dụ → giải hộ bài đang mở ngay trong lúc giảng. | ③ | Gắn nhãn "đề bài đang mở" và loại các đoạn này khỏi kết quả dùng làm ví dụ. | Không chấp nhận được |
| 7 | **Tool không trả trạng thái thành công / thất bại.** | `chuyen_TA` bị lỗi nhưng AI mặc định là thành công và nói "đã báo TA"; học viên chờ một câu trả lời không bao giờ đến, sát hạn nộp. | ③ | Tool trả kết quả rõ ràng; giao diện chỉ hiện "đã gửi" khi có xác nhận, có nút [Thử lại]. | Sửa được |
| 8 | **Hội thoại vượt giới hạn ngữ cảnh.** | Phần luật và dòng "bài 3 đang mở" ở đầu ngữ cảnh bị cắt; AI quên luật và gọi `goi_y_bai_tap` với lời giải đầy đủ. | ③ | Luật cứng nằm ngoài model: hệ thống tự kiểm trạng thái bài trước khi gọi tool; ghim luật mỗi lượt; hội thoại quá dài thì tóm tắt và mở phiên mới. | Không chấp nhận được |

**Hai kịch bản đắt nhất**
- **#4:** lỗi ngữ cảnh. Hệ thống trích đúng nguồn nhưng nguồn sai, nên học viên học sai âm thầm và có thể lan ra cả lớp.
- **#5:** thiếu một dữ kiện nền nên mọi luật "bài đang mở" đều vô hiệu. Sửa câu chữ không cứu được; phải để hệ thống tự tính trạng thái bài.