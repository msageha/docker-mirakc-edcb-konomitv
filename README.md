# docker-mirakc-konomitv

## initialize channel

```bash
curl -sf https://raw.githubusercontent.com/heisannn/docker-mirakc-konomitv/main/setup.sh | sh -s
chmod +x ./scan_ch_mirakc_docker.sh
./scan_ch_mirakc_docker.sh
rm ./scan_ch_mirakc_docker.sh

mv mirakc_channels.yml mirakc/channels.yaml
cat mirakc_channels.yml >> mirakc/config.yml
```
