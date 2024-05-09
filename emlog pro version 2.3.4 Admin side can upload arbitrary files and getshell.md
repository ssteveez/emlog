# emlog pro version 2.3.4 Admin side can upload arbitrary files and getshell

emlog is a lightweight blog and CMS system based on PHP and MYSQL.

Project address： https://github.com/emlog/emlog



The background management terminal can change the type of the file to be uploaded

![image-20240508162334706](https://img2023.cnblogs.com/blog/1964477/202405/1964477-20240509155924482-2021638096.png)

The corresponding source code location is `admin/setting.php`

![image-20240508162425453](https://img2023.cnblogs.com/blog/1964477/202405/1964477-20240509155924056-573358377.png)

There is a filter, and when the modified type contains php, it is replaced with an x, which means that uploading files of PHP-related types is not allowed.



However, you can bypass this by adding a `phtml` type

![image-20240508163159115](https://img2023.cnblogs.com/blog/1964477/202405/1964477-20240509155923602-759351071.png)

Add `phtml` type, then find an upload point, upload `.phtml` suffix php file:

![image-20240508162813853](https://img2023.cnblogs.com/blog/1964477/202405/1964477-20240509155923196-745675628.png)

The upload interface in the `admin/media.php` location is used here

![image-20240508171119501](https://img2023.cnblogs.com/blog/1964477/202405/1964477-20240509155922808-1062959260.png)

success

![image-20240508171145514](https://img2023.cnblogs.com/blog/1964477/202405/1964477-20240509155922464-18148902.png)

access this file:

![image-20240508174717740](https://img2023.cnblogs.com/blog/1964477/202405/1964477-20240509155921997-662543300.png)

The php script was successfully executed

