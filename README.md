# Add new feed:

```
sed -i "/lwrt/d" "feeds.conf.default"
echo "src-git lwrt https://github.com/724899020/lwrt.git" >> "feeds.conf.default"
```
# Pull upstream commits:
```
./scripts/feeds update lwrt
./scripts/feeds install -a -f -p lwrt
```
# Remove
```
sed -i "/lwrt/d" "feeds.conf.default"
./scripts/feeds clean
./scripts/feeds update -a
./scripts/feeds install -a
```


app list:
+ openresty
