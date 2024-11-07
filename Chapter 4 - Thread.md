# Multicore Programming
**Lập trình đa lõi (Multicore Programming)** đề cập đến việc phát triển phần mềm có khả năng tận dụng nhiều lõi xử lý trong một hệ thống đa lõi. Điều này cho phép thực hiện nhiều tác vụ đồng thời, cải thiện hiệu suất và tốc độ xử lý.
## Các thách thức trong lập trình đa lõi:
1. **Chia nhỏ hoạt động**: Cần phân chia công việc thành các phần nhỏ có thể thực hiện song song.
2. **Cân bằng tải**: Đảm bảo rằng tất cả các lõi đều được sử dụng hiệu quả, tránh tình trạng một số lõi bị quá tải trong khi các lõi khác nhàn rỗi.
3. **Phân chia dữ liệu**: Dữ liệu cần được chia sẻ giữa các lõi mà không gây ra xung đột hoặc lỗi.
4. **Phụ thuộc dữ liệu**: Các tác vụ có thể phụ thuộc vào nhau, yêu cầu quản lý thứ tự thực hiện.
5. **Kiểm tra và gỡ lỗi**: Việc phát hiện và sửa lỗi trong môi trường đa lõi phức tạp hơn do tính đồng thời của các tác vụ.
## Lợi ích:
- Tăng cường hiệu suất ứng dụng bằng cách tận dụng tối đa tài nguyên phần cứng.
- Cải thiện khả năng phản hồi và thời gian xử lý cho các ứng dụng nặng.
# User thread vs Kernel Thread
Luồng người dùng được quản lý bởi thư viện luồng cấp người dùng và không được hệ điều hành biết đến. Ngược lại, luồng kernel được hỗ trợ và quản lý trực tiếp bởi hệ điều hành.

| Đặc điểm             | Luồng người dùng           | Luồng kernel                   |
| -------------------- | -------------------------- | ------------------------------ |
| Quản lý              | Thư viện luồng             | Hệ điều hành                   |
| Hiệu suất            | Nhanh, ít tốn kém          | Chậm, tốn kém hơn              |
| Song song            | Giới hạn                   | Thực sự                        |
| Tác động khi bị chặn | Toàn bộ tiến trình bị chặn | Chỉ luồng bị chặn bị ảnh hưởng |
# Multithreading Model
Có ba mô hình chính trong lập trình đa luồng:
1. **Many-to-One**: Nhiều luồng người dùng được ánh xạ tới một luồng kernel. Mô hình này đơn giản nhưng có nhược điểm là nếu luồng kernel bị chặn, tất cả các luồng người dùng cũng sẽ bị chặn.
2. **One-to-One**: Mỗi luồng người dùng tương ứng với một luồng kernel. Mô hình này cho phép thực hiện đồng thời nhiều luồng, cải thiện hiệu suất và khả năng phản hồi. Tuy nhiên, nó có thể tiêu tốn nhiều tài nguyên hệ thống.
3. **Many-to-Many**: Nhiều luồng người dùng có thể được ánh xạ tới nhiều luồng kernel. Mô hình này linh hoạt và cho phép tối ưu hóa hiệu suất bằng cách điều chỉnh số lượng luồng kernel theo nhu cầu của ứng dụng.
## Lợi ích của mô hình đa luồng:
- Tăng cường khả năng sử dụng CPU và cải thiện hiệu suất ứng dụng.
- Cho phép phát triển các ứng dụng phản hồi nhanh và hiệu quả hơn.

# Threading Issues
**Vấn đề liên quan đến đa luồng** là những khó khăn chính mà lập trình viên gặp phải khi phát triển ứng dụng đa luồng:
1. **Đồng bộ hóa**: Nhiều luồng cùng truy cập và thay đổi dữ liệu chung có thể gây xung đột. Đồng bộ hóa đảm bảo chỉ một luồng truy cập dữ liệu tại một thời điểm, tránh dữ liệu không nhất quán.
2. **Deadlock (Tình trạng chết lặng)**: Xảy ra khi hai hoặc nhiều luồng chờ nhau giải phóng tài nguyên, khiến không luồng nào tiếp tục thực hiện được. Đây là thách thức lớn trong lập trình đa luồng.
3. **Starvation (Thiếu tài nguyên)**: Một luồng có thể bị thiếu tài nguyên nếu các luồng khác liên tục chiếm giữ tài nguyên đó, gây gián đoạn công việc.
4. **Race Conditions (Điều kiện đua)**: Khi nhiều luồng truy cập dữ liệu chung mà không có đồng bộ hóa, kết quả thực thi có thể không dự đoán được, do thứ tự thực hiện ảnh hưởng đến kết quả cuối cùng.
5. **Hiệu suất**: Dù đa luồng có thể cải thiện hiệu suất, nhưng quản lý luồng không hiệu quả có thể tạo ra chi phí bổ sung, thậm chí làm giảm hiệu suất nếu tạo quá nhiều luồng hoặc sử dụng tài nguyên không tối ưu.

# `fork()` and `exec()` 
Chương trình con `fork()` sao chép tiến trình cha, nhưng chỉ sao chép luồng đang gọi; tiến trình con là một tiến trình đơn luồng. `exec()` thay thế toàn bộ tiến trình (và tất cả các luồng của nó) bằng một chương trình mới, tạo ra một tiến trình đơn luồng mới chạy chương trình mới.

# Thread Cancellation
| Phương pháp                                       | Ưu điểm                                                                                                                                                             | Nhược điểm                                                                                                                                                                 |
| ------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Hủy không đồng bộ (**Asynchronous cancellation**) | Đảm bảo luồng bị ***chấm dứt ngay lập tức*** khi yêu cầu hủy được đưa ra.                                                                                           | - Có thể gây ra vấn đề về tính nhất quán dữ liệu nếu luồng đang xử lý dữ liệu quan trọng khi bị hủy. <br> - Không cho phép luồng dọn dẹp tài nguyên trước khi bị chấm dứt. |
| Hủy trì hoãn (**Deferred cancellation**)          | - Cho phép luồng mục tiêu dọn dẹp tài nguyên và ***hoàn thành các thao tác quan trọng trước khi bị chấm dứt***. <br> - Giảm thiểu rủi ro về tính nhất quán dữ liệu. | Luồng có thể tiếp tục thực thi trong một khoảng thời gian sau khi yêu cầu hủy được đưa ra.                                                                                 |

# Signal Handling
Bộ xử lý tín hiệu (Signal handler) được sử dụng để xử lý các tín hiệu này. Quá trình xử lý tín hiệu bao gồm ba bước:
- Tạo tín hiệu: Một sự kiện cụ thể sẽ tạo ra tín hiệu.
- Gửi tín hiệu: Tín hiệu được gửi đến một tiến trình.
- Xử lý tín hiệu: Tiến trình xử lý tín hiệu nhận được.

Có một số tùy chọn cho việc xử lý tín hiệu:
- Gửi tín hiệu đến luồng mà tín hiệu áp dụng.
- Gửi tín hiệu đến tất cả các luồng trong tiến trình.
- Gửi tín hiệu đến một số luồng nhất định trong tiến trình.
- Chỉ định một luồng cụ thể để nhận tất cả tín hiệu.

# Thread Pools
Là một kỹ thuật quản lý luồng trong đó một số lượng luồng được tạo sẵn và chờ đợi để thực thi các tác vụ. Khi một tác vụ mới đến, nó sẽ được giao cho một luồng có sẵn trong bể (Pool) để xử lý. Sau khi hoàn thành tác vụ, luồng đó sẽ được trả về bể và sẵn sàng cho tác vụ tiếp theo

## Lợi ích của Thread Pools:
1. **Tăng hiệu suất**: Việc sử dụng một luồng đã tồn tại để xử lý yêu cầu thường nhanh hơn so với việc tạo ra một luồng mới từ đầu, do chi phí khởi tạo luồng có thể cao.
2. **Quản lý tài nguyên hiệu quả**: Số lượng luồng trong ứng dụng có thể được giới hạn theo kích thước của pool, giúp kiểm soát việc sử dụng tài nguyên hệ thống và ngăn ngừa tình trạng quá tải.

# Thread Specific Data
Là một kỹ thuật cho phép mỗi luồng trong một ứng dụng đa luồng có bản sao riêng của dữ liệu. Điều này rất hữu ích trong các tình huống mà bạn không kiểm soát được quá trình tạo luồng, chẳng hạn như khi sử dụng một pool luồng.
## Lợi ích của Thread Specific Data:
1. **Tách biệt dữ liệu**: Mỗi luồng có thể lưu trữ và truy cập dữ liệu mà không bị ảnh hưởng bởi các luồng khác, giúp tránh xung đột và đảm bảo tính nhất quán của dữ liệu.
2. **Dễ dàng quản lý**: Khi mỗi luồng có dữ liệu riêng, việc quản lý và xử lý dữ liệu trở nên đơn giản hơn, đặc biệt trong các ứng dụng phức tạp.

# Scheduler Activation
**Scheduler Activations** là một cơ chế trong hệ thống quản lý luồng cho phép giao tiếp giữa kernel (hệ điều hành) và thư viện luồng (thread library) để duy trì số lượng luồng kernel phù hợp với yêu cầu của ứng dụng.
## Chức năng chính của Scheduler Activations:
1. **Giao tiếp hiệu quả**: Cung cấp một cơ chế gọi là **upcalls**, cho phép kernel thông báo cho thư viện luồng về các sự kiện cần thiết, như khi một luồng cần được đánh thức hoặc khi có tài nguyên sẵn sàng.
2. **Quản lý luồng linh hoạt**: Giúp ứng dụng duy trì số lượng luồng kernel cần thiết, cho phép điều chỉnh linh hoạt giữa các luồng người dùng và luồng kernel, từ đó tối ưu hóa hiệu suất.
## Ví dụ:
- Giả sử một ứng dụng có nhiều luồng người dùng đang chờ tài nguyên I/O.
- Khi một tài nguyên I/O khả dụng, nhân sẽ gửi một upcall đến thư viện luồng.
- Thư viện luồng sau đó có thể đánh thức một luồng người dùng đang chờ để xử lý tài nguyên I/O đó.

# Windows XP vs Linux Thread
| Đặc điểm           | Windows XP Threads                                                                                            | Linux Threads                                             |
| ------------------ | ------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------- |
| Mô hình ánh xạ     | Ánh xạ một-một (One-to-One), cấp nhân                                                                         | Ánh xạ một-một (One-to-One), cấp nhân                     |
| Cấu trúc dữ liệu   | - ETHREAD (Executive Thread Block) <br> - KTHREAD (Kernel Thread Block) <br> - TEB (Thread Environment Block) | task_struct                                               |
| Chia sẻ tài nguyên | Không chia sẻ giữa các luồng                                                                                  | Chia sẻ tài nguyên trong cùng tiến trình                  |
| Tạo luồng          | API Win32                                                                                                     | Gọi hệ thống clone()                                      |
| Hiệu suất          | Có thể có overhead cao khi tạo luồng                                                                          | Thường hiệu quả hơn nhờ chia sẻ tài nguyên                |
| Hỗ trợ API         | API Win32 (CreateThread, ExitThread)                                                                          | Pthreads (pthread_create, pthread_exit)                   |
| Quản lý ngữ cảnh   | Mỗi luồng có ngữ cảnh riêng biệt (register set, stack, private storage area)                                  | Chia sẻ ngữ cảnh giữa các luồng trong cùng một tiến trình |
