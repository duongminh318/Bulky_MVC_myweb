# ASP .NET core 2024

# Over view
- udemy link
- main : https://www.dotnetmastery.com/Home/Details?courseId=9
- github source code : https://github.com/bhrugen/Bulky_MVC
- demo : https://bulky.azurewebsites.net/

- source
- lesson 53: Toastr Notification : https://codeseven.github.io/toastr/
- 
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