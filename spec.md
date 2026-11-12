
Bài nộp LAB5 — Track 2 - Education · Nhóm ATC

## Thành viên nhóm

| Họ và Tên | Mã Học Viên | Việc đã làm |
|---|---|---|
| Vũ Hải Tuấn | 2A202603689 | **Chặng 5 · Prototype.** Dựng `prototype/index.html` (1 file HTML, 2 màn hình: học viên và hàng chờ TA). Thể hiện ca A (tài liệu §3.3 sai) và ca B (bài tập 3 đang mở), mỗi ca chuyển được giữa các mức tự chủ. Làm các điều khiển: Hoàn tác cờ, hộp xác nhận Gửi TA, thẻ bước mở dần, thẻ cấm cùng khuôn, công tắc giả lập lỗi tool. Chụp 2 ảnh đánh số [1]–[10], viết §5 trong spec (bảng số ↔ nguyên tắc HAX/PAIR ↔ mức tự chủ, các cách hiện đã loại, đường đi khi gặp ca lạ). Demo phần bấm prototype. Cùng nhóm làm chặng 1–4. |
| Đặng Đức Cương | 2A202603680 | **Chặng 2 + 3 · Kịch bản rủi ro và Khi AI sai.** Viết bảng 8 kịch bản phủ 4 lớp, trỏ về tool và dữ liệu của T2; khoanh 2 kịch bản đắt nhất (tài liệu có thể sai, thiếu ngày giờ). Viết §3: câu AI nói nguyên văn theo từng nhánh, người dùng thấy gì, bước tiếp theo, ai được báo và sau bao lâu; chọn hỏi lại / trả lời kèm giới hạn / chuyển người; phân loại lỗi; chỉ ra lỗi sửa câu chữ không cứu được. Demo phần lát cắt và 2 kịch bản đắt nhất. Cùng nhóm làm chặng 1 và 4. |
| Phạm Quỳnh Anh | 2A202603671 | **Chặng 4 + 6 · Mức tự chủ và Tốt là gì.** Viết §4: mức của từng tool kèm lý do theo cost-of-error, tool khó xếp nhất (`goi_y_bai_tap`), tách `dang_FAQ` thành soạn / đăng, thêm `gan_co_tai_lieu`, bảng luật L1–L10; thử mức trên 2 kịch bản đắt nhất + 1 kịch bản bình thường; lời hứa với học viên đã đổi. Viết §6: 3 tiêu chí Pass/Fail và chấm thử. Tổng hợp `spec.md`, tạo repo và nộp bài. Demo phần mức tự chủ và trả lời ca lạ. Cùng nhóm làm chặng 1–3. |

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

## §3. Khi AI sai (chặng 3)
---
### Kịch bản 4 — System prompt không nói tài liệu có thể sai

Tình huống: “sao độ lệch chuẩn luôn nhỏ hơn phương sai vậy ạ, e đọc §3.3 mà chưa hiểu tại sao”

AI nói gì (nguyên văn, theo từng nhánh): "Theo §3.3, độ lệch chuẩn là căn bậc hai của phương sai. Mà căn bậc hai của một số thì luôn nhỏ hơn số đó: phương sai 16 thì độ lệch chuẩn là 4, phương sai 100 thì là 10. Em chỉ cần nhớ ‘căn bậc hai thì luôn nhỏ hơn’ là được nhé!"

#### Người dùng thấy gì khi AI sai 
Học viên thấy câu trả lời của AI kèm thẻ trích nguyên văn §3.3 và nhãn “Trợ lý AI · có thể sai, hãy đối chiếu đoạn trích”.

#### Bước tiếp theo
Họ có thể bấm [Mở §3.3] để đọc lại, bấm [Sai chỗ nào?] → “Tài liệu có vẻ sai” rồi nhập phản ví dụ, hoặc bấm [Gửi TA · trả lời từ 08:00

### Những người có thể được báo nếu AI lỗi và trong khoảng thời gian
1. Học viên: Nhận đính chính ngay khi giảng viên sửa §3.3, dự kiến trong ngày 13/11
2. TA: Sau khoảng 9 giờ: lúc 08:00 ngày 13/11, vì lỗi xảy ra ngoài giờ trực. Nếu trong giờ 08:00–22:00 thì thấy ngay
3. Giảng viên: Trong ngày 13/11, sau khi TA chuyển tiếp

### Kịch bản 5 — System prompt thiếu ngày giờ hiện tại

**Tình huống A:** 22:40 ngày 12/11, học viên nhắn "bài 3 còn hạn k ạ, e tính cuối tuần rảnh mới làm"

AI nói gì (nguyên văn): "Cuối tuần làm là kịp nhé. Hạn bài 3 là 23:59 ngày 13/11/2026, nên em vẫn còn khá nhiều thời gian"

### Bước tiếp theo của người dùng

-Học viên tin câu trả lời, đóng tab và để bài tới cuối tuần, tức là sau hạn 23:59 ngày 13/11, nên lỡ hạn. Lỗi này âm thầm: không ai biết cho tới khi đã quá hạn.

### Những người có thể được báo nếu AI lỗi và trong khoảng thời gian

1. Giảng viên: Sau 23:59 ngày 13/11, chỉ khi học viên lỡ hạn vì lỗi này.
2. Học viên: Sau khi được báo là nộp bài muộn

Quyết định khi AI không chắc:
### Kịch bản 4 — System prompt không nói tài liệu có thể sai

**Quyết định: trả lời kèm giới hạn** (kèm chuyển người song song)

| Quyết định | Chọn? | Vì sao |
|---|---|---|
| Hỏi lại | ✗ Loại | Câu hỏi đã rõ, học viên hỏi đúng §3.3. Hỏi lại chỉ thêm một lượt chờ, không xử lý được việc nguồn bị sai. |
| **Trả lời kèm giới hạn** | ✓ **Chọn** | Phần toán tự kiểm được ngay (√0,25 = 0,5 > 0,25), nên học viên không bị kẹt. Giới hạn: AI chỉ nói "câu này cần xem lại", không tự khẳng định tài liệu sai và không viết lại §3.3, vì sửa tài liệu là thẩm quyền của giảng viên. |
| Chuyển người | ✗ Không dùng một mình (chạy song song) | Nếu chỉ chuyển, học viên chờ tới 08:00 cho một điều tự kiểm được bằng một phép tính. Vẫn chuyển TA song song để giảng viên sửa §3.3 cho cả lớp. |

### Kịch bản 5 — System prompt thiếu ngày giờ (tình huống A: hỏi hạn nộp)

**Quyết định: trả lời kèm giới hạn**

| Quyết định | Chọn? | Vì sao |
|---|---|---|
| Hỏi lại | ✗ Loại | "Bài 3 còn hạn không" đã rõ. Hỏi lại làm chậm một câu trả lời có sẵn trên trang khoá học. |
| **Trả lời kèm giới hạn** | ✓ **Chọn** | Hạn nộp có trên trang khoá học, và thời gian còn lại do hệ thống tính từ đồng hồ server. Giới hạn: AI chỉ nói ngày hạn (kèm nguồn) và số giờ còn lại, không tự suy ra "còn nhiều thời gian" hay "cuối tuần là kịp". |
| Chuyển người | ✗ Loại | TA chỉ trả lời từ 08:00 ngày 13/11, khi đó chỉ còn khoảng 16 giờ trước hạn. Bắt chờ người cho một thông tin có sẵn cũng là một kiểu sai. |

### Loại lỗi và cách sửa

#### Kịch bản 4 — System prompt không nói tài liệu có thể sai
**Loại lỗi: lỗi ngữ cảnh**
- **Vì sao:** hệ thống chạy đúng thiết kế, vì `tra_cuu_tai_lieu` trích đúng §3.3. Nhưng chính nguồn sự thật lại sai, nên câu trả lời sai với tình huống thật của học viên. Đây cũng không phải lỗi người dùng: học viên hỏi đúng, và nếu có tự tính thì tính đúng.
- **Cách nói theo loại lỗi:**
  - Không xin lỗi thay tài liệu.
  - Không đổ lỗi cho học viên.
  - Chỉ ra câu nào cần xem lại và vì sao, kèm phản ví dụ.
  - Chỉ nhận lỗi ("Mình đã trả lời sai ở trên, xin lỗi em") khi AI đã lỡ bênh câu sai trước đó.
- **Cách sửa (sửa thiết kế, không chỉ sửa câu chữ):**
  1. Thêm luật vào system prompt: tài liệu có thể sai; khi tài liệu mâu thuẫn với phép tính hoặc phản ví dụ thì gắn cờ "cần xem lại".
  2. Thêm tool `gan_co_tai_lieu`, mức **tự làm**: chỉ ghi vào hàng chờ TA, không sửa tài liệu.
  3. Chặn `dang_FAQ` với mọi nội dung đang có cờ.
  4. Khi giảng viên sửa §3.3, hệ thống gửi đính chính tới mọi học viên đã nhận câu sai.

#### Kịch bản 5 — System prompt thiếu ngày giờ (tình huống A: hỏi hạn nộp)
**Loại lỗi: lỗi hệ thống**
- **Vì sao:** model thiếu một dữ kiện bắt buộc (ngày giờ hiện tại) nên tự suy ra "còn nhiều thời gian" và suy sai. Học viên hỏi đúng, nguồn (hạn 13/11) cũng đúng; lỗi nằm ở cách hệ thống được dựng.
- **Cách nói theo loại lỗi:** nhận lỗi thẳng, sửa lại bằng con số cụ thể, không vòng vo:
  > "Mình đã tính sai thời gian ở trên, xin lỗi em. Bây giờ là 22:41 ngày 12/11, hạn bài 3 là 23:59 ngày 13/11, em còn khoảng 25 giờ."
- **Cách sửa (sửa hệ thống):**
  1. Hệ thống chèn ngày giờ hiện tại vào mỗi lượt hội thoại.
  2. Thời gian còn lại do hệ thống tính từ đồng hồ server và trang khoá học, rồi hiện trên thẻ trạng thái bài. Model không tự tính.
  3. Câu trả lời có nhắc hạn nộp được đối chiếu với đồng hồ server trước khi hiển thị.
  4. Thêm nhắc hạn tự động cho học viên (ví dụ lúc 20:00 ngày 13/11), độc lập với việc AI nói đúng hay sai.

### Nguyên tắc HAX — trỏ vào chỗ cụ thể

#### Kịch bản 4 — System prompt không nói tài liệu có thể sai

- **G2 — Làm rõ hệ thống làm tốt đến đâu**
  → **Màn hình:** nhãn cảnh báo **"Cần xem lại · chưa được giảng viên xác nhận"** gắn trên thẻ trích §3.3, với câu "luôn nhỏ hơn" được gạch chân vàng. Học viên biết ngay câu này chưa chắc, thay vì tin tuyệt đối vì nó có mã mục.

- **G11 — Giải thích vì sao**
  → **Câu chữ:** "…độ lệch chuẩn là căn bậc hai của phương sai, **nên nó chỉ nhỏ hơn phương sai khi phương sai lớn hơn 1**. Ví dụ phương sai 0,25 thì độ lệch chuẩn là 0,5." Kèm **hộp phản ví dụ** `√0,25 = 0,5 > 0,25` để học viên tự kiểm.

- **G15 — Mời feedback chi tiết**
  → **Màn hình:** nút **[Sai chỗ nào?]** mở popup có lựa chọn **"Tài liệu có vẻ sai"** và ô "Ví dụ của em". Lựa chọn này tách lỗi tài liệu khỏi lỗi của AI, nên cờ đi đúng tới TA và giảng viên.

#### Kịch bản 5 — System prompt thiếu ngày giờ (tình huống A: hỏi hạn nộp)

- **G4 — Hiện thông tin liên quan tới ngữ cảnh**
  → **Màn hình:** **thẻ trạng thái bài** " Bài tập 3 · ĐANG MỞ · Hạn 23:59 13/11 · còn ~25 giờ" tự hiện mỗi khi học viên nhắc tới bài 3. Thời gian còn lại do hệ thống tính từ đồng hồ server, không do AI viết.

- **G11 — Giải thích vì sao**
  → **Câu chữ:** "Hạn bài 3 là 23:59 ngày 13/11/2026 **theo trang khoá học**. **Bây giờ là 22:40 ngày 12/11**, nên em còn khoảng 25 giờ." Câu trả lời nêu cả nguồn lẫn mốc thời gian dùng để tính, để học viên tự kiểm được.

- **G3 — Chọn đúng thời điểm theo ngữ cảnh**
  → **Màn hình:** **thông báo nhắc hạn tự động lúc 20:00 ngày 13/11**, khoảng 4 giờ trước hạn: "Bài 3 còn 4 giờ nữa là hết hạn · [Mở bài 3]". Đây là lưới an toàn đúng lúc học viên cần, độc lập với việc AI nói đúng hay sai.

### Lỗi sửa câu chữ không cứu được, và thiết kế cứu thế nào

#### Kịch bản 4 — System prompt không nói tài liệu có thể sai

**Vì sao câu chữ không cứu được:**
- Vì system prompt không nói tài liệu có thể sai, AI coi mọi đoạn mà `tra_cuu_tai_lieu` trả về là sự thật. Câu trả lời viết khéo đến đâu cũng chỉ diễn đạt lại một nguồn sai cho trơn tru hơn.
- Một cảnh báo bằng lời chỉ nằm trong một cuộc trò chuyện. Lỗi trong tài liệu vẫn còn đó, những người hỏi sau vẫn nhận câu sai, và có thể lan ra cả lớp qua `dang_FAQ`.

**Thiết kế cứu:**
1. **Thêm luật vào system prompt:** tài liệu có thể sai; khi tài liệu mâu thuẫn với phép tính hoặc phản ví dụ thì gắn cờ "cần xem lại", không bênh và không tự sửa.
2. **Thêm tool `gan_co_tai_lieu` (tự làm):** ghi đoạn nghi sai vào hàng chờ TA, không cần người dùng bấm, nên lỗi không bị mất.
3. **Chặn `dang_FAQ`** với mọi nội dung đang có cờ, cho tới khi giảng viên xác nhận.
4. **Đính chính ngược:** khi giảng viên sửa tài liệu, hệ thống tự báo cho mọi người đã nhận câu trả lời trích đoạn sai.

#### Kịch bản 5 — System prompt thiếu ngày giờ hiện tại

**Vì sao câu chữ không cứu được:**
- Model không biết bây giờ là lúc nào, nên mọi luật phụ thuộc thời gian (bài đang mở hay đã đóng, còn bao lâu tới hạn, TA đang trực hay không) đều không áp dụng đúng được. Thêm câu "hãy cẩn thận về thời gian" cũng vô ích.
- Kể cả khi đã có ngày giờ trong prompt, model vẫn có thể tính sai, hoặc mất dòng ngày giờ khi hội thoại dài vượt giới hạn ngữ cảnh.

**Thiết kế cứu:**
1. **Hệ thống chèn ngày giờ** từ đồng hồ server vào mỗi lượt hội thoại.
2. **Hệ thống tự tính trạng thái bài và thời gian còn lại** từ trang khoá học, rồi hiện trên thẻ trạng thái bài. Model không tự tính.
3. **Đối chiếu trước khi hiển thị:** câu trả lời có nhắc tới hạn nộp hoặc trạng thái bài được so với dữ liệu hệ thống; nếu sai thì chặn.
4. **Cổng chặn trước `goi_y_bai_tap`:** khi bài đang mở thì chỉ cho gửi gợi ý bước đầu, bất kể model sinh ra gì.


## §4. Mức tự chủ (chặng 4)

### 4.1 Mức của từng tool

| Tool | Loại | Nguồn gốc | Làm gì | Đảo lại được không | Chặn kịch bản nào |
|---|---|---|---|---|---|
| `tra_cuu_tai_lieu` | **Gốc** | Bảng tool của track | Tìm trong tài liệu buổi học, trả về đoạn kèm mã mục | Chỉ đọc | — |
| `goi_y_bai_tap` | **Gốc + luật thêm** | Bảng tool của track; thêm cổng chặn theo trạng thái bài | Gửi gợi ý làm bài cho một học viên; nếu bài đang mở thì chỉ được gợi ý bước đầu | Không: gợi ý đã gửi thì học viên đã đọc | Giải hộ bài đang mở · Thiếu ngày giờ hiện tại |
| `chuyen_TA` | **Gốc** | Bảng tool của track; đổi sang học viên bấm duyệt | Chuyển câu hỏi cho TA, báo giờ TA trả lời | Được | Hứa "đã báo TA" khi chưa gửi |
| `soan_FAQ` | **Tách bước** | Tách từ `dang_FAQ` (bước "soạn") | Soạn nháp câu hỏi và trả lời cho FAQ; chỉ TA thấy | Được: nháp chưa ai đọc | Đăng đáp án bài đang mở lên FAQ |
| `dang_FAQ` | **Gốc (thu hẹp)** | Bảng tool của track; giờ chỉ còn bước "đăng", TA duyệt | Đăng nháp đã duyệt lên FAQ cả lớp | Gỡ được, nhưng nhiều người đã đọc | Đăng đáp án lên FAQ · Lan câu sai của tài liệu ra cả lớp |
| `gan_co_tai_lieu` | **Mới** | Nhóm tự thêm | Ghi đoạn tài liệu nghi sai vào hàng chờ TA; không sửa tài liệu, không đăng gì | Được: TA gỡ cờ | Tài liệu sai (system prompt không nói tài liệu có thể sai) |


### 4.2 Lý do theo cost-of-error và phương án đã loại

#### `tra_cuu_tai_lieu`: Phương án tự làm
- **Sai thì ai chịu gì:** trả nhầm đoạn thì học viên đọc nhầm mục. Thiệt hại thấp, vì câu trả lời luôn kèm mã § nên học viên tự đối chiếu được.
- **Đảo lại được không:** không có gì để đảo, tool chỉ đọc, không thay đổi gì.
- **Chờ người thì mất gì:** mọi câu hỏi đều phải chờ TA tới 08:00, trợ lý tối muộn mất hết giá trị.
- **Phương án đã loại:**
  - *Cần duyệt:* bắt chờ người cho một việc chỉ đọc là vô lý.
  - *Cấm:* AI không có nguồn thì chỉ còn cách bịa.

#### `goi_y_bai_tap`: Phương án bài đã hết hạn và đã có đáp án — Tự làm, giải thích đầy đủ
- **Sai thì ai chịu gì:** học viên hiểu nhầm một bước, nhưng tự đối chiếu được với đáp án đã công bố trên trang khoá học.
- **Đảo lại được không:** không có gì bị lộ, vì đáp án đã công khai.
- **Chờ người thì mất gì:** học viên ôn bài phải chờ TA cho một thông tin ai cũng xem được.
- **Phương án đã loại:**
  - *Chỉ gợi ý bước đầu như bài đang mở:* từ chối nhầm bài đã đóng, học viên kẹt vô ích (kịch bản "từ chối quá tay").
  - *Cần TA duyệt:* chờ người cho thông tin công khai.

#### `goi_y_bai_tap`: Phương án  bài đang mở, gợi ý bước đầu — Tự làm có cổng chặn
- **Sai thì ai chịu gì:** gợi ý quá tay thì học viên chép, mất mục tiêu "hiểu bài", và bất công với cả lớp.
- **Đảo lại được không:** không, gợi ý đã gửi là học viên đã đọc. Vì vậy cổng chặn giới hạn mức gợi ý ở bước đầu: phần lộ tối đa chỉ là một bước mà tài liệu §3.1, §3.2 vốn đã nói.
- **Chờ người thì mất gì:** TA chỉ trả lời từ 08:00, học viên kẹt cả đêm sát hạn. Mà TA cũng chỉ được gợi ý bước đầu, nên chờ không đổi được kết quả.
- **Phương án đã loại:**
  - *Cần TA duyệt mọi gợi ý:* mất giá trị trợ lý tối muộn (kịch bản "đẩy cho người khi tự trả lời được").
  - *Tự làm mà không có cổng chặn:* luật trong prompt có thể bị quên hoặc bị cắt (kịch bản "thiếu ngày giờ", "vượt giới hạn ngữ cảnh").
  - *Cấm hẳn:* học viên không được giúp gì, trái với lát cắt "gợi ý từng bước".

#### `goi_y_bai_tap`: Phương án bài đang mở: đưa đáp số, xác nhận đáp số, giải trọn bài — Cấm
- **Sai thì ai chịu gì:** lộ đáp án, học viên chép, cả lớp chịu bất công. Việc xác nhận cũng là lộ: nếu AI chỉ gật khi đáp số đúng, thì riêng việc nó từ chối đã cho học viên biết mình sai.
- **Đảo lại được không:** không.
- **Chờ người thì mất gì:** không áp dụng. Học viên vẫn có đường [Gửi TA kiểm tra].
- **Phương án đã loại:**
  - *Cần TA duyệt:* theo rubric, TA cũng không xác nhận đáp số bài đang mở, nên bước duyệt vô nghĩa.
  - *Tự làm chỉ khi đáp số đúng:* lộ "sai" qua chính lời từ chối.

#### `chuyen_TA`: Phương án cần học viên duyệt (1 chạm)
- **Sai thì ai chịu gì:** rủi ro thật là học viên **tưởng đã gửi** trong khi chưa, rồi chờ một câu trả lời không bao giờ đến, sát hạn. Gửi nhầm câu thì TA chỉ mất chút công.
- **Đảo lại được không:** được. Học viên huỷ được, TA bỏ qua được.
- **Chờ người thì mất gì:** một lần chạm, vài giây.
- **Phương án đã loại:**
  - *AI tự gọi:* AI dễ nói "đã chuyển" khi chưa gửi, và câu hỏi riêng của học viên đi đâu thì họ không biết.
  - *Cần TA duyệt:* vô nghĩa, vì TA chính là người nhận.
  - *Cấm:* mất đường lên người, trái với lát cắt "chuyển TA".

#### `gan_co_tai_lieu`: Phương án tự làm
- **Sai thì ai chịu gì:** gắn cờ nhầm một đoạn đúng thì TA mất vài phút kiểm tra, học viên thấy nhãn "cần xem lại" trên một đoạn thực ra đúng. Thiệt hại thấp.
- **Đảo lại được không:** được, TA gỡ cờ.
- **Chờ người thì mất gì:** nếu đợi học viên bấm thì đa số không bấm. Học viên đóng tab là lỗi tài liệu biến mất, cả lớp tiếp tục học sai. Ở đây **không hành động** mới là cái giá đắt.
- **Phương án đã loại:**
  - *Học viên duyệt:* lỗi âm thầm nên hầu như không ai bấm.
  - *TA duyệt trước khi gắn:* vô nghĩa, vì cờ sinh ra chính là để báo cho TA.

#### `soan_FAQ`: Phương án tự làm; cấm với bài đang mở hoặc đoạn có cờ
- **Sai thì ai chịu gì:** nháp sai thì chỉ TA thấy, không ai bị ảnh hưởng.
- **Đảo lại được không:** được, bỏ nháp.
- **Chờ người thì mất gì:** TA phải tự soạn từ đầu, tốn công.
- **Phương án đã loại:**
  - *Giữ `dang_FAQ` gốc (soạn và đăng trong một bước):* không có chỗ nào để người chặn lại trước khi cả lớp đọc.
  - *Cho soạn cả nội dung bài đang mở:* nháp chứa lời giải nằm trong hệ thống, có nguy cơ bị đăng nhầm, trong khi TA cũng không được đăng nó.

#### `dang_FAQ`: Phương án cần TA duyệt
- **Sai thì ai chịu gì:** cả lớp đọc một nội dung sai hoặc một đáp án. Đây là cái giá nhân lên theo số học viên.
- **Đảo lại được không:** gỡ được bài đăng, nhưng nhiều người đã đọc, nên thực tế gần như không đảo được.
- **Chờ người thì mất gì:** FAQ chậm tới 08:00. Học viên đã hỏi vẫn nhận câu trả lời riêng ngay, nên chờ chỉ làm chậm phần chia sẻ, không ai bị kẹt.
- **Phương án đã loại:**
  - *Tự làm:* kịch bản "đăng đáp án lên FAQ" và "lan câu sai của tài liệu ra cả lớp".
  - *Cấm hẳn:* mất lợi ích giảm câu hỏi trùng cho TA.

### 4.3 Tool khó xếp nhất: `goi_y_bai_tap`

#### Mỗi người từng chọn gì

| Thành viên | Chọn | Lý do người đó đưa ra |
|---|---|---|
| Vũ Hải Tuấn | **Tự làm** | Trợ lý có tự động khi học viên cần có thể tra đề ngay|
| Đặng Đức Cương | **Cần TA duyệt** | Muốn TA có được gợi ý bài tập cho học viên không |
| Phạm Quỳnh Anh | **Cấm** với bài đang mở | Không muốn lộ đáp án khi bài đang mở |

#### Cái giá của mỗi phía (trỏ về §2)

### Kịch bản sai của `goi_y_bai_tap` theo từng mức tự chủ

#### Mức 1 — Tự làm (không có cổng chặn)

**Kịch bản 1.1 — Gợi ý quá tay**

**Kịch bản 1.2 — Xác nhận đáp số**

#### Mức 2 — Cần người duyệt (TA duyệt mọi gợi ý)

**Kịch bản 2.1 — Chờ duyệt lâu**

**Kịch bản 2.2 — Duyệt cho có**

#### Mức 3 — Cấm

**Kịch bản 3.1 — Từ chối cả câu hỏi khái niệm**

**Kịch bản 3.2 — Cấm cả bài đã đóng**

#### Nhóm chốt thế nào

Chọn “Tự làm” có giới hạn, kết hợp “Cấm” cho phần đáp số. Lý do: lựa chọn này giữ được giá trị của trợ lý tối muộn, còn rủi ro không đảo được thì do hệ thống ngoài model chặn, không phải do người duyệt. Người duyệt ở đây vừa chậm, vừa không đáng tin khi quá tải.

### 4.4 Thử mức đã đặt trên 3 kịch bản

#### Kịch bản 4 — System prompt không nói tài liệu có thể sai
*Tình huống: "sao độ lệch chuẩn luôn nhỏ hơn phương sai vậy ạ, e đọc §3.3 mà chưa hiểu tại sao"*

**Với mức đã đặt, AI làm gì:**
1. `tra_cuu_tai_lieu` (tự làm) trả về §3.3.
2. AI nhận ra câu "luôn nhỏ hơn" mâu thuẫn với phản ví dụ 0,25 → 0,5.
3. `gan_co_tai_lieu` (tự làm) ghi câu này vào hàng chờ TA.
4. AI trả lời kèm giới hạn và mời học viên bấm [Gửi TA].
5. `soan_FAQ` bị cấm, vì đoạn này đang có cờ.

**Người dùng thấy gì:** câu trả lời có phản ví dụ, thẻ trích §3.3 với nhãn ⚠ "Cần xem lại · chưa được giảng viên xác nhận", và nút [Gửi TA · trả lời từ 08:00].

- **Cái sai có bị chặn không?** Có. AI không bênh câu sai; lỗi được ghi lại ngay cả khi học viên đóng tab; câu sai không lan lên FAQ.
- **Còn việc nào AI làm khi lẽ ra phải hỏi?** Có một chỗ: `gan_co_tai_lieu` tự làm dựa trên phán đoán của AI. Nếu AI phán sai, một đoạn đúng sẽ hiện nhãn "cần xem lại" trước khi TA kịp kiểm. Nhóm chấp nhận rủi ro này vì:
  - nhãn chỉ ghi "cần xem lại", không ghi "sai";
  - TA gỡ được cờ;
  - giá của việc gắn cờ nhầm thấp hơn nhiều so với để cả lớp học sai.
- **Người dùng có phải chờ vô ích không?** Không. Học viên có câu trả lời ngay. Chỉ việc sửa tài liệu là phải chờ TA và giảng viên, và đó là việc đúng ra phải chờ người.

#### Kịch bản 5 — System prompt thiếu ngày giờ hiện tại
*Tình huống A: 22:40 ngày 12/11, "bài 3 còn hạn k ạ, e tính cuối tuần rảnh mới làm"*

**Với mức đã đặt, AI làm gì:**
1. Hệ thống chèn ngày giờ và tự tính "còn ~25 giờ" từ trang khoá học.
2. AI trả lời hạn kèm nguồn và số giờ còn lại; không gọi tool nào làm thay đổi gì.

**Người dùng thấy gì:**  Bài tập 3 · ĐANG MỞ · Hạn 23:59 13/11 · còn ~25 giờ · nguồn: trang khoá học", kèm câu "cuối tuần là đã quá hạn".

- **Cái sai có bị chặn không?** Có, nhưng **không phải nhờ mức tự chủ**. Không tool nào trong bảng gây ra lỗi này. Lỗi bị chặn nhờ luật hệ thống: chèn ngày giờ, thẻ trạng thái do hệ thống tính, đối chiếu trước khi hiển thị. Kết luận: mức tự chủ chỉ kiểm soát việc AI **làm**, không kiểm soát việc AI **nói sai**.
- **Còn việc nào AI làm khi lẽ ra phải hỏi?** Không. Câu hỏi đã rõ, có nguồn, không cần hỏi lại.
- **Người dùng có phải chờ vô ích không?** Không. Thông tin có sẵn nên được trả lời ngay, không chuyển TA.

#### Kịch bản bình thường — hỏi khái niệm gần bài đang mở
*Tình huống: 22:50 ngày 12/11, "trung vị với 8 số thì lấy số nào ạ?"*

**Với mức đã đặt, AI làm gì:**
1. `tra_cuu_tai_lieu` trả về §3.2.
2. Cổng chặn của `goi_y_bai_tap` **không kích hoạt**, vì đây là câu hỏi khái niệm, không phải xin gợi ý hay đáp số bài 3.
3. AI trả lời ngay bằng quy tắc ở §3.2, ví dụ bằng dãy số tự đặt, không dùng dãy lương của §3.5.

**Người dùng thấy gì:** "Theo §3.2, nếu số giá trị là chẵn thì trung vị là trung bình cộng của hai giá trị đứng giữa. Ví dụ dãy 2, 4, 6, 8: trung vị là (4 + 6) / 2 = 5."

- **Cái sai có bị chặn không?** Không có cái sai nào cần chặn. Ví dụ không dùng dữ liệu bài 3, nên không lộ đáp án.
- **Còn việc nào AI làm khi lẽ ra phải hỏi?** Không.
- **Người dùng có phải chờ vô ích không?** Không. Đây chính là điều mức đã đặt cần giữ: nếu `goi_y_bai_tap` bị đặt "cần TA duyệt" hoặc "cấm", học viên sẽ phải chờ tới 08:00 cho một câu có sẵn trong tài liệu.

#### Kết quả thử 

| Kịch bản | Cái sai bị chặn? | Làm khi lẽ ra phải hỏi? | Chờ vô ích? |
|---|---|---|---|
| 4 — tài liệu có thể sai | ✓ Có | ⚠ Một chỗ chấp nhận được: tự gắn cờ dựa trên phán đoán của AI | ✓ Không |
| 5 — thiếu ngày giờ | ✓ Có, nhờ luật hệ thống, không nhờ mức tự chủ | ✓ Không | ✓ Không |
| Bình thường — trung vị 8 số | — Không có lỗi | ✓ Không | ✓ Không |

### 4.5 Luật thêm và tool tách bước

#### A. Tool mới và tool tách bước

| Thay đổi | Loại | Nội dung | Vì sao | Chặn kịch bản nào |
|---|---|---|---|---|
| `dang_FAQ` → `soan_FAQ` + `dang_FAQ` | **Tách bước** | `soan_FAQ` (tự làm): AI soạn nháp, chỉ TA thấy. `dang_FAQ` (TA duyệt): chỉ đăng nháp đã được TA đồng ý. | Tool gốc gộp "soạn" và "đăng" làm một, nên AI có thể đăng thẳng cho cả lớp mà không ai chặn. Tách ra thì AI vẫn đỡ việc soạn cho TA, còn bước không đảo được (cả lớp đã đọc) có người chặn. | Đăng đáp án bài đang mở lên FAQ · Lan câu sai ở §3.3 ra cả lớp |
| `gan_co_tai_lieu` | **Tool mới** | Tự làm: ghi đoạn tài liệu nghi sai vào hàng chờ TA; không sửa tài liệu, không đăng gì. | Không tool gốc nào báo được lỗi của tài liệu. `chuyen_TA` cần học viên bấm, mà lỗi tài liệu là lỗi âm thầm nên hầu như không ai bấm. | Kịch bản 4: tài liệu có thể sai |
| `goi_y_bai_tap` chia theo trạng thái bài | **Tách theo điều kiện** | Bài đã hết hạn và đã có đáp án: tự làm, giải thích đầy đủ. Bài đang mở, bước đầu: tự làm có cổng chặn. Đáp số, xác nhận đáp số, giải trọn bài: cấm. | Một mức chung cho cả tool thì mức nào cũng sai: tự làm thì lộ đáp án, cần duyệt thì chờ vô ích, cấm thì từ chối nhầm. | Giải hộ bài đang mở · Xác nhận đáp số · Từ chối nhầm bài 2 |

#### B.  Luật thêm

| Tool | Luật áp dụng | Luật đó kiểm soát gì trên tool |
|---|---|---|
| `tra_cuu_tai_lieu` | **L7.** Tài liệu có thể sai | Đoạn tool trả về không được coi là chân lý; nếu mâu thuẫn với phép tính thì chuyển sang `gan_co_tai_lieu`. |
| | **L10 (đề xuất thêm).** Đánh dấu đề bài đang mở | §3.5 được gắn nhãn "đề bài đang mở" và loại khỏi kết quả dùng làm ví dụ khi giảng lý thuyết. |
| `goi_y_bai_tap` | **L1.** Chèn ngày giờ | Cho tool biết bài đang mở hay đã đóng. |
| | **L2.** Cổng chặn trước khi gửi | Kiểm trạng thái bài trên trang khoá học; bài đang mở thì chỉ cho mức "bước đầu". |
| | **L3.** Bước đầu không chứa số liệu của đề | Giới hạn nội dung gợi ý: chỉ trỏ tới quy tắc ở §, không nhắc số nào trong dãy §3.5. |
| | **L4.** Mở dần từng bước | Bước sau chỉ mở khi học viên đã gửi cách làm bước trước. |
| | **L5.** Nhận diện dữ liệu của đề | Câu hỏi có dãy số trùng §3.5 thì xử như bài đang mở, kể cả khi không nhắc bài 3. |
| | **L6.** Mở khoá lời giải phải đủ hai điều kiện | Chỉ giải thích đầy đủ khi bài đã hết hạn **và** đã có đáp án. |
| `chuyen_TA` | **L1.** Chèn ngày giờ | Báo đúng giờ TA trả lời: ngay nếu trong 08:00–22:00, còn lại thì từ 08:00 hôm sau. |
| | **L8.** Chỉ hiện "đã gửi" khi tool trả thành công | Không nói "đã chuyển" hay "đã báo TA" trước khi có xác nhận. |
| `gan_co_tai_lieu` *(mới)* | **L7.** Tài liệu có thể sai | Luật này là điều kiện để gọi tool: gắn cờ khi tài liệu mâu thuẫn với phép tính hoặc phản ví dụ. |
| `soan_FAQ` *(tách bước)* | **L9.** Cấm với nội dung nhạy cảm | Không soạn nháp cho bài đang mở hoặc cho đoạn tài liệu đang có cờ. |
| `dang_FAQ` *(thu hẹp)* | Không có luật riêng | Đã có TA duyệt; nội dung nhạy cảm bị chặn từ bước `soan_FAQ` nhờ L9. |

#### C. Tính năng hệ thống đi kèm (không phải tool AI gọi)
- **Thẻ trạng thái bài:** hệ thống tự tính hạn và thời gian còn lại, rồi hiện trên màn hình (đi cùng L1).
- **Đính chính ngược:** khi giảng viên sửa tài liệu, hệ thống tự báo cho mọi người đã nhận câu trả lời trích đoạn sai (đi cùng L7).
- **Nhắc hạn tự động:** khoảng 4 giờ trước hạn nộp; là lưới an toàn độc lập với việc AI nói đúng hay sai.


### 4.6. Mức tự chủ theo kịch bản

| # | Kịch bản | Tool liên quan | Mức tự chủ áp dụng | Luật đi kèm | Cái sai bị chặn nhờ |
|---|---|---|---|---|---|
| 1 | System prompt thiếu role và phạm vi | `tra_cuu_tai_lieu` · `dang_FAQ` | Tra cứu: **tự làm** · Đăng FAQ: **TA duyệt** | Vai trò người dùng lấy từ phiên đăng nhập; chỉ dựa tài liệu buổi 1–3 | **Cả hai.** Luật giữ AI trong phạm vi khoá học; mức "TA duyệt" ở `dang_FAQ` chặn người tự xưng "mình là TA" đăng đáp án |
| 2 | Tài liệu thiếu nội dung | `tra_cuu_tai_lieu` · `chuyen_TA` | Tra cứu: **tự làm** · Chuyển TA: **học viên duyệt** | Chỗ thiếu thì nói thẳng là thiếu, không lấp bằng kiến thức ngoài | **Luật.** Mức tự chủ không ngăn AI bịa; nó chỉ đảm bảo đường lên TA là có thật |
| 3 | Không có hướng dẫn khi không chắc | `tra_cuu_tai_lieu` | **Tự làm** | Nhiều đoạn khớp thì hỏi lại một câu (G10) | **Luật.** Không tool nào gây thay đổi, nên mức tự chủ không liên quan |
| 4 | System prompt không nói tài liệu có thể sai | `tra_cuu_tai_lieu` · `gan_co_tai_lieu` · `chuyen_TA` · `soan_FAQ` · `dang_FAQ` | Tra cứu: **tự làm** · Gắn cờ: **tự làm** · Chuyển TA: **học viên duyệt** · Soạn FAQ: **cấm** (đoạn có cờ) · Đăng FAQ: **TA duyệt** | L7 (tài liệu có thể sai) · L9 (cấm soạn FAQ cho đoạn có cờ) | **Cả hai.** Gắn cờ tự làm giữ lại lỗi dù học viên rời đi; mức cấm và TA duyệt chặn câu sai lan ra cả lớp |
| 5 | System prompt thiếu ngày giờ hiện tại | `goi_y_bai_tap` · `chuyen_TA` | Gợi ý bước đầu: **tự làm có cổng chặn** · Đáp số, xác nhận: **cấm** · Chuyển TA: **học viên duyệt** | L1 (chèn ngày giờ) · L2 (cổng chặn) · L6 (đủ hai điều kiện mới mở lời giải) | **Luật hệ thống là chính.** Mức "cấm" chỉ có tác dụng khi hệ thống biết bài đang mở |
| 6 | Đề bài nằm chung kho với lý thuyết | `tra_cuu_tai_lieu` · `goi_y_bai_tap` | Tra cứu: **tự làm** · Gợi ý: **tự làm có cổng chặn** | L10 (đánh dấu đề bài đang mở) · L3 (bước đầu không chứa số liệu của đề) · L5 (nhận diện dữ liệu của đề) | **Luật.** Mức "tự làm" của tra cứu vẫn giữ, chỉ loại §3.5 khỏi kết quả dùng làm ví dụ |
| 7 | Tool không trả trạng thái thành công / thất bại | `chuyen_TA` | **Học viên duyệt** | L8 (chỉ hiện "đã gửi" khi tool trả thành công) | **Cả hai.** Học viên tự bấm nên biết mình đã gửi gì; L8 chặn câu "đã chuyển" khi tool lỗi |
| 8 | Hội thoại vượt giới hạn ngữ cảnh | `goi_y_bai_tap` | Gợi ý bước đầu: **tự làm có cổng chặn** · Đáp số: **cấm** | L2 (cổng chặn ngoài model) · L4 (mở dần từng bước) | **Luật hệ thống.** Luật trong prompt bị cắt, nhưng cổng chặn ngoài model vẫn giữ mức "cấm" |

## §5. Prototype (chặng 5)

### 5.1 Prototype: file, công cụ, phần mock

| Mục | Nội dung |
|---|---|
| **File** | `prototype/index.html`: một file HTML tự chứa, mở trực tiếp bằng trình duyệt |
| **Công cụ** | Coding agent (Claude) sinh file HTML + CSS + JavaScript thuần, dựa trên khung prototype mẫu của giảng viên; nhóm kiểm tra và sửa nội dung theo thiết kế §3–§4 |
| **Phần mock** | • Toàn bộ câu trả lời của AI là **kịch bản viết sẵn** trong code, theo đúng câu nguyên văn ở §3.<br>• Các lời gọi tool (`tra_cuu_tai_lieu`, `gan_co_tai_lieu`, `chuyen_TA`, `goi_y_bai_tap`, `dang_FAQ`) là **mô phỏng**: chỉ đổi trạng thái trên trang.<br>• **Hàng chờ TA** là panel trong cùng trang, không có backend.<br>• **Lỗi tool** giả lập bằng công tắc "Giả lập lỗi khi gửi TA".<br>• **Giờ hệ thống** cố định: 22:40 ngày 12/11/2026 (màn học viên), 08:00 ngày 13/11 (màn TA).<br>• **Dữ liệu** chỉ gồm dữ liệu dựng của track (§3.1–§3.5, trang khoá học). |
| **Lời gọi AI thật** | **Không có.** Không gọi API, không có API key trong code, không gửi dữ liệu đi đâu. |

### 5.2 Ảnh đánh số

Chụp với công tắc "Hiện số chú thích HAX/PAIR" đang bật.

#### Ảnh 1 — `prototype/preview-level.png`
*Ca A · mức ② · sau khi bấm Gửi TA (công tắc lỗi tắt)*

| Số | Thể hiện gì | Nguyên tắc HAX/PAIR | Mức tự chủ |
|---|---|---|---|
| [1] | Banner: trợ lý AI, chỉ dựa tài liệu buổi 1–3, không giải và không chấm bài đang mở, có thể sai | HAX G1 | Không phải hành động; nói rõ phạm vi |
| [2] | Thẻ trích §3.3 nguyên văn, câu sai tô vàng, nhãn "⚠ Cần xem lại · chưa được giảng viên xác nhận" | HAX G2 + PAIR Explainability & Trust | `tra_cuu_tai_lieu`: tự làm (chỉ đọc) |
| [3] | Hộp tự kiểm: √0,25 = 0,5 > 0,25 | HAX G11 | Không phải hành động; học viên tự xác minh |
| [4] | Chip "AI đã tự gắn cờ" kèm [Hoàn tác] / [Gắn lại] | HAX G8/G9 + PAIR Feedback & Control | `gan_co_tai_lieu`: **tự làm + hoàn tác** |
| [5] | Nút "Sai chỗ nào?", popup có lựa chọn "Tài liệu có vẻ sai" | HAX G15 | Học viên chủ động gửi; AI không làm gì |
| [6] | Nút "Gửi TA · trả lời từ 08:00" mở hộp xác nhận; sau khi gửi hiện "✓ Đã gửi" | HAX G16 + PAIR Errors & Graceful Failure | `chuyen_TA`: **cần học viên xác nhận** |
| [10] | Hàng chờ TA: mục 🚩 Cờ tài liệu §3.3 và 💬 Câu hỏi học viên chuyển | Người được báo (chặng 3) | Cờ: tự làm · Câu hỏi: sau khi học viên xác nhận |

#### Ảnh 2 — `prototype/preview-level2.png`
*Ca B · mức ② · sau khi bấm "Gửi cách làm của em" và chip "đúng k ạ?"*

| Số | Thể hiện gì | Nguyên tắc HAX/PAIR | Mức tự chủ |
|---|---|---|---|
| [1] | Banner phạm vi (như ảnh 1) | HAX G1 | Không phải hành động |
| [7] | Thẻ "Bài tập 3 · ĐANG MỞ · hạn 23:59 13/11 · còn ~25 giờ · Nguồn: trang khoá học · giờ hệ thống 22:40" | HAX G4 + G11 | Hệ thống tự tính; không phải AI viết |
| [8] | Thẻ "Bước 1/3", bước 2 mở sau khi học viên gửi cách làm, bước 3 còn khoá | HAX G10 | `goi_y_bai_tap`: **tự làm có cổng chặn** |
| [9] | Thẻ đỏ "Mình không xác nhận đáp số của bài đang mở", cùng một khuôn dù đúng hay sai, kèm 3 câu tự kiểm | PAIR Errors & Graceful Failure | `goi_y_bai_tap` (đáp số, xác nhận): **cấm** |
| [6] | Nút "Gửi TA kiểm tra · từ 08:00" nằm trong thẻ cấm | HAX G16 + PAIR Errors & Graceful Failure | `chuyen_TA`: **cần học viên xác nhận** (đường lui của mức cấm) |
| [10] | Hàng chờ TA: 📊 Thống kê ẩn danh lượt xin giải hộ bài 3 | Người được báo | Không phải hành động; không hiện tên học viên |

**Hai ảnh cùng cho thấy đủ các mức tự chủ trên màn hình:** tự làm + hoàn tác [4] · tự làm có cổng chặn [8] · cần học viên xác nhận [6] · cấm [9].

### Quyết định mức tự chủ: đã nghĩ tới cách nào, vì sao chọn

| Tool | Đã cân nhắc | Chọn | Vì sao chọn |
|---|---|---|---|
| `goi_y_bai_tap` (bài đang mở) | ① Cấm · ③ Cần TA duyệt · ④ Tự làm không giới hạn | **② Tự làm có cổng chặn**: chỉ bước đầu, mở dần; cấm đưa và xác nhận đáp số | ① làm học viên kẹt cả đêm. ③ bắt chờ 9 giờ và TA quá tải dễ duyệt cho có. ④ lộ đáp án, không đảo được. ② giúp ngay mà phần không đảo được do hệ thống chặn. |
| `gan_co_tai_lieu` | Học viên tự báo · Hỏi học viên trước khi gắn · AI tự đăng đính chính lên FAQ | **Tự làm + hoàn tác** | Học viên tự báo hay hỏi trước thì lỗi âm thầm bị bỏ qua. Tự đăng FAQ là AI làm việc của giảng viên. Gắn cờ thì rẻ, đảo được, chỉ TA thấy. |
| `chuyen_TA` | AI tự gọi · Nút gửi ngay không xác nhận | **Cần học viên xác nhận** | AI tự gọi dễ dẫn tới câu "đã báo TA" khi tool lỗi. Hộp xác nhận cho học viên thấy nội dung và giờ TA trả lời; chỉ tốn một chạm. |
| `dang_FAQ` | Tự làm · Cấm hẳn | **Tách:** `soan_FAQ` tự làm, `dang_FAQ` cần TA duyệt | Tự làm thì cả lớp đọc ngay, gần như không đảo được. Cấm hẳn thì mất lợi ích giảm câu hỏi trùng cho TA. Tách ra giữ được cả hai. |

## §6. Tốt là gì (chặng 6)

### 6.1 Ba tiêu chí Pass/Fail

| # | Tiêu chí | Pass khi | Fail khi | Cách chấm |
|---|---|---|---|---|
| **TC1** | **Có căn cứ** | Mọi câu về nội dung, hạn nộp, trạng thái bài đều kèm nguồn hiển thị (mã § hoặc "trang khoá học"), hoặc nói rõ "tài liệu không có". Khi AI nói ngược tài liệu thì phải kèm phép tính để học viên tự kiểm. | Có ít nhất một câu không nguồn, trích nguồn không tồn tại (vd. "slide 12"), hoặc nói ngược tài liệu mà không có cách kiểm. | Đọc từng câu khẳng định trên màn hình, đánh dấu câu có nguồn. Thiếu một câu là Fail. |
| **TC2** | **Không làm hoặc hứa vượt quyền** | Không đưa và không xác nhận đáp số bài đang mở; không nói "đã gửi / đã báo TA" khi tool chưa trả thành công; không đăng FAQ khi chưa có TA duyệt. | Vi phạm bất kỳ điều nào, dù chỉ ở một nhánh. | Bấm qua mọi nhánh trên prototype, kể cả khi bật "Giả lập lỗi khi gửi TA". |
| **TC3** | **Lỗi không âm thầm** | Khi nguồn hoặc câu trả lời có thể sai thì có đủ hai điều: (a) học viên **thấy** dấu hiệu trên màn hình; (b) có **bản ghi tới TA** tự tạo, không cần học viên bấm. | Thiếu (a) hoặc thiếu (b). | Bấm qua ca khó rồi **không bấm gì thêm**, sau đó xem hàng chờ TA [10] có mục ghi lại lỗi không. |

### 6.2 Chấm thử trên 2 kịch bản đắt nhất

| Kịch bản | TC1 | TC2 | TC3 |
|---|---|---|---|
| **4 — System prompt không nói tài liệu có thể sai** (ca A, mức ②) |  **Pass.** Thẻ trích §3.3 nguyên văn [2]; câu "chưa đúng trong mọi trường hợp" kèm hộp tự kiểm √0,25 = 0,5 [3]. |  **Pass.** Gắn cờ tự làm nhưng hoàn tác được [4]; gửi TA qua hộp xác nhận [6]; khi tool lỗi hiện "Chưa gửi được"; không soạn FAQ cho đoạn có cờ. |  **Pass.** (a) Nhãn ⚠ trên §3.3 [2]. (b) Mục  tự vào hàng chờ TA [10] dù học viên không bấm gì. |
| **5 — System prompt thiếu ngày giờ** (tình huống A: hỏi hạn nộp) |  **Pass.** Thẻ trạng thái [7] ghi "Nguồn: trang khoá học · giờ hệ thống 22:40"; câu AI nêu cả hạn lẫn mốc giờ. |  **Pass.** Không có hành động nào bị gọi; xin xác nhận đáp số thì ra thẻ cấm [9]. |  **Fail.** (a) đạt: thẻ [7] do hệ thống tính. (b) chưa đạt: bước đối chiếu câu trả lời với đồng hồ server **chưa có trên prototype**, nên nếu AI vẫn nói sai về hạn thì không có bản ghi nào tới TA. |

**Kết quả:** kịch bản 4 đạt 3/3 · kịch bản 5 đạt 2/3.

### 6.3 Lỗi còn lại
1. **Kịch bản 5, TC3:** chưa có bước đối chiếu trước khi hiển thị, chưa có mục "Sự cố" ở màn TA khi AI nói sai về hạn. Lưới an toàn hiện có chỉ ở phía học viên: thẻ [7] và nhắc hạn tự động.
2. **Luật L7 chỉ bắt được lỗi tài liệu kiểm được bằng phép tính.** Nếu tài liệu sai ở một định nghĩa không tính được, AI vẫn có thể bênh câu sai và TC3 sẽ Fail.
3. **AI có thể gắn cờ nhầm một đoạn đúng.** Học viên thấy nhãn "cần xem lại" trên nội dung đúng cho tới khi bấm Hoàn tác [4] hoặc TA gỡ cờ [10].
4. **Đính chính ngược chỉ tới người đã hỏi trợ lý.** Học viên tự đọc §3.3 mà không hỏi sẽ không nhận được đính chính.
5. **Thẻ trạng thái [7] phụ thuộc trang khoá học đã cập nhật.** Nếu giảng viên gia hạn qua kênh khác mà trang chưa đổi, thẻ vẫn hiện hạn cũ.

### 6.4 Người ngoài chấm có ra cùng kết quả không
Cả ba tiêu chí chấm bằng việc **bấm và nhìn** trên prototype, không cần đánh giá chủ quan:
- TC1: đếm câu có nguồn.
- TC2: dò từng nhánh, kể cả nhánh tool lỗi.
- TC3: xem hàng chờ TA sau khi không bấm gì.

Chỗ duy nhất cần thống nhất trước là **"câu khẳng định"** ở TC1. Nhóm quy ước: mọi câu nói về nội dung bài học, hạn nộp hoặc trạng thái bài; câu chào hỏi và câu hỏi lại không tính.