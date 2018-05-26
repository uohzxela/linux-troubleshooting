# Linux Troubleshooting Guide

## Sluggish system

Determine system load average using `uptime`.

```
$ uptime
13:35:03 up 103 days, 8 min, 5 users, load average: 2.03, 20.17, 15.09
```

Diagnose load problems with `top`.
 
```
top - 14:08:25 up 38 days,  8:02,  1 user,  load average: 1.70, 1.77, 1.68
Tasks: 107 total,   3 running, 104 sleeping,   0 stopped,   0 zombie
Cpu(s): 11.4%us, 29.6%sy, 0.0%ni, 58.3%id,  .7%wa, 0.0%hi, 0.0%si, 0.0%st
Mem:   1024176k total,   997408k used,    26768k free,    85520k buffers
Swap:  1004052k total,     4360k used,   999692k free,   286040k cached

  PID USER      PR  NI  VIRT  RES  SHR S %CPU %MEM      TIME+  COMMAND
 9463 mysql     16   0  686m 111m 3328 S   53  5.5  569:17.64  mysqld
18749 nagios    16   0  140m 134m 1868 S   12  6.6    1345:01  nagios2db_status
24636 nagios    17   0 34660  10m  712 S    8  0.5    1195:15  nagios
22442 nagios    24   0  6048 2024 1452 S    8  0.1    0:00.04  check_time.pl
```

`us`: user CPU time

This is the percentage of CPU time spent running users’ processes that aren’t niced. (Nicing is a process that allows you to change its priority in relation to other processes.)

`sy`: system CPU time

This is the percentage of CPU time spent running the kernel and kernel processes.

`ni`: nice CPU time

If you have user processes that have been niced, this metric will tell you the percentage of CPU time spent running them.

`id`: CPU idle time

This is one of the metrics that you want to be high. It represents the percentage of CPU time that is spent idle. If you have a sluggish system but this number is high, you know the cause isn’t high CPU load.

`wa`: I/O wait

This number represents the percentage of CPU time that is spent waiting for I/O. It is a particularly valuable metric when you are tracking down the cause of a sluggish system, because if this value is low, you can pretty safely rule out disk or network I/O as the cause.

`hi`: hardware interrupts

This is the percentage of CPU time spent servicing hardware interrupts.

`si`: software interrupts

This is the percentage of CPU time spent servicing software interrupts.

`st`: steal time

If you are running virtual machines, this metric will tell you the percentage of CPU time that was stolen from you for other tasks.