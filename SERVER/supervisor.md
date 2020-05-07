# SUPERVISOR

control processes of Linux

create new configuration file in `/etc/supervisor/conf.d/SERVER.conf`

```
[program: Portfolio]
command=node /home/ubuntu/SERVER/Portfolio/Portfolio.js
directory=/home/ubuntu/SERVER/Portfolio
autostart=true
autorestart=true
stderr_logfile=/home/ubuntu/SERVER/log/Portfolio.err.log
stdout_logfile=/home/ubuntu/SERVER/log/Portfolio.out.log

[program: Vocabulary]
command=/home/ubuntu/SERVER/Vocabulary/Vocabulary
directory=/home/ubuntu/SERVER/Vocabulary
autostart=true
autorestart=true
stderr_logfile=/home/ubuntu/SERVER/log/Vocabulary.err.log
stdout_logfile=/home/ubuntu/SERVER/log/Vocabulary.out.log

[program: SongsBook]
command=/home/ubuntu/SERVER/SongsBook/SongsBook
directory=/home/ubuntu/SERVER/SongsBook
autostart=true
autorestart=true
stderr_logfile=/home/ubuntu/SERVER/log/SongsBook.err.log
stdout_logfile=/home/ubuntu/SERVER/log/SongsBook.out.log

[program: Climbing]
command=/home/ubuntu/SERVER/Climbing/Climbing
directory=/home/ubuntu/SERVER/Climbing
autostart=true
autorestart=true
stderr_logfile=/home/ubuntu/SERVER/log/Climbing.err.log
stdout_logfile=/home/ubuntu/SERVER/log/Climbing.out.log

[program: Code]
command=/home/ubuntu/SERVER/Code/Code
directory=/home/ubuntu/SERVER/Code
autostart=true
autorestart=true
stderr_logfile=/home/ubuntu/SERVER/log/Code.err.log
stdout_logfile=/home/ubuntu/SERVER/log/Code.out.log

[program: Vyznamne-stromy]
command=node /home/ubuntu/SERVER/Vyznamne-stromy/Vyznamne-stromy.js
directory=/home/ubuntu/SERVER/Vyznamne-stromy
autostart=true
autorestart=true
stderr_logfile=/home/ubuntu/SERVER/log/Vyznamne-stromy.err.log
stdout_logfile=/home/ubuntu/SERVER/log/Vyznamne-stromy.out.log

```

`sudo supervisorctl reread` to write changes
`sudo supervisorctl update` to star program being manage by supervisor
`sudo supervisorctl` tells me which programs are running
`sudo supervisorctl restart programName`
