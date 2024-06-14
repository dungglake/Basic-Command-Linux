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

### Kill một tiến trình
```bash
kill [PID]
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

### Traceroute
```bash
traceroute 103.200.22.11
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

