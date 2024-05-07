

emlog is a lightweight blog and CMS system based on PHP and MYSQL.

Project address： https://github.com/emlog/emlog

### 

emlog pro 2.3.4 has RCE caused by the zip decompression function when installing plugins



#### Vulnerability description

Install plugins function corresponding source code in `admin/plugin.php`

![image-20240507170845622](https://img2023.cnblogs.com/blog/1964477/202405/1964477-20240507181636074-1756491618.png)



Call the emUnZip function to process the zip file. If it returns 0, the installation is successful

![image-20240507171014302](https://img2023.cnblogs.com/blog/1964477/202405/1964477-20240507181635701-982465048.png)



Following the emUnZip function, you can see that it uses PHP's ZipArchive class to extract files from the ZIP archive:

![image-20240507173641004](https://img2023.cnblogs.com/blog/1964477/202405/1964477-20240507181635294-2062170424.png)

The `getFromName()`method retrieves the contents of a file from the ZIP archive based on the file name. In this case, it retrieves the contents of a file named `$dir. $plugin_name. '.php'`.



The whole process is not filtered, as long as the folder in the compressed package and the file name in the folder can be uploaded successfully



#### Vulnerablility reproduction

First create a test folder containing the test.php file

![image-20240507174050237](https://img2023.cnblogs.com/blog/1964477/202405/1964477-20240507181634691-1207022381.png)

Then compress the test folder to test.zip

![image-20240507174135536](https://img2023.cnblogs.com/blog/1964477/202405/1964477-20240507181634286-462137551.png)

Set up the emlog2.3.3 environment and enter the background.

The vulnerability points are as follows:

![image-20240507174304366](https://img2023.cnblogs.com/blog/1964477/202405/1964477-20240507181633861-1342847102.png)

Click 'Install Plugin' and upload test.zip

![image-20240507174341387](https://img2023.cnblogs.com/blog/1964477/202405/1964477-20240507181633479-394569297.png)

The installation is successful:

![image-20240507174556574](https://img2023.cnblogs.com/blog/1964477/202405/1964477-20240507181633078-602507942.png)

Installation directory in ` content/plugins/test/test.php `

![image-20240507175425217](https://img2023.cnblogs.com/blog/1964477/202405/1964477-20240507181632322-1804594559.png)

Success



