# 3. Find the first process in the system by looking at its process ID (PID) 

OK. So basically, List all running processes and inspect their process IDs (PIDs):

> The BROKEN ENGLISH question states "Find the first process in the system by looking at its process ID (PID). But then continues with a disussion point that was clearly written by someone with english as there third language.
>
> - Which ones were stated first? WTF?
> - Which ones were started some time ago? Ruh?
> - Which ones were started recently? Huh?
>
>
> In addition. The terminal command (Hint) provided is not enought to answer the question properly.

```bash
ps -ef | more
```

Using the `ps -ef | more` command, you should see output similar to the following:
```zsh
┌──(kali㉿kali)-[~]
└─$ ps -ef | more    
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 Jan18 ?        00:00:01 /sbin/init splash
root           2       0  0 Jan18 ?        00:00:00 [kthreadd]
root           3       2  0 Jan18 ?        00:00:00 [pool_workqueue_release]
root           4       2  0 Jan18 ?        00:00:00 [kworker/R-rcu_gp]
root           5       2  0 Jan18 ?        00:00:00 [kworker/R-sync_wq]
root           6       2  0 Jan18 ?        00:00:00 [kworker/R-kvfree_rcu_reclaim]
root           7       2  0 Jan18 ?        00:00:00 [kworker/R-slub_flushwq]
root           8       2  0 Jan18 ?        00:00:00 [kworker/R-netns]
root          12       2  0 Jan18 ?        00:00:00 [kworker/u8:0-ipv6_addrconf]
root          13       2  0 Jan18 ?        00:00:00 [kworker/R-mm_percpu_wq]
root          14       2  0 Jan18 ?        00:00:00 [ksoftirqd/0]
root          15       2  0 Jan18 ?        00:00:02 [rcu_preempt]
root          16       2  0 Jan18 ?        00:00:00 [rcu_exp_par_gp_kthread_worker/0]
root          17       2  0 Jan18 ?        00:00:00 [rcu_exp_gp_kthread_worker]
root          18       2  0 Jan18 ?        00:00:00 [migration/0]
root          19       2  0 Jan18 ?        00:00:00 [idle_inject/0]
root          20       2  0 Jan18 ?        00:00:00 [cpuhp/0]
root          21       2  0 Jan18 ?        00:00:00 [cpuhp/1]
root          22       2  0 Jan18 ?        00:00:00 [idle_inject/1]
root          23       2  0 Jan18 ?        00:00:00 [migration/1]
root          24       2  0 Jan18 ?        00:00:01 [ksoftirqd/1]
root          26       2  0 Jan18 ?        00:00:00 [kworker/1:0H-events_highpri]
root          31       2  0 Jan18 ?        00:00:00 [kdevtmpfs]
root          32       2  0 Jan18 ?        00:00:00 [kworker/R-inet_frag_wq]
root          33       2  0 Jan18 ?        00:00:00 [rcu_tasks_kthread]
root          34       2  0 Jan18 ?        00:00:00 [rcu_tasks_rude_kthread]
root          35       2  0 Jan18 ?        00:00:00 [rcu_tasks_trace_kthread]
root          36       2  0 Jan18 ?        00:00:00 [kauditd]
root          37       2  0 Jan18 ?        00:00:00 [khungtaskd]
root          38       2  0 Jan18 ?        00:00:00 [oom_reaper]
root          40       2  0 Jan18 ?        00:00:00 [kworker/R-writeback]
root          42       2  0 Jan18 ?        00:00:02 [kcompactd0]
root          43       2  0 Jan18 ?        00:00:00 [ksmd]
root          44       2  0 Jan18 ?        00:00:01 [khugepaged]
root          45       2  0 Jan18 ?        00:00:00 [kworker/R-kblockd]
root          46       2  0 Jan18 ?        00:00:00 [kworker/R-blkcg_punt_bio]
root          47       2  0 Jan18 ?        00:00:00 [kworker/R-kintegrityd]
root          48       2  0 Jan18 ?        00:00:00 [irq/9-acpi]
root          49       2  0 Jan18 ?        00:00:01 [kworker/1:1-events]
root          50       2  0 Jan18 ?        00:00:00 [kworker/R-tpm_dev_wq]
```

Note the output shows the last Kernal thread in this snippet with PID 50.

**Discussion points:**

* Which process started first?
```zsh
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 Jan18 ?        00:00:01 /sbin/init splash
```
* Which processes have been running the longest?

Using `ps -ef | more`, you can see that the processes with the earliest `STIME` (start time) are the ones that have been running the longest. In this case, all processes shown started on Jan 18, but you can identify the longest-running by their PID and STIME.

* Which ones started recently?



_Using the ps -ef command, processes can be examined along with their process IDs and start times. The first process started by the system is the one with the lowest PID. On Kali Linux, this is PID 1, which corresponds to the systemd (/sbin/init) process. Many system processes have no associated TTY because they are started at boot and run in the background._




```zsh
┌──(kali㉿kali)-[~]
└─$ ps -p 1 -o pid,ppid,stime,tty,cmd

    PID    PPID STIME TT       CMD
      1       0 Jan18 ?        /sbin/init splash
                                                                                              
┌──(kali㉿kali)-[~]
└─$ ps -eo pid,stime,tty,cmd | head  
    PID STIME TT       CMD
      1 Jan18 ?        /sbin/init splash
      2 Jan18 ?        [kthreadd]
      3 Jan18 ?        [pool_workqueue_release]
      4 Jan18 ?        [kworker/R-rcu_gp]
      5 Jan18 ?        [kworker/R-sync_wq]
      6 Jan18 ?        [kworker/R-kvfree_rcu_reclaim]
      7 Jan18 ?        [kworker/R-slub_flushwq]
      8 Jan18 ?        [kworker/R-netns]
     12 Jan18 ?        [kworker/u8:0-ipv6_addrconf]
                                                                                              
┌──(kali㉿kali)-[~]
└─$ ps -eo pid,stime,tty,cmd | tail
  65815 01:57 pts/0    su - gemma
  65851 01:57 pts/0    -bash
  66196 01:58 pts/0    su - kali
  66224 01:58 pts/0    -zsh
  69255 02:04 ?        [kworker/0:1-events]
  83400 02:35 ?        [kworker/u9:3-events_unbound]
  85877 02:40 ?        [kworker/0:0-ata_sff]
  88246 02:46 ?        [kworker/0:2-ata_sff]
  89709 02:49 pts/0    ps -eo pid,stime,tty,cmd
  89710 02:49 pts/0    tail

```

```zsh
┌──(kali㉿kali)-[~]
└─$ sudo service ssh status    
○ ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; disabled; preset: disabled)
     Active: inactive (dead)
       Docs: man:sshd(8)
             man:sshd_config(5)

```