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
Sau khi ổn định:
merge vào
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
Main → Dev → Feature → Dev → Bugfix → Dev → Release → Main
Nếu production lỗi:
Main → Hotfix → Main & Dev
Nếu khách test release chưa ok:
Release → Hotfix → Release

# Mục tiêu repo
Thực hành:
* Gitflow đầy đủ
* Quy trình commit chuẩn
* Push code lên nhiều remote repo
