# python-torch cho Termux ARM64

Gói PyTorch biên dịch riêng cho **Termux trên Android ARM64 (`aarch64`)**.
Bản build cá nhân do [@khocvidau9x](https://github.com/khocvidau9x) duy trì;
đây không phải repository chính thức của PyTorch.
GitHub không hỗ trợ tắt fork cho repository công khai thuộc tài khoản cá nhân;
giấy phép BSD 3-Clause cũng cho phép phân phối lại theo các điều khoản của nó.

## Thông tin gói

- Tên gói: `python-torch`
- Phiên bản: `2.14.1-3`
- Kiến trúc: `aarch64`
- Python: `3.14`
- Tăng tốc: CPU; bản build này tắt CUDA (`USE_CUDA=OFF`)
- Vulkan: bật trong cấu hình build; khả năng sử dụng phụ thuộc thiết bị và driver
- Tệp cài đặt: `python-torch_2.14.1-3_aarch64.deb`

Đây là gói `.deb` dành riêng cho Termux, không phải wheel dùng chung cho Linux
hoặc Android khác. Không cài trên máy `x86_64`, môi trường Pydroid, hay Python
không phải Python của Termux.

## Cài đặt trong Termux

1. Cập nhật gói Termux:

   ```sh
   pkg update
   pkg upgrade
   ```

2. Đảm bảo các phụ thuộc runtime có trong kho Termux. APT thường tự cài chúng
   khi cài gói `.deb`; có thể cài trước bằng lệnh:

   ```sh
   pkg install abseil-cpp libandroid-execinfo libc++ libopenblas \
     libprotobuf python python-numpy python-pip
   ```

3. Tải tệp `.deb` từ mục **Releases** của dự án vào thư mục Termux, sau đó cài
   bằng APT để APT xử lý phụ thuộc:

   ```sh
   cd "$HOME"
   apt install ./python-torch_2.14.1-3_aarch64.deb
   ```

   Nếu tải tệp về bộ nhớ dùng chung của Android, hãy chép nó vào `$HOME` trước:

   ```sh
   cp /sdcard/Download/python-torch_2.14.1-3_aarch64.deb "$HOME/"
   apt install "$HOME/python-torch_2.14.1-3_aarch64.deb"
   ```

Không dùng `pip install torch` để thay thế gói này. Không dùng `dpkg -i` nếu
các phụ thuộc chưa được cài; `apt install ./tệp.deb` phù hợp hơn vì có thể
giải quyết phụ thuộc từ kho Termux.

## Kiểm tra sau khi cài

```sh
python -c 'import torch; x = torch.tensor([1, 2, 3]); print(torch.__version__); print((x * 2).tolist())'
```

Kết quả mong đợi gồm phiên bản `2.14.1` và `[2, 4, 6]`.

## Phát hành dự án trên GitHub

Dự án cá nhân: <https://github.com/khocvidau9x/python-torch>. Tệp `.deb`
cũng được đính kèm trong GitHub Release có tag `v2.14.1-3`.

Trước khi cài, người dùng có thể kiểm tra tính toàn vẹn của tệp:

```sh
sha256sum -c SHA256SUMS
```

## Giấy phép

PyTorch được phân phối theo BSD 3-Clause. Xem tệp [`LICENSE`](LICENSE).
