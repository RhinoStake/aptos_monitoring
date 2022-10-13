# Grafana Dashboard for Monitoring APTOS Validator Operations

This is a work-in-progress Grafana dashboard for monitoring Aptos Validators. Setting up Prometheus/Grafana is outside the scope of this repo. Use the [excellent guide from Artifact Staking](https://artifact-staking.medium.com/setting-up-validator-monitoring-for-aptos-testnet-2-85d5c4e94c80).

**New!** This Dashboard is also available on the [Grafana Dashboard page for one-click install](https://grafana.com/grafana/dashboards/16846-aptos-validator-monitoring/).

![aptos monitoring dashboard](https://grabup.teamhim.com/palaeogaea-calycozoic-liquidatorship-crosshatcher.png?raw=true)

## A few assumptions and instructions for setup:

- This is in-progress and will have significant updates in 2022 as I (and other operators) better understand the important metrics and alerts for proper node operations.
- This requires a Prometheus data source (obviously), pulling data from the Aptos node's metric port at `9101`
- This also requires the [Infinity Plugin](https://grafana.com/grafana/plugins/yesoreyeram-infinity-datasource/) (for pulling API/JSON information). Install this plugin by executing `grafana-cli plugins install yesoreyeram-infinity-datasource` on the grafana server, or you can install for [grafana.net cloud installs](https://grafana.com/grafana/plugins/yesoreyeram-infinity-datasource/?tab=installation).
- After you install the Infinity Plugin, go to your Datasources and add a new Datasource. Choose type Infinity and hit save. This requires no other configuration.
- Ensure that node-exporter is installed on your Validator to pull machine metrics: `apt install prometheus-node-exporter`.
- This dashboard assumes you have a `chain` tag that is used in the prometheus metrics capture. I use this to flip between testnet/mainnet monitoring. This dashboard assumes you have this `chain` label set and will not show data without it. Setup your `prometheus.yml` file like this:

```yaml
  - job_name: aptos
      static_configs:
      - targets: ['val.llt.ip.addy.here:9100','val.llt.ip.addy.here:9101','valFullNode.llt.ip.addy.here:9100','valFullNode.llt.ip.addy.here:9101']
          labels:
          chain: 'llt'
      - targets: ['val.mainnet.ip.addy.here:9100','val.mainnet.ip.addy.here:9101','valFullNode.mainnet.ip.addy.here:9100','valFullNode.mainnet.ip.addy.here:9101']
          labels:
          chain: 'mainnet'

# 9100 is prometheus-node-exporter, 9101 is the default APTOS metrics port.  Ensure these are available from the prometheus server
# Add both your Validator and Validator Full Node IP addresses.  No need for additional tags.
```

**Note:** These exact prometheus chain labels (`llt` and `mainnet`) are used in variables in the dashboard for pulling metrics from the API. If you choose NOT use these chain names in your `prometheus.yml` file, you will need to change these names in the Variables section within the dashboard itself.

### Additional Functionality

- Dashboard can determine validator vs. full-node metrics from data, no need to tag
- PeerID is determined in variable from data
- If you utilize annotations, use tag `restart` and annotation will occur on all graphs

## How to use this file

- Download the `.json` file from the Grafana folder in this repository
- Hit Import in Grafana

![grafana import](https://grabup.teamhim.com/unalimentative-winterage-lucently-pharyngotonsillitis.png?raw=true)

- Click Upload JSON and select the file downloaded
- Select your Prometheus datasource from the dropdown & import!

![grafana import](https://grabup.teamhim.com/tabescence-jamshid-tiou-stinkier.png?raw-true)

Have ideas/changes/additions? Great! Feel free to push a PR to this repo or reach out to [me on Discord](https://discord.gg/SGhQzj5tyz)!

## Who is RHINO?

RHINO is a professionally managed, highly available validator service. Earn rewards and help secure networks by staking your tokens with RHINO. We operate across the Aptos, Cosmos, Chainlink, and Helium ecosystems. Read more at [https://rhinostake.com](https://rhinostake.com).
