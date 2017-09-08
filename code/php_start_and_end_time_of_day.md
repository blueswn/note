$getTimeInterval = function ($day){
            return [
                strtotime(date('Y-m-d 00:00:00', strtotime($day.' day'))),
                strtotime(date('Y-m-d 23:59:59', strtotime($day.' day'))),
            ];
        };
