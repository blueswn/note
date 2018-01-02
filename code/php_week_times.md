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

        $thisWeek = date('W', time());
        $diffWeek = $week - $thisWeek;
        $diffYear = $year - date('Y', time());

        $date = new \DateTime();
        $date->modify("this year $diffYear years");
        $date->modify("this week $diffWeek weeks");
        $startDate = $date->format('Y-m-d').' 00:00:00';
        $date->modify("this week +6 days");
        $endDate = $date->format('Y-m-d').' 23:59:59';

        $weekTimes['start_time'] = strtotime($startDate);
        $weekTimes['end_time'] = strtotime($endDate);
        $weekTimes['start_date'] = $startDate;
        $weekTimes['end_date'] = $endDate;
        $weekTimes['week'] = $week;
        $weekTimes['year'] = $year;

        return $weekTimes;
    }
