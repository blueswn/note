## Supervisor

### 命令

    supervisorctl help

### 配置`vim /etc/supervisord.conf`

    [program:queue_order]
    process_name=%(program_name)s_%(process_num)02d
    command=php /sitepath/artisan queue:work --queue=order --sleep=3 --tries=3
    directory = /sitepath/
    autostart=true
    autorestart=true
    user=www
    numprocs=1
    stdout_logfile_maxbytes = 1MB
    log_stdout=true             ; if true, log program stdout (default true)
    log_stderr=true             ; if true, log program stderr (def false)
    logfile = /mnt/logs/v4queue_order.log
    startsecs=5               ; number of secs prog must stay running (def. 10)
    startretries=500             ; max # of serial start failures (default 3)
