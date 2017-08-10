## 根据月份获取周和周的起始结束日期列表

  function getWeeksOfMonth($month){
     $month = request()->input('month');
      if(empty($month)){
          $month = date('m');
      }

      $firstDayOfMonth = date('Y-'.$month.'-01 00:00:00');

      $date = $firstDayOfMonth;

      $firstAndEndDayOfWeekByDate = function ($date) {
          $checkDate = function ($date) {
              return $date == date('Y-m-d H:i:s', strtotime($date)) ? 1 : 0;
          };
          if (strlen($date) == 19 && $checkDate($date)) {

          } elseif (strlen($date) == 10 && $checkDate($date . ' 00:00:00')) {
              $date = $date . ' 00:00:00';
          } else {

          }

          $theWeek = date('W', strtotime($date));
          $thisWeek = date('W', time());
          $diffWeek = $theWeek - $thisWeek;

          $date = new \DateTime();
          $date->modify("this week $diffWeek weeks");
          $firstDayOfWeek = $date->format('Y-m-d') . ' 00:00:00';
          $date->modify("this week +6 days");
          $endDayOfWeek = $date->format('Y-m-d') . ' 23:59:59';

          return [$firstDayOfWeek, $endDayOfWeek, $theWeek];
      };

      $arr = [];
      $time = strtotime($date);
      $daysTheMonth = date('t', $time);
      $endDayOfMonth = date('Y-m-'.$daysTheMonth.' 00:00:00', $time);
      while (true){
          list($firstDayOfWeek, $endDayOfWeek, $week) = $firstAndEndDayOfWeekByDate($date);
          if($firstDayOfWeek > $endDayOfMonth){
              break;
          }
          $arr[] = [
              'first_day' => $firstDayOfWeek,
              'end_day' => $endDayOfWeek,
              'week' => $week
          ];
          $date = date('Y-m-d H:i:s',strtotime($endDayOfWeek) + 1);
      }

      dd($arr);
  }
