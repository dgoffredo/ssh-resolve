`ssh-resolve`
=============
My `~/.ssh/config` files looks something like this:
```ssh-config
# kubernetes minion node 1
Host dgoffredo-k8s-m1
  User ubuntu
  HostName 10.142.15.197

# kubernetes minion node 2
Host dgoffredo-k8s-m2
  User ubuntu
  HostName 10.142.15.198

# Mom's old phone, using it as a time-lapse camera
Host weedcam-local
  HostName 192.168.1.112
  Port 2222
```
The section `Host weedcam-local` doesn't define an actual host name on my
system (in the sense that `/etc/hosts` or DNS would).  However, it's convenient
to be able to refer to hosts using these names, e.g. with `ping`.

`ssh-resolve` translates the ssh alias name into the host name, e.g.
```console
$ ssh-resolve weedcam-local
192.168.1.112

$ ping $(ssh-resolve weedcam-local)
PING 192.168.1.112 (192.168.1.112) 56(84) bytes of data.
64 bytes from 192.168.1.112: icmp_seq=1 ttl=64 time=1291 ms
64 bytes from 192.168.1.112: icmp_seq=2 ttl=64 time=282 ms
64 bytes from 192.168.1.112: icmp_seq=3 ttl=64 time=48.8 ms
^C
--- 192.168.1.112 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2009ms
rtt min/avg/max/mdev = 48.760/540.680/1291.277/539.225 ms, pipe 2
```
Run `ssh-resolve --help` for more information.
