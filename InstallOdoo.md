
## HƯỚNG DẪN CÀI ĐẶT MÔI TRƯỜNG PHÁT TRIỂN ODOO (WINDOWS)

I.	Download các phần mềm cần thiết

1.	[Download Odoo 15: | Odoo bản Community](https://nightly.odoo.com/15.0/nightly/exe/)( Nếu nghịch addons)

2.	[Download Visual Code](https://code.visualstudio.com/download)

    - Add command to Environment Variable

    ```bash
        C:\Users\Admin\AppData\Local\Programs\Microsoft VS Code\bin
    ```

3.	Hoặc [Download Pycharm](https://www.jetbrains.com/pycharm/download/?section=windows)

4.	[Download Python 3.10.0](https://www.python.org/ftp/python/3.10.0/python-3.10.0-amd64.exe)

    - Add command to Environment Variable

    ```bash
        C:\Users\Admin\AppData\Local\Programs\Python\Python310\Scripts\
        C:\Users\Admin\AppData\Local\Programs\Python\Python310\
    ```

5.	[Download pgAdmin](https://www.pgadmin.org/download/pgadmin-4-windows/)

    - Add command to Environment Variable

    ```bash
        C:\Program Files\PostgreSQL\15\bin
    ```

    - Create a new PostgreSQL user with a password by following these steps:
    - Open pgAdmin.
    - Double-click the server to establish a connection.
    - Select Object ‣ Create ‣ Login/Group Role.
    - Enter the desired username in the Role Name field (db_user = odoo).
    - Go to the Definition tab and input the password (db_password = odoo), then click Save.
    - Navigate to the Privileges tab and set Can login? and Create database? to Yes. Adding these privileges makes the database user, equivalent to the administrator.
    - These steps will allow you to create a new PostgreSQL user with the necessary privileges to use Odoo.
  
    - Note: Database restore error: Go to File-> Preferences-> Paths->Binary paths
                                    Change PostgreSQL Binary Path to "C:\Program Files\PostgreSQL\15\bin"

6.	[Download Git](https://github.com/git-for-windows/git/releases/download/v2.43.0.windows.1/Git-2.43.0-64-bit.exe)

7.  Hoặc dùng [Download Git Desktop](https://central.github.com/deployments/desktop/desktop/latest/win32)

    - Add command to Environment Variable

    ```bash
        C:\Users\Admin\AppData\Local\GitHubDesktop\bin
    ```

8.  [Download Build Tools for Visual Studio](https://aka.ms/vs/17/release/vs_BuildTools.exe)

    - Choose C++ build tools and install

9.  [Download Wkhtmltox](https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6-1/wkhtmltox-0.12.6-1.msvc2015-win64.exe)(Trong trường hợp lỗi in file PDF, Excel,...)

    - Add command to Environment Variable

    ```bash
        C:\Program Files\wkhtmltopdf\bin
    ```

II. Cài đặt Odoo 15(Nếu nghịch addons)

III. Cài đặt các ứng dụng đã tải ở trên

1.  Cấu hình VSCode với Python

    Cài đặt các extension sau:

    ![Extension](/image/1.png)

    [Plugin Odoo](https://marketplace.visualstudio.com/items?itemName=trinhanhngoc.vscode-odoo)

2.  Nếu cấu hình với Pycharm thì xem [ở đây](https://www.youtube.com/playlist?list=PLqRRLx0cl0hoZM788LH5M8q7KhiXPyuVU)


IV. Clone code về máy(Chắc không cần phải hướng dẫn đâu nhỉ)

![Clone Project](/image/3.png)

```bash
    # Clone trên command

    git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY
```

V. Debug với Python

1.  Cài đặt các gói Python cho Odoo

    * Mở project: New -> Open Folder -> đến thư mục code -> Select Folder

        ![Select Folder](/image/2.png)

    * Mở terminal VSCode

        ```bash
        # Gõ lệnh sau

            pip3 install --upgrade pip
        ```

        ![Run](/image/4.png)

        ```bash
        # Chạy requirements.txt

            pip3 install -r requirements.txt
        ```

        ![Run](/image/5.png)

    * Chú ý: Sẽ có vài lỗi phát sinh khi cài gói do không phù hợp version. Giải pháp comment lại gói trong file requirement.txt cài tay trên terminal.

    * Cũng có thể dùng môi trường ảo trên command

        ```bash
            cd Odoo
            python -m venv python3.10
            python3.10\Scripts\activate
            pip install setuptools wheel
            pip install -r requirements.txt
            deactivate // out
        ```

        Và vào Select Interpreter và chọn python3.10(Nếu chưa có thì -> Enter interpreter path -> file python.exe trong python3.10)

        ![Run](/image/7.png)

2.  Cấu hình debug cho VSCode

    * Vào Run -> Add Configuration -> nhập nội dung sau

        ![Add Configuration](/image/6.png)

        ```json
            {
                "version": "0.2.0",
                "configurations": [
                    {
                        "name": "Python: Odoo15",
                        "type": "python",
                        "request": "launch",
                        "stopOnEntry": false,
                        "python": "python.exe",
                        "console": "integratedTerminal",
                        "program": "${workspaceRoot}\\odoo-bin",
                        "args":[
                            "--config=${workspaceRoot}\\odoo.conf"
                        ],
                        "cwd": "${workspaceFolder}",
                        "env": {},
                        "envFile": "${workspaceFolder}/.env",
                        "debugOptions":[
                            "RedirectOutput"
                        ]
                    }
                ]
            }

        ```

3.	Tạo file odoo.conf

    * Nội dung

        ```conf
            [options]
            ; This is the password that allows database operations:
            admin_passwd = odoo15
            db_host = localhost
            db_port = 5432
            db_user = odoo
            db_name = odoo_dev
            db_password = odoo
            xmlrpc_port = 8069
            list_db = True
            addons_path = D:\Odoo_15\addons,D:\Odoo_15\custom-addons
            pg_path = C:\Program Files\PostgreSQL\15\bin
        ```

4.  Run debug

    * Nhấn F5 và run url trên trình duyệt [http://localhost:8069/](http://localhost:8069/)
