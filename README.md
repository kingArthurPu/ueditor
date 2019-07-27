# 修改

1. `Uploader.class.php`文件中，原代码：

    ```PHP
        $this->stateMap['ERROR_TYPE_NOT_ALLOWED'] = iconv('unicode', 'utf-8', $this->stateMap['ERROR_TYPE_NOT_ALLOWED']);
    ```
    修改后：

    ```php
        // todo 修改编码的转换方式，避免因没有检测到编码类型强制转换的错误
        $encoding = mb_detect_encoding($this->stateMap['ERROR_TYPE_NOT_ALLOWED'],["unicode","ASCII",'utf-8',"GB2312","GBK",'BIG5']);
        $this->stateMap['ERROR_TYPE_NOT_ALLOWED'] = iconv($encoding, 'utf-8', $this->stateMap['ERROR_TYPE_NOT_ALLOWED']);
    ```

2. `Uploader.class.php`文件中，原代码：

    ```php
        //替换随机字符串
        $randNum = rand(1, 10000000000) . rand(1, 10000000000);
    ```

    修改后：

    ```php
        //替换随机字符串
        // todo 修改最大整数值的获取，避免超出范围
        $randNum = rand(1, PHP_INT_MAX) . rand(1, PHP_INT_MAX);
    ```