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
                'mulit_key1'=>'desc',
                'mulit_key2'=>'desc',
                'mulit_key3'=>'asc'
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
