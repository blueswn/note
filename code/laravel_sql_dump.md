
DB::connection()->enableQueryLog(); // 打开query log
\DB::listen(function ($sql) {
            $i = 0;
            $bindings = $sql->bindings;
            $rawSql = preg_replace_callback('/\?/', function ($matches) use ($bindings, &$i) {
                $item = isset($bindings[$i]) ? $bindings[$i] : $matches[0];
                $i++;
                return gettype($item) == 'string' ? "'$item'" : $item;
            }, $sql->sql);
            echo $rawSql, "\n<br /><br />\n";
        });




        创建监听器

        php artisan make:listener QueryListener --event=Illuminate\Database\\Events\\QueryExecuted
        打开 app/ProvidersEventServiceProvider.PHP ，在$listen中添加
        protected $listen = [
            'Illuminate\Database\Events\QueryExecuted' => [
                'App\Listeners\QueryListener,
            ]
        ];
        #头部添加
        use App\Listeners\QueryListener;
        打开QueryListener文件
        public function handle (QueryExecuted $event)
        {
            if (env('APP_ENV', 'production') == 'local') {
                $sql = str_replace("?", "'%s'", $event->sql);
                $log = vsprintf($sql, $event->bindings);
                Log::info($log);
            }
        }
