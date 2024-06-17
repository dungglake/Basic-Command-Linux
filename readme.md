# Hướng dẫn các lệnh cơ bản trên Linux

## Tìm kiếm file, directory

### Bằng tên hoặc bằng extension (ví dụ .jpg)
```bash
find /path/to/search -name "*.jpg"
find /path/to/search -type d -name "directory_name"
```

### Với giá trị -maxdepth, -mindepth
```bash
find /path/to/search -maxdepth 2 -name "*.jpg"
find /path/to/search -mindepth 1 -name "*.jpg"
```

### Với giá trị -mtime
```bash
find /path/to/search -mtime -7 -name "*.jpg"
```

## Xem dung lượng disk
```bash
df -h
```

## Kiểm tra phân vùng /
```bash
df -h /
```

## Kiểm tra phân vùng tmpfs
```bash
df -h | grep tmpfs
```

## Kiểm tra inodes
```bash
df -i
```

## Kiểm tra phân vùng LVM (physical volume, volume group, logical volume)
```bash
pvs
vgs
lvs
```

## Kiểm tra CPU
```bash
lscpu
```

### Kiểm tra CPU bằng top command
```bash
top
```

- **Load average:** Số lượng tiến trình đang đợi CPU.
- **us:** Thời gian CPU dùng cho user.
- **sy:** Thời gian CPU dùng cho hệ thống.
- **ni:** Thời gian CPU dùng cho các tiến trình có mức ưu tiên thay đổi.
- **id:** Thời gian CPU không hoạt động.
- **wa:** Thời gian CPU chờ đợi I/O.
- **hi:** Thời gian CPU xử lý gián đoạn phần cứng.
- **si:** Thời gian CPU xử lý gián đoạn phần mềm.
- **st:** Thời gian bị đánh cắp từ máy ảo.
- **Zombie process:** Tiến trình đã kết thúc nhưng chưa được giải phóng.
- **Sleeping process:** Tiến trình đang chờ sự kiện.

### Cài phần mềm stress và kiểm tra CPU load
```bash
sudo apt install stress
sudo stress --cpu 2 --timeout 120
top
```

- **Tại sao %cpu lại load được 200%:** Vì có 2 CPU ảo đang được sử dụng hoàn toàn.

## Kiểm tra RAM
```bash
free -h
```

### Giải thích RAM
- **used:** RAM đang được sử dụng.
- **free:** RAM còn trống.
- **shared:** RAM dùng cho các filesystem.
- **buff/cache:** RAM dùng cho bộ nhớ đệm.
- **available:** RAM có sẵn để sử dụng.
- Để kiểm tra dung lượng RAM còn trống trên hệ thống Linux bằng lệnh free, ta cần chú ý đến cột "available".

## Quản lý tiến trình

### Show một tiến trình bất kì
```bash
ps aux | grep [process_name]
```

### Kill Process
Các cách cơ bản để kill một process trong Linux gồm:

1. **Kill bằng PID (Process ID)**:
   ```sh
   kill <PID>
   ```

2. **Kill với tín hiệu cụ thể**:
   ```sh
   kill -9 <PID>
   ```

3. **Kill bằng tên process**:
   ```sh
   pkill <tên_process>
   ```

4. **Kill tất cả các process của một user cụ thể**:
   ```sh
   killall <tên_user>
   ```

## Liệt kê danh sách file/thư mục
```bash
ls -al
```

### Show các file ẩn
```bash
ls -a
```

## Tìm kiếm, copy, di chuyển file/thư mục
```bash
find /path/to/search -name "file_name"
cp /path/to/source /path/to/destination
mv /path/to/source /path/to/destination
```

## Phân quyền thư mục, file
```bash
chmod 755 file_name
chown user:group file_name
chattr +i file_name
```

## Sử dụng trình editor

### Vim
- **Insert:** Nhấn `i`
- **Lưu và thoát:** Nhấn `Esc`, gõ `:wq`, rồi nhấn `Enter`
- **Thoát không lưu:** Nhấn `Esc`, gõ `:q!`, rồi nhấn `Enter`

### Nano
- **Insert:** Chỉ cần bắt đầu gõ
- **Lưu:** Nhấn `Ctrl+O`
- **Thoát:** Nhấn `Ctrl+X`

## Mount/Umount một phân vùng

### Mount
```bash
sudo mount /dev/sdb1 /mnt/test
```

### Umount
```bash
sudo umount /mnt/test
```

## Symbolic Links, Hard Links

### Symbolic Links
```bash
ln -s /path/to/original /path/to/link
```

### Hard Links
```bash
ln /path/to/original /path/to/link
```

## Nén, giải nén

### Nén/Giải nén file tar.gz
```bash
tar -czvf archive.tar.gz /path/to/folder
tar -xzvf archive.tar.gz
```

### Nén/Giải nén file .zip
```bash
zip -r archive.zip /path/to/folder
unzip archive.zip
```

## Các lệnh cơ bản

### Telnet
```bash
telnet [hostname] [port]
```

### Ping
```bash
ping [hostname or IP]
```

### Hping3
```bash
hping3 -S [hostname] -p [port]
```

### SSH
```bash
ssh user@hostname
ssh -p [custom_port] user@hostname
ssh -i /path/to/key user@hostname
```

### SCP
```bash
scp /path/to/local/file user@hostname:/path/to/remote/file
scp -r /path/to/local/folder user@hostname:/path/to/remote/folder
```

### Rsync
```bash
rsync -av /path/to/source /path/to/destination
rsync -av --progress /path/to/source /path/to/destination
```

## Xem nhanh nội dung file

### Chèn text vào cuối file
```bash
echo "text" >> file_name
```

### Show 2 dòng đầu file
```bash
head -n 2 file_name
```

### Show 2 dòng cuối file
```bash
tail -n 2 file_name
```

### Dùng sed để find and replace
```bash
sed -i 's/old_string/new_string/g' file_name
```

### Netstat
```bash
netstat -tuln
```

### Print
```bash
lp file_name
```

### Sort, Uniq, Wc, Cut, Join
```bash
sort file_name
uniq file_name
wc file_name
cut -d 'delimiter' -f [field_number] file_name
join file1 file2
```

## Standard Input, Output, Error

### Redirect error to a file
```bash
command 2> error_file
```

### Redirect output to a file
```bash
command > output_file
```

### Redirect error and output to a file
```bash
command > all_output_file 2>&1
```
```

### Symlink và Hardlink
Symlink (Symbolic Link):
- Là một file đặc biệt chứa đường dẫn tới file gốc.
- Khi symlink bị xóa, file gốc không bị ảnh hưởng.
- Sử dụng khi muốn tạo shortcut tới file hoặc thư mục ở một vị trí khác.
  
Hardlink:
- Là một liên kết trực tiếp đến dữ liệu của file gốc trên ổ đĩa.
- Khi hardlink bị xóa, file gốc và các hardlink khác vẫn tồn tại.
- Sử dụng khi muốn có nhiều tên file trỏ đến cùng một dữ liệu để tiết kiệm không gian.

Khi nào sử dụng:
- Symlink: Khi cần shortcut hoặc cần liên kết tới file/thư mục trên phân vùng khác.
- Hardlink: Khi cần tiết kiệm không gian hoặc tạo nhiều đường dẫn đến cùng dữ liệu trong cùng một phân vùng.

### SCP và Rsync
SCP (Secure Copy):
- Dùng để sao chép file giữa hai hệ thống qua SSH.
- Không có khả năng đồng bộ hóa dữ liệu.
- Cú pháp đơn giản hơn:
  ```sh
  scp source_file user@remote_host:/path/to/destination
  ```

Rsync:
- Dùng để sao chép và đồng bộ hóa file/directory.
- Chỉ sao chép những phần thay đổi, tiết kiệm băng thông.
- Có thể làm việc qua SSH:
  ```sh
  rsync -avz source_file user@remote_host:/path/to/destination
  ```

### Traceroute
Để trace route từ máy remote đến IP 103.200.22.11 và nêu ra các hop, dùng lệnh sau:

```sh
traceroute 103.200.22.11
```
dung@dung-Inspiron-15-3530:~/Desktop$ traceroute 103.200.22.11
traceroute to 103.200.22.11 (103.200.22.11), 30 hops max, 60 byte packets
 1  192.168.0.1 (192.168.0.1)  11.470 ms  11.968 ms  12.952 ms
 2  localhost (27.71.251.149)  24.651 ms  24.642 ms  24.633 ms
 3  10.255.39.241 (10.255.39.241)  24.625 ms 10.255.39.243 (10.255.39.243)  24.612 ms 10.255.39.247 (10.255.39.247)  24.603 ms
 4  * * *
 5  localhost (27.68.236.34)  24.611 ms localhost (27.68.236.242)  24.600 ms  24.542 ms
 6  203.113.187.98 (203.113.187.98)  24.531 ms  13.279 ms  18.542 ms
 7  static.vnpt.vn (113.171.45.66)  19.161 ms *  22.269 ms
 8  static.vnpt.vn (113.171.46.226)  21.584 ms  23.344 ms  20.691 ms
 9  172.16.34.38 (172.16.34.38)  21.034 ms static.vnpt.vn (113.171.49.86)  20.249 ms 172.16.34.46 (172.16.34.46)  23.780 ms
10  172.16.34.38 (172.16.34.38)  26.607 ms  27.008 ms 172.16.34.46 (172.16.34.46)  24.114 ms
11  103.200.22.11 (103.200.22.11)  22.432 ms  22.434 ms  24.600 ms
