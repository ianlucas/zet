# MacOS

## Check CPU temperature

Use this to check MacOS CPU temperature. Parsec makes Mac mini 2014 fry - don't use it.

```bash
sudo powermetrics --samplers smc | grep -i "CPU die temperature"
```
