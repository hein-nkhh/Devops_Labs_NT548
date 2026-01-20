**Bước 1: Đi vào thư mục terraform**

cd terraform

**Bước 2: Thực hiện các lệnh terraform**

terraform init

terraform plan

terraform apply -auto-approve

**Bước 3: Thiết lập quyền cho key pem để có thể sử dụng key để SSH vào Public EC2 bằng icals** 

icacls.exe my-aws-key.pem /reset

icacls.exe my-aws-key.pem /grant:r "$($env:username):R"

icacls.exe my-aws-key.pem /inheritance:r

**Bước 4: Check tài nguyên trên AWS Console và thực hiện các test case theo report**

| ID | Tên Kiểm Thử | Lệnh Thực Hiện | Kết Quả Mong Đợi |
|:---:|:---|:---|:---|
| **TC-01** | **SSH Public** | `ssh -i my-aws-key.pem ec2-user@<Public_IP>` | Login thành công vào máy Public EC2 (Bastion Host). |
| **TC-02** | **SSH Private** | `ssh -i my-aws-key.pem ec2-user@<Private_IP>` | SSH từ máy Public sang máy Private qua IP nội bộ thành công. |
| **TC-03** | **NAT Gateway** | `ping -c 4 google.com` | Máy Private nhận được tín hiệu phản hồi từ Internet. |
| **TC-04** | **Security** | `ssh -i my-aws-key.pem ec2-user@<Private_IP>` | Kết nối trực tiếp từ máy cá nhân vào máy Private bị chặn (Timeout). |

---
