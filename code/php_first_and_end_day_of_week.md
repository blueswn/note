## PHP根据周数获取周的第一天和最后一天

    <?php

    function first_and_end_day_of_week($week)
    {
        $thisWeek = date('W', time());
        $diffWeek = $week - $thisWeek;

        //本周的第一天和最后一天
        $date = new \DateTime();
        $date->modify("this week $diffWeek weeks");
        $firstDayOfWeek = $date->format('Y-m-d') . ' 00:00:00';
        $date->modify("this week +6 days");
        $endDayOfWeek = $date->format('Y-m-d') . ' 23:59:59';

        $result = [$firstDayOfWeek, $endDayOfWeek];

        return $result;
    }

    list(firstDayOfWeek, endDayOfWeek) = first_and_end_day_of_week(1);
