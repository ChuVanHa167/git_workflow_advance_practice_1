# git_workflow_advance_practice_1
repo 1

## Giả sử dự án
Một công ty đang phát triển **website bán hàng online**.
Team gồm nhiều developer nên cần quy trình Git rõ ràng để:
* phát triển nhiều feature song song
* tích hợp code an toàn
* release phiên bản ổn định
* sửa lỗi production nhanh

Team quyết định sử dụng **Gitflow Workflow**.

# Branch trong dự án
## Main
Nhánh **production**
Chỉ chứa code đang chạy thật.

Nguyên tắc:
* Không commit trực tiếp
* Chỉ merge từ `release` hoặc `hotfix`

## Develop
Nhánh **tích hợp code của team**
Mọi feature sẽ merge vào đây.

## Feature
Phát triển tính năng mới.
Ví dụ:
feature/login
feature/cart
feature/payment

Quy tắc:
* Tách từ `develop`
* Merge lại `develop`
* Sau khi merge **xóa branch**

## Bugfix
Nếu tester phát hiện bug ở môi trường dev.

Quy tắc:
* Tách từ `develop`
* Fix bug
* Merge lại `develop`

## Release
Khi chuẩn bị phát hành.
Tách từ `develop`.

Chỉ được phép:
* fix bug nhỏ
* update version
  
Sau khi ổn định, merge vào:
* main
* develop

## Hotfix
Nếu production bị lỗi nghiêm trọng.
Tách từ `main`.

Fix xong merge vào:
* main
* develop
* release (nếu release đang tồn tại)

# Gitflow tổng thể
`Main → Dev → Feature → Dev → Bugfix → Dev → Release → Main`

Nếu production lỗi:
`Main → Hotfix → Main & Dev`

Nếu khách test release chưa ok:
`Release → Hotfix → Release`

# Mục tiêu repo
Thực hành:
* Gitflow đầy đủ
* Quy trình commit chuẩn
* Push code lên nhiều remote repo
  
# Cần nhớ:
_**hiện tại:**_

origin(tên mặc định) -> repo 1 (this repo)

github (tên tự đặt) -> repo 2(trên github)

_**Nhớ:**_

`git push origin main` push chỉ repo 1

`git push github main` push chỉ repo 2

`git remote -v` kiểm tra remote

`git remote set-url --add --push origin repo_2` nghĩa là:

```
origin
 ├── push → repo_1
 └── push → repo_2
```

`git remote show origin` xem push URLs của origin

`git remote set-url --delete --push origin <repo_url>` xóa push của repo khỏi origin

thêm remote 3 đặt tên repo3
```
git remote add repo3 https://github.com/ChuVanHa167/git_workflow_advance_practice_3.git
``` 

Cấu hình origin push nhiều url:
```
git remote set-url --add --push origin repo1_url
git remote set-url --add --push origin repo2_url
git remote set-url --add --push origin repo3_url
```
khi đó `git push origin main` sẽ push tới 3 repo cùng lúc

# Khi phát triển một tính năng:
- Bước 1: git chechout -b(chuyển và tạo nhánh mới)
- Bước 2: code(done)
- Bước 3: git status
- Bước 4: git diff(xem thay đổi chưa add của các file hiệ tại)
- Bước 5: git add file 1 file 2 file3(không add hết mà add từng file tránh add những file ẩn)
- Bước 6: git status
- Bước 7: git commit
- Bước 8: git pull(nếu k conflig thì ok nếu có conflig thì quay về bước 2)
- Bước 9: git push

# Lưu ý đặt tên:
Feature/*: * ở featue thể hiện một tính năng(vd: feature/login).

Release/v*: * ở release thể hiện phiên bản phát hành(vd: hiện tại là v1.2.0 thì release/v1.3.0)

Hotfix/v*: * ở hotfix thể hiện phiên bản sửa lỗi(v0.0.0 thì số thứ 3 thể hiện phiên bản của hotfix và số thứ 2 thể hiện release)


