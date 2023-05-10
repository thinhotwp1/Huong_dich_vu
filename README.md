# team-project-n1_14
team-project-n1_14 created by GitHub Classroom

Chủ đề: Web bán hàng mỹ phẩm
## 1. Quy trình nghiệp vụ: Lên đơn hàng và xuất hóa đơn theo thông tin khách hàng cung cấp
-   Nhận đơn hàng từ khách hàng, bao gồm thông tin khách hàng, số lượng hàng đặt và ưu đãi
-   Kiểm tra đơn hàng hợp lệ
-   Tạo đơn hàng trên hệ thống, cập nhật các CSDL
-   Gửi hóa đơn cho khách hàng

![SOA-Flowchart](https://user-images.githubusercontent.com/103843005/234435707-3972895e-d642-41a4-904d-3defd6af586e.png)

## 2. Phân tích và mô hình hóa dịch vụ
### 1. Phân tách quy trình thành các hành động chi tiết
-   Bắt đầu quy trình lên đơn
-   Nhận thông tin từ khách hàng
-   Kiểm tra thông tin khách hàng (địa chỉ, sđt hợp lệ)
-   Nếu thông tin khách hàng không hợp lệ, báo lỗi
-   Kiểm tra đơn hàng về mặt kho hàng (còn hàng hay không?), ưu đãi (nếu có)
-   Nếu hết hàng hoặc ưu đãi không hợp lệ, báo lỗi
-   Nếu có lỗi, thông báo lỗi về cho khách hàng, ghi log và kết thúc
-   Xác nhận đơn hợp lệ thủ công
-   Cập nhật CSDL tồn kho
-   Tạo đơn hàng và thêm vào CSDL đơn hàng
-   Tạo hóa đơn và gửi cho khách hàng
-   Kết thúc quy trình

### 2.	Gạch bỏ các bước không phù hợp
 **Không phải tất cả các các logic quy trình đều phù hợp để thực hiện mô hình REST service. Các hành động không phù hợp bị gạch bỏ là:**
-   Xác nhận đơn hợp lệ thủ công

### 3.	Xác định ứng viên dịch vụ thực thể
 **Xem xét các hành động còn lại từ bước, xác định và phân loại những hành động được coi là bất khả tri (Được in đậm):**
-   Bắt đầu quy trình lên đơn
-   **Nhận thông tin từ khách hàng**
-   Kiểm tra thông tin giao hàng (địa chỉ, sđt hợp lệ)
-   Nếu thông tin giao hàng không hợp lệ, báo lỗi
-   Kiểm tra đơn hàng về mặt kho hàng (còn hàng hay không?), ưu đãi (nếu có)
-   Nếu hết hàng hoặc ưu đãi không hợp lệ, báo lỗi
-   **Nếu có lỗi, thông báo lỗi về cho khách hàng, ghi log và kết thúc**
-   Cập nhật CSDL tồn kho
-   Tạo đơn hàng và thêm vào CSDL đơn hàng
-   Tạo hóa đơn và gửi cho khách hàng
-   Kết thúc quy trình

**Các ứng viên dịch vụ thực thể được xác định:**
 
 -	Ứng viên **Customer**
  ```bash
  Để lấy thông tin của khách đặt hàng, ta thiết lập ứng viên Get Detail
  ```
  
 ![Customer1](https://user-images.githubusercontent.com/103843005/234381868-cb95c047-eec9-47ed-ac4a-de22b1dadfbb.png)

 -	Ứng viên **Item**
  ```bash
  Để lấy thông tin của mặt hàng gồm tên mặt hàng, số lượng,… ta thiết lập ứng viên Get Detail
  ```  
  ```bash
  Để cập nhật số lượng của mặt hàng sau khi lên đơn, ta thiết lập ứng viên Update Stock
  ```
 
 ![Item1](https://user-images.githubusercontent.com/103843005/234381913-212926dd-5096-411e-bede-798a2e0faed2.png)

 -	Ứng viên **Order**
  ```bash
  Để lấy thông tin đặt hàng, ta thiết lập ứng viên Get Detail
  ```

![Order1](https://user-images.githubusercontent.com/103843005/234382327-d550389d-b155-4ea1-89d9-fba1f5451d58.png)

### 4.	Xác định logic cụ thể của cả quá trình

 **Các bước không bất khả tri:**
-   Bắt đầu quy trình lên đơn
-   Kiểm tra thông tin khách hàng (địa chỉ, sđt hợp lệ)
-   Nếu thông tin khách hàng không hợp lệ, báo lỗi
-   Kiểm tra đơn hàng về mặt kho hàng (còn hàng hay không?), ưu đãi (nếu có)
-   Nếu hết hàng hoặc ưu đãi không hợp lệ, báo lỗi
-   Cập nhật CSDL tồn kho
-   Tạo đơn hàng và thêm vào CSDL đơn hàng
-   Tạo hóa đơn và gửi cho khách hàng
-   Kết thúc quy trình

Ta chọn “Bắt đầu quy trình lên đơn” là ứng viên năng lực dịch vụ cho ứng viên dịch vụ “Đặt hàng online”

Ứng viên "Create Order" sẽ được gọi bởi một chương trình phần mềm riêng biệt, chương trình này sẽ hoạt động như một bộ khởi tạo tích hợp

![CreateOrder1](https://user-images.githubusercontent.com/103843005/234382639-b532d987-3f76-4525-b4de-c6d8cb7efc8f.png)

### 5.	Xác định tài nguyên
 -	Customer: /customers/
 -	Item: /items/
 -	Order: /orders/


### 6.	Liên kết các dịch vụ với tài nguyên tương ứng
 -	Create Order service

![CreateOrder2](https://user-images.githubusercontent.com/103843005/234382790-57b0af2d-d815-4021-bbd0-ac9a59b9c938.png)

 -	Customer service

![Customer2](https://user-images.githubusercontent.com/103843005/234382811-e5e1fa56-c262-4f03-be38-c08a165ffccd.png)

 -	Item service

![Item2](https://user-images.githubusercontent.com/103843005/234382826-341519b0-9ad2-48ee-ba21-63295e2e0204.png)

 -	Order service

![Orders](https://user-images.githubusercontent.com/103843005/234383048-c834b759-7cce-4ce8-8523-9341c7c543d5.png)

### 7.	Áp dụng hướng dịch vụ
### 8.	Xác định các ứng viên tổ hợp dịch vụ 

![Diagram1](https://user-images.githubusercontent.com/103843005/234381798-762a1ee7-2159-478f-80d4-58716fac2b28.png)

### 9.	Phân tích yêu cầu xử lý
### 10.	Xác định các ứng viên dịch vụ tiện ích

-	  Hành động thông báo từ chối và ghi log nội bộ được hợp thành một ứng viên khả năng dịch vụ chung:
 
![Notification](https://user-images.githubusercontent.com/103843005/234381746-fa4b1e1d-7670-4054-bf42-c41c1d9aeec2.png)

-   Hành động gửi hóa đơn cho khách hàng được hợp thành một ứng viên khả năng dịch vụ khác:

![SendReceipt](https://user-images.githubusercontent.com/103843005/234381700-5064bac5-e9bd-4e20-b8d7-4582b4386ac0.png)

### 11.	Xác định các ứng viên vi dịch vụ
-  	 Để hỗ trợ tách rời xử lý cho hành động “xác minh đơn hàng”, bao gồm kiểm tra thông tin khách hàng và lượng tồn kho của hàng, đề xuất một ứng viên vi dịch vụ là Verify Order:
 
![VerifyOrder](https://user-images.githubusercontent.com/103843005/234381659-3dba6a6d-b64f-45b2-8ced-985ed9a0a992.png)

### 12.	Áp dụng hướng dịch vụ
### 13.	Sửa đổi các ứng viên tổ hợp dịch vụ

![Diagram2](https://user-images.githubusercontent.com/103843005/234381606-5a410cd2-d879-4268-80cf-77c37223c5e6.png)

### 14.	Sửa đổi định nghĩa nguồn lực và phân nhóm ứng viên năng lực

## 3. Thiết kế API dịch vụ và hợp đồng
-   Một đơn hàng nhận từ khách hàng sẽ bao gồm các thông tin: thông tin về người/địa chỉ đặt hàng (bao gồm tên, địa chỉ, số điện thoại), danh sách các mặt hàng đặt, số lượng của từng sản phẩm, ưu đãi giảm giá (nếu có). Khách hàng sẽ tạo đơn thông qua một giao diện front-end, và việc gửi đơn hàng tới hệ thống sẽ bắt đầu task service xử lý đơn hàng.
-   Sau khi nhận được thông tin đơn hàng, hệ thống sẽ xử lý thông tin này thành dạng Java Object. Dưới đây là biểu diễn của một đơn hàng mẫu (gồm id đơn hàng, thông tin khách hàng và một list sản phẩm):

![image](https://github.com/jnp2018/team-project-n1_14/assets/61654110/52a525b0-1325-4ed2-a9e2-87a55cb93f22)
  
### 1. Create Order service (Task): bổ sung 2 phương thức
-  	GET /incoming-orders/{id}: lấy thông tin về tình trạng của một đơn hàng đang xử lý – nhân viên và khách hàng cập nhật tình trạng đơn hàng
-	  DELETE /incoming-orders/{id}: ngừng quá trình xử lý một đơn hàng – nhân viên hoặc khách hàng hủy đơn hàng khi đơn đang được xử lý

![Create Order 2](https://github.com/jnp2018/team-project-n1_14/assets/103843005/e9df466e-41bc-4f94-8055-b15e78d2f95c)

### 2.	Customer service (Entity): bổ sung 2 phương thức
-	  PUT + /customers/{id}: cập nhật thông tin khách hàng khi có thay đổi
-	  DELETE + /customers/{id}: xóa thông tin khách hàng – dùng khi khách hàng yêu cầu xóa tài khoản

![Customer 2](https://github.com/jnp2018/team-project-n1_14/assets/103843005/95fbe964-0b0f-4ed2-bad1-e3ffa467bf84)

### 3.	Item service (Entity): bổ sung 2 phương thức
-	  POST + /items/: thêm sản phẩm vào CSDL
-	  DELETE + /items/{id}: xóa sản phẩm khỏi CSDL

![Item 2](https://github.com/jnp2018/team-project-n1_14/assets/103843005/1f0dc6e0-7258-4c74-9e00-fcde81f8d4aa)

### 4.	Order service (Entity): bổ sung
-	  POST + /api/order: order đơn hàng với thông tin đơn hàng 

![Order 2](https://github.com/jnp2018/team-project-n1_14/assets/103843005/bb263291-a2af-4d7a-b3c7-318631474f32)

### 5.	Notification service và Send Receipt service (utility): cập nhật thành phương thức POST
POST + /api/email: Gửi email tới email khách hàng khi đặt đơn hàng thành công

![Notification + Receipt 2](https://github.com/jnp2018/team-project-n1_14/assets/103843005/ad06f414-58e1-4053-becc-6cf744171bba)

## 4. Mô tả công nghệ:
Công nghệ sử dụng: 


![image](https://user-images.githubusercontent.com/61654110/234435890-f80a6430-2357-4c74-9d1b-2f90e5a45b34.png)


Luồng hoạt động:
Đầu tiên client sẽ đi qua api gate way để vào hệ thống, sau khi nhận oder service tạo đơn hàng sản phẩm và oder,  message service sẽ gửi tin nhắn tới inventory service để cập nhật số lượng tồn kho của sản phẩm và gửi tới module message báo về điện thoại của khách hàng 


Cấu hình máy chủ: 

![image](https://user-images.githubusercontent.com/61654110/232797771-65461bc4-4784-40a3-9d03-d79e9c57656a.png)


Ở dự án này, các module được chia thành nhỏ thành module product-service, oder-service, message-service, inventory-service, api-gateway, discovery-service với các chức năng chính:
product-service: Quản lý sản phẩm
oder-service: Quản lý oder, mua bán sản phẩm
inventory-service: Quản lý kho hàng
api-gateway: Chia các request từ client đến dựa theo config của ứng dụng web
discovery-service: Đăng kí cổng với eureka
message-service: Tạo hóa đơn với hàng đợi tin nhắn rabbitmq (Kiến trúc hướng sự kiện)

Đăng kí các service lên eureka:

![image](https://user-images.githubusercontent.com/61654110/232809505-b75d4b6e-7c83-4975-ac0b-f22a32ed5ffd.png)

Đóng vai trò là người gác cổng, chia tải và định tuyến các request từ người dùng tới phần mềm, tránh quá tải hệ thống, …Người dùng thay vì gọi đến localhost:8082,8083,... thì chỉ cần gọi đến 8080 của api gateway từ đó nó sẽ tự phân tải sang các service còn lại

![image](https://user-images.githubusercontent.com/61654110/232827822-38449e02-5692-43db-a392-c6d38602f560.png)


Quản lý hàng đợi tin nhắn giao tiếp giữa các service: (sử dụng RabbitMQ)

![image](https://user-images.githubusercontent.com/61654110/232810007-78818f94-47b0-49df-96e7-c9f60288cf1d.png)

Mô tả giao tiếp các service với kịch bản bất đồng bộ: 

![image](https://user-images.githubusercontent.com/61654110/232814081-cde67cf8-f21d-4bc1-9761-f0952ce22154.png)

- Khi hoàn thành đơn hàng sẽ đẩy tin nhắn đến message-service để gửi tin nhắn tới khách hàng qua gmail, zalo , tránh lưu lượng lớn người truy cập cùng lúc gây sập database, các request/response được xử lý nhanh hơn nhiều lần

Chạy các service: 

![image](https://user-images.githubusercontent.com/61654110/232810136-78ebe9e3-9a38-4cca-b8a1-087cbb0c65ea.png)

