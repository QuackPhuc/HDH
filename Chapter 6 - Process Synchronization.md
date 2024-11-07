# Keyword
**1. Các vấn đề cơ bản trong đồng bộ hóa:**
- **Miền găng (Critical Section):**
    - Khái niệm: Đoạn mã nguồn trong một tiến trình truy cập và thao tác trên tài nguyên dùng chung (shared resource).
    - Vấn đề: Khi nhiều tiến trình cùng muốn truy cập miền găng cùng một lúc, có thể xảy ra xung đột dữ liệu, dẫn đến kết quả không chính xác.
- **Tranh đoạt điều khiển (Race Condition):**
    - Khái niệm: Tình huống xảy ra khi kết quả của chương trình phụ thuộc vào thứ tự thực thi không xác định của các tiến trình trong miền găng.
    - Hậu quả: Dẫn đến kết quả không thể đoán trước và tiềm ẩn nhiều lỗi khó phát hiện.
- **Deadlock:** Tình trạng hai hay nhiều tiến trình bị khóa mãi mãi, chờ đợi lẫn nhau để giải phóng tài nguyên.
- **Starvation:** Tình trạng một tiến trình không thể tiếp tục thực thi do liên tục bị từ chối truy cập vào tài nguyên cần thiết.
**2. Nguyên tắc đồng bộ hóa (Synchronization Primitives):**
- **Mutual Exclusion:** Cơ chế đảm bảo chỉ một tiến trình được phép thực thi trong miền găng tại một thời điểm.
    - Mục tiêu: Ngăn chặn tranh đoạt điều khiển và đảm bảo tính nhất quán của dữ liệu.
    - Yêu cầu:
        - Chỉ một tiến trình được thực thi trong miền găng tại một thời điểm.
        - Không có giả thiết về tốc độ CPU, số lượng CPU.
        - Không có tiến trình ở ngoài miền găng có thể khóa không cho tiến trình khác vào miền găng.
        - Không có tiến trình nào chờ đợi mãi mãi để vào miền găng.
**3. Các giải pháp đồng bộ hóa:**
- **Giải pháp Busy Waiting:**
    - Cơ chế: Tiến trình liên tục kiểm tra một điều kiện nhất định trước khi vào miền găng.
    - Nhược điểm: Tiêu tốn tài nguyên CPU do vòng lặp kiểm tra liên tục.
    - Phân loại:
        - **Giải pháp phần mềm:**
            - Sử dụng cờ hiệu (Flags): Dùng một biến để biểu thị trạng thái của miền găng, nhưng có thể dẫn đến cả hai tiến trình cùng vào miền găng.
            - Kiểm tra luân phiên (Turn): Cho phép các tiến trình thay phiên nhau vào miền găng, nhưng có thể vi phạm điều kiện tiến trình bên ngoài miền găng ngăn không cho tiến trình khác vào.
            - Giải pháp Peterson: Sử dụng hai biến để đảm bảo loại trừ lẫn nhau và tránh bế tắc.
        - **Giải pháp phần cứng:**
            - Vô hiệu hóa ngắt (Disable Interrupts): Ngăn chặn ngắt khi tiến trình ở trong miền găng, đơn giản nhưng không hiệu quả trên hệ thống đa xử lý.
            - Chỉ thị TSL (Test-and-Set): Hướng dẫn nguyên tử kiểm tra và đặt giá trị của một vị trí bộ nhớ, dùng để triển khai khóa spinlock.
- **Giải pháp Sleep and Wakeup:**
    - Cơ chế: Tiến trình "ngủ" khi không thể vào miền găng và được đánh thức bởi một tiến trình khác khi miền găng khả dụng.
    - Ưu điểm: Tiết kiệm tài nguyên CPU hơn so với Busy Waiting.
    - Phân loại:
        - **Semaphores:** Biến nguyên dùng để kiểm soát truy cập vào tài nguyên dùng chung.
            - Thao tác: wait() (giảm giá trị semaphore) và signal() (tăng giá trị semaphore).
            - Phân loại:
                - Semaphore nhị phân: Giá trị 0 hoặc 1, dùng cho loại trừ lẫn nhau.
                - Semaphore đếm: Giá trị nguyên bất kỳ, dùng để kiểm soát truy cập vào tài nguyên có giới hạn.
        - **Monitors:** Cấu trúc dữ liệu cung cấp cơ chế an toàn và có cấu trúc hơn để đồng bộ hóa tiến trình.
**4. Ứng dụng của đồng bộ hóa:**
- **Bài toán Producer-Consumer:** Mô hình hóa tình huống một tiến trình tạo ra dữ liệu (Producer) và một tiến trình khác tiêu thụ dữ liệu (Consumer). Semaphore được sử dụng để đồng bộ hóa việc sản xuất và tiêu thụ dữ liệu.
- **Bài toán Buổi ăn tối của các triết gia:** Minh họa vấn đề deadlock và starvation khi nhiều tiến trình cạnh tranh tài nguyên hạn chế. Các giải pháp sử dụng semaphore được đề xuất để giải quyết vấn đề này.

# Ví dụ Busy Waiting
**Busy Waiting** là một kỹ thuật đồng bộ hóa trong đó tiến trình liên tục kiểm tra một điều kiện nhất định trước khi vào miền găng.
## 1. Giải Pháp Phần Mềm
### a) Sử Dụng Cờ Hiệu (Flags)
```cpp
while (TRUE) {
  while (lock == 1); // Chờ đến khi lock = 0
  lock = 1;          // Đặt lock = 1 để báo hiệu đang vào miền găng
  critical_section(); // Thực thi đoạn mã trong miền găng
  lock = 0;          // Đặt lại lock = 0 sau khi thoát miền găng
  noncritical_section(); // Thực thi đoạn mã ngoài miền găng
}
```

Trong ví dụ này, biến `lock` được sử dụng như một cờ hiệu để báo hiệu trạng thái của miền găng. Tuy nhiên, giải pháp này **có thể dẫn đến cả hai tiến trình cùng vào miền găng**, vì có khả năng cả hai tiến trình đều kiểm tra thấy `lock == 0` trước khi một trong hai tiến trình kịp đặt `lock = 1`.

### b) Kiểm Tra Luân Phiên (Turn)
```cpp
// Tiến trình A
while (TRUE) {
  while (turn != 0); // Chờ đến lượt
  critical_section(); // Thực thi đoạn mã trong miền găng
  turn = 1;          // Nhường lượt cho tiến trình B
  noncritical_section(); // Thực thi đoạn mã ngoài miền găng
}

// Tiến trình B
while (TRUE) {
  while (turn != 1); // Chờ đến lượt
  critical_section(); // Thực thi đoạn mã trong miền găng
  turn = 0;          // Nhường lượt cho tiến trình A
  noncritical_section(); // Thực thi đoạn mã ngoài miền găng
}
```

Giải pháp này sử dụng biến `turn` để cho phép các tiến trình thay phiên nhau vào miền găng. Tuy nhiên, nó **có thể vi phạm điều kiện tiến trình bên ngoài miền găng ngăn không cho tiến trình khác vào miền găng**, ví dụ nếu tiến trình A kết thúc `noncritical_section()` rất nhanh và quay lại kiểm tra `turn` trước khi tiến trình B kịp thực thi.
### **c) Giải Pháp Peterson**
```cpp
int turn;             // Lưu lượt hiện tại
int interested;   // Khởi động là FALSE

void enter_region(int process) { // process sẽ là 0 hoặc 1
  int other = 1 - process;       // Tiến trình còn lại
  interested[process] = TRUE;   // Muốn vào miền găng
  turn = other;                  // Nhường lượt cho tiến trình kia
  while (turn == other && interested[other] == TRUE); // Chờ đến lượt
}

void leave_region(int process) {
  interested[process] = FALSE; // Thoát khỏi miền găng
}
```

Giải pháp Peterson sử dụng hai biến `turn` và `interested` để đảm bảo loại trừ lẫn nhau và tránh bế tắc. Tiến trình muốn vào miền găng sẽ đặt `interested` của mình là `TRUE` và nhường lượt cho tiến trình kia. Tiến trình chỉ được vào miền găng khi đến lượt của nó và tiến trình kia không muốn vào.
## 2. Giải Pháp Phần Cứng
### a) Vô Hiệu Hóa Ngắt
Giải pháp này đơn giản là vô hiệu hóa tất cả các ngắt khi một tiến trình vào miền găng. Điều này đảm bảo rằng tiến trình sẽ không bị gián đoạn trong khi đang thao tác trên dữ liệu dùng chung. Tuy nhiên, giải pháp này **không khả thi trên hệ thống đa xử lý**, vì nó sẽ ngăn chặn tất cả các tiến trình khác chạy trên các bộ xử lý khác.
### b) Chỉ Thị TSL (Test-and-Set)

```cpp
enter_region:
  TSL RX, LOCK     // Chép giá trị lock vào RX và gán lock = 1
  CMP RX, #0       // So sánh với 0
  JNE enter_region // Nhảy nếu khác 0
  RET              // Vào miền găng

leave_region:
  MOVE LOCK, #0     // Gán lock = 0
  RET              // Trả về
```

Chỉ thị TSL là một hướng dẫn nguyên tử kiểm tra và đặt giá trị của một vị trí bộ nhớ. Nó được sử dụng để triển khai khóa spinlock, đảm bảo rằng chỉ một tiến trình có thể "giành" được khóa tại một thời điểm. Tiến trình muốn vào miền găng sẽ liên tục thử đặt khóa bằng TSL cho đến khi thành công.

# Ví dụ Sleep and Wakeup
```cpp
while (TRUE) {
  if (busy){
    blocked = blocked + 1;
    sleep();
  }
  else busy = 1;
  critical_section ();
  busy = 0;
  if(blocked){
    wakeup(process);
    blocked = blocked - 1;
  }
  noncritical_section ();
}
```
Đoạn mã này thể hiện ý tưởng **tiến trình sẽ "ngủ" (sleep) khi tài nguyên đang bận (busy) và được "đánh thức" (wakeup) bởi tiến trình khác sau khi tài nguyên được giải phóng.**

Để minh họa rõ hơn, dưới đây là một ví dụ giả định về cách sleep and wake up có thể được sử dụng trong bài toán Producer-Consumer:
```cpp
#define N 100 // Kích thước buffer
int count = 0; // Số lượng items trong buffer

// Hàm sleep
void sleep() {
  // Tạm dừng tiến trình hiện tại
  // ...
}

// Hàm wakeup
void wakeup(int process) {
  // Tiếp tục tiến trình được chỉ định
  // ...
}

// Producer
void Producer(void) {
  int item;
  while (TRUE) {
    item = produce_item(); // Sản xuất 1 item
    if (count == N) { // Buffer đầy, Producer ngủ
      sleep();
    }
    count++; // Tăng số lượng items
    insert_item(item); // Đặt item vào buffer
    if (count == 1) { // Nếu trước đó buffer rỗng, đánh thức Consumer
      wakeup(Consumer);
    }
  }
}

// Consumer
void Consumer(void) {
  int item;
  while (TRUE) {
    if (count == 0) { // Buffer rỗng, Consumer ngủ
      sleep();
    }
    count--; // Giảm số lượng items
    item = remove_item(); // Lấy 1 item từ buffer
    if (count == N - 1) { // Nếu trước đó buffer đầy, đánh thức Producer
      wakeup(Producer);
    }
    consume_item(item); // Tiêu thụ item
  }
}
```
Trong ví dụ này, **Producer "ngủ" khi buffer đầy**, và **Consumer "ngủ" khi buffer rỗng.**
Khi một **Producer thêm item vào buffer rỗng**, nó sẽ **đánh thức Consumer** đang ngủ.
Tương tự, khi một **Consumer lấy item từ buffer đầy**, nó sẽ **đánh thức Producer** đang ngủ.

