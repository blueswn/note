## Laravel查看队列

    Route::any('/queues', function (){
    //    $keys = Redis::KEYS('*');
    Redis::SELECT(0);
    $list = Redis::LRANGE('queues:default', 0, 9);
    $len = Redis::LLEN('queues:default');

    $collection = new \Illuminate\Support\Collection();
    foreach ($list as $k => $item){
        //        if($k != count($ret2)) continue;
            $payload = json_decode($item, true);
            $payload['data']['command'] = unserialize($payload['data']['command']);
            $collection[] = $payload;
        }
        return response()->json([compact('len', 'collection')]);
    });
