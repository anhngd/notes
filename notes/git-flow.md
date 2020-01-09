## Quy ước
- Các loại repo khi làm việc:
    - Central Repo: Repo chính của dự án (do leader quản lý)
    - Forked Repo: Repo của mỗi thành viên trong nhóm dự án khi đã fork về tài khoản cá nhân.
    - Local Repo: Repo khi làm việc trên máy cá nhân.
- Phân loại issue chính:
    - feature: Tính năng mới
    - bug: Báo lỗi
    - enhancement: Cải thiện tính năng

## Quy tắc khi làm việc nhóm
* Mỗi pull-request tương ứng với một issue, không giới hạn số commit trong 1 pull-request
* Tiêu đề của pull-request phải đặt sao cho tương ứng với title của task với format `refs [Loại issue] #[Số issue] [Nội dung issue]` （Ví dụ: `refs bug #8888 Sửa lỗi cache`).
* Đối với commit, trong trường hợp pull-request đó chỉ có 1 commit thì có thể đặt tiêu đề commit tương tự như trên là `refs [Loại issue] #[Số issue] [Nội dung issue]` （Ví dụ: `refs bug #8888 Sửa lỗi cache`）.\
  Tuy nhiên với trường hợp 1 pull-request có chứa nhiều commit thì cần phải ghi rõ trong nội dung Tiêu đề commit là trong commit đó xử lý đối ứng vấn đề gì.
    * Ví dụ:
        1. Tiêu đề Pull-request: `refs bug #8888 Sửa lỗi cache`
        2. Trong trường hợp pull-request có 2 commit thì nội dung tiêu đề commit của 2 commit sẽ tương ứng như sau
            * `Tạo method thực hiện việc clear cache trong Model`
            * `Tại controller gọi method ở Model để thực hiện việc clear cache`
* Tại Local Repo (trên máy lập trình viên), **tuyệt đối không được thay đổi** code tại nhánh ```master```. Tất cả mọi thay đổi thực hiện trên nhánh riêng.

## Quy trình làm việc

1. Trên git server (Github, gitlab,...), fork Central Repo về tài khoản của cá nhân (được gọi là Forked Repo.

2. Clone (tạo bản sao) Forked Repo lên môi trường local. Tại thời điểm này, Forked Repository sẽ được tự động đăng ký dưới tên là `origin`.
    ```bash
    $ git clone [URL của Forked Repo]
    ```

3. Truy cập vào thư mục đã được tạo ra sau khi clone, đăng ký Central Repo dưới tên `upstream`.
    ```bash
    $ cd [thư mục được tạo ra]
    $ git remote add upstream [URL của Central Repo]
    ```

## Các thao tác xử lý trên kho mã nguồn

**Chú ý:** Central Repo và Forked Repo sẽ được gọi tương ứng là `upstream` và `origin`.

1. Đồng bộ hóa nhánh master tại local với upstream.
    ```bash
    $ git checkout master
    $ git pull upstream master
    ```

2. Tạo nhánh để làm task từ branch master ở local. Tên branch là số issue của task（Ví dụ: `task/1234`）.
    ```bash
    $ git checkout master
    $ git checkout -b task/1234
    ```

3. Tiến hành làm task（Có thể commit bao nhiêu tùy ý.

4. Push code lên origin.

    ```bash
    $ git push origin task/1234
    ```

5. Tại origin trên git server, từ nhánh `task/1234` đã được push lên hãy gửi pull-request đối với branch `master` của `upstream`.
   
6. Quay trở lại 1.

### Xử lý conflict xảy ra trong quá trình rebase

Khi xảy ra conflict trong quá trình rebase, sẽ có hiển thị như dưới đây (tại thời điểm này sẽ bị tự động chuyển về một branch vô danh)
```bash
$ git rebase master
First, rewinding head to replay your work on top of it...
Applying: refs #1234 Sửa lỗi cache
Using index info to reconstruct a base tree...
Falling back to patching base and 3-way merge...
Auto-merging path/to/conflicting/file
CONFLICT (add/add): Merge conflict in path/to/conflicting/file
Failed to merge in the changes.
Patch failed at 0001 refs #1234 Sửa lỗi cache
The copy of the patch that failed is found in:
    /path/to/working/dir/.git/rebase-apply/patch

When you have resolved this problem, run "git rebase --continue".
If you prefer to skip this patch, run "git rebase --skip" instead.
To check out the original branch and stop rebasing, run "git rebase --abort".
```

1. Hãy thực hiện fix lỗi conflict thủ công（những phần được bao bởi <<< và >>> ）.
Trong trường hợp muốn dừng việc rebase lại, hãy dùng lệnh `git rebase --abort`.

2. Khi đã giải quyết được tất cả các conflict, tiếp tục thực hiện việc rebase bằng:

    ```bash
    $ git add .
    $ git rebase --continue
    ```

### Một số câu lệnh git hay dùng

#### Xóa một nhánh

```
git branch -d [Tên branch]
```
