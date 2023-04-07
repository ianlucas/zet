# MacOS

## Check CPU temperature

I'm currently using a Mini Mac 2014 for developing in MacOS, and I was using it remotely using Parsec, however it was demanding so much of the Mini Mac that ended up using it only via SSH. With this command I can monitor its temperature.

```bash
sudo powermetrics --samplers smc | grep -i "CPU die temperature"
```
