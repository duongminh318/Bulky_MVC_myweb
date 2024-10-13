# ASP .NET core 2024

# Over view
- udemy link
- main : https://www.dotnetmastery.com/Home/Details?courseId=9
- github source code : https://github.com/bhrugen/Bulky_MVC
- demo : https://bulky.azurewebsites.net/

- source
- lesson 53: Toastr Notification : https://codeseven.github.io/toastr/
- lesson 95: Rich Text Editor : https://www.tiny.cloud/
- lesson 101: Datatables API: https://datatables.net/ (sử dụng api để lấy ra sản phẩm)
- lesson 102: load Datatables : https://datatables.net/manual/ajax - hướng dẫn chuyền data
	-	https://jsonformatter.org/  - định dạng lại  json trả về cho dễ nhìn
- lesson 106: SweetAlerts : https://sweetalert2.github.io/, (cảnh báo xác nhận 1 tác vụ nào đó)
- 124: Why do we have a Company Role?
	- Customer: khách hàng, đăng ký và mua hàng
	- Company: công ty, được uỷ quyền để mua hàng, nên có 30 ngày để thanh toán
	- Admin: quản trị web, toàn quyền
	- Employee: xử lý các đơn hàng của khách
	- https://www.udemy.com/course/complete-aspnet-core-21-course/learn/lecture/37136340#notes
- 152. Register for Stripe Account - tích hợp thanh toán Stripe 
	1. https://stripe.com/ - registes account
	1. https://dashboard.stripe.com/test/apikeys
# proseeging
- đang tới 
# note
- setup các package
	+ sqlserver
	+ tools
	+ core
- PM > create-migration --> tạo migration
-	 > update database --> cập nhật DB

# flow
- tạo model với các file tương ứng
- add các nuget package


# Cấu trúc thư mục ASP .NET CORE
- Data
- IRepository và IUnitOfWork chỉ là bản thiết kế (giao diện/contract) quy định
- các phương thức và tính năng mà các lớp triển khai cụ thể phải tuân theo. 
- Chúng không chứa logic thực hiện mà chỉ định nghĩa những gì cần có.

Repository và UnitOfWork là những lớp triển khai cụ thể (concrete classes), 
chịu trách nhiệm thực hiện các phương thức và logic mà các interface đã định nghĩa.

Bạn có thể hiểu nôm na như sau:

- IRepository giống như một hợp đồng yêu cầu các repository phải có các 
- chức năng như thêm, sửa, xóa, lấy dữ liệu.

- Repository sẽ thực hiện cụ thể những chức năng đó, ví dụ: lấy sản phẩm
- từ cơ sở dữ liệu, thêm sản phẩm mới, v.v.

- IUnitOfWork giống như hợp đồng yêu cầu quản lý các repository và đảm bảo 
- các thao tác dữ liệu được thực hiện thành công, thường thông qua các giao dịch (transactions).

- UnitOfWork sẽ đảm bảo việc commit toàn bộ thay đổi vào cơ sở dữ liệu hoặc
- rollback nếu có lỗi.
 Repository Pattern
Mục đích: Tách biệt logic truy cập dữ liệu khỏi logic nghiệp vụ, giúp làm sạch mã nguồn và dễ bảo trì.
Cấu trúc:
IRepository: Giao diện chung định nghĩa các phương thức cơ bản như Add, Update, Delete, GetById, và GetAll.
Repository: Triển khai cụ thể của IRepository, thực hiện các phương thức truy cập dữ liệu cho một loại thực thể cụ thể.
Ví dụ: IProductRepository định nghĩa các phương thức cho việc quản lý sản phẩm, trong khi ProductRepository triển khai các phương thức này.
2. Unit of Work Pattern
Mục đích: Quản lý và phối hợp nhiều thao tác thay đổi dữ liệu (thêm, sửa, xóa) trong một giao dịch duy nhất, giúp đảm bảo tính toàn vẹn của dữ liệu.
Cấu trúc:
IUnitOfWork: Giao diện định nghĩa các phương thức cho việc hoàn thành hoặc hủy giao dịch, cũng như truy cập đến các repository cụ thể.
UnitOfWork: Triển khai cụ thể của IUnitOfWork, thực hiện các phương thức để quản lý các repository và lưu trữ thay đổi vào cơ sở dữ liệu.
Ví dụ: UnitOfWork có thể chứa các thuộc tính cho IProductRepository, ICategoryRepository, và các repository khác, đồng thời cung cấp phương thức để lưu tất cả các thay đổi vào cơ sở dữ liệu.
3. Mối quan hệ giữa Repository và UnitOfWork
Repository chịu trách nhiệm thực hiện các thao tác cụ thể trên dữ liệu.
UnitOfWork quản lý các repository và đảm bảo rằng tất cả các thay đổi được thực hiện trong một giao dịch duy nhất, giúp duy trì tính toàn vẹn của dữ liệu.
4. Lợi ích
Tăng cường khả năng tái sử dụng mã nguồn.
Dễ dàng kiểm tra đơn vị (unit testing) do tách biệt logic.
Cải thiện khả năng mở rộng và bảo trì ứng dụng.


- Các Interface Con
a. IProductRepository
Mục đích: Cung cấp các phương thức cụ thể cho việc quản lý sản phẩm.
Ví dụ phương thức:
Product GetProductById(Guid id);
IEnumerable<Product> GetProductsByCategoryId(Guid categoryId);
b. ICategoryRepository
Mục đích: Cung cấp các phương thức cụ thể cho việc quản lý danh mục sản phẩm.
Ví dụ phương thức:
Category GetCategoryById(Guid id);
IEnumerable<Category> GetAllCategories();
c. IRepository
Mục đích: Cung cấp giao diện chung cho các repository khác nhau.
Phương thức cơ bản:
void Add(T entity);
void Update(T entity);
void Delete(T entity);
T GetById(Guid id);
IEnumerable<T> GetAll();
d. IUnitOfWork
Mục đích: Định nghĩa các phương thức để quản lý giao dịch.
Ví dụ phương thức:
void Save();
IProductRepository Products { get; }
ICategoryRepository Categories { get; }
6. Mối Quan Hệ Giữa Các Interface
Các interface con như IProductRepository và ICategoryRepository mở rộng từ IRepository, cung cấp các phương thức cụ thể hơn cho từng loại thực thể.
IUnitOfWork chứa các thuộc tính để truy cập các repository con, đảm bảo rằng tất cả các thay đổi được quản lý trong một giao dịch duy nhất.
7. Lợi Ích Của Việc Sử Dụng Các Interface Con
Tính linh hoạt: Cho phép thay đổi hoặc mở rộng chức năng của các repository mà không làm ảnh hưởng đến các phần khác của mã nguồn.
Tái sử dụng mã: Có thể dễ dàng tái sử dụng mã trong các lớp khác nhau thông qua các interface.
Dễ dàng kiểm tra: Giúp đơn giản hóa việc kiểm tra đơn vị do việc cung cấp các giao diện rõ ràng cho các chức năng cụ thể.

# Lập trình bất đồng bộ
## KHÁI NIỆM
- a) Đồng bộ:
Ứng dụng console tính toán hoặc xử lý dữ liệu đơn giản.
Xử lý các tác vụ nhỏ không gây ra chờ đợi
	 (ví dụ: tính toán toán học, truy xuất dữ liệu bộ nhớ).
b) Bất đồng bộ:
Ứng dụng web xử lý nhiều yêu cầu từ người dùng và thực hiện các tác
	vụ như truy vấn cơ sở dữ liệu.
Ứng dụng giao diện người dùng (UI) khi bạn cần đảm bảo người 
	 dùng vẫn có thể tương tác với giao diện trong khi chờ dữ liệu từ API hoặc đọc/ghi file.
- lập trình bất đồng bộ có thể được hình dung giống như chạy tiếp sức.
Mỗi tác vụ bất đồng bộ giống như một vận động viên trong đội chạy
tiếp sức. Mỗi người chỉ chạy khi đã nhận được que tiếp sức từ người
chạy trước, và đến lượt mình, họ sẽ đưa que tiếp sức cho người tiếp theo.

Trong lập trình bất đồng bộ:

Khi một tác vụ (Task) đang chờ một việc gì đó hoàn thành (ví dụ: đọc dữ liệu từ cơ sở dữ liệu, chờ phản hồi từ API), nó không chiếm giữ tài nguyên mà có thể "tạm nghỉ" và chờ kết quả.
Khi kết quả đã sẵn sàng, nó tiếp tục chạy và trả kết quả cho tác vụ tiếp theo, giống như người chạy nhận que tiếp sức và chạy tiếp.
Cách này giúp hệ thống không bị lãng phí tài nguyên khi chờ đợi và có thể làm những việc khác trong lúc chờ đợi, làm tăng hiệu suất chung. Đây là điểm mạnh của lập trình bất đồng bộ so với lập trình đồng bộ truyền thống, nơi mà một nhiệm vụ phải đợi xong trước khi tiếp tục nhiệm vụ tiếp theo.

Cơ chế này giúp ứng dụng có thể phục vụ nhiều yêu cầu hơn mà không bị "nghẽn" bởi những tác vụ dài hạn, như truy cập cơ sở dữ liệu hoặc gọi API từ bên ngoài.

Anh có thể tưởng tượng thêm, mỗi tác vụ không cần phải đứng đợi ở đó mà có thể đi làm việc khác, khi que tiếp sức (kết quả) tới thì lập tức quay lại chạy tiếp.
- async: Được đặt trước một phương thức để chỉ ra rằng phương thức 
	- này thực hiện bất đồng bộ.
- Task<string>: Cho biết rằng phương thức trả về một tác vụ 
	- (task) có kết quả là một chuỗi (string).
- await: Sử dụng để chờ một tác vụ hoàn thành mà không chặn luồng
	- chính. Khi gặp await, luồng chính có thể thực hiện những tác vụ khác cho đến khi tác vụ chờ hoàn thành.


## Mối quan hệ giữa Repository và Unit of Work
Repository chịu trách nhiệm cung cấp các thao tác CRUD cơ bản cho 
- một thực thể (Entity) cụ thể (ví dụ như Product, Category,...).
Unit of Work kết hợp các repository khác nhau và đảm bảo rằng tất 
- cả các thay đổi trong phiên làm việc sẽ được thực hiện trong một 
- giao dịch (transaction). Nếu có lỗi xảy ra, Unit of Work sẽ rollback 
- tất cả các thay đổi để bảo toàn tính nhất quán của dữ liệu.

# Note ngẫu nhiên
- SD
Class SD trong đoạn mã trên là một lớp tĩnh chứa các hằng số liên quan đến vai trò người dùng 
và trạng thái đơn hàng trong ứng dụng.

Mục đích:
Vai trò người dùng: Xác định các vai trò như Customer, Company, Admin, và Employee.
Trạng thái đơn hàng: Định nghĩa các trạng thái khác nhau của đơn hàng, 
như Pending, Approved, Processing, Shipped, Cancelled, và Refunded.
Trạng thái thanh toán: Định nghĩa các trạng thái liên quan đến thanh toán,
bao gồm Pending, Approved, ApprovedForDelayedPayment, và Rejected.
