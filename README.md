# MULTIMODEL INTERACTION IN ROBOTICS

*Trong bài nghiên cứu này sẽ đưa ra những cái nhìn tổng quan về việc phát triển một hệ thống tương tác đa phương thức giữa người và Robot. Cụ thể hơn, hệ thống sẽ có khả năng nhận diện giọng nói và khuôn mặt của người dùng, phản hồi lại thông tin thông qua âm thanh và và giao diện thị giác (màn hình). Ngoài ra, hệ thống robot cũng có khả năng tương tác và cử chỉ chào hỏi để tạo ra trải nghiệm tự nhiên cho người dùng.*

 **Tổng quan**

![image](https://github.com/mylehust/Robot_interaction/assets/109675981/5966072a-2746-47b9-bf8e-5566ec0c35f0)


*Hình ảnh sự phát triển của HRI trong các bài báo từ năm 2013 đến 2023*

Trước đây, để có thể thu thập được thông tin hữu ích, con người thông qua việc gõ bàn phím truyền thống, nhấp chuột, chạm màn hình và có tiên tiến hơn là công nghệ nhận dạng giọng nói. Tuy nhiên, bằng cách kết hợp các phương thức với nhau, thông tin có thể được truyền đạt tới người dùng một cách hiệu quả hơn và có tính biểu cảm. Thuật ngữ “*multimodel – đa phương thức*” tập trung vào việc kết hợp các kênh nhận thức khác nhau của con người (6 giác quan), liên hệ tới những khả năng của con người: giao tiếp, nhận tức, tư duy… nhằm cải thiện, nâng cao sự thông hiểu của con người về những gì đang được trình bày. 

Một hệ thống đa phương thức cho phép tác nhân đầu vào gửi các dữ liệu khác nhau, và đối với đầu ra, màn hình hiển thị, tổng hợp giọng nói, nét mặt cũng như những cử chỉ sẽ được sử dụng.

![image](https://github.com/mylehust/Robot_interaction/assets/109675981/4cec91c1-a89f-41c5-9f93-0f3a8091d23b)


*Multimodel System*

Câu hỏi đặt ra chính là làm thế nào để thống xử lý đầu vào và đầu ra của nhiều kênh? Đầu tiên là cách tiếp nhận và phân tích nhiều thông tin đầu vào và thứ hai là tạo ra nhiều thông tin đầu ra thích hợp. Trái ngược hoàn toàn với trải nghiệm của con người với thế giới tự nhiên, tương tác giữa con người và máy tính trước đây tập trung vào giao tiếp đơn phương thức - tức là thông tin hoặc dữ liệu được truyền giữa con người và máy tính chủ yếu thông qua một chế độ hoặc kênh duy nhất, chẳng hạn như văn bản trên màn hình bằng bàn phím cho đầu vào. Trong khi, về mặt kỹ thuật, hầu hết mọi tương tác với máy tính đều mang tính đa phương thức ở một mức độ nào đó. Do đó có thể thấy thách thức lớn nhất của việc tạo hệ thống đa phương thức là cách hợp nhất các kiểu dữ liệu không đồng nhất, kiến trúc xử lý thời gian thực.



**Đề xuất phương pháp sử dụng** 

Một hệ thống tương tác người máy yêu cầu 3 thành phần chính: người dùng tương tác, hệ thống, và sự tương tác của người dùng và hệ thống. Trong nghiên cứu này, chúng ta sẽ đi chi tiết về cả 3 phần trên.

![image](https://github.com/mylehust/Robot_interaction/assets/109675981/d9b54995-e4ef-4b01-b8ec-4df38433a928)


*Bảng: Giới hạn của các model*

Dựa vào đánh giá thông số những giới hạn của các phương pháp, ta sẽ lựa chọn các input model đầu vào bao gồm audio và vision để đơn giản hóa bài toán đưa ra.

Đầu tiên, quy trình bắt đầu với một camera để nhận diện con người. Khi robot nhận diện được người trong tầm nhìn và cần thiết, nó sẽ cập nhật hướng và điều chỉnh máy ảnh về phía người này. Tiếp theo, một mô-đun phát hiện giọng nói được sử dụng. Nếu không có hoạt động giọng nói nào được phát hiện, hệ thống có thể chuyển sang chế độ chờ đợi, cho rằng không có người dùng nào muốn tương tác. Khi hoạt động giọng nói được phát hiện, âm thanh sẽ được đưa qua quá trình khử nhiễu. Trong trường hợp tỷ lệ tín hiệu so với nhiễu thấp (SNR), việc khử nhiễu là quan trọng để làm sạch tín hiệu âm thanh. Sau đó âm thanh được chuyển thành tín hiệu đầu vào, Robot sẽ tiếp tục hoạt động và trích xuất các câu hỏi thông qua hệ thống của mình để tương tác với người dùng.

Trong nghiên cứu này, tôi đề xuất tích hợp các thành phần nhận thức âm thanh và hình ảnh vào hệ thống qua ROS (Robot Operating System), sử dụng nhận dạng cử chỉ và khuôn mặt thông qua camera độ sâu. Các dãy micrô sẽ được sử dụng để định vị nguồn âm thanh và nhận thức thính giác. Điều này sẽ cho phép robot tương tác hiệu quả trong các tình huống đa người, như chú ý đến người nói hoặc người vẫy tay.

![image](https://github.com/mylehust/Robot_interaction/assets/109675981/03c08520-0d8e-46bc-8c91-5a4baf221ad3)


*Chu trình làm việc*

Đối với việc chuyển đổi giọng nói thành văn bản và phản hồi thông tin từ người dùng, để đơn giản hóa cho bước mở đầu, chúng tôi đề xuất sử dụng máy tính cá nhân và xây dựng một chatbot. Các API chuyển đổi giọng nói thành văn bản và ngược lại đã được tích hợp sẵn có thể tìm kiếm trên google (Speech Recognition to text). Chatbot này sẽ có khả năng nhận dạng và xử lý thông tin đầu vào từ người dùng (văn bản), sau đó tạo ra câu trả lời và chuyển đổi thành giọng nói đầu ra.

![image](https://github.com/mylehust/Robot_interaction/assets/109675981/6ed62bd9-f5e9-4b08-b16a-1f6532bfdb0c)


Cuối cùng, chúng tôi đề xuất sử dụng phương pháp học tăng cường dựa trên mạng thần kinh để điều khiển robot thông qua ánh mắt. Điều này cho phép robot tự động học cách tìm kiếm và ưu tiên người trong môi trường, đồng thời tối ưu hóa việc tương tác với họ. Việc đào tạo trước trên môi trường mô phỏng sẽ giúp cải thiện hiệu suất trước khi triển khai vào môi trường thực tế, ưu tiên những người nói chuyện. 

