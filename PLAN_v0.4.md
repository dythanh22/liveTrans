# PLAN — Phụ đề tiếng Việt trực tiếp cho âm thanh máy tính

> **Phiên bản:** v0.4 — Windows và Ubuntu song song từ đầu, ngày 09/11/2026.
> **Trạng thái:** đủ cấu trúc để bắt đầu xác nhận phạm vi và thử nghiệm kỹ thuật; chưa phải SRS đã nghiệm thu, chưa chứng minh tính khả thi.
> **Cơ sở:** PLAN v0.3 và yêu cầu ngày 09/11/2026: triển khai Windows và Ubuntu song song từ đầu, có phương án chính và dự phòng. Bản này thay thế v0.3; chỉ cập nhật kế hoạch, chưa triển khai mã nguồn ứng dụng.
> **Nguyên tắc:** chứng minh một luồng dùng được trước, mở rộng bằng bằng chứng sau.

## 0. Cách sử dụng tài liệu

### 0.1 Nhãn và thứ tự ưu tiên

| Nhãn | Ý nghĩa |
|---|---|
| **Kế thừa** | Mục tiêu hoặc lựa chọn được v0.2 ghi là đã thống nhất; không đồng nghĩa đã kiểm chứng kỹ thuật |
| **Đề xuất v0.3/v0.4** | Thiết kế hoặc ngưỡng dự kiến, chưa mặc nhiên được xác minh |
| **Đã chốt 09/11/2026** | Chủ dự án yêu cầu hỗ trợ Windows và Ubuntu từ đầu, có phương án chính/dự phòng; không đồng nghĩa mọi phương án kỹ thuật đã chạy được |
| **Cần xác nhận** | Quyết định của chủ dự án còn thiếu; không tự ghi là đã chốt |
| **Cần thử** | Giả thuyết phải đo trên môi trường thực tế |
| **Đã đo** | Chỉ sử dụng khi có kết quả, ngày đo và môi trường; hiện chưa có mục nào mang nhãn này |

Thứ tự xử lý mâu thuẫn: quyết định mới được chủ dự án xác nhận → phạm vi tại mục 2 → yêu cầu tại mục 5–6 → thiết kế dự kiến. Những ý tưởng từ Cicada không tự trở thành yêu cầu bắt buộc.

Các ngưỡng số mới trong v0.3 là **đề xuất để thử**, chưa phải cam kết chất lượng. Ghi ngưỡng trước mỗi thử nghiệm; nếu sửa sau khi đo phải lưu lý do, giá trị cũ và chạy lại phép thử liên quan.

### 0.2 Đọc theo nhu cầu

- Muốn hiểu sản phẩm và phạm vi: mục 1–3.
- Muốn hiểu hành vi và tiêu chí đạt: mục 4–7.
- Muốn bắt đầu công việc: mục 8–10.
- Muốn kiểm soát quyết định, rủi ro và thay đổi: mục 11–14.

**Chưa thực hiện trong lần biên soạn này:** khảo sát đối thủ, kiểm tra giá API hiện hành, xác minh khả năng thư viện, đọc mã nguồn Cicada hoặc chạy spike. Không coi tên công nghệ hay mức chi phí trong tài liệu là kết quả kiểm chứng.

## 1. Product Brief — Bài toán và giá trị

### 1.1 Tầm nhìn

Ứng dụng desktop thu **lời nói trong âm thanh đang phát trên thiết bị đầu ra được chọn**, nhận dạng, dịch sang tiếng Việt và hiển thị phụ đề nổi. Người dùng có thể theo dõi YouTube, phim, tin tức và livestream mà không phụ thuộc phụ đề của từng trình phát.

“Mọi âm thanh trên máy” là **tầm nhìn về độ phủ nguồn**, không phải cam kết nhận dạng mọi loại âm thanh, mọi thiết bị cùng lúc, mọi nội dung bảo vệ hay mọi chế độ toàn màn hình. Ma trận hỗ trợ thực tế phải công bố theo kết quả thử.

### 1.2 Người dùng và mục tiêu

| Nội dung | Lựa chọn |
|---|---|
| Người dùng dẫn dắt | Chủ dự án, xem video/phim/tin tức; kế thừa v0.2 |
| Công việc cần hoàn thành | Bật phụ đề nhanh, hiểu nội dung chính, đọc kịp, không phải tìm sub riêng |
| Ngôn ngữ đích | Tiếng Việt |
| Ngôn ngữ nguồn hướng tới | Anh, Trung, Nhật, Hàn; đánh giá riêng từng ngôn ngữ |
| Livestream | Thử trong MVP; chỉ công bố phù hợp nếu đạt tiêu chí độ trễ khi xem thật |
| Game | V2; không chặn MVP dành cho video |
| Mục tiêu dài hạn | Cá nhân trước, cân nhắc dịch vụ sau; giảm công sức thay đổi kiến trúc về sau, không hứa “không phải viết lại” |

### 1.3 Thước đo giá trị

1. Bản dịch giúp hiểu đúng nội dung chính, không đảo nghĩa các chi tiết quan trọng.
2. Người xem theo kịp phụ đề và hình ảnh, ít phải tua lại vì phụ đề.
3. Bật/tạm dừng thuận tiện; overlay không giành focus hay chặn điều khiển trình phát.
4. Chi phí thực phù hợp số giờ dùng; không tích lũy phụ đề trễ kéo dài.
5. Cài được và dùng được trên máy mục tiêu ngoài môi trường lập trình.

Sau khi có bản MVP, dùng thực tế ít nhất hai tuần. Mục tiêu đề xuất: tự nguyện dùng ≥ 3 buổi/tuần, ghi lý do bỏ dùng và các lần phải tắt phụ đề. Đây là tín hiệu giá trị cá nhân, không phải bằng chứng có thị trường.

### 1.4 Không làm trong MVP

Biên bản họp, tóm tắt, giọng đọc dịch, nhận diện/tách người nói, lưu ghi âm thường trực, tài khoản, đồng bộ, backend dịch vụ, xử lý file phụ đề ngoại tuyến, tự cập nhật, game, macOS và toàn bộ chế độ thu riêng từng ứng dụng.

Không tự xây chức năng hát/nhạc chuyên biệt. Nhạc có lời là nhóm thử riêng; chỉ bổ sung công tắc phân biệt hát/nói nếu đã chứng minh làm được.

## 2. Phạm vi theo giai đoạn

### 2.1 Các mốc sản phẩm

| Mốc | Phải chứng minh | Phạm vi |
|---|---|---|
| **G0 — Chuẩn bị** | Môi trường và giới hạn sử dụng đã rõ | Xác nhận máy mục tiêu, ngân sách, clip mẫu; khảo sát giải pháp thay thế có giới hạn thời gian |
| **G1 — Spike và bản chạy xuyên suốt** | Thu → STT → dịch → hiển thị trên cả Windows và Ubuntu | Một lõi dùng chung, hai bộ tích hợp OS; một STT, một dịch vụ dịch, một ngôn ngữ thử đầu tiên, ưu tiên bản dịch cuối |
| **G2 — MVP cá nhân hai nền tảng** | Xem video đủ tốt, có bản cài riêng cho Windows và Ubuntu | Hoàn thiện luồng lỗi, phụ đề, cấu hình, chi phí; đánh giá bốn ngôn ngữ và nghiệm thu riêng từng OS/profile |
| **G3 — V2** | Các cải tiến đem lại lợi ích đo được | Game borderless, local STT, glossary, fallback, song ngữ; chọn theo nhu cầu dùng thật |
| **G4 — Mở rộng/phát hành rộng** | Có nhu cầu ngoài cá nhân và vận hành được | macOS, cập nhật, phân phối rộng hoặc dịch vụ; lập kế hoạch riêng |

### 2.2 Hai nền tảng từ đầu — quyết định đã chốt

**Windows và Ubuntu cùng thuộc G0, G1 và MVP G2**, theo yêu cầu chủ dự án ngày 09/11/2026. Không còn giai đoạn “M2 mới bắt đầu Ubuntu”. Chủ dự án đang sử dụng cả hai OS; G0 chỉ cần xác nhận cấu hình/phiên bản và cách bố trí kiểm thử, không hỏi lại có muốn hỗ trợ cả hai hay không.

Dùng **một repo, một lõi và một bộ yêu cầu chung**. STT, dịch, VAD, session, queue, chi phí và phần lớn UI dùng chung; adapter riêng cho capture, cửa sổ, hotkey, keyring và vòng đời. Có thể lập trình từng phần tuần tự khi làm một mình, nhưng mỗi lát tích hợp phải được kiểm tra trên cả hai trước khi coi là hoàn tất đa nền tảng.

**Phương án chính:** Windows native và Ubuntu trên phiên Wayland thực tế của chủ dự án. Rust + Tauri là ứng viên ban đầu có điều kiện S1/S2/S5, chưa bảo đảm mọi tính năng overlay/hotkey hoạt động. Ghi chính xác Windows build, Ubuntu release, desktop/compositor, session và cấu hình màn hình tại G0; không suy từ tên OS ra khả năng hỗ trợ.

**Phương án dự phòng:** thử có điều kiện và nghiệm thu riêng theo mục 2.4. Không tự đổi phiên đăng nhập, cài lại hệ thống hoặc tuyên bố X11/XWayland luôn sẵn có. Nếu chỉ một OS đạt trước, cho phép bản thử riêng OS đó, nhưng chưa gọi là hoàn tất MVP hai nền tảng.

### 2.3 Giảm phạm vi có chủ đích

- Thiết kế interface nhà cung cấp ngay từ đầu; MVP chỉ cần **một adapter STT và một adapter dịch hoạt động tốt**.
- Bản dịch cuối là bắt buộc. Chữ nháp và dịch hai tầng chỉ đưa vào MVP nếu thử nghiệm cho thấy cải thiện khả năng theo dõi mà không vượt chi phí/độ trễ.
- Tiếng Việt là UI mặc định; tiếng Anh có thể thêm sau MVP. Không xây hệ thống dịch giao diện lớn ở G1.
- Giữ bốn ngôn ngữ là mục tiêu đánh giá. Nếu một ngôn ngữ chưa đạt, công bố rõ “thử nghiệm/chưa hỗ trợ tốt”, hoặc quyết định hoãn phát hành đủ bốn; không lấy trung bình chung để che kết quả yếu.
- Windows và Ubuntu đều thuộc MVP; game và local STT vẫn để sau. Các bản thử có thể ra khác ngày, nhưng không bỏ nhiệm vụ Ubuntu vì Windows đã chạy được.

### 2.4 Phương án chính và dự phòng theo thành phần

Các dòng sau là **kế hoạch thử**, không phải kết luận tương thích. Chỉ hiện phương án được xác minh là khả dụng trên máy đang chạy.

| Thành phần | Phương án chính | Dự phòng khi cần | Điều kiện/giới hạn |
|---|---|---|---|
| Overlay Windows | Tauri với tích hợp cửa sổ Windows đáp ứng focus/click-through | Adapter cửa sổ native; chỉ cân nhắc Qt/Electron nếu thử hẹp chứng minh có lợi | Không viết lại core; chạy lại S1/S5 và kiểm đóng gói |
| Overlay Ubuntu | Tauri trên Wayland, theo khả năng compositor hiện dùng | Thử XWayland nếu có; nếu vẫn không đạt, thử phiên X11 nếu hệ thống cung cấp và người dùng chọn | XWayland vẫn nằm trong phiên Wayland, không tương đương đăng nhập X11 và không mặc định giải quyết hotkey/always-on-top |
| Khi overlay Ubuntu chưa đủ | Điều chỉnh adapter theo khả năng môi trường đã xác minh | Cửa sổ phụ đề riêng, xem video ở cửa sổ và bố trí cạnh phụ đề | Chế độ dùng tạm có giới hạn; không đánh dấu FR-05 đạt overlay đầy đủ |
| Hotkey | Global hotkey qua cơ chế OS/framework hỗ trợ và đã thử | Thử cơ chế desktop/portal nếu có; nếu chưa đạt, nút Bắt đầu/Tạm dừng trong cửa sổ điều khiển | Tray chỉ dùng khi đã xác minh; không hứa nút trên cửa sổ thay thế trải nghiệm hotkey. Ghi FR-07 chưa đạt hoặc ngoại lệ được chấp nhận |
| Thu Windows | WASAPI loopback qua binding phù hợp | Đổi binding/adapter cùng API khi vấn đề nằm ở thư viện | Không tự đổi sang micro hoặc yêu cầu driver ảo |
| Thu Ubuntu | Thử monitor/loopback theo cấu hình PipeWire của máy | Thử giao diện tương thích PulseAudio hoặc monitor trên PulseAudio nếu thực tế có | Kiểm tra endpoint/backend; độc lập với việc đổi Wayland/X11. Không mặc định đổi display session sẽ sửa lỗi audio |
| Kho key | Kho bí mật của OS | Nhập key mỗi phiên, chỉ giữ trong bộ nhớ nếu kho bí mật không dùng được | Thông báo rõ; không lưu plaintext; không đồng bộ key giữa hai OS trong MVP |
| Phân phối | Một định dạng cài Windows và một định dạng Ubuntu phù hợp sau spike | Bản chạy thử đóng gói tự chứa nếu khả thi | Đều phải thử trên môi trường sạch; chưa đạt cài/gỡ thì chỉ ghi bản thử, không coi FR-32 hoàn tất |

**Trình tự chọn phương án:**

1. Chạy phép thử tối thiểu trên phương án chính, ghi lỗi tái hiện và phân biệt lỗi app, framework hay hạn chế môi trường.
2. Đặt timebox riêng cho từng thử nghiệm dự phòng; ưu tiên thay adapter nhỏ nhất. Không duy trì đồng thời nhiều framework UI nếu chưa có bằng chứng cần thiết.
3. Chỉ chọn dự phòng khi đã đạt AC liên quan, chi phí bảo trì chấp nhận được và có hướng dẫn quay lại. Các nhánh dự phòng không cần đều được xây ngay.
4. Thay đổi session/thiết lập OS do người dùng chủ động lựa chọn; trong app chỉ hiển thị hướng dẫn và profile đang dùng, không âm thầm chuyển.
5. Nếu dự phòng làm mất tính năng Must, ghi bản thử có giới hạn và kế hoạch xử lý; muốn coi đó là phạm vi MVP mới phải có quyết định rõ của chủ dự án.

### 2.5 Mức hỗ trợ và điều kiện phát hành

| Nhãn | Điều kiện | Cách công bố |
|---|---|---|
| Chưa kiểm thử | Chưa có kết quả trên đúng profile | Không suy diễn hỗ trợ từ việc build thành công |
| Bản thử có giới hạn | Chạy được nhưng còn Must chưa đạt, ví dụ cửa sổ phụ đề thay overlay hoặc chưa có hotkey | Liệt kê tính năng thiếu, cách dùng tạm và việc tiếp theo |
| MVP đạt trên profile | Tất cả Must và ngưỡng đã chốt đạt trên profile đó, gồm bản cài | Nêu OS, session, desktop/compositor, trình duyệt, phiên bản app |
| MVP hai nền tảng hoàn tất | Windows đạt và ít nhất một profile Ubuntu đã chọn đạt; đã đánh giá phương án Wayland chính | Nếu Ubuntu chỉ đạt trên X11, ghi rõ “Ubuntu X11 đạt; Wayland chưa đạt/giới hạn”, không công bố hỗ trợ Ubuntu chung chung |

Mục tiêu chính vẫn là Windows + Ubuntu Wayland. X11 là profile dự phòng hợp lệ nếu khả dụng và người dùng chọn. Nếu X11 đạt đầy đủ, có thể nghiệm thu MVP hai nền tảng theo profile này và giữ cải thiện Wayland trong backlog, không che giới hạn hoặc buộc hai bản phát hành cùng ngày.

## 3. Ngân sách và ràng buộc sử dụng

### 3.1 Mức dự kiến, chưa phải báo giá

V0.2 đề xuất $5–20 cho spike và $15–30/tháng cho dùng cá nhân. Giữ làm **ngân sách dự kiến cần chủ dự án xác nhận**, không coi là hạn mức đã cho phép chi tiêu. Chưa có giá API hiện hành được xác minh trong bản này.

Chi phí mục tiêu phải tính theo **giờ xem**, gồm cả khoảng im lặng, retry, chữ nháp, phần âm thanh gửi lặp và ngữ cảnh dịch:

`Chi phí/giờ xem = Tổng phí STT + dịch + các phí liên quan của phiên, chia số giờ phiên`

`Trần chi phí/giờ xem = Ngân sách tháng / Số giờ xem dự kiến trong tháng`

| Thời lượng giả định, 30 ngày/tháng | Giờ/tháng | Với $15/tháng | Với $30/tháng |
|---|---:|---:|---:|
| 1 giờ/ngày | 30 | $0,50/giờ | $1,00/giờ |
| 2 giờ/ngày | 60 | $0,25/giờ | $0,50/giờ |
| 3 giờ/ngày | 90 | khoảng $0,17/giờ | khoảng $0,33/giờ |

Đây là phép chia ngân sách, **không phải giá nhà cung cấp**. Thuế, tỷ giá và phí thanh toán nếu có phải cộng khi quyết định khả năng chi trả.

Ngân sách thử là **tổng cho cả hai nền tảng**, không tự nhân đôi. Ưu tiên audio mẫu/mock và replay cho phép thử logic; chỉ gọi API thật khi cần kiểm chất lượng hoặc tích hợp. Nếu tổng thử vượt dự kiến, giảm tổ hợp thử hoặc điều chỉnh ngân sách trước khi tiếp tục. Khi dùng cả hai OS, trần phía app chỉ theo phiên/cài đặt; cùng key có thể chia sẻ quota và hóa đơn ở nhà cung cấp, MVP chưa có bộ đếm tháng đồng bộ.

### 3.2 Chính sách chi phí

- Trước khi gọi API tính phí: ghi giá từ tài liệu chính thức, ngày kiểm tra, đơn vị tính, mức làm tròn/tối thiểu, cách tính streaming và retry.
- Đo số phút thực gửi, số request, token và mức ước tính; đối chiếu dashboard/hóa đơn khi có số liệu.
- MVP có ước tính chi phí phiên hoặc lượng dùng đủ để quy đổi, kèm ngày bảng giá và cảnh báo ngân sách phiên. Bộ đếm tháng, preset và tự chuyển cấu hình để V2.
- Nếu nhà cung cấp hỗ trợ trần cứng thì cấu hình; không mặc định mọi nhà cung cấp đều có. Trần do app tính là biện pháp bổ sung dựa trên ước tính.
- Đạt trần ước tính: ngừng tạo yêu cầu mới và thông báo. Yêu cầu đã gửi có thể vẫn bị tính phí; không hứa hóa đơn tuyệt đối không vượt trần.
- VAD không tự bảo đảm im lặng miễn phí. Phải kiểm tra hợp đồng streaming/phiên và tác động đóng/mở kết nối tới độ trễ.

## 4. Use case và hành vi sản phẩm

### 4.1 Trạng thái

| Trạng thái | Thu âm | Yêu cầu xử lý mới | Hiển thị |
|---|---|---|---|
| Tạm dừng | Không | Không | Ẩn phụ đề, tray báo dừng |
| Đang chạy | Có | Theo cấu hình, VAD và ngân sách | Phụ đề và chỉ báo thu |
| Suy giảm | Chỉ tiếp tục nếu cần để phục hồi và vẫn được phép | Retry có giới hạn; không xếp hàng vô hạn | Trạng thái lỗi rõ, không giả làm bản dịch |
| Đã thoát | Không | Không | Không |

Khởi động app, khởi động lại sau crash hoặc thức dậy sau sleep đều về **Tạm dừng**. Một phím tắt đổi Tạm dừng ↔ Đang chạy; nhấn khi Suy giảm thì về Tạm dừng. Thoát qua tray. MVP không có “ẩn nhưng vẫn nghe”. Khi profile chưa hỗ trợ hotkey/tray, cửa sổ điều khiển phải luôn cung cấp Bắt đầu/Tạm dừng/Thoát; đây là dự phòng có nhãn giới hạn theo mục 2.4–2.5, không thay đổi quy tắc phiên và bảo vệ dữ liệu.

Tạm dừng vô hiệu hóa phiên hiện tại, xóa hàng đợi và ngừng gửi nội dung mới; hủy yêu cầu tại client nếu hỗ trợ. Phản hồi của phiên cũ không được hiển thị sau đó, kể cả khi bật lại nhanh. Không thể thu hồi dữ liệu đã gửi hoặc bảo đảm nhà cung cấp ngừng xử lý ngay.

### 4.2 Danh mục use case và nghiệm thu hành vi

| ID | Tình huống và luồng chính | Ngoại lệ/hành vi bắt buộc | Mốc |
|---|---|---|---|
| UC-01 | Cài mới → thông tin dữ liệu → chọn nguồn, nhập key → kiểm tra → clip mẫu → Tạm dừng | Key sai/mất mạng vẫn sửa được cấu hình; clip dùng API chỉ chạy sau thao tác chủ động | MVP |
| UC-02 | Bật bằng tray/phím tắt → thu → dịch → phụ đề | Không có tiếng nói thì không hiện câu bịa; lỗi có dấu hiệu riêng | MVP |
| UC-03 | Tự nhận ngôn ngữ hoặc khóa thủ công | Đoạn quá ngắn không đổi ngôn ngữ liên tục; khóa nguồn được áp dụng cho dữ liệu mới; nguồn ngoài phạm vi báo rõ | MVP |
| UC-04 | Tạm dừng/tiếp tục | Không hiện câu đến muộn; tiếp tục chỉ nhận âm thanh mới | MVP |
| UC-05 | Chỉnh font, nền, cỡ, vị trí, màn hình; xem trước bằng văn bản mẫu | Chế độ chỉnh vị trí riêng mới nhận chuột; tháo màn hình thì đưa overlay về màn hình còn dùng được | MVP |
| UC-06 | Chuyển thiết bị mặc định hoặc chọn thiết bị cố định | Theo dõi thiết bị mặc định chỉ khi đang ở chế độ đó; mất thiết bị cố định phải báo, không âm thầm đổi nguồn thu | MVP |
| UC-07 | Nhạc nền, tiếng ồn, nói chồng | Kiểm tra/lọc câu lặp bất thường; không hứa VAD loại bỏ hoàn toàn nhạc; không tách người nói | MVP |
| UC-08 | Im lặng rồi có lời nói trở lại | Đo chi phí thực khi im lặng và độ trễ phục hồi; không tự bỏ mất đầu câu vì tiết kiệm phí | MVP; tối ưu V2 |
| UC-09 | Mất mạng, key sai, giới hạn tốc độ hoặc hết tín dụng | Phân loại lỗi; timeout/retry giới hạn; key sai/hết tín dụng không retry liên tục; chỉ phục hồi từ âm thanh hiện tại | MVP |
| UC-10 | Nhập/sửa key và cấu hình adapter | Không lưu key vào log; đổi adapter chỉ khi Tạm dừng trong MVP; chọn nhiều nhà cung cấp/local để V2 | MVP/V2 |
| UC-11 | Xem lượng dùng và ước tính chi phí | MVP cảnh báo/ngừng gửi theo trần phiên ước tính; thống kê tháng và preset để V2 | MVP/V2 |
| UC-12 | Thêm glossary, biến thể nghe sai | Phải đo giảm lỗi và tránh sửa nhầm từ thường; không coi thay chuỗi đơn giản là giải pháp đủ | V2 |
| UC-13 | Xuất chẩn đoán thủ công | Log có mốc thời gian, mã lỗi, phiên bản; không key, audio, transcript hay bản dịch mặc định | MVP |
| UC-14 | Xem thoại game borderless | Đo focus, FPS và thời gian khung hình; exclusive fullscreen chỉ hỗ trợ khi có bằng chứng; không inject game | V2 |
| UC-15 | Cuộc gọi/thông báo/ứng dụng khác phát tiếng | Nói rõ thu đầu ra có thể gồm mọi ứng dụng trên đầu ra đó; không thu micro không có nghĩa loại được voice chat | MVP |
| UC-16 | Crash hoặc sleep/wake | Giữ cấu hình, về Tạm dừng, xóa phiên cũ; không tự khôi phục việc gửi audio | MVP |
| UC-17 | Tua, đổi video/tab hoặc nội dung | Có thao tác “Phiên mới/Xóa phụ đề và ngữ cảnh”; không giả định biết sự kiện tua của trình phát qua loopback | MVP |
| UC-18 | Xem toàn màn hình trình duyệt, đổi cửa sổ, thay DPI/màn hình | Thử trên trình duyệt mục tiêu; nếu không hỗ trợ phải có cách xem thay thế và giới hạn công bố | MVP |
| UC-19 | Nhiều ứng dụng phát đồng thời; video 1,25×/1,5× | MVP thu hỗn hợp của một đầu ra; hướng dẫn tắt nguồn không muốn dịch. Kiểm thử tăng tốc, chưa cam kết chất lượng ở mọi tốc độ | MVP kiểm tra giới hạn |
| UC-20 | Xử lý chậm, câu dài, kết quả trả sai thứ tự | Giới hạn độ dài đoạn và hàng đợi; bỏ câu quá cũ; không để bản nháp ghi đè bản cuối | MVP |

### 4.3 Quy tắc phụ đề

- Điểm khởi đầu thử: tối đa hai dòng, khoảng 40 ký tự/dòng, chữ sáng có viền trên nền bán trong suốt. Kích thước thực, cách xuống dòng và thời gian giữ phải hiệu chuẩn theo tiếng Việt và màn hình.
- Bản cuối có thể hiển thị theo cụm ngắn. Không bắt buộc chờ một câu dài hoàn tất; không cắt mất thông tin phủ định, số liệu, tên hoặc quan hệ nhân quả chỉ để đủ dòng.
- Chữ nháp nếu bật: phân biệt trực quan, giới hạn tần suất sửa, giữ vùng hiển thị ổn định; đánh giá mức gây rối mắt so với chỉ bản cuối.
- Câu hết hạn không chen vào trước nội dung hiện tại. Khi ưu tiên bắt kịp và phải bỏ câu, ghi số lượng bỏ vào thống kê, tránh đạt độ trễ tốt bằng cách bỏ phần lớn nội dung.
- Dịch lỗi: mặc định chỉ báo lỗi nhỏ. Văn bản nguồn “chưa dịch” là tùy chọn rõ ràng, không ngầm bật song ngữ.
- Overlay không cướp focus khi xem; Settings và chế độ chỉnh vị trí được nhận tương tác chủ động. Mờ khi hover là tùy chọn sau thử nghiệm, không là điều kiện MVP.
- Chỉ báo thu ở tray; khi overlay ẩn do im lặng, trạng thái thu vẫn phải kiểm tra được. Nếu tray không nhìn thấy ở toàn màn hình, thử chỉ báo nhỏ không gây phiền.

## 5. Yêu cầu chức năng và truy vết

Giữ ID FR từ v0.2 để theo dõi thay đổi. **Must** là điều kiện nghiệm thu của đúng mốc ghi trong bảng; **Conditional** chỉ vào MVP khi quyết định sau spike; **Later** không chặn MVP.

| ID | Yêu cầu v0.4 | Ưu tiên/mốc | UC |
|---|---|---|---|
| FR-01 | Thu một đầu ra, chế độ theo mặc định hoặc chọn cố định | Must MVP | 02, 06, 15, 19 |
| FR-02 | Phát hiện lời nói và chia đoạn có giới hạn thời gian | Must MVP | 07, 08, 20 |
| FR-03 | Nhận dạng và nhận diện ngôn ngữ; đánh giá en/zh/ja/ko riêng | Must MVP | 02, 03 |
| FR-04 | Dịch tiếng Việt với ngữ cảnh có giới hạn | Must MVP | 02, 17 |
| FR-05 | Overlay trong suốt, không chặn thao tác, không giành focus | Must MVP | 02, 05, 18 |
| FR-06 | Cập nhật bản cuối ổn định; partial có revision nếu được bật | Final Must; partial Conditional | 02, 20 |
| FR-07 | Phím tắt Tạm dừng/Đang chạy; thoát từ tray | Must MVP | 04 |
| FR-08 | Font/cỡ/nền/vị trí/màn hình; xem trước; lưu cấu hình | Must MVP | 05 |
| FR-09 | Cấu hình một STT + một dịch vụ dịch, lưu key an toàn; adapter thay thế được | Must MVP; chọn nhiều provider V2 | 01, 10 |
| FR-10 | Giải thích audio/text đi đâu, đồng ý trước lần gửi đầu | Must MVP | 01, 15 |
| FR-11 | Fallback chỉ sang provider đã được người dùng chọn và cho phép | Later V2 | 09, 10 |
| FR-12 | Lượng dùng và ước tính chi phí phiên; thống kê tháng/preset sau | Must MVP cơ bản | 11 |
| FR-13 | Glossary và cách xử lý xung đột | Later V2 | 12 |
| FR-14 | STT local, tải và quản lý model | Later V2; có thể nâng ưu tiên sau spike | 10 |
| FR-15 | Chế độ game, đo tác động tài nguyên | Later V2 | 14 |
| FR-16 | Song ngữ tùy chọn | Later V2 | 05 |
| FR-17 | Hỗ trợ Ubuntu từ G1, ưu tiên Wayland và có profile dự phòng được kiểm chứng | Must MVP | 02, 18 |
| FR-18 | Xuất SRT, xác định rõ mốc thời gian phiên | Later V2 | 02 |
| FR-19 | Tối ưu gửi/kết nối khi im lặng | Later V2; phép đo có từ MVP | 08 |
| FR-20 | macOS | Later G4 | 02 |
| FR-21 | Tự cập nhật | Later G4 | 01 |
| FR-22 | Khóa ngôn ngữ thủ công | Must MVP | 03 |
| FR-23 | Chỉ báo thu và thao tác dừng dễ tìm | Must MVP | 02, 15 |
| FR-24 | Lỗi mạng, provider và âm thanh được báo đúng loại | Must MVP | 06, 09 |
| FR-25 | Hướng dẫn cấu hình ngắn và clip mẫu sau khi có key | Must MVP tối giản | 01 |
| FR-26 | Xuất log chẩn đoán đã loại dữ liệu nhạy cảm | Must MVP tối giản | 13 |
| FR-27 | Trần phiên ước tính: cảnh báo và ngừng gửi; trần tháng/preset sau | Must MVP cơ bản | 11 |
| FR-28 | Phục hồi thiết bị/mạng; sleep/crash về Tạm dừng | Must MVP | 06, 09, 16 |
| FR-29 | Hướng dẫn xử lý game không hiện overlay; tự phát hiện chỉ khi khả thi | Later V2 | 14 |
| FR-30 | Phiên mới: xóa ngữ cảnh, hàng đợi và phụ đề cũ | Must MVP | 17 |
| FR-31 | Timeout, hàng đợi hữu hạn, hủy/vô hiệu kết quả cũ, revision | Must MVP | 04, 09, 20 |
| FR-32 | Bản cài, mở/đóng/gỡ trên máy sạch; không cần môi trường dev | Must MVP | 01 |
| FR-33 | Ma trận hỗ trợ Windows/Ubuntu, session, nguồn, thiết bị, trình duyệt, toàn màn hình và giới hạn | Must MVP | 06, 18, 19 |
| FR-34 | Nhận diện profile/capability đã kiểm chứng; hiển thị giới hạn và hướng dẫn dự phòng; không tự đổi session OS | Must MVP | 01, 04, 05, 18 |

## 6. Chất lượng, cách đo và ngưỡng nghiệm thu

### 6.1 Định nghĩa độ trễ

Không dùng một số “≤ 4 giây” cho mọi cách đo. Với mỗi đoạn/cụm được đánh giá, ghi mốc trên cùng đồng hồ đơn điệu:

- `t_audio_start`: khởi đầu phần lời nói nguồn tương ứng, theo timeline audio.
- `t_audio_end`: kết thúc phần lời nói tương ứng; không thay bằng thời điểm VAD quyết định đóng đoạn.
- `t_segment_closed`, `t_stt_final`, `t_translate_done`: mốc từng chặng.
- `t_first_vi_shown`, `t_final_shown`: UI xác nhận đã hiển thị, không dùng thời điểm backend phát event thay thế.

`L_first = t_first_vi_shown − t_audio_start`: thời gian tới chữ Việt đầu tiên có nghĩa.

`L_final = t_final_shown − t_audio_end`: độ trễ hoàn tất sau phần lời nói tương ứng.

`L_start_to_final = t_final_shown − t_audio_start`: tổng chờ từ đầu đoạn; báo kèm độ dài đoạn để không che thời gian chờ câu dài.

Với clip chuẩn, dùng mốc lời nói tham chiếu. Khi không căn chỉnh được tự động, ghi rõ mốc ước tính và chấm tay một tập con. Nhãn “final” của STT và “final” của phụ đề phải được phân biệt.

### 6.2 NFR đề xuất

| ID | Nội dung | Ngưỡng/cách nghiệm thu đề xuất |
|---|---|---|
| NFR-01 | Độ trễ cuối | L_final p50 ≤ 4 giây, p90 ≤ 6 giây; báo L_start_to_final, độ dài đoạn, số mẫu và tỷ lệ câu bỏ. Đây là cách cụ thể hóa mới cần xác nhận sau spike |
| NFR-02 | Phản hồi sớm | Nếu bật partial: L_first p50 ≤ 2 giây, p90 ≤ 3 giây. Nếu chỉ final: vẫn báo L_first và kiểm thử theo kịp hình ảnh; không mặc định được miễn trải nghiệm chờ |
| NFR-03 | Tài nguyên | Đo CPU, RAM, GPU trên máy mục tiêu. Chốt trần sau G1 trước G2; so với trình phát chạy cùng nội dung không có app |
| NFR-04 | Game | V2 mới chốt ngưỡng FPS và p95 thời gian khung hình; không dùng nhận xét “không thấy giật” thay phép đo |
| NFR-05 | Ổn định | MVP cá nhân: phiên 1 giờ; bản đưa cho người ngoài: 3 giờ. Không crash, không hàng đợi tăng vô hạn. Mức tăng RAM cho phép phải chốt sau baseline G1 |
| NFR-06 | Không làm phiền | 0 lần giành focus/chặn điều khiển trong kịch bản thao tác đã ghi; thử cả video toàn màn hình |
| NFR-07 | Riêng tư | Không audio/text/key trong log mặc định; chỉ gửi tới endpoint đã cấu hình/cho phép; dữ liệu mẫu/chẩn đoán không gửi tự động |
| NFR-08 | Chi phí | Chi phí/giờ xem không vượt trần được tính theo mục 3; báo riêng im lặng, nội dung nói liên tục và retry |
| NFR-09 | Dễ đọc | ≥ 80% đoạn chấm đọc xong không phải tua vì phụ đề; điểm thoải mái trung vị ≥ 4/5; số dòng/ký tự chỉ là tham số hiệu chuẩn |
| NFR-10 | Đúng nghĩa | Đề xuất: ≥ 90% ý chính trong đoạn tham chiếu được giữ; ≤ 2% đơn vị chấm có lỗi nghiêm trọng. Luôn báo số lỗi tuyệt đối và loại lỗi; tiêu chí bảo đảm hiểu phải do người đủ khả năng ngôn ngữ kiểm |
| NFR-11 | Bám thời gian thực | Đề xuất tuổi tối đa câu được hiển thị: 8 giây từ t_audio_end; phần lời nói bị bỏ do quá hạn/quá tải ≤ 5% trên clip bình thường. Chốt lại bằng thử đọc; không áp dụng để che lỗi nhận dạng |
| NFR-12 | Cài đặt/phục hồi | Cài/mở/gỡ trên máy sạch; cấu hình lần đầu mục tiêu ≤ 5 phút khi đã có key và mạng. Sau khi hệ điều hành sẵn sàng, đổi đầu ra mục tiêu ≤ 2 giây hoặc báo trạng thái rõ |

Các ngưỡng đúng nghĩa và độ trễ phải xem **theo từng ngôn ngữ và từng profile nền tảng**, không chỉ tổng hợp. Tài nguyên và soak đo riêng từng máy/OS; không gộp số liệu Windows với Ubuntu. Cùng chuẩn chất lượng, nhưng CPU/RAM phải có baseline riêng nếu phần cứng khác nhau. Đủ nhanh nhưng dịch sai, hoặc đúng nhưng người xem không đọc kịp, đều chưa đạt.

## 7. Bộ thử và nghiệm thu MVP

### 7.1 Dữ liệu thử

Dùng **20 clip nội dung × 2–5 phút**, phân bố chính xác như sau; có thể dùng trích đoạn do chủ dự án được phép sử dụng để thử nghiệm. Clip dùng để phân phối kèm app phải có quyền sử dụng phù hợp.

| Nhóm | Anh | Trung | Nhật | Hàn | Tổng |
|---|---:|---:|---:|---:|---:|
| Tin tức/lời nói rõ | 1 | 1 | 1 | 1 | 4 |
| YouTube nói chuyện/tên riêng | 1 | 1 | 1 | 1 | 4 |
| Phim có nhạc/hiệu ứng | 1 | 1 | 1 | 1 | 4 |
| Phỏng vấn/nói chồng | 1 | 1 | 1 | 1 | 4 |
| Livestream/tốc độ không đều | 1 | 1 | 1 | 1 | 4 |
| **Tổng** | **5** | **5** | **5** | **5** | **20** |

Thêm kịch bản chức năng riêng: im lặng, nhạc không lời/có lời, đổi ngôn ngữ, tua/chuyển video, tiếng Việt đầu vào, nguồn ngoài phạm vi, mất mạng, rút thiết bị, đổi màn hình, sleep/wake và nhiều ứng dụng phát tiếng.

Mỗi clip ghi nguồn, thời lượng, ngôn ngữ, đặc điểm, quyền sử dụng, đoạn tham chiếu 30–60 giây, transcript/ý chính và bản dịch được kiểm tra. Người chấm đúng nghĩa cần biết ngôn ngữ nguồn hoặc có tham chiếu đáng tin cậy; tự chấm “dễ hiểu” không thay được kiểm tra đúng nghĩa.

Đề xuất chia 12 clip hiệu chỉnh và 8 clip kiểm tra giữ lại (mỗi ngôn ngữ 3 + 2). Không liên tục sửa prompt theo tập giữ lại rồi gọi đó là kết quả độc lập. Tập nhỏ chỉ phục vụ quyết định MVP, không tuyên bố chất lượng tổng quát.

### 7.2 Rubric chấm

- **Đúng nghĩa:** chia đoạn tham chiếu thành các ý/cụm có nghĩa; đếm ý giữ đúng, bị bỏ và sai nghiêm trọng.
- **Sai nghiêm trọng:** đảo phủ định, sai chủ thể/hành động trọng yếu, sai số liệu quan trọng, bịa thông tin làm thay đổi ý chính.
- **Dễ đọc:** tỷ lệ đọc kịp, số lần tua vì phụ đề, mức khó chịu khi chữ bị thay; chủ dự án và thêm 2–3 người nếu có.
- **Độ phủ:** đo riêng lời nói bỏ do quá tải, VAD/nhận dạng bỏ sót và lỗi API. Không chỉ chấm những câu thành công.
- **Chi phí/độ trễ:** cùng cấu hình và cùng clip; ghi mạng, máy, provider/model, prompt, VAD, phiên bản app.

### 7.3 Ma trận nghiệm thu

| AC | Kịch bản | Điều kiện đạt | Yêu cầu chính |
|---|---|---|---|
| AC-01 | Máy sạch, key có sẵn, cài và chạy mẫu | Cài/mở/gỡ được; vào Tạm dừng; lần gửi đầu chủ động | FR-09, 10, 25, 32; NFR-12 |
| AC-02 | Bộ 20 clip, báo riêng 8 clip giữ lại | Đạt độ trễ, đúng nghĩa, độ phủ, đọc và chi phí theo từng ngôn ngữ công bố | FR-02, 03, 04, 06; NFR-01, 02, 08, 09, 10, 11 |
| AC-03 | Im lặng, nhạc và nói chồng | Không phụ đề bịa kéo dài; có số đo phí im lặng; giới hạn được ghi | FR-02, 24; NFR-08, 10 |
| AC-04 | Đổi thiết bị, DPI, tháo màn hình | Phục hồi hoặc báo lỗi rõ; không âm thầm đổi nguồn cố định | FR-01, 08, 28; NFR-12 |
| AC-05 | Mất mạng, timeout, rate limit, sai key, hết tín dụng | Retry đúng loại/giới hạn; bỏ nội dung cũ; không treo | FR-24, 28, 31 |
| AC-06 | Bật/tạm dừng nhanh khi có request đang chạy | Không tạo request nội dung mới sau dừng; không hiện kết quả phiên cũ | FR-07, 30, 31; NFR-07 |
| AC-07 | 1 giờ liên tục; thêm 3 giờ trước bản thử ngoài | Không crash; đạt trần RAM/hàng đợi đã chốt; thống kê không mất | FR-31; NFR-03, 05 |
| AC-08 | Trình duyệt mục tiêu, cửa sổ/toàn màn hình | Không giành focus; điều khiển video không bị chặn; giới hạn minh bạch | FR-05, 33; NFR-06 |
| AC-09 | Xuất chẩn đoán và kiểm tra key/log | Không key/audio/text mặc định; đủ mốc truy lỗi | FR-26; NFR-07 |
| AC-10 | Tua/chuyển video, xóa phiên, cố ý làm API chậm | Xóa được ngữ cảnh; không trộn phiên; giữ giới hạn tuổi và hàng đợi | FR-30, 31; NFR-11 |
| AC-11 | Cấu hình ngưỡng chi phí thấp để thử | Cảnh báo/ngừng gửi đúng; nói rõ ước tính và request đang chạy | FR-12, 27; NFR-08 |
| AC-12 | Sleep/wake, restart, đổi khóa ngôn ngữ | Về Tạm dừng khi cần; khóa nguồn có hiệu lực; giữ cấu hình | FR-22, 28 |
| AC-13 | Profile không có hotkey/tray/overlay đầy đủ, thử phương án dự phòng | Có điều khiển dừng/thoát, thông báo đúng giới hạn, không tự đổi session hoặc nguồn thu; dự phòng được nghiệm thu riêng | FR-05, 07, 17, 23, 33, 34; NFR-06, 07 |

Không ghi “MVP đạt” nếu còn ngưỡng bắt buộc chưa chốt. Có thể phát hành bản thử giới hạn, nhưng phải ghi rõ phạm vi chưa đạt và quyết định chấp nhận giới hạn đó.

### 7.4 Ma trận kiểm thử hai nền tảng

| Profile | Ưu tiên | Phép thử bắt buộc | Trạng thái ban đầu |
|---|---|---|---|
| W — Windows thực tế | Chính | S1/S2/S5, AC-01…AC-13; cài/gỡ, audio, hotkey, focus, full screen, lifecycle | Chưa kiểm thử |
| UW — Ubuntu Wayland thực tế | Chính | Như W; thêm compositor, tray/portal nếu dùng, capability và giới hạn | Chưa kiểm thử |
| UXW — Ubuntu Wayland chạy app qua XWayland | Dự phòng có điều kiện | Chỉ thử khi S1 cần; nếu chọn hỗ trợ thì chạy đủ AC, không suy từ X11 | Chưa xác nhận khả dụng |
| UX — Ubuntu phiên X11 | Dự phòng có điều kiện | Nếu có và người dùng chọn: chạy S1/S2/S5 và đầy đủ AC trước công bố | Chưa xác nhận khả dụng |

Không cần hỗ trợ mọi desktop/compositor hoặc mọi phiên bản Windows/Ubuntu trong MVP. Chọn đúng môi trường chủ dự án, ghi profile chi tiết; thêm môi trường là mở rộng phạm vi có kiểm thử.

- Một bộ 20 clip và tham chiếu dùng chung; sàng lọc provider có thể làm một lần trên PCM mẫu cố định. Trước nghiệm thu, chạy capture → hiển thị trên cả W và profile Ubuntu công bố bằng cùng cấu hình; báo riêng kết quả và giữ nguyên tập kiểm tra độc lập.
- Kiểm logic bằng mock/replay để tiết kiệm API; kiểm thật audio/overlay/hotkey trên desktop thật. CI headless, VM hoặc remote desktop không thay được kiểm chứng trên phiên dùng thực tế.
- Một vòng tính năng: sửa core một lần → build/test cả hai → smoke test một clip + bật/dừng trên từng OS → ghi lỗi theo profile. Nếu dual boot, có thể thử luân phiên nhưng không bỏ cột OS chưa thử.
- AC-07 chạy 1 giờ riêng từng OS/profile được chọn; 3 giờ riêng trước bản thử ngoài. Nếu đổi chế độ hiển thị hoặc capture thì chạy lại các AC bị ảnh hưởng.
- Báo cáo gồm commit/build, OS/session, capture backend, UI backend, máy, mạng, số đo và mức hỗ trợ. Cấu hình logic chung không có nghĩa thiết bị ID, tọa độ cửa sổ hoặc key được sao chép trực tiếp giữa OS.

## 8. Spike — Trả lời câu hỏi trước khi xây đầy đủ

Timebox khởi điểm: 1–2 ngày làm việc tập trung cho một câu hỏi hẹp. Đây là giới hạn để ra quyết định, không phải cam kết giải quyết xong mọi nền tảng/ngôn ngữ. Quá timebox thì ghi đã biết/chưa biết, giảm phạm vi hoặc chọn thử nghiệm tiếp theo; không kéo dài âm thầm.

| Spike | Câu hỏi và cách thử | Đầu ra/quyết định |
|---|---|---|
| **S1 — Overlay** | Windows và Ubuntu Wayland thực tế, mỗi bên một trình duyệt chính: trong suốt, click-through, focus, hotkey, toàn màn hình, DPI. Dùng văn bản giả, chưa cần AI | Bảng theo profile W/UW; thử UXW/UX hoặc UI khác chỉ khi cần theo mục 2.4. Không đưa game và mọi desktop Linux vào điều kiện đầu |
| **S2 — Thu âm** | Mỗi OS một đầu ra, 30 phút, đổi thiết bị, Bluetooth nếu có; phát hiện mất frame/đứt luồng. Mục tiêu trễ capture < 100 ms nếu có phương pháp đo đáng tin | Chọn backend; cách phục hồi; giới hạn nguồn bảo vệ. Không dùng WAV nghe được làm bằng chứng duy nhất không mất frame |
| **S3 — STT/dịch và kinh tế** | Bắt đầu một cặp provider, clip ngắn một ngôn ngữ để kiểm pipeline; sau đó sàng lọc hai STT cloud và hai cách dịch bằng cùng tập con. Local chỉ thử sớm nếu cloud không đạt ngân sách/riêng tư | So chất lượng, độ trễ, chi phí và cách chia đoạn. Ghi giá chính thức; không nhất thiết chạy mọi tổ hợp trên toàn bộ clip |
| **S4 — Khả năng đọc** | ≥ 10 đoạn có bản dịch tham chiếu; thử hai dòng, thời gian giữ, chỉ final so với có partial; sau đó thử lại với pipeline thật | Chọn cách hiển thị, có cần partial không; kiểm font/DPI và độ dễ đọc trên cả hai OS, tránh chỉ đạt khi dùng bản dịch có sẵn |
| **S5 — Tích hợp xuyên suốt** | Capture → STT → dịch → overlay trên nội dung phát thật trên cả W và Ubuntu, gồm câu dài, mạng chậm và tạm dừng | Chứng minh các phần kết hợp được; số đo baseline, hàng đợi, câu bỏ, chi phí; cơ sở chốt SRS |

S1 và S2 có thể làm độc lập; timebox được tính theo câu hỏi/profile, không coi 1–2 ngày là tổng ngân sách thời gian cho mọi nhánh dự phòng. Chạy S1-W/S1-UW và S2-W/S2-U trong cùng giai đoạn G1; không hoàn thiện UI Windows rồi mới thử Ubuntu. S3/S4 dùng clip cố định. S5 bắt buộc trước khi triển khai rộng G2: từng thành phần đạt riêng chưa chứng minh trải nghiệm tổng thể đạt.

Mỗi biên bản spike phải có: giả thuyết; cấu hình; tiêu chí ghi trước; cách đo; kết quả thô; kết luận đạt/không đạt/chưa đủ dữ liệu; quyết định; ảnh hưởng tới FR/NFR; bước tiếp theo. Không có số đo thì không đánh dấu đã xác minh.

**Khi thất bại:**

- Overlay không đạt: theo thứ tự dự phòng mục 2.4, ghi mức hỗ trợ mục 2.5; không tự bỏ Ubuntu khỏi MVP và không khẳng định đổi framework sẽ sửa mọi lỗi. Core vẫn có thể tiến triển trong khi xử lý adapter còn lỗi.
- Độ trễ/chi phí không đạt: thử chia cụm, streaming, giảm partial/ngữ cảnh hoặc local; đo lại cả chất lượng và độ phủ.
- Không đọc kịp: điều chỉnh chia cụm/thời gian giữ; thử diễn đạt gọn nhưng đo lại mất nghĩa. Không tự chuyển dịch thành tóm tắt.
- Một ngôn ngữ chưa đạt: đổi cấu hình, đánh dấu thử nghiệm hoặc thu hẹp bản đầu bằng quyết định minh bạch.

## 9. Thiết kế kỹ thuật sơ bộ

### 9.1 Nguyên tắc

1. Lõi xử lý không phụ thuộc UI; các module giao tiếp qua sự kiện/lệnh rõ ràng.
2. Khác biệt nền tảng được cô lập ở thu âm, cửa sổ, phím tắt, kho key, đóng gói và vòng đời app; không giả định chỉ khác AudioSource.
3. Callback âm thanh không chờ mạng, model hoặc UI; buffer và hàng đợi đều có giới hạn.
4. Audio không lưu bền mặc định. Buffer trong RAM chỉ đủ cho xử lý; xóa khi dừng/đổi phiên. File WAV phục vụ spike là chế độ riêng chủ động bật, có thời hạn xóa.
5. Mỗi phiên và mỗi sửa đổi phụ đề có định danh; bỏ phản hồi không còn hợp lệ trước khi sửa UI hoặc ngữ cảnh.
6. Quản lý rate/concurrency, retry và chi phí cho cả STT lẫn dịch. Chia sẻ quota theo provider/key khi cần; không ép mọi provider đi qua một khóa toàn cục gây nghẽn.
7. Log ưu tiên metadata; không ghi key, audio, nguồn chữ hoặc bản dịch mặc định. Chế độ log nội dung nếu bổ sung phải chủ động bật, có thời hạn và thao tác xóa.
8. Provider dự phòng chỉ dùng khi đã được phép; không tự đổi nơi nhận dữ liệu nhạy cảm.
9. Một core, schema cấu hình và hợp đồng sự kiện chung; adapter Windows/Linux được chọn theo nền tảng/capability. Không tạo hai nhánh sản phẩm sao chép logic STT/dịch.
10. Capability gồm capture, transparency, click-through, focus, always-on-top, hotkey, tray và key store. Khả năng chưa kiểm chứng được ghi unknown; nhận diện OS không đủ để đánh dấu supported. Có lệnh trạng thái cho UI giải thích giới hạn và chọn chế độ đã thử.
11. Key, device ID, vị trí cửa sổ và đường dẫn là dữ liệu cục bộ theo OS; chỉ tái sử dụng cấu hình logic an toàn khi cần. Không thêm đồng bộ tài khoản/config giữa hai OS vào MVP.

### 9.2 Hai cách xử lý cần so trong S3

- **Theo đoạn:** Audio → buffer/VAD có giới hạn → STT → dịch → quản lý phụ đề → UI.
- **Streaming:** Audio → luồng STT theo hợp đồng provider → sự kiện partial/final → dịch → quản lý phụ đề → UI; VAD hỗ trợ quyết định gửi/kết thúc đoạn nhưng phải kiểm tác động nối lại và phí.

Không bắt buộc cắt thành file ngắn nếu API hỗ trợ streaming. Sample rate, mono/stereo và resampling phải theo yêu cầu adapter; “16 kHz mono” là ứng viên, không phải ràng buộc chung chưa kiểm chứng.

### 9.3 Hợp đồng sự kiện và vòng đời

Hợp đồng nháp để kiểm trong S5:

```text
SubtitleEvent {
  session_id, segment_id, revision,
  kind: Partial | Final | Error,
  src_lang, src_text?, vi_text?,
  t_audio_start, t_audio_end?, t_segment_closed?,
  t_stt_final?, t_translate_done?, expires_at?,
  error_code?
}
DisplayAck { session_id, segment_id, revision, t_shown }
```

- Thứ tự nguồn lấy theo timeline audio, không lấy thứ tự HTTP trả về.
- `Final` không bị `Partial` ghi đè; revision thấp hơn bị bỏ.
- Đổi phiên, đổi key/provider hoặc nguồn ngôn ngữ phải định nghĩa rõ việc vô hiệu kết quả đang chạy; MVP ưu tiên dừng rồi đổi để giảm lỗi.
- Ngữ cảnh dịch chỉ gồm số câu/token giới hạn và còn phù hợp phiên; lỗi dịch hoặc văn bản bất thường không tự đi vào ngữ cảnh dài hạn.
- Có giới hạn độ dài đoạn, số request đang chạy, kích thước queue, tuổi câu, số retry và timeout. Giá trị được ghi trong kết quả S5 rồi chốt vào cấu hình/SRS.
- Nếu quá tải: giảm/loại partial trước; loại dữ liệu hết hạn; giữ thống kê phần bị bỏ; không cố xử lý hết quá khứ.

### 9.4 Stack ứng viên

| Thành phần | Ứng viên kế thừa | Điều kiện chốt |
|---|---|---|
| Core | Rust | Công sức phát triển/build/debug phù hợp, tích hợp được adapter cần dùng |
| UI | Tauri + một framework web chủ dự án quen | S1 và thử đóng gói; không dùng đồng thời React và Svelte |
| Capture | WASAPI trên Windows; PipeWire/PulseAudio trên Ubuntu | S2 kiểm backend/binding thực tế; không mặc định một crate hỗ trợ đủ loopback |
| VAD/resample | Silero/ONNX Runtime, rubato hoặc ứng viên phù hợp | Đo latency, build và ảnh hưởng chất lượng; rà giấy phép trước đóng gói |
| STT/dịch | Chưa chọn nhà cung cấp | S3; phải hỗ trợ ngôn ngữ, quota, cách gọi và điều kiện dữ liệu cần dùng |
| Local STT | whisper.cpp/whisper-rs hoặc sherpa-onnx là ứng viên | Chỉ chốt sau thử trên phần cứng và rà model/license |
| Async/network/log | tokio, reqwest, WebSocket khi cần, tracing | Kiểm tương thích khi scaffold; không thêm dependency chưa cần |
| Key/config | Kho key hệ điều hành + config không chứa bí mật | Không có keyring thì báo rõ hoặc dùng key chỉ trong bộ nhớ; không âm thầm lưu plaintext |

Khi scaffold, khóa dependency Rust và frontend bằng lockfile tương ứng; ghi toolchain và phiên bản model/provider. Không ghim phiên bản bằng trí nhớ trong plan.

### 9.5 Cấu trúc ban đầu

Đề xuất ít module để một người quản lý được; chưa cần tách mỗi chức năng thành một crate:

```text
PLAN.md
AGENTS.md
app/                 # UI chung, điều khiển, cấu hình, gói Windows/Ubuntu
core/                # pipeline, session, subtitle, metrics, interface chung
platform/            # adapter Windows/Linux, capability; chưa cần tách nhiều crate
samples/             # manifest clip và tài nguyên được phép dùng
scripts/             # chạy clip, tổng hợp số đo; CLI đầy đủ khi cần
docs/
  decisions.md
  spikes.md
  srs.md             # lập baseline sau G1
  test-results.md
```

Không bắt buộc tạo toàn bộ thư mục rỗng ngay. Tách crate/module khi có ranh giới rõ, nhu cầu build riêng hoặc tái sử dụng thực tế.

## 10. Lộ trình, công việc đầu tiên và cổng quyết định

### 10.1 G0 — Chuẩn bị đủ để bắt đầu

| ID | Công việc | Đầu ra/điều kiện xong |
|---|---|---|
| T-001 | Ghi cấu hình hai môi trường W/UW | Windows build, Ubuntu release/session/compositor, CPU/RAM/GPU, trình duyệt/âm thanh; dual boot hay hai máy; kiểm khả dụng UXW/UX nếu cần |
| T-002 | Xác nhận số giờ dùng, ngân sách và cloud | Trần tháng/giờ/phiên dự kiến; chấp nhận audio/text gửi đi đâu |
| T-003 | Khảo sát tối đa khoảng 5 giải pháp phù hợp trong một buổi | Bảng nền tảng, ngôn ngữ đích, nguồn thu, độ trễ/giá có nguồn; chưa thử thì ghi chưa thử. Lý do tiếp tục xây |
| T-004 | Chuẩn bị tập nhỏ khởi đầu rồi đủ bộ 20 clip | Có ít nhất 4 clip đại diện để bắt đầu; bổ sung tham chiếu và tập giữ lại trước nghiệm thu |
| T-005 | Ghi quyết định và backlog G1 | Profile chính W/UW, điều kiện dự phòng, ngưỡng spike, tổng chi phí thử cả hai OS |

**Cổng G0:** T-001, T-002 và phạm vi spike rõ. Khảo sát đối thủ không kéo dài vô hạn; nếu vẫn muốn làm để học/cá nhân dù có sản phẩm tương tự, ghi đó là mục tiêu hợp lệ.

### 10.2 G1 — Chứng minh khả thi

- [ ] T-006 Một repo, CI matrix Windows/Ubuntu: build/test core và kiểm build adapter; chuẩn bị kiểm tra desktop thật riêng.
- [ ] T-007 S1-W/S1-UW overlay; kết luận dự phòng UXW/UX hoặc adapter khác nếu cần.
- [ ] T-008 S2-W/S2-U thu âm và đổi thiết bị trên cả hai OS.
- [ ] T-009 S3 STT/dịch/chi phí.
- [ ] T-010 S4 khả năng đọc.
- [ ] T-011 S5 trên Windows/Ubuntu, bản đóng gói sớm từng OS; ghi profile và mode đang dùng.
- [ ] T-012 Chốt lựa chọn công nghệ, provider, partial và giới hạn pipeline bằng Decision Log.
- [ ] T-013 Viết SRS gọn từ FR/NFR/UC đã hiệu chỉnh; không sao chép mọi ý tưởng V2 thành Must.

**Cổng G1:** có S1/S2/S5 và số đo riêng trên cả Windows và Ubuntu; chọn profile chính/dự phòng, chốt baseline và giới hạn. Profile còn vướng có thể tiếp tục spike trong khi core và OS kia tiến triển, nhưng không ghi G1 hai nền tảng đã hoàn tất. Cửa sổ phụ đề tạm chỉ là bằng chứng pipeline, không thay nghiệm thu overlay. Nếu mục tiêu chính chưa khả thi thì điều chỉnh hoặc dừng, không tiếp tục dựng UI đầy đủ chỉ vì đã có plan.

### 10.3 G2 — MVP dùng được

Triển khai từng lát có thể chạy thử trên Windows và Ubuntu; không xây hai sản phẩm độc lập:

1. Phiên và điều khiển: bật/dừng, xóa phiên, khóa ngôn ngữ, chỉ báo.
2. Phụ đề ổn định: queue, timeout, revision, lỗi, giới hạn tuổi câu.
3. Dùng hằng ngày: cấu hình, key, đổi thiết bị, sleep/wake, toàn màn hình.
4. Chi phí, chẩn đoán và bản cài trên máy sạch.
5. Chạy AC-01…AC-13 riêng mỗi profile công bố, dùng thật hai tuần luân phiên hai OS, sửa lỗi ảnh hưởng mục tiêu chính.

**Cổng G2:** Windows và ít nhất một profile Ubuntu đã chọn đều đạt Must theo mục 2.5; có bản cài và hướng dẫn riêng. Chưa đạt một bên thì chỉ phát hành bản thử/phạm vi đã đạt, không ghi MVP hai nền tảng hoàn tất. Ngoại lệ làm giảm Must phải có quyết định rõ. Không tự nâng tính năng Later thành điều kiện xong.

### 10.4 G3/G4 — Chỉ mở rộng theo bằng chứng

- Nếu MVP Ubuntu dùng profile dự phòng, tiếp tục cải thiện Wayland theo lỗi đã đo; thêm desktop/compositor khác chỉ khi có nhu cầu. Ubuntu đã là phạm vi G1/G2, không hoãn khởi động tới V2.
- Local nếu chi phí/riêng tư là trở ngại; glossary nếu tên riêng là lỗi nổi trội; partial nếu người xem chờ quá lâu; game nếu đã có nhu cầu thật.
- Fallback chỉ thêm khi lỗi provider thực sự ảnh hưởng đủ lớn để bù chi phí bảo trì.
- Trước dịch vụ: có người ngoài thử, chi phí thật, khả năng hỗ trợ, rà điều khoản provider/model/tài nguyên, bảo mật và quy trình dữ liệu. Backend, xác thực, thanh toán và vận hành là phạm vi mới cần thiết kế riêng.

Chưa đặt ngày phát hành khi chưa biết thời gian rảnh, kinh nghiệm stack và máy thử. Sau G1 mới ước lượng theo lát công việc, số giờ thực có mỗi tuần và phần tích hợp/kiểm thử/đóng gói riêng từng OS. Không giả định khối lượng tăng đúng gấp đôi; ghi thời gian thực cho core chung và adapter riêng.

## 11. Quy trình làm việc cho một người

### 11.1 Tài liệu tối thiểu

| Tài liệu | Vai trò | Thời điểm |
|---|---|---|
| PLAN.md | Mục tiêu, phạm vi, roadmap và chỉ dẫn tới tài liệu chi tiết | Hiện tại |
| Decision Log + Spike Log | Lựa chọn và bằng chứng, lý do thay đổi | Từ G0/G1; có thể gộp khi còn ít |
| SRS gọn | Baseline FR/NFR/UC, giới hạn và AC của MVP | Sau G1 |
| Test results | Cấu hình, số đo, lỗi, ma trận hỗ trợ, nghiệm thu | Từ spike, cập nhật theo bản |

Không cần thêm BRD dài, nhiều sơ đồ UML hoặc tài liệu mô tả lại cùng nội dung nếu chúng không phục vụ quyết định. Khi tách SRS, PLAN chỉ giữ bản tóm tắt và liên kết; không duy trì hai bản yêu cầu chi tiết dễ lệch nhau.

### 11.2 Một vòng phát triển

Issue nhỏ có FR/UC/AC → tiêu chí đạt → thay đổi → kiểm tra phù hợp → dùng thử → ghi kết quả → cập nhật quyết định nếu cần.

Nhánh/PR nhỏ hữu ích để tự review, nhưng không bắt buộc nghi thức phức tạp cho mọi sửa chữ. Conventional Commits có thể dùng từ đầu. Luôn giữ một bản chạy được để so trước/sau.

**Definition of Done:** hành vi đạt AC liên quan trên cả hai OS/profile đã chọn, hoặc issue ghi rõ mới xong một bên và còn mở phần kia; không lộ key; lỗi có cách nhận biết; giới hạn được ghi; đo lại khi chạm latency/chi phí/queue; có thể tái tạo build và cách chạy.

**Kiểm thử ưu tiên:**

- Logic có rủi ro: session/revision, request trả muộn, retry, giới hạn queue, quy đổi chi phí, config migration.
- Tích hợp: audio, provider giả lập lỗi, UI focus và vòng đời.
- Bộ clip chuẩn: dùng lại để so thay đổi nhận dạng/dịch; smoke test nhỏ mỗi vòng, bộ đầy đủ ở mốc nghiệm thu.
- Soak 1 giờ riêng mỗi profile nghiệm thu MVP; 3 giờ riêng trước bản đưa ra ngoài hoặc thay đổi có rủi ro vòng đời. Không chạy 3 giờ cho mọi sửa nhỏ. CI không thay thế soak và kiểm focus/audio trên desktop thật.

### 11.3 Kiểm soát thay đổi phạm vi

Mọi tính năng mới phải trả lời: giải quyết vấn đề nào của người dùng, có bằng chứng gì, thuộc mốc nào, thay thế/bỏ việc gì nếu muốn làm sớm? Không thêm chỉ vì công nghệ có sẵn.

## 12. Decision Log và những điểm cần xác nhận

### 12.1 Trạng thái hiện tại

| ID | Quyết định | Trạng thái |
|---|---|---|
| D-01 | Repo mới, lấy cảm hứng Cicada; không lấy fork macOS làm mặc định cho sản phẩm đa nền tảng | Kế thừa v0.2; rà lại nếu đọc code cho thấy khả năng dùng lại hữu ích |
| D-02 | Rust/Tauri là ứng viên ban đầu | Có điều kiện S1, S2, S5; chưa chốt cuối |
| D-03 | Windows và Ubuntu song song từ G0/G1 tới MVP; một core, hai bộ tích hợp | Đã chốt với chủ dự án 09/11/2026; thay quyết định đề xuất cũ |
| D-04 | Một STT cloud mặc định trong MVP | Hướng cloud kế thừa; provider cụ thể cần S3 |
| D-05 | Một dịch vụ dịch; final trước, partial sau bằng chứng | Đề xuất v0.3 |
| D-06 | Game V2; exclusive fullscreen không cam kết mặc định | Kế thừa hướng ưu tiên video |
| D-07 | Giấy phép sản phẩm | Chưa chọn; chốt trước phân phối |
| D-08 | Tên dự án | Chưa chọn; không chặn spike |
| D-09 | P1 xem video dẫn dắt, game không chặn MVP | Kế thừa v0.2 |
| D-10 | Đủ nhanh, hiểu đúng ý chính, dễ đọc | Kế thừa mục tiêu; định nghĩa độ trễ/ngưỡng mới ở mục 6 cần hiệu chuẩn |
| D-11 | Cloud có thông báo rõ; local là hướng bổ sung | Kế thừa v0.2; không hứa local ngay MVP |
| D-12 | Cá nhân trước, xem xét dịch vụ sau | Kế thừa v0.2 |
| D-13 | $5–20 spike, $15–30/tháng | Ngân sách dự kiến, cần xác nhận; Q-03 |
| D-14 | 20 clip, đủ bốn ngôn ngữ, có tham chiếu và tập giữ lại | Đề xuất cấu trúc v0.3 |
| D-15 | Tạm dừng/Đang chạy/Suy giảm, không có ẩn vẫn nghe | Đề xuất v0.3 thống nhất toàn tài liệu |
| D-16 | Hosting/backend | Hoãn tới phạm vi dịch vụ; chưa có ước lượng giá |
| D-17 | Kiểm soát chi phí cơ bản và bản cài thuộc MVP | Đề xuất v0.3 |
| D-18 | SRS baseline sau pipeline xuyên suốt | Kế thừa v0.3, cập nhật baseline riêng W/Ubuntu |
| D-19 | Windows native + Ubuntu Wayland chính; UXW/UX và chế độ có giới hạn là các nhánh dự phòng có điều kiện | Yêu cầu có chính/dự phòng đã chốt 09/11/2026; khả dụng và lựa chọn cụ thể chờ S1/S2/S5 |
| D-20 | Nghiệm thu riêng từng profile; bản thử có thể ra khác ngày, hoàn tất hai nền tảng theo mục 2.5 | Đề xuất tổ chức v0.4 |

### 12.2 Câu hỏi cần trả lời theo thời điểm

| ID | Thông tin cần biết | Chặn phần nào? |
|---|---|---|
| Q-01 | Cấu hình/phiên bản Windows và Ubuntu; desktop/compositor, CPU/RAM/GPU; dual boot hay hai máy? | Cần để lập môi trường thử, không hỏi lại quyết định hỗ trợ cả hai |
| Q-02 | Trình duyệt, thiết bị phát, số màn hình; số giờ xem/ngày và thời gian làm dự án/tuần | Cần cho phép đo, ngân sách và ước lượng công việc |
| Q-03 | Xác nhận ngân sách spike/tháng và hạn mức từng thử nghiệm cloud | Trước gọi dịch vụ tính phí |
| Q-04 | Ai kiểm tra bản dịch của từng ngôn ngữ hoặc nguồn tham chiếu nào đáng tin? | Trước kết luận đúng nghĩa/nghiệm thu; không chặn thử thu âm |
| Q-05 | Có chấp nhận bản đầu công bố ít hơn bốn ngôn ngữ nếu một số chưa đạt? | Chỉ cần khi kết quả S3/S5 cho thấy phải giảm phạm vi |
| Q-06 | Khi cần chuyển sang UXW/UX hoặc cửa sổ phụ đề tạm, profile đó có sẵn và mức giới hạn có phù hợp cách dùng thực tế không? | Chỉ cần khi nhánh chính không đạt; không chặn thử Wayland. Mọi đổi session do người dùng chủ động chọn |

Không cần hỏi ngay tên app, giấy phép cuối cùng, game cụ thể hoặc hosting để được bắt đầu G0.

## 13. Sổ rủi ro và phản ứng

Chưa có cơ sở định lượng xác suất. Ưu tiên dưới đây dựa trên mức ảnh hưởng tới mục tiêu; cập nhật bằng kết quả thực tế.

| ID | Rủi ro | Dấu hiệu cần hành động | Phản ứng |
|---|---|---|---|
| R-01 | Overlay/hotkey không phù hợp profile | S1-W/UW không đạt trên môi trường dùng thật | Theo nhánh dự phòng mục 2.4; không suy UXW = X11, không tự bỏ một OS |
| R-02 | Độ trễ tích lũy | Queue tăng, tuổi câu vượt ngưỡng | Giới hạn pipeline, bỏ partial, đo lại chia đoạn/streaming |
| R-03 | Dịch trôi chảy nhưng sai | Sai phủ định/số liệu, chấm đúng nghĩa không đạt | Sửa STT/dịch, tham chiếu tốt hơn; không chỉ tối ưu câu văn |
| R-04 | Không đọc kịp | Nhiều lần tua, sửa chữ gây rối | Thử final-only, chia cụm và hold time; đo lại mất nghĩa |
| R-05 | Chi phí vượt ngân sách | Phí/request, phần gửi lặp hoặc context tăng | Trần phiên; giảm tần suất; thử provider/local; điều chỉnh thời lượng dùng |
| R-06 | Thu nhầm tiếng nhạy cảm | Voice chat/thông báo lẫn trong loopback | Chỉ báo, dừng nhanh, giải thích nguồn thu; thu riêng ứng dụng là nghiên cứu sau |
| R-07 | Không có tiếng từ nguồn bảo vệ | Audio im lặng trong phép thử | Công bố không hỗ trợ; không coi vượt bảo vệ là nhiệm vụ MVP |
| R-08 | Mất thiết bị, sleep hoặc request cũ | Crash, câu cũ xuất hiện | Session mới, phục hồi có trạng thái, kiểm thử lifecycle |
| R-09 | Nhiều tiếng cùng lúc/nhạc gây nhận sai | Câu bịa hoặc sai ngôn ngữ | Khóa ngôn ngữ, lọc có đo, giới hạn nguồn; không hứa tách giọng |
| R-10 | Phụ thuộc API | Lỗi/hạn mức/chất lượng thay đổi | Adapter và log phiên bản; thêm fallback khi có nhu cầu |
| R-11 | MVP quá lớn cho một người | Nhiều module chưa nối thành luồng | Quay về lát xuyên suốt, hoãn Later; giảm số adapter |
| R-12 | Không có nhu cầu dùng thật | Ít dùng hoặc luôn tắt phụ đề | Ghi lý do, so giải pháp thay thế, điều chỉnh hoặc dừng |
| R-13 | Game/local tranh tài nguyên | FPS/frame time xấu | Kiểm riêng V2, cấu hình nhẹ; không inject game |
| R-14 | Điều kiện phân phối không phù hợp | Chưa rõ license model/clip/provider | Rà nguồn chính thức trước đóng gói/phân phối; không suy từ tên công nghệ |
| R-15 | Phạm vi hai OS làm chậm MVP | Một bên lâu không được build/thử hoặc logic bị sao chép | Một core, smoke mỗi lát, giảm tính năng; theo dõi riêng công sức tích hợp, không nhân số provider |
| R-16 | CI xanh nhưng desktop thật lỗi | Capture/focus/overlay khác máy CI hoặc session | Kiểm trên phiên dùng thật, ghi compositor/backend và ma trận hỗ trợ |
| R-17 | Dự phòng X11/XWayland không có hoặc không giải quyết lỗi | Kiểm khả dụng thất bại, S1 dự phòng không đạt | Không hứa sẵn; thử cửa sổ tạm có nhãn giới hạn, giữ việc sửa adapter mở |

## 14. Phụ lục — Cicada, nguồn và lịch sử

### 14.1 Vai trò của Cicada

Nguồn tham khảo từ bản cũ: [wquguru/cicada](https://github.com/wquguru/cicada). V0.2 ghi đã đọc README/AGENTS và mô tả app dùng Swift/SwiftUI cùng API Apple; chưa đọc đầy đủ code. **Bản v0.3 không xác minh lại các mô tả này.**

Vì khác nền tảng mục tiêu, dự kiến tái sử dụng trực tiếp ít; chưa đủ bằng chứng để kết luận “gần như bằng 0”. Việc đọc code Cicada có thể hữu ích cho chia đoạn, quản lý phụ đề và điều phối dịch, nhưng không chặn S1/S2.

| Ý tưởng giữ | Áp dụng trong dự án |
|---|---|
| Lõi phụ đề, overlay không giành focus | Bắt buộc cho trải nghiệm xem |
| Điều phối request, log latency, bảo vệ key | Áp dụng từ pipeline đầu |
| Clip mẫu, chẩn đoán, thử lặp lại | Áp dụng tối giản |
| Partial/final, fallback, glossary | Chỉ thêm theo kết quả và ưu tiên thực tế |
| Notes/họp/đồng thanh dịch | Ngoài phạm vi |

Các danh sách I1–I20 và nhận định F1–F21 của v0.2 là lịch sử phân tích, không còn dùng làm danh sách Must. Nếu sao chép code hoặc đóng gói tài nguyên, đọc đúng LICENSE/NOTICE và điều kiện liên quan tại thời điểm sử dụng; ghi nguồn và thay đổi theo yêu cầu thực tế. Không coi nhận xét pháp lý trong bản cũ là kết luận đã được thẩm định.

### 14.2 Hồ sơ bằng chứng cần bổ sung khi triển khai

| Chủ đề | Nguồn cần ghi | Mốc |
|---|---|---|
| Provider | Tài liệu chính thức về giá, ngôn ngữ, streaming, quota, lưu giữ dữ liệu; ngày truy cập | S3 |
| Công nghệ | Tài liệu chính thức, phiên bản, thử nghiệm trên OS mục tiêu | S1/S2/S5 |
| Chất lượng | Manifest clip, tham chiếu, cách chấm, cấu hình, kết quả thô | S3/S4/S5 và G2 |
| Phân phối | License code/model/clip, thành phần đi kèm, cách cài/gỡ | Trước bản thử ngoài |
| Giải pháp thay thế | Trang sản phẩm và kết quả tự thử, phân biệt công bố với đã đo | G0 |

### 14.3 Lịch sử

| Phiên bản | Ngày | Nội dung |
|---|---|---|
| v0.1 | 06/11/2026 theo bản đầu được cung cấp | Khung mục tiêu, kiến trúc, spike và roadmap |
| v0.2 | 08/11/2026 | Thêm Product Brief, use case, ngân sách và khả năng đọc |
| v0.3 | 08/11/2026 | Thống nhất phạm vi; final-first và một cặp provider; đưa chi phí/bản cài vào MVP; thêm tình huống video và lifecycle; chuẩn hóa số đo, tập giữ lại, truy vết AC; thêm S5 và cổng triển khai; tách rõ quyết định, đề xuất và bằng chứng |
| v0.4 | 09/11/2026 | Chốt Windows + Ubuntu từ đầu; một core và adapter riêng; Wayland chính, UXW/UX và chế độ giới hạn dự phòng có điều kiện; cập nhật spike, CI, FR-17/34, AC-13, ngân sách, cổng G1/G2, rủi ro và quyết định |

**Trạng thái kết thúc biên soạn:** đã chốt phạm vi triển khai Windows và Ubuntu song song cùng yêu cầu có phương án chính/dự phòng. Chưa có spike, phép đo, provider hoặc kết luận tương thích nào được xác minh; tiếp theo là G0 cho hai môi trường thực tế.
