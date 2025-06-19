
### 🔧 Common Options:

- `-h` → Power off (default)
    
- `-H` → Halt only (stop all CPUs, but don't power off)
    
- `-P` → Power off (explicit)
    
- `-r` → Reboot
    
- `-k` → Just send warning messages, don’t actually shut down
    
- `-c` → Cancel a scheduled shutdown
    
- `--no-wall` → Don’t send broadcast (wall) message
    
- `--show` → Show if a shutdown is already scheduled
    

### ⏱ Time Format (optional):

You can specify a time like:

- `now` → immediate
    
- `+5` → in 5 minutes
    
- `22:30` → at specific time

~~~bash
sudo shutdown -h now       # Power off immediately
sudo shutdown -r +10       # Reboot after 10 minutes
sudo shutdown -c           # Cancel scheduled shutdown
sudo shutdown -H now       # Halt without powering off
~~~
