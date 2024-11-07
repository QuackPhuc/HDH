# Khái niệm:
- Hệ điều hành là chương trình hoạt động trung gian giữa người dùng và phần cứng máy tính
- Mục tiêu của hệ điều hành:
	- Thực thi chương trình của người dùng.
	- Giúp giải quyết các vấn đề liên quan đến máy tính của người dùng một cách dễ dàng hơn.
	- Sử dụng phần cứng hiệu quả
- Hệ điều hành thực hiện nhiều chức năng quan trọng, bao gồm quản lý tiến trình, quản lý bộ nhớ, quản lý lưu trữ, bảo vệ an ninh, cũng như hỗ trợ các hệ thống phân tán và hệ thống đặc biệt.
- Hệ điều hành là một bộ phân bổ tài nguyên (resource allocator): 
	- Quản lý tất cả các tài nguyên của hệ thống.
	- Quyết định giữa các yêu cầu xung đột về việc sử dụng tài nguyên, giúp sử dụng tài nguyên công bằng hiệu quả
- Hệ điều hành là một chương trình điều khiển: 
	- Kiểm soát việc thực thi các chương trình để ngăn ngừa lỗi và việc sữ dụng không đúng cách của máy tính
- Hệ điều hành không của có một định nghĩa thống nhất.
- "Mọi thứ mà nhà cung cấp gửi bạn khi bạn đặt một **Hệ điều hành**"
- "Chương trình duy nhất chạy liên tục trên máy tính" là cốt lõi(kernel). Những thứ khác là phần mềm khác.
# Cấu trúc hệ thống máy tính
Hệ thống máy tính có thể được chia làm 4 phần:
- Phần cứng: CPU, bộ nhớ, I/O device
- Hệ điều hành: Đây là phần mềm điều khiển và phối hợp việc sử dụng phần cứng giữa các ứng dụng và người dùng. Hệ điều hành quản lý tài nguyên, thực thi chương trình, và cung cấp giao diện cho người dùng.
- Chương trình ứng dụng:  Đây là các chương trình định nghĩa cách mà tài nguyên hệ thống được sử dụng để giải quyết các vấn đề của người dùng. Ví dụ bao gồm các trình xử lý văn bản, biên dịch, trình duyệt web, hệ thống cơ sở dữ liệu, và trò chơi điện tử.
- Người dùng: người, máy móc hoặc máy tính khác.

# Khởi động máy tính
- Chương trình khởi động (bootstrap program) được tải vào bộ nhớ khi bật hoặc khởi động lại máy tính:
	- Thường được lưu trữ trong ROM hoặc EPROM, được biết đến với tên gọi firmware
	- Khởi tạo tất cả các khía cạnh của hệ thống: Khởi tạo các thành phần của hệ thống, đảm bảo phần cứng và phần mềm cần thiết điều sẵn sàng để hoạt động.
	- Tải kernel của hệ điều hành và bắt đầu thực thi.
- ***Lưu ý:*** 
	- restart thường được hiểu là khởi động lại các chương trình. Ngụ ý sẽ đóng lại tất cả các ứng dụng và dịch vụ đang chạy trước khi khởi động lại.
	- reboot: có thể bao gồm khởi động lại từ phần cứng

# Tổ chức hệ thống máy tính
- Bao gồm một hoặc nhiều CPU, các bộ điều khiển các thiết bị kết nối thông qua một bus chung, cho phép truy cập vào shared memory.
- Các CPU và thiết bị có thể thực thi đồng thời và cạnh tranh để chiếm quyền sử dụng chu kỳ bộ nhớ. Điều này có nghĩa là nhiều tác vụ có thể diễn ra cùng lúc, giúp tối ưu hóa hiệu suất.

# Hoạt động của hệ thống máy tính
- Thực thi đồng thời: I/O device và CPU có thể thực hiện các tác vụ đồng thời. Điều này có nghĩa là trong khi CPU đang xử lý một tác vụ, các thiết bị I/O có thể thực hiện các hoạt động khác mà không làm gián đoạn quá trình của CPU.
- Bộ điều khiển thiết bị: Mỗi bộ điều khiển thiết bị chịu trách nhiệm quản lý một loại thiết bị cụ thể. Bộ điều khiển này có nhiệm vụ điều phối các hoạt động của thiết bị và giao tiếp với CPU.
- Bộ đệm cục bộ: Mỗi bộ điều khiển thiết bị có một bộ đệm cục bộ(local buffer) để lưu trữ dữ liệu tạm thời. Khi CPU cần dữ liệu từ thiết bị, nó sẽ di chuyển dữ liệu từ bộ nhớ chính đến bộ đệm cục bộ của bộ điều khiển thiết bị và ngược lại.
- Quá trình I/O: quá trình nhập xuất(I/O) diễn ra từ thiết bị đến bộ đệm cục bộ của bộ điều khiển. Điều này cho phép CPU không phải chờ đợi quá trình I/O hoàn tất mà có thể tiếp tục thực hiện các tác vụ khác.
- Ngắt(Interrupt): khi bộ điều khiển thiết bị hoàn thành hoạt động của nó, nó sẽ thông báo cho CPU thông qua một tín hiệu ngắt (interrupt). Tín hiệu này cho phép CPU tạm dừng công việc hiện tại để xử lý yêu cầu từ thiết bị, đảm bảo rằng hệ thống có thể phản hồi nhanh chóng với các sự kiện I/O

# Chức năng chung của ngắt
- Chuyển giao quyền điều khiển: Ngắt chuyển giao điều khiển đến routine phục vụ ngắt(interruppt service routine) thông qua vector ngắt(interrupt vector), chứa địa chỉ của tất cả các routine phục vụ. Mỗi loại ngắt sẽ có một routine phục vụ riêng, và địa chỉ của các routine này được lưu trữ trong vector ngắt (interrupt vector) để hệ thống có thể nhanh chóng chuyển giao điều khiển đến routine phù hợp khi ngắt xảy ra.
- Lưu trữ địa chỉ: Kiến trúc  ngắt phải lưu trử địa chỉ của lệnh bị ngắt để có thể tiếp tục thực hiện sau khi xử lý ngắt hoàn tất.
- Vô hiệu hóa ngắt: các ngắt đến sẽ bị vô hiệu hóa khi một ngắt khác đang được xử lý để ngăn chặn việc mất ngắt. Điều này đảm bảo rằng không có ngắt nào bị bỏ qua trong quá trình xử lý.
- Ngắt do phần mềm: Một ***trap*** là một ngắt do phần mềm tạo ra, có thể xảy ra do lỗi hoặc yêu cầu từ người dùng. Điều này cho phép hệ thống phản hồi với các tính huống đặc biệt mà không cần đến phần cứng. Điều này có nghĩa là các lỗi và yêu cầu từ người dùng có thể được xử lý hoàn toàn trong không gian phần mềm, giúp cho việc quản lý và bảo trì hệ thống trở nên dễ dàng hơn. Ví dụ: Lỗi chia cho 0, khi chươn trình thực hiện phép chia cho 0, hệ thồng sẽ phát hiện lỗi và tạo ra 1 trap. Hệ điều hành sẽ dừng chương trình và có thể thông báo cho người dùng về lỗi này hoặc thực hiện các biện pháp khắc phục.
- Hệ điều hành dựa trên ngắt: hệ điều hành được thiết kế để hoạt động dựa trên cơ chế ngắt, cho phép  nó phản hồi nhanh chóng với các sự kiện và quản lý tài nguyên hiệu quả.

# Xử lý ngắt
- **Bảo tồn trạng thái của CPU**: khi một ngắt xảy ra, hệ điều hành sẽ lưu trữ trạng thái của CPU bằng cách lưu các thanh ghi và bộ đếm chương trình(program counter). Điều này cho phép hệ thống quay lại trạng thái trước khi ngắt.
- **Xác định loại ngắt**: 
	- Poolling: Kiểm tra từng thiết bị để xác định xem có ngắt nào đã xảy ra hay không
	- Hệ thống ngắt vectored: sử dụng một bảng ngắt để xác định địa chỉ của các đoạn mã xử lý cho từng loại ngắt.
- **Thực hiện hành động tương ứng**: Sau khi xác định loại ngắt, hệ điều hành sẽ chuyển điều khiển đến đoạn mã xử lý tương ứng để thực hiện các hành  động cần thiết

# Cấu trúc nhập - xuất (I/O structure)
- Sau khi bắt đầu I/O, điều khiển sẽ trở lại chương trình người dùng chỉ khi I/O hoàn tất
	- Chờ đợi(wait instruction): CPU sẽ ở trạng thái chờ cho đến khi có ngắt tiếp theo
	- Vòng lặp chờ(wait loop): CPU sẽ liên tục kiểm tra trạng thái của thiết bị I/O. Điều này có thể dẫn đến tranh chấp truy cập bộ nhớ.
	- Chỉ có một yêu cầu I/O d0ang chờ xử lý tại một thời điểm, không có xử lý I/O nào đồng thời xảy ra.
- Sau khi bắt đầu I/O, điều khiển quay lại chương trình người dùng mà không cần đợi I/O hoàn tất:
	- System call: Đây là yêu cầu từ chương trình người dùng đến hệ điều hành để cho phép người dùng chờ cho đến khi I/O hoàn tất.
	- Device-status table: bảng trạng thái thiết bị chứa thông tin cho mỗi thiết bị I/O, bao go6m22 loại thiết bị, địa chỉ và trạng thái của nó.
	- Chỉ mục vào bảng thiết bị I/O: hệ điều hành sẽ tra cứu vào bảng trạng thái thiết bị để xác định trạng thái của thiết bị và để sửa đỗi mục bảng nhằm bao gồm thông tin về ngắt

# Direct Memory Access Structure
- **Truyền dữ liệu nhanh**: DMA được thiết kế cho các thiết bị I/O tốc độ cao, cho phép chùng truyền tải thông tin gần với bộ nhớ. 
- **Chuyển khối dữ liệu**: giúp giảm tải cho CPU vì CPU không cần phải xử lý từng byte dữ liệu. Thay vì tạo ra một ngắt cho mỗi byte dữ liệu được truyền, DMA chỉ tạo ra một ngắt duy nhất cho mỗi khối dữ liệu. Điều này giúp giảm số lượng ngắt mà CPU phải xử lý, từ đó cải thiện hiệu suất tổng thể của hệ thống.
- **Thiết bị điều khiển**: Mỗi thiết bị I/O có một bộ điều khiển thiết bị (device controller) chịu trách nhiệm quản lý việc truyền dữ liệu. Bộ điều khiển này sẽ thực hiện việc chuyển dữ liệu từ bộ đệm (buffer) của thiết bị trực tiếp đến bộ nhớ chính.
- **Giảm thiểu sự can thiệp của CPU**: Khi DMA hoạt động, CPU có thể tiếp tục thực hiện các tác vụ khác mà không bị gián đoạn, giúp tối ưu hóa việc sử dụng tài nguyên hệ thống.
- **Quản lý ngắt**: Sau khi hoàn tất việc truyền dữ liệu, bộ điều khiển thiết bị sẽ gửi một tín hiệu ngắt đến CPU để thông báo rằng quá trình truyền đã hoàn tất, cho phép CPU xử lý dữ liệu đã được truyền vào bộ nhớ.

# Cấu trúc lưu trữ
- **Bộ nhớ chính (Main Memory)**: Đây là loại bộ nhớ mà CPU có thể truy cập trực tiếp. Nó thường được sử dụng để lưu trữ dữ liệu và chương trình đang hoạt động. Bộ nhớ chính có tốc độ truy cập nhanh nhưng có dung lượng hạn chế và là bộ nhớ dễ bay hơi (volatile), nghĩa là dữ liệu sẽ bị mất khi nguồn điện tắt.
-  **Bộ nhớ thứ cấp (Secondary Storage)**: Đây là loại bộ nhớ không bay hơi (non-volatile) và thường được sử dụng để lưu trữ dữ liệu lâu dài. Bộ nhớ thứ cấp bao gồm các thiết bị như ổ đĩa cứng (HDD), ổ đĩa thể rắn (SSD), và các thiết bị lưu trữ khác. Bộ nhớ thứ cấp có dung lượng lớn hơn nhiều so với bộ nhớ chính nhưng tốc độ truy cập chậm hơn.
- **Đĩa từ (Magnetic Disks)**: Đây là một dạng bộ nhớ thứ cấp, bao gồm các đĩa kim loại hoặc thủy tinh được phủ vật liệu ghi từ. Bề mặt đĩa được chia thành các track và sector, cho phép tổ chức và truy cập dữ liệu một cách hiệu quả. Bộ điều khiển đĩa (disk controller) quản lý việc tương tác giữa thiết bị và máy tính.

# Caching
- **Khái niệm Caching**: Caching là một nguyên tắc quan trọng, cho phép sao chép thông tin từ một hệ thống lưu trữ chậm hơn (như ổ đĩa cứng hoặc RAM) sang một hệ thống lưu trữ nhanh hơn (như bộ nhớ cache). Điều này giúp tăng tốc độ truy cập dữ liệu.
- **Quy trình hoạt động**:
    - Khi CPU cần truy cập thông tin, nó sẽ kiểm tra bộ nhớ cache trước tiên.
    - Nếu thông tin có trong cache (gọi là cache hit), CPU sẽ sử dụng trực tiếp từ cache, giúp tiết kiệm thời gian.
    - Nếu thông tin không có trong cache (gọi là cache miss), dữ liệu sẽ được sao chép từ bộ nhớ chậm hơn vào cache và sau đó được sử dụng.
- **Kích thước Cache**: Bộ nhớ cache thường nhỏ hơn so với bộ nhớ mà nó đang cache. Điều này có nghĩa là không phải tất cả dữ liệu đều có thể được lưu trữ trong cache cùng một lúc.
- **Quản lý Cache**: Việc quản lý cache là một vấn đề thiết kế quan trọng. Điều này bao gồm việc xác định kích thước cache và chính sách thay thế cache (cache replacement policy), tức là quyết định dữ liệu nào sẽ được giữ lại trong cache và dữ liệu nào sẽ bị xóa khi cache đầy.
- **Lợi ích của Caching**: Caching giúp cải thiện hiệu suất của hệ thống bằng cách giảm thời gian truy cập dữ liệu, từ đó tăng tốc độ xử lý của các ứng dụng và hệ thống.

# Kiến trúc hệ thống máy tính
Đề cập đến cách mà các thành phần của một hệ thống máy tính được tổ chức và tương tác với nhau
- **Thành phần chính**: Hệ thống máy tính thường được chia thành bốn thành phần cơ bản:
    - **Phần cứng (Hardware)**: Cung cấp các tài nguyên tính toán cơ bản như CPU, bộ nhớ và thiết bị I/O.
    - **Hệ điều hành (Operating System)**: Kiểm soát và phối hợp việc sử dụng phần cứng giữa các ứng dụng và người dùng.
    - **Chương trình ứng dụng (Application Programs)**: Định nghĩa cách mà tài nguyên hệ thống được sử dụng để giải quyết các vấn đề tính toán của người dùng, ví dụ như trình xử lý văn bản, biên dịch, trình duyệt web, hệ thống cơ sở dữ liệu, và trò chơi điện tử.
    - **Người dùng (Users)**: Bao gồm con người, máy móc, và các máy tính khác.
- **Kiến trúc CPU**: Hệ thống máy tính thường sử dụng một hoặc nhiều bộ xử lý đa năng (general-purpose processors), từ các thiết bị cầm tay đến các máy tính lớn (mainframes). Ngoài ra, nhiều hệ thống còn có các bộ xử lý chuyên dụng (special-purpose processors) để thực hiện các tác vụ cụ thể.
- **Hệ thống đa xử lý (Multiprocessor Systems)**: Sự phát triển của các hệ thống đa xử lý đang gia tăng. Các hệ thống này, còn được gọi là hệ thống song song (parallel systems) hoặc hệ thống liên kết chặt chẽ (tightly-coupled systems), có những lợi ích như:
    - **Tăng thông lượng (Increased throughput)**: Có thể xử lý nhiều tác vụ đồng thời.
    - **Kinh tế quy mô (Economy of scale)**: Giảm chi phí trên mỗi đơn vị công việc.
    - **Độ tin cậy cao hơn (Increased reliability)**: Hệ thống có khả năng phục hồi tốt hơn khi gặp sự cố (graceful degradation) hoặc khả năng chịu lỗi (fault tolerance).
- **Các loại hệ thống đa xử lý**: Có hai loại chính:
    - **Đa xử lý không đối xứng (Asymmetric Multiprocessing)**: Một bộ xử lý chính điều khiển các bộ xử lý khác.
    - **Đa xử lý đối xứng (Symmetric Multiprocessing)**: Tất cả các bộ xử lý đều có quyền truy cập bình đẳng vào bộ nhớ và thiết bị I/O.

# Clusterd systems
Clustered systems là một loại kiến trúc máy tính trong đó nhiều hệ thống (máy tính) làm việc cùng nhau để cung cấp dịch vụ cao hơn và độ tin cậy tốt hơn.

 - **Định nghĩa**
	- Clustered systems bao gồm nhiều máy tính kết nối với nhau, thường chia sẻ lưu trữ thông qua một mạng lưu trữ (Storage Area Network - SAN). Điều này cho phép các máy tính trong cụm làm việc cùng nhau để xử lý các tác vụ.
- **Tính năng**
	- Dịch vụ có độ sẵn sàng cao: Clustered systems được thiết kế để duy trì hoạt động ngay cả khi một hoặc nhiều máy tính trong cụm gặp sự cố. Điều này có nghĩa là nếu một máy tính bị lỗi, các máy tính khác vẫn có thể tiếp tục cung cấp dịch vụ mà không bị gián đoạn.
- **Các loại clustering**
	- **Asymmetric Clustering**: Trong mô hình này, có một máy tính hoạt động chính (chạy ứng dụng) và một hoặc nhiều máy tính khác ở chế độ chờ (hot-standby). Nếu máy chính gặp sự cố, một trong các máy chờ sẽ được kích hoạt để thay thế.
    - **Symmetric Clustering**: Tất cả các máy tính trong cụm đều chạy ứng dụng và giám sát lẫn nhau. Nếu một máy gặp sự cố, các máy khác có thể tiếp tục hoạt động mà không bị ảnh hưởng.
- **Ứng dụng**

	- Một số cụm máy tính được sử dụng cho tính toán hiệu suất cao (High-Performance Computing - HPC). Để tận dụng tối đa khả năng của các hệ thống này, các ứng dụng cần được viết để sử dụng song song (parallelization), cho phép chia nhỏ công việc và xử lý đồng thời trên nhiều máy tính.

# Cấu trúc hệ điều hành
Cấu trúc của hệ điều hành là cách mà các thành phần của nó được tổ chức và tương tác với nhau

- Multiprogramming cần thiết cho việc tối ưu hiệu suất:
	- Một người dùng đơn lẻ không thể luôn luôn giữ cho CPU và các thiết bị I/O hoạt động liên tục. Điều này có thể dẫn đến việc lãng phí tài nguyên, vì CPU có thể không có công việc để thực hiện trong khi chờ đợi các thiết bị I/O hoàn thành.
	- Hệ điều hành tổ chức các công việc (bao gồm mã và dữ liệu) để CPU luôn có một công việc để thực hiện. Điều này có nghĩa là một tập hợp con của tổng số công việc trong hệ thống được giữ trong bộ nhớ.
	- Khi một công việc đang chạy phải chờ (ví dụ, chờ I/O), hệ điều hành sẽ chuyển sang một công việc khác để sử dụng CPU, giúp tối ưu hóa việc sử dụng tài nguyên.
	- Hệ điều hành sử dụng **job scheduling** (lập lịch công việc) để chọn một công việc từ bộ nhớ và thực hiện nó. Khi công việc đó không thể tiếp tục (do chờ I/O hoặc lý do khác), hệ điều hành sẽ chuyển sang công việc khác.
- Timesharing(multitasking) là một sự mở rộng hợp lý của đa lập trình, trong đó CPU chuyển đổi giữa các công việc một cách thường xuyên đến mức người dùng có thể tương tác với từng công việc trong khi nó đang chạy. Điều này tạo ra một trải nghiệm tính toán tương tác.
	- Để đảm bảo trải nghiệm người dùng tốt, thời gian phản hồi cho mỗi công việc nên nhỏ hơn 1 giây.
	- Mỗi người dùng có ít nhất một chương trình đang thực thi trong bộ nhớ, được gọi là **tiến trình**
	- Nếu có nhiều công việc sẵn sàng để chạy cùng một lúc, hệ điều hành sẽ thực hiện **lập lịch CPU** để quyết định công việc nào sẽ được thực hiện tiếp theo.
	- Nếu các tiến trình không vừa vặn trong bộ nhớ, hệ điều hành sẽ sử dụng kỹ thuật **swapping** để di chuyển chúng vào và ra khỏi bộ nhớ để có thể thực thi.
	- **Bộ nhớ ảo** cho phép thực thi các tiến trình mà không cần phải hoàn toàn nằm trong bộ nhớ.

# Hoạt động của hệ điều hành
- Hệ điều hành được **điều khiển bởi ngắt** (interrupt-driven by hardware).
- Các lỗi phần mềm hoặc yêu cầu dịch vụ tạo ra **ngoại lệ** (exception) hoặc **bẫy** (trap).
    - Ví dụ: phép chia cho 0 hoặc yêu cầu dịch vụ từ hệ điều hành.
- Một số vấn đề của tiến trình bao gồm vòng lặp vô hạn hoặc tiến trình tự ý chỉnh sửa hệ điều hành hoặc tiến trình khác.
- **Hoạt động ở hai chế độ**: Chế độ người dùng và chế độ nhân (kernel mode) giúp bảo vệ hệ điều hành và các thành phần hệ thống khác.
- Hệ điều hành phân biệt được khi nào hệ thống đang chạy mã người dùng và khi nào đang chạy mã nhân thông qua **bit chế độ** (mode bit).
- Một số lệnh chỉ có thể thực hiện trong chế độ nhân (privileged instructions).
- Khi có **lời gọi hệ thống** (system call), chế độ chuyển từ người dùng sang nhân, sau khi thực hiện xong sẽ quay lại chế độ người dùng.

# Chuyển từ User to Kernel Mode
- **Bộ hẹn giờ** (timer) được sử dụng để ngăn chặn các tiến trình vô hạn hoặc việc một tiến trình sử dụng quá nhiều tài nguyên.
    - Bộ hẹn giờ sẽ thiết lập **ngắt** sau một khoảng thời gian nhất định.
    - Hệ điều hành sẽ giảm **bộ đếm** mỗi khi một tiến trình chạy.
    - Khi bộ đếm về 0, một **ngắt** sẽ được tạo ra.
- Bộ hẹn giờ được thiết lập trước khi hệ điều hành lên lịch cho một tiến trình để giành lại quyền kiểm soát hoặc **chấm dứt chương trình** nếu chương trình đó vượt quá thời gian cho phép.

# Quản lý tiến trình
- **Tiến trình** là một chương trình đang được thực thi. Nó là đơn vị công việc trong hệ thống. Chương trình là một thực thể thụ động, còn **tiến trình** là một thực thể hoạt động.
	- **Thụ động** ở đây có nghĩa là chương trình **không làm gì cả** khi nó chỉ tồn tại ở dạng mã nguồn hoặc tập tin, không tương tác với hệ thống.
	- Khi một chương trình được **thực thi** (tức là được chạy bởi CPU), nó trở thành **tiến trình**. Tiến trình là chương trình **đang hoạt động** trên hệ thống, nó yêu cầu tài nguyên như CPU, bộ nhớ, thiết bị I/O, v.v. để thực hiện các lệnh trong chương trình.
- Tiến trình cần tài nguyên để hoàn thành nhiệm vụ của nó, bao gồm: CPU, Bộ nhớ, Thiết bị vào/ra (I/O), Tập tin, Dữ liệu khởi tạo
- Khi tiến trình kết thúc, hệ thống phải thu hồi lại các tài nguyên có thể sử dụng lại.
- **Tiến trình đơn luồng** có một bộ đếm chương trình, chỉ định vị trí của lệnh tiếp theo sẽ được thực thi. Tiến trình thực hiện các lệnh tuần tự, từng lệnh một, cho đến khi hoàn thành.
- **Tiến trình đa luồng** có một bộ đếm chương trình cho mỗi luồng.
- Hệ thống thường có nhiều tiến trình hoạt động cùng lúc, bao gồm các tiến trình người dùng và tiến trình của hệ điều hành.
- **Tính đồng thời** (Concurrency) được thực hiện bằng cách **đa hợp hóa CPU** giữa các tiến trình hoặc các luồng.

# Hoạt động quản lý tiến trình
- Tạo và xóa tiến trình
- Tạm dừng và tiếp tục tiến trình
- Cung cấp các cơ chế đồng bộ hóa tiến trình
- Cung cấp các cơ chế giao tiếp giữa các tiến trình
- Xử lý tình trạng kẹt tiến trình

# Quản lý bộ nhớ
- **Tất cả dữ liệu và lệnh phải có trong bộ nhớ trước và sau khi xử lý**:
    - Mọi dữ liệu và lệnh đều cần được tải vào bộ nhớ (RAM) để có thể xử lý và thực thi. Sau khi xử lý, dữ liệu có thể được lưu trữ trở lại bộ nhớ thứ cấp (như ổ cứng).
- **Quản lý bộ nhớ quyết định phần nào của bộ nhớ sẽ được sử dụng**:
    - Bộ nhớ là tài nguyên giới hạn, do đó hệ điều hành phải quyết định **phần nào** của bộ nhớ sẽ được phân bổ cho tiến trình nào, và khi nào cần di chuyển tiến trình vào hoặc ra khỏi bộ nhớ (paging, swapping) để tối ưu hóa việc sử dụng CPU và đáp ứng nhanh chóng yêu cầu của người dùng.
- **Các hoạt động quản lý bộ nhớ bao gồm**:
    - **Theo dõi các phần của bộ nhớ** hiện đang được sử dụng và phần nào trống.
    - **Quyết định tiến trình hoặc dữ liệu nào** sẽ được chuyển vào bộ nhớ và khi nào.
    - **Phân bổ và giải phóng không gian bộ nhớ** khi cần thiết để tối ưu hóa tài nguyên hệ thống.

# Quản lý lưu trữ
Hệ điều hành cung cấp một cái nhìn nhất quán và hợp lý về lưu trữ dữ liệu:
- **Trừu tượng hóa thuộc tính vật lý thành đơn vị lưu trữ logic**: Các phương tiện lưu trữ vật lý (như ổ đĩa cứng, băng từ) được hệ điều hành trừu tượng hóa thành các **tập tin** và **thư mục** để người dùng dễ dàng thao tác.
- **Các thuộc tính khác nhau của thiết bị lưu trữ**: Các thiết bị lưu trữ khác nhau có các đặc điểm như:
    - **Tốc độ truy cập** (access speed),
    - **Dung lượng** (capacity),
    - **Tốc độ truyền dữ liệu** (data-transfer rate),
    - **Phương thức truy cập** (tuần tự hoặc ngẫu nhiên).
- **Hệ thống quản lý tập tin** (File-System management):
    - Các tập tin thường được tổ chức thành **thư mục** để dễ dàng quản lý.
    - Hệ điều hành cung cấp các phương thức để:
        - Tạo và xóa tập tin và thư mục.
        - Điều khiển truy cập tập tin và thư mục để bảo đảm an ninh.
        - Quản lý ánh xạ các tập tin lên bộ nhớ phụ (như ổ đĩa cứng).
        - Sao lưu tập tin lên phương tiện lưu trữ ổn định để đảm bảo dữ liệu không bị mất.

# Quản lý lưu trữ đại chúng (Mass-storage Management)
Lưu trữ đại chúng thường là nơi lưu trữ dữ liệu lâu dài, chủ yếu là các ổ đĩa.
- **Quản lý lưu trữ** là một hoạt động cực kỳ quan trọng vì:
    - Tốc độ hoạt động của toàn bộ hệ thống máy tính phụ thuộc rất nhiều vào hiệu suất của hệ thống đĩa và thuật toán quản lý đĩa.
- **Các hoạt động của hệ điều hành liên quan đến quản lý lưu trữ** bao gồm:
    - **Quản lý không gian trống** (Free-space management).
    - **Phân bổ lưu trữ** (Storage allocation).
    - **Lập lịch truy cập đĩa** (Disk scheduling).
- **Lưu trữ bậc ba** (Tertiary storage): Đôi khi hệ thống lưu trữ không yêu cầu tốc độ cao (như băng từ hoặc ổ đĩa quang), nhưng vẫn cần được quản lý để đảm bảo truy xuất dữ liệu khi cần.

# Hiệu suất của các cấp độ lưu trữ khác nhau (Performance of Various Levels of Storage)
- **Hệ thống lưu trữ** được tổ chức thành **các cấp độ** với sự khác biệt về **tốc độ**, **chi phí**, và **tính chất ổn định** (volatility).
- **Di chuyển dữ liệu giữa các cấp độ lưu trữ**:
    - **Chủ động** hoặc **bị động** di chuyển dữ liệu giữa các cấp độ lưu trữ khác nhau nhằm tối ưu hóa hiệu suất của hệ thống.
    - Ví dụ: thông tin tạm thời có thể được di chuyển từ bộ nhớ phụ lên bộ nhớ chính hoặc bộ nhớ cache để truy xuất nhanh hơn.

# Di chuyển một số nguyên đến thanh ghi (from Disk to Register)
- Trong **môi trường đa nhiệm**, cần cẩn thận để đảm bảo sử dụng giá trị mới nhất của dữ liệu, bất kể nó được lưu trữ ở cấp độ nào của hệ thống lưu trữ.
- **Trong môi trường đa xử lý** (multiprocessor environment), cần đảm bảo **tính nhất quán bộ nhớ đệm** (cache coherency) trong phần cứng, để tất cả các bộ xử lý có phiên bản mới nhất của dữ liệu trong bộ nhớ đệm của chúng.
- **Trong môi trường phân tán** (distributed environment), vấn đề trở nên phức tạp hơn khi có thể có nhiều bản sao của một dữ liệu tồn tại.

# Hệ thống con nhập/xuất (I/O Subsystem)
Hệ điều hành có vai trò **che giấu sự phức tạp của các thiết bị phần cứng** nhập/xuất khỏi người dùng:
- **Hệ thống con I/O** chịu trách nhiệm:
    - **Quản lý bộ nhớ I/O**, bao gồm:
        - **Buffering** (lưu dữ liệu tạm thời khi nó đang được truyền),
        - **Caching** (lưu trữ một phần dữ liệu trong bộ nhớ nhanh hơn để tăng hiệu suất),
        - **Spooling** (xử lý đan xen đầu ra của một công việc với đầu vào của công việc khác).
    - **Giao diện driver thiết bị**: Cung cấp giao diện chung cho các thiết bị phần cứng cụ thể, với các **driver** tương ứng để quản lý từng loại thiết bị.

# Protection and Security
Hệ điều hành đảm bảo **bảo vệ** (protection) và **an ninh** (security) trong hệ thống:
- **Bảo vệ** là cơ chế kiểm soát quyền truy cập của các tiến trình và người dùng đến các tài nguyên hệ thống.
- **An ninh** là bảo vệ hệ thống khỏi các cuộc tấn công nội bộ và bên ngoài.
- Những vấn đề an ninh thường gặp bao gồm:
    - **Tấn công từ chối dịch vụ** (Denial of Service),
    - **Sâu máy tính** (worms),
    - **Virus**,
    - **Đánh cắp danh tính**,
    - **Lạm dụng dịch vụ**.
- **Hệ thống phân biệt người dùng** bằng cách sử dụng:
    - **ID người dùng** (user IDs, security IDs) để quản lý các quyền truy cập vào tập tin và tiến trình.
    - **ID nhóm** (group ID) để quản lý quyền truy cập của các nhóm người dùng.
    - **Leo thang đặc quyền** (privilege escalation) cho phép người dùng tạm thời nâng quyền hạn để thực hiện các tác vụ đặc biệt.

# Computing Environments
- Truyền thống, máy tính được sử dụng trong môi trường văn phòng với các **máy tính cá nhân (PCs)** kết nối qua mạng hoặc thông qua các **terminal** gắn với máy chủ lớn để chia sẻ tài nguyên.
- **Mạng gia đình** ngày càng trở nên phổ biến, với các máy tính kết nối mạng thông qua tường lửa để bảo vệ khỏi các mối đe dọa từ internet.
- **Tính toán khách-chủ** (Client-Server Computing): Các máy tính cá nhân thông minh (smart PCs) thay thế các **terminal** cũ. Các hệ thống này giờ đây hoạt động như **máy chủ** (server), phản hồi các yêu cầu từ máy khách.
	- **Compute-server** cung cấp các dịch vụ tính toán.
	- **File-server** cung cấp dịch vụ lưu trữ và truy xuất tập tin.

# Tính toán ngang hàng (Peer-to-Peer Computing)
- Mô hình **Peer-to-Peer (P2P)** không phân biệt giữa máy khách và máy chủ, mọi **node** đều được coi là **ngang hàng** (peer).
    - Mỗi node có thể hoạt động như một máy khách, máy chủ, hoặc cả hai.
    - Để tham gia mạng P2P, một **node** cần phải:
        - Đăng ký dịch vụ với máy chủ tìm kiếm trung tâm, hoặc
        - Phát yêu cầu dịch vụ và phản hồi các yêu cầu từ các node khác thông qua giao thức khám phá dịch vụ.
- Ví dụ về các hệ thống P2P bao gồm **Napster** và **Gnutella**.

# Tính toán dựa trên web (Web-Based Computing)
- **Web** đã trở nên phổ biến và các **máy tính cá nhân** (PCs) là thiết bị phổ biến nhất được sử dụng để truy cập web.
- Các thiết bị khác đang dần kết nối vào mạng để truy cập web.
- Một loại thiết bị mới, gọi là **cân bằng tải** (load balancer), được sử dụng để quản lý lưu lượng truy cập web giữa các máy chủ tương tự.
- Hệ điều hành như **Windows 95**, **Linux**, và **Windows XP** đã phát triển để có thể hoạt động như cả máy khách và máy chủ.

# Hệ điều hành mã nguồn mở (Open-Source Operating Systems)
- **Hệ điều hành mã nguồn mở** cho phép truy cập mã nguồn thay vì chỉ bản nhị phân.
- Phong trào này đi ngược lại các nỗ lực bảo vệ bản quyền phần mềm và **Quản lý Quyền Kỹ thuật Số (Digital Rights Management - DRM)**.
- Nó được khởi xướng bởi **Free Software Foundation (FSF)** với giấy phép **GNU Public License (GPL)**.
- Các ví dụ về hệ điều hành mã nguồn mở bao gồm **GNU/Linux**, **BSD UNIX** (bao gồm cả nhân của Mac OS X), và **Sun Solaris**.