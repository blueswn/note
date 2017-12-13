## PHP根据周数获取周的第一天和最后一天

    <?php

    function week_times($week, $year = null)
    {
        $week = (string)$week;
        if (is_null($year)) {
            $year = date('Y', time());
        } else {
            $year = (string)$year;
        }

        $time = strtotime($year . 'W' . $week);
        $weekTimes['start_time'] = $time;
        $weekTimes['end_time'] = $time + 7*24*60*60 - 1;
        $weekTimes['start_date'] = date('Y-m-d 00:00:00', $weekTimes['start_time']);
        $weekTimes['end_date'] = date('Y-m-d 23:59:59', $weekTimes['end_time']);
        $weekTimes['week'] = $week;
        $weekTimes['year'] = $year;

        return $weekTimes;
    }
