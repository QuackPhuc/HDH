# Các dịch vụ của OS
- **Giao diện người dùng (User Interface)**: Hầu hết các hệ điều hành đều có một giao diện người dùng, có thể là:
    - **Command-Line Interface (CLI)**: Giao diện dòng lệnh, nơi người dùng nhập lệnh để thực hiện các tác vụ.
    - **Graphical User Interface (GUI)**: Giao diện đồ họa, cho phép người dùng tương tác với hệ thống thông qua các biểu tượng và cửa sổ.
    - **Batch**: Chế độ xử lý theo lô, nơi các lệnh được thực hiện theo nhóm mà không cần sự can thiệp của người dùng.
- **Thực thi chương trình (Program Execution)**: Hệ điều hành phải có khả năng tải một chương trình vào bộ nhớ và thực thi nó. Điều này bao gồm việc kết thúc chương trình, có thể là bình thường hoặc bất thường (khi có lỗi xảy ra).
- **Hoạt động I/O (I/O Operations)**: Một chương trình đang chạy có thể cần thực hiện các hoạt động nhập/xuất, có thể liên quan đến tệp hoặc thiết bị I/O.
- **Quản lý hệ thống tệp (File-System Manipulation)**: Hệ điều hành cung cấp các chức năng để đọc và ghi tệp, tạo và xóa tệp, thư mục, tìm kiếm, liệt kê thông tin tệp, quản lý quyền truy cập.
- **Giao tiếp (Communications)**:
    - Các tiến trình có thể trao đổi thông tin với nhau, có thể xảy ra trên cùng một máy tính hoặc giữa các máy tính qua mạng.
    - Giao tiếp có thể được thực hiện thông qua **bộ nhớ chia sẻ**(shared memory) hoặc **truyền tin nhắn** (message passing), trong đó các gói tin được di chuyển bởi hệ điều hành.
- **Phát hiện lỗi (Error Detection)**:
    - Hệ điều hành cầ   n phải liên tục theo dõi các lỗi có thể xảy ra trong hệ thống.
    - Lỗi có thể xảy ra trong phần cứng CPU và bộ nhớ, trong các thiết bị I/O, hoặc trong chương trình người dùng.
    - Đối với mỗi loại lỗi, hệ điều hành nên thực hiện các hành động thích hợp để đảm bảo tính chính xác và nhất quán trong quá trình tính toán.
- **Công cụ gỡ lỗi (Debugging Facilities)**:
    - Các công cụ gỡ lỗi có thể nâng cao khả năng của người dùng và lập trình viên trong việc sử dụng hệ thống một cách hiệu quả.
    - Những công cụ này giúp phát hiện và sửa lỗi trong chương trình, từ đó cải thiện hiệu suất và độ tin cậy của phần mềm.
- **Phân bổ tài nguyên (Resource Allocation)**:
    - Khi có nhiều người dùng hoặc nhiều công việc chạy đồng thời, hệ điều hành cần phân bổ tài nguyên cho từng người dùng hoặc công việc.
    - Có nhiều loại tài nguyên khác nhau, chẳng hạn như chu kỳ CPU, bộ nhớ chính và lưu trữ tệp. Một số tài nguyên có thể có mã phân bổ đặc biệt, trong khi những tài nguyên khác (như thiết bị I/O) có thể sử dụng mã yêu cầu và giải phóng chung.
- **Kế toán (Accounting)**:
    - Hệ điều hành cần theo dõi việc sử dụng tài nguyên của từng người dùng, bao gồm loại tài nguyên và mức độ sử dụng.
    - Điều này giúp quản lý tài nguyên hiệu quả và đảm bảo rằng người dùng không lạm dụng tài nguyên của hệ thống.
- **Bảo vệ và an ninh (Protection and Security)**:
    - Các chủ sở hữu thông tin lưu trữ trong hệ thống máy tính đa người dùng hoặc mạng có thể muốn kiểm soát việc sử dụng thông tin đó.
    - Các tiến trình đồng thời không nên can thiệp vào nhau, và bảo vệ liên quan đến việc đảm bảo rằng tất cả quyền truy cập vào tài nguyên hệ thống đều được kiểm soát.
    - An ninh của hệ thống từ những người bên ngoài yêu cầu xác thực người dùng và mở rộng đến việc bảo vệ các thiết bị I/O bên ngoài khỏi các nỗ lực truy cập không hợp lệ.
- **Chuỗi bảo vệ (Chain of Protection)**:
    - Để hệ thống được bảo vệ và an toàn, các biện pháp phòng ngừa phải được thiết lập xuyên suốt hệ thống. Một chuỗi chỉ mạnh như liên kết yếu nhất của nó.

# Giao diện dòng lệnh(CLI)
- **CLI (Giao diện dòng lệnh)** cho phép người dùng nhập trực tiếp các lệnh. CLI có thể được thực hiện trong kernel hoặc thông qua các chương trình hệ thống.
- CLI có nhiều phiên bản khác nhau, thường được gọi là **shells**. Một số lệnh có thể được tích hợp sẵn, trong khi các lệnh khác chỉ là tên của các chương trình.
- Các hệ điều hành như **Windows** có giao diện **CLI** "command shell", trong khi **Mac OS X** sử dụng giao diện **Aqua** (GUI) với **kernel UNIX** bên dưới và cung cấp cả shell.

# Giao diện đồ họa(GUI)
Một số đặc điểm chính của GUI bao gồm:
- GUI là giao diện thân thiện, sử dụng các biểu tượng (icons), nút chuột và bàn phím để thực hiện các thao tác.
- **Các biểu tượng**(icon) đại diện cho tệp tin, chương trình, và các hành động khác.
- Người dùng có thể thao tác với giao diện bằng cách nhấn các nút chuột trên các biểu tượng khác nhau để mở tệp, thư mục (folder) hoặc thực hiện các chức năng.
- GUI nổi tiếng được phát minh tại **Xerox PARC** và hiện nay phổ biến trong nhiều hệ điều hành, chẳng hạn như **Microsoft Windows** và **Apple Mac OS X**.
- Các hệ điều hành hiện đại thường kết hợp cả **CLI** và **GUI**, ví dụ: Windows có GUI nhưng vẫn có **command shell**, macOS có **Aqua GUI** với kernel UNIX bên dưới.

# System Calls
**Lời gọi hệ thống (system calls)** - giao diện lập trình để truy cập các dịch vụ của hệ điều hành:
- **Lời gọi hệ thống** là các giao diện mà qua đó các chương trình có thể yêu cầu các dịch vụ từ hệ điều hành, chẳng hạn như quản lý tệp, xử lý I/O, và quản lý bộ nhớ.
- Thường được viết bằng ngôn ngữ cấp cao như **C** hoặc **C++**.
- Các lập trình viên thường không tương tác trực tiếp với lời gọi hệ thống mà sử dụng các **API** (Application Program Interface) cấp cao hơn như **Win32 API** cho Windows, **POSIX API** cho các hệ thống UNIX và Linux.
- API giúp đơn giản hóa việc sử dụng các dịch vụ của hệ điều hành bằng cách cung cấp các thư viện chuẩn, dễ sử dụng thay vì phải gọi trực tiếp vào hệ điều hành.

# Triển khai lời gọi hệ thống (System Call Implementation)
- Mỗi lời gọi hệ thống được liên kết với một **số định danh** riêng (system call number).
- Khi một ứng dụng gọi một **API** (như `ReadFile()`), nó sẽ thông qua **system call interface** của hệ điều hành.
- **System call interface** sẽ tìm kiếm đúng số định danh và gọi đúng lời gọi hệ thống tương ứng trong kernel của hệ điều hành.
- **Kernel** sẽ thực hiện hành động cần thiết (ví dụ, đọc từ tệp) và trả về kết quả cho chương trình gọi.

# Truyền tham số vào lời gọi hệ thống (System Call Parameter Passing)
- Khi một chương trình yêu cầu một lời gọi hệ thống, nó có thể cần truyền tham số cho hệ điều hành (ví dụ: tên tệp, số byte cần đọc).
- Có **ba phương pháp chính** để truyền tham số:
    - **Truyền qua các thanh ghi** (register): Đơn giản nhất, truyền trực tiếp qua các thanh ghi của CPU. Tuy nhiên, phương pháp này bị giới hạn bởi số lượng thanh ghi có sẵn.
    - **Truyền qua một khối bộ nhớ (memory block)**: Tham số được lưu trong một khối nhớ và địa chỉ của khối này được truyền vào một thanh ghi. Phương pháp này được sử dụng bởi **Linux** và **Solaris**.
    - **Đặt tham số vào stack**: Các tham số được đặt trên stack và sau đó được hệ điều hành truy xuất từ stack.

# Các loại System call
**Các loại lời gọi hệ thống** phổ biến, được chia thành các nhóm chính sau:
1. **Quản lý tiến trình (Process control)**:
    - Bao gồm các lời gọi liên quan đến việc khởi tạo, kết thúc, tạo tiến trình con, chờ tiến trình, hoặc huỷ tiến trình.
    - Ví dụ: `fork()`, `exit()`, `wait()`.
2. **Quản lý tệp (File management)**:
    - Liên quan đến việc mở, đóng, đọc, ghi và thay đổi thuộc tính của tệp.
    - Ví dụ: `open()`, `read()`, `write()`, `close()`.
3. **Quản lý thiết bị (Device management)**:
    - Bao gồm các lời gọi để yêu cầu truy cập, đọc/ghi từ các thiết bị I/O như ổ đĩa hoặc thiết bị ngoại vi.
    - Ví dụ: `ioctl()`, `read()`, `write()`.
4. **Bảo trì thông tin (Information maintenance)**:
    - Liên quan đến việc thu thập hoặc thiết lập thông tin về hệ thống hoặc các tiến trình.
    - Ví dụ: `getpid()` (lấy ID tiến trình), `alarm()` (thiết lập báo thức).
5. **Truyền thông (Communications)**:
    - Bao gồm các lời gọi để gửi và nhận thông điệp giữa các tiến trình hoặc hệ thống khác nhau.
    - Ví dụ: `pipe()`, `shmget()` (truy cập bộ nhớ chia sẻ).
6. **Bảo mật (Protection)**:
    - Liên quan đến việc kiểm soát quyền truy cập vào tài nguyên và thông tin hệ thống.

# Các chương trình hệ thống (System Programs)
**System Programs** (chương trình hệ thống): là các chương trình cung cấp một môi trường thuận tiện cho việc phát triển và thực thi chương trình.
- **Chức năng của chương trình hệ thống**:
    - **Quản lý tệp tin**: Các chương trình cho phép tạo, xóa, sao chép, đổi tên, và thao tác với tệp và thư mục.
    - **Thông tin trạng thái**: Các chương trình hiển thị thông tin trạng thái của hệ thống như thời gian, ngày tháng, lượng bộ nhớ khả dụng, dung lượng đĩa cứng còn trống và số người dùng hiện tại.
    - **Chỉnh sửa tệp tin**: Các chương trình như trình soạn thảo văn bản giúp tạo và sửa đổi các tệp tin.
    - **Hỗ trợ ngôn ngữ lập trình**: Các công cụ như trình biên dịch, trình thông dịch, và trình gỡ lỗi giúp phát triển chương trình.
    - **Tải và thực thi chương trình**: Các công cụ này bao gồm các **loader** và các trình **debugger** cho chương trình ngôn ngữ bậc cao và máy.
    - **Chương trình giao tiếp**: Bao gồm các công cụ hỗ trợ kết nối giữa các tiến trình, người dùng, và hệ thống máy tính, cho phép gửi tin nhắn, duyệt web, và truy cập từ xa.
- Phần lớn người dùng tương tác với hệ điều hành qua **system programs** thay vì trực tiếp qua các lời gọi hệ thống.

# Thiết kế và triển khai hệ điều hành (Operating System Design and Implementation)
- **Thiết kế và triển khai hệ điều hành** là một bài toán không có lời giải cụ thể, nhưng có nhiều phương pháp đã được chứng minh là hiệu quả. Nội dung thiết kế hệ điều hành thay đổi tùy thuộc vào phần cứng và loại hệ thống.
- **Mục tiêu của người dùng và hệ thống**:
    - **Mục tiêu người dùng**: Hệ điều hành nên ***dễ sử dụng, dễ học, đáng tin cậy, an toàn***, và ***nhanh***.
    - **Mục tiêu hệ thống**: Hệ điều hành nên ***dễ thiết kế***, ***triển khai***, và ***bảo trì***, cũng như ***linh hoạt***, ***đáng tin cậy***, ***không có lỗi***, và ***hiệu quả***.
- Nguyên tắc: 
	- Chính sách(Policy): Quyết định cái gì sẽ được thực hiện
	- Cơ chế(Mechanism): Quyết định làm thế nào để thực hiện

# Cấu trúc đơn giản
Một ví dụ điển hình là hệ điều hành **MS-DOS**.
- **MS-DOS** được thiết kế để cung cấp nhiều chức năng nhất trong không gian bộ nhớ nhỏ nhất. Vì lý do này, MS-DOS không được chia thành các mô-đun riêng biệt, dẫn đến việc thiếu sự phân tách rõ ràng giữa các lớp và chức năng.
- **Hạn chế của cấu trúc đơn giản**:
    - Do không được tổ chức theo mô-đun, các **giao diện** và **cấp độ chức năng** trong MS-DOS không được phân tách tốt.
    - Điều này làm cho hệ điều hành khó duy trì và phát triển, vì sự thay đổi ở một phần của hệ điều hành có thể ảnh hưởng đến toàn bộ hệ thống.

# Cấu trúc phân lớp(Layered Approach)
- **Cấu trúc phân lớp** là cách tiếp cận mà trong đó hệ điều hành được chia thành nhiều lớp (layers), mỗi lớp được xây dựng dựa trên các dịch vụ của lớp dưới nó.
- **Lớp thấp nhất** (Layer 0) là **phần cứng**, và lớp cao nhất (Layer N) là **giao diện người dùng**.
- **Lợi ích của cấu trúc phân lớp**:
    - Cung cấp sự **modularity** (tính mô-đun), giúp dễ dàng quản lý, duy trì và phát triển hệ điều hành.
    - Mỗi lớp chỉ sử dụng các dịch vụ của lớp bên dưới nó, điều này giúp đơn giản hóa việc phát triển các lớp cao hơn mà không cần biết chi tiết của lớp thấp hơn.

# UNIX
- Hệ điều hành **UNIX** được phát triển với một cấu trúc đơn giản nhưng mạnh mẽ.
- **UNIX** có hai phần chính:
    1. **System Programs** (Các chương trình hệ thống): Bao gồm các chương trình người dùng sử dụng để tương tác với hệ điều hành.
    2. **Kernel** (Nhân hệ điều hành): Là phần nằm giữa **giao diện gọi hệ thống** (system-call interface) và **phần cứng**. Kernel chịu trách nhiệm quản lý tệp tin, lập lịch CPU, quản lý bộ nhớ và các chức năng hệ thống khác.
- Kernel của UNIX cung cấp nhiều chức năng, nhưng không được chia thành các mô-đun nhỏ hơn. Do đó, mặc dù cấu trúc của UNIX khá đơn giản, việc mở rộng và bảo trì hệ thống có thể phức tạp

# Cấu trúc microkernel (Microkernel System Structure)
**Cấu trúc microkernel**, một cách tiếp cận hiện đại để thiết kế hệ điều hành:
- **Microkernel** di chuyển nhiều chức năng từ **kernel** vào **user space** (không gian người dùng). Chức năng chính của kernel chỉ là cung cấp các dịch vụ cơ bản như giao tiếp giữa các tiến trình, quản lý bộ nhớ, và quản lý thiết bị.
- **Giao tiếp giữa các mô-đun** của hệ thống trong microkernel thường được thực hiện thông qua phương thức **truyền thông tin dạng thông điệp** (message passing), giúp các mô-đun hoạt động một cách độc lập.
- **Lợi ích của microkernel**:
    - **Dễ mở rộng**: Thêm các dịch vụ mới vào hệ điều hành mà không cần thay đổi cấu trúc kernel.
    - **Dễ port** (di chuyển hệ điều hành sang kiến trúc phần cứng mới): Kernel nhỏ gọn và đơn giản hơn, giúp dễ di chuyển sang các phần cứng khác nhau.
    - **An toàn hơn**: Vì phần lớn các dịch vụ chạy trong không gian người dùng, ít mã chạy ở chế độ kernel, làm giảm nguy cơ lỗi hệ thống.
- **Nhược điểm**:
    - Do phải thực hiện nhiều thao tác giao tiếp giữa không gian kernel và user space, điều này có thể làm giảm hiệu suất của hệ thống.

# Modules
- Hệ điều hành hiện đại thường được thiết kế theo cấu trúc mô-đun. Mỗi thành phần của hệ điều hành được thiết kế như một mô-đun độc lập và có thể nạp hoặc hủy nạp khi cần thiết.
- **Tính mô-đun** trong thiết kế hệ điều hành dựa trên phương pháp **hướng đối tượng** (Object-Oriented):
    - Mỗi thành phần của hệ điều hành là một mô-đun riêng biệt, giao tiếp với các mô-đun khác thông qua các giao diện đã được định nghĩa trước.
    - Các mô-đun này có thể được nạp vào hoặc loại bỏ khỏi kernel khi cần thiết mà không làm ảnh hưởng đến toàn bộ hệ thống.
- **Lợi ích**:
    - **Tính linh hoạt**: Có thể dễ dàng thêm hoặc bớt các tính năng mà không cần thay đổi toàn bộ hệ điều hành.
    - **Tăng hiệu năng**: Chỉ những thành phần cần thiết mới được nạp vào, giúp giảm tải cho hệ thống.

# Máy ảo
- **Máy ảo** là một kỹ thuật mà ở đó, phần cứng thực được ảo hóa để tạo ra các môi trường máy tính riêng biệt (máy ảo) chạy trên cùng một máy vật lý.
- **Máy ảo cung cấp**:
    - Một giao diện **giống hệt** với phần cứng thực sự bên dưới, nhưng các tài nguyên của phần cứng được chia sẻ giữa các máy ảo.
    - Hệ điều hành chủ (host OS) tạo ra ảo giác rằng mỗi máy ảo có phần cứng riêng và có thể cài đặt hệ điều hành khác lên đó.
- **Ưu điểm của máy ảo**:
    - **Cô lập**: Các máy ảo được cô lập hoàn toàn với nhau. Nếu một máy ảo bị lỗi, nó sẽ không ảnh hưởng đến các máy ảo khác.
    - **Chia sẻ tài nguyên**: Giúp tận dụng hiệu quả hơn tài nguyên của máy vật lý, nhiều hệ điều hành có thể chạy song song.
    - **Phát triển và kiểm thử**: Máy ảo rất hữu ích cho việc phát triển và thử nghiệm các hệ điều hành và phần mềm mà không làm ảnh hưởng đến hệ điều hành thật.
    - **Hợp nhất hệ thống**: Nhiều hệ thống nhẹ nhàng có thể được hợp nhất vào một máy vật lý mạnh mẽ hơn, giúp giảm chi phí phần cứng và tối ưu hóa tài nguyên.

# Debugging
- **Định nghĩa Gỡ lỗi**: Gỡ lỗi là quá trình xác định và sửa chữa các lỗi hoặc bug trong phần mềm.
- **Tập tin Log**: Các hệ điều hành tạo ra các tập tin log ghi lại thông tin lỗi, giúp trong việc khắc phục sự cố.
- **Core Dump**: Khi một ứng dụng gặp sự cố, một core dump sẽ được tạo ra, ghi lại trạng thái bộ nhớ của ứng dụng tại thời điểm gặp lỗi.
- **Crash Dump**: Tương tự như core dump, crash dump được tạo ra khi hệ điều hành gặp sự cố, chứa thông tin quan trọng về bộ nhớ kernel.
- **Tối ưu hiệu suất**: Ngoài việc sửa chữa các sự cố, việc tối ưu hiệu suất cũng được nhấn mạnh như một phương pháp để cải thiện hiệu suất hệ thống.
- **Luật Kernighan**: Luật này nhấn mạnh thách thức của việc gỡ lỗi, nói rằng việc gỡ lỗi thường khó hơn việc viết mã ban đầu. Mã viết thông minh có thể dẫn đến những phức tạp làm cho việc gỡ lỗi trở nên khó khăn hơn.
- **Công cụ DTrace**: Được đề cập như một công cụ mạnh mẽ có sẵn trong Solaris, FreeBSD và Mac OS X, DTrace cho phép thực hiện giám sát trực tiếp trên các hệ thống sản xuất. Nó có thể theo dõi hành vi của hệ thống trong thời gian thực.
- **Probe**: DTrace sử dụng các probe sẽ kích hoạt khi mã cụ thể được thực thi, ghi lại trạng thái của hệ thống và gửi dữ liệu cho các đối tượng khác để phân tích.

# Thế hệ Hệ điều hành (Operating System Generation)
- **Thiết kế hệ điều hành**: Hệ điều hành được thiết kế để hoạt động trên bất kỳ máy nào trong một nhóm máy tính nhất định. Tuy nhiên, hệ thống phải được cấu hình cho từng máy tính cụ thể.
- **Chương trình SYSGEN**: Chương trình SYSGEN thu thập thông tin liên quan đến cấu hình cụ thể của hệ thống phần cứng. Nó giúp xác định các thành phần phần cứng và cách thức chúng hoạt động.
- **Khởi động (Booting)**: Đây là quá trình khởi động máy tính bằng cách tải nhân (kernel) của hệ điều hành vào bộ nhớ.
- **Chương trình Bootstrap**: Đây là mã lệnh được lưu trữ trong ROM, có khả năng xác định vị trí của nhân, tải nó vào bộ nhớ và bắt đầu thực thi.

# Khởi động Hệ thống (System Boot)
- **Cung cấp hệ điều hành cho phần cứng**: Một hệ điều hành phải được cung cấp cho phần cứng để phần cứng có thể khởi động nó.
- **Trình tải khởi động (bootstrap loader)**: Đây là một đoạn mã nhỏ có nhiệm vụ xác định vị trí của nhân (kernel), tải nó vào bộ nhớ và bắt đầu thực thi.
- **Quá trình hai bước**: Đôi khi, quá trình khởi động có thể là một quá trình hai bước, trong đó khối khởi động (boot block) ở một vị trí cố định sẽ tải trình tải khởi động.
- **Khởi động khi nguồn được cấp**: Khi nguồn điện được khởi động trên hệ thống, quá trình thực thi sẽ bắt đầu từ một vị trí bộ nhớ cố định.
- **Firmware**: Firmware được sử dụng để lưu trữ mã khởi động ban đầu.