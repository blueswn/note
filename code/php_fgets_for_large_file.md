

    <? PHP

    $results = [];
    try {
      $path = 'test.csv';
      $file_handler = fopen($path, 'r');//以可读方式打开文件
      while (1) {
          $con = fgets($file_handler);
          if (feof($file_handler)) {
              break;
          }

          try{
              list($v1, $v2, $3) = explode(',', $con);
          }catch (\Exception $e) {
              continue;
          }

          echo $con.PHP_EOL;
      }
      fclose($file_handler);
      return $results;
  }catch (\Exception $e){
      Log::error($e);
      return null;
  }
