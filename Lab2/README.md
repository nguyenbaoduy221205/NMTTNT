# Thuật toán BFS & DFS - README

## 1. Công nghệ sử dụng
- Python 3 (>= 3.7)  
- Module `collections` (sử dụng deque cho BFS, defaultdict cho đồ thị)  
- Module `heapq` (sử dụng cho hàng đợi ưu tiên trong thuật toán Dijkstra)  
- Modules `time` và `statistics` (đo thời gian và tính toán hiệu suất)  
- Module `typing` (sử dụng type hint cho hàm và cấu trúc dữ liệu)  
- Môi trường Jupyter Notebook (hoặc Google Colab) để chạy và minh họa code  

## 2. Tổng quan cách hoạt động
**Thuật toán BFS (Breadth-First Search)** duyệt đồ thị theo chiều rộng, khám phá từng lớp nút một. BFS sử dụng cấu trúc **hàng đợi (FIFO)** để lưu trữ các nút sẽ duyệt. Nhờ duyệt theo tầng, BFS luôn tìm được **đường đi ngắn nhất theo số bước** trong **đồ thị không trọng số**. (Tuy nhiên, trên **đồ thị có trọng số**, BFS không đảm bảo đường đi có **tổng trọng số nhỏ nhất** do không xét trọng số các cạnh.)  

Ví dụ mã giả Python cho BFS trên đồ thị không trọng số (dùng deque):  
```python
from collections import deque

def bfs(graph, start, goal):
    # Khởi tạo hàng đợi với nút bắt đầu và đường đi ban đầu
    queue = deque([(start, [start])])
    # Khởi tạo tập hợp các nút đã thăm để tránh lặp
    visited = set([start])

    # Lặp cho đến khi hàng đợi rỗng
    while queue:
        # Lấy nút đầu tiên và đường đi tương ứng từ hàng đợi
        node, path = queue.popleft()
        # Nếu nút hiện tại là đích, trả về đường đi
        if node == goal:
            return path
        # Duyệt qua các nút kề của nút hiện tại
        for neighbor in graph[node]:
            # Nếu nút kề chưa được thăm
            if neighbor not in visited:
                visited.add(neighbor)                 # Đánh dấu đã thăm
                queue.append((neighbor, path + [neighbor]))  # Thêm vào hàng đợi
    # Trả về None nếu không tìm thấy đường đi
    return None
```  

**Thuật toán DFS (Depth-First Search)** duyệt đồ thị theo chiều sâu, đi sâu vào một nhánh cho đến khi không thể đi tiếp, sau đó quay lui. DFS thường được cài đặt bằng **ngăn xếp (LIFO)** hoặc đệ quy. Do đi theo nhánh, DFS **không đảm bảo tìm đường đi ngắn nhất** trên cả đồ thị không trọng số lẫn có trọng số (kết quả phụ thuộc vào thứ tự duyệt các nút kề). DFS phù hợp để tìm **bất kỳ** đường đi tới đích, nhưng có thể bỏ sót đường ngắn hơn nếu không điều chỉnh thứ tự duyệt.  

Trong notebook này, nhiều biến thể của BFS và DFS đã được triển khai nhằm phục vụ mục đích học tập:
- **BFS đếm số đỉnh đã thăm:** Biến thể BFS trả về cả đường đi tìm được và **số lượng đỉnh đã duyệt**. Ví dụ, trên đồ thị mẫu 4 (dạng lưới), BFS tìm đường đi từ S đến G đồng thời đếm số nút duyệt để so sánh với tổng số nút của đồ thị.  
- **BFS và DFS liệt kê mọi đường đi:** Cả BFS và DFS đều được mở rộng để liệt kê **tất cả các đường đi** từ nút bắt đầu. Cụ thể, khi không chỉ định đích (goal), hàm BFS/DFS sẽ duyệt toàn bộ đồ thị và lưu lại tất cả đường đi có thể. Điều này hữu ích để hiểu cấu trúc đồ thị và kiểm tra độ phủ của thuật toán.  
- **Thuật toán Dijkstra (Uniform-Cost Search):** Được triển khai để tìm **đường đi có tổng trọng số nhỏ nhất** trong đồ thị có trọng số. Dijkstra sử dụng hàng đợi ưu tiên (`heapq`) để luôn chọn mở rộng nút có chi phí nhỏ nhất trước. Thuật toán này giúp khắc phục hạn chế của BFS/DFS trên đồ thị trọng số, đảm bảo tìm được đường đi tối ưu về chi phí.  

**Đồ thị mẫu sử dụng:** Notebook đã sử dụng nhiều ví dụ đồ thị để minh họa:
- **Đồ thị mẫu 2:** Đồ thị vô hướng **không trọng số** có chu trình (ví dụ vòng A–B–A). Dùng để kiểm chứng cơ chế tránh lặp vô hạn của BFS/DFS với tập `visited`.  
- **Đồ thị mẫu 4:** Đồ thị **dạng lưới, không trọng số** (7 đỉnh) với nhiều kết nối dạng lưới. Dùng để minh họa BFS và đếm số nút đã duyệt.  
- **Đồ thị mẫu 6:** Đồ thị **có trọng số** với nhiều đường khác nhau từ S đến H và chứa chu trình. Minh họa sự khác biệt giữa BFS, DFS trên đồ thị trọng số và lý do cần đến Dijkstra (BFS/DFS không tối ưu chi phí trên đồ thị này).  
- **Đồ thị mẫu 7:** Đồ thị **không trọng số, mật độ cạnh cao** (nhiều kết nối, nhiều chu trình). Dùng để so sánh hiệu suất BFS/DFS trên đồ thị dày đặc, nơi có nhiều đường đi cùng độ dài.  
- **Đồ thị tùy thiết kế (10 đỉnh trở lên):** Một đồ thị có trọng số gồm **10 đỉnh (A–J)** và **15 cạnh** được tạo ra để so sánh trực quan kết quả BFS, DFS và Dijkstra. Đồ thị này cho phép kiểm chứng trực tiếp đường đi và tổng trọng số mà mỗi thuật toán tìm được, qua đó rút ra nhận xét về tính tối ưu và hiệu suất.

## 3. Cách chạy mã
Để chạy notebook **BFS-DFS.ipynb**, bạn có thể sử dụng Jupyter Notebook trên máy hoặc Google Colab trực tuyến:
1. Mở Jupyter Notebook và điều hướng đến file `BFS-DFS.ipynb` (nếu đang dùng Google Colab thì tải lên file notebook này). Đảm bảo môi trường có đầy đủ các thư viện Python cần thiết.  
2. Thực thi tuần tự từng ô (cell) từ trên xuống dưới. Các ô đầu tiên thường thiết lập môi trường và định nghĩa hàm, các ô tiếp theo minh họa thuật toán trên các đồ thị mẫu, và cuối cùng là phần so sánh kết quả.  
3. Quan sát kỹ **đầu ra (output)** sau khi chạy mỗi ô mã. Notebook có in ra các bước duyệt BFS/DFS thủ công, đường đi tìm được, số nút duyệt, và so sánh kết quả giữa các thuật toán. Các chú thích (comment) trong code sẽ giúp hiểu rõ từng bước hoạt động.  
4. *Gợi ý:* Sau khi thử nghiệm trên notebook, bạn có thể tách các hàm BFS, DFS, Dijkstra ra một file Python riêng (ví dụ: `search_algorithms.py`). Sau đó, có thể chạy các hàm này từ **command-line** hoặc tích hợp vào các chương trình khác. Ví dụ, chạy `python search_algorithms.py` (sau khi thêm đoạn `if __name__ == "__main__":` để thử nghiệm) hoặc import các hàm trong dự án khác để sử dụng lại.

## 4. So sánh kết quả
Notebook đã so sánh kết quả đường đi tìm được bởi BFS, DFS và Dijkstra trên cùng một đồ thị có trọng số (đồ thị 10 đỉnh A–J). Bảng dưới đây minh họa sự khác biệt về **số bước (số cạnh)** và **tổng trọng số** của đường đi từ đỉnh A đến đỉnh J do mỗi thuật toán tìm được:

| Thuật toán | Đường đi A → J            | Số bước | Tổng trọng số |
|-----------|---------------------------|---------|--------------|
| **BFS**   | A → B → F → J             | 3 bước  | 16           |
| **DFS**   | A → B → E → I → F → C → G → D → H → J | 9 bước  | 42           |
| **Dijkstra** | A → B → E → I → J       | 4 bước  | 10           |

*Kết luận:* Trên đồ thị có trọng số, BFS tìm được đường đi với **ít bước nhất** (3 bước) nhưng tổng trọng số rất lớn (16) do không quan tâm trọng số các cạnh. DFS có thể đi theo một nhánh rất sâu tùy thứ tự duyệt (trong ví dụ trên là một đường vòng phức tạp, tận 9 bước với trọng số 42). Thuật toán Dijkstra cho kết quả tối ưu về chi phí với tổng trọng số nhỏ nhất (10), mặc dù số bước có thể nhiều hơn BFS một chút.  

## 5. Hiệu suất
Notebook tiến hành đo hiệu suất của BFS và DFS bằng cách chạy lặp lại thuật toán **10.000 lần** trên các đồ thị mẫu 6 và 7, sau đó tính thời gian chạy trung bình của mỗi thuật toán:
- **Đồ thị mẫu 6** (có trọng số, nhiều đường đi): Kết quả benchmark cho thấy **DFS** chạy nhanh hơn **BFS** trên đồ thị thưa này. Cụ thể, DFS hoàn thành trung bình nhanh hơn khoảng 30–40% so với BFS.  
- **Đồ thị mẫu 7** (không trọng số, đồ thị mật độ cao): Cả BFS và DFS đều tìm đích rất nhanh (đích H kết nối trực tiếp S qua 2 bước), do đó thời gian trung bình của hai thuật toán **không chênh lệch nhiều**. Thực tế đo được cho thấy DFS nhỉnh hơn BFS một chút về thời gian, nhưng sự khác biệt không đáng kể.  

**Phân tích chung:** Hiệu suất của BFS vs DFS phụ thuộc lớn vào **cấu trúc đồ thị** và **vị trí của nút đích**:
- Với **đồ thị dày đặc** hoặc trường hợp đích nằm nông, BFS thường hoạt động ổn định và dễ dự đoán hơn.  
- Với **đồ thị thưa** hoặc trường hợp đích nằm sâu theo một nhánh, DFS có thể tận dụng đi thẳng tới đích và do đó **nhanh hơn BFS**, miễn là đích nằm trên nhánh được duyệt đầu tiên.  
- Nhìn chung, BFS tốn bộ nhớ hơn (do phải lưu nhiều nút cùng tầng trong hàng đợi), còn DFS tốn ít bộ nhớ hơn nhưng thời gian có thể dao động nhiều tùy đường đi.  

## 6. Mục đích và ứng dụng
**Mục đích giáo dục:** Notebook này được xây dựng để giúp sinh viên hiểu và thực hành các **thuật toán tìm kiếm mù** kinh điển BFS và DFS. Thông qua các ví dụ minh họa chi tiết, người học nắm vững nguyên lý hoạt động, ưu/nhược điểm của từng thuật toán, cũng như thấy được hạn chế của chúng trên đồ thị có trọng số để từ đó tìm hiểu thêm thuật toán nâng cao (*Dijkstra/UCS*).  

**Ứng dụng thực tế:** BFS và DFS là nền tảng cho nhiều bài toán và ứng dụng:
- **Giải mê cung/labyrinth:** BFS giúp tìm đường đi ngắn nhất khi mỗi bước có chi phí bằng nhau.  
- **Mạng xã hội:** BFS tính khoảng cách kết nối giữa hai người dùng; DFS có thể kiểm tra thành phần liên thông.  
- **Backtracking (Sudoku, tô màu đồ thị):** DFS là cơ sở cho kỹ thuật thử – sai.  
- **Hệ thống GPS / định tuyến mạng:** Dijkstra (và A*) mở rộng BFS để tìm lộ trình tối ưu chi phí.  

