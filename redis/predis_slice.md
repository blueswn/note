#

## Hashes

    Redis::SELECT(0);
    $key = 'hash_key';
    // 删除
    $hFields = Redis::HKEYS($key);
    foreach ($hFields as $hField){
        Redis::HDEL($key, $hField);
    }

    $field = 'hash_field_1';
    $value_str = json_encode(['name'=>'1', 'id'=>1]);
    //Redis::HDEL($key, $field);
    Redis::HSET($key, $field, $value_str);

## Sorted Sets

    $key = 'sorted_sets_1';
    foreach ($members as $member) {
        $tmpScore = Redis::ZSCORE($key, $member);
        if (is_null($tmpScore)) {
            Redis::ZADD($key, 'nx', 'ch', 'incr', $score, $member);
        } else {
            Redis::ZINCRBY($key, $score, $member);
        }
    }

    Redis::ZREVRANGEBYSCORE($key, '+inf', '-inf', 'WITHSCORES');
