## 多维数组多字段排序

    <?php

    class example
    {
        public index()
        {
            usort($mulit, [$this, 'multi_compare']);
        }

        protected function multi_compare($a, $b)
        {
            $criteria = array(
                'week_learn_count'=>'desc',
                'week_total_stars'=>'desc',
                'en_name'=>'asc'
            );
            foreach($criteria as $what => $order){
                if($a[$what] == $b[$what]){
                    continue;
                }
                return (($order == 'desc')?-1:1) * (($a[$what] < $b[$what]) ? -1 : 1);
            }
            return 0;
        }
    }
