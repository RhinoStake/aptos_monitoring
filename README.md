# Grafana Dashboard for Monitoring APTOS Validator Operations

This is a work-in-progress Grafana dashboard for monitoring Aptos Validators. Setting up Prometheus/Grafana is outside the scope of this repo. Use the [excellent guide from Artifact Staking](https://artifact-staking.medium.com/setting-up-validator-monitoring-for-aptos-testnet-2-85d5c4e94c80).

![](https://grabup.teamhim.com/consequents-freckled-apprehensiveness-puncturing.png?raw=true)

## A few assumptions notes about using this dashboard:

- This is in-progress and will have significant updates in 2022 as I (and other operators) better understand the important metrics and alerts for proper node operations.
- Come back often, re-download the json and re-import the dashboard json for updates.
- Ensure that node-exporter is installed on your Validator to pull machine metrics: `apt install prometheus-node-exporter`.
- This dashboard assumes you have a `chain` tag that is used in the prometheus metrics capture. I use this to flip between testnet/mainnet monitoring. This dashboard assumes you have this `chain` label set and will not show data without it. Setup your `prometheus.yml` file like this:

```yaml
  - job_name: aptos
      static_configs:
      - targets: ['your.ip.addy.here:9100','your.ip.addy.here:9101']
          labels:
          chain: 'testnet'

# 9100 is prometheus-node-exporter, 9101 is the default APTOS metrics port
```

## To use this file

- Download the `.json` file from the Grafana folder in this repository
- Hit Import in Grafana

![](https://grabup.teamhim.com/unalimentative-winterage-lucently-pharyngotonsillitis.png?raw=true)

- Click Upload JSON and select the file downloaded
- Select your Prometheus datasource from the dropdown & import!

![](https://grabup.teamhim.com/neurocity-thumbkins-hooping-arabs.png?raw-true)

### Have ideas/changes/additions? Great! Feel free to push a PR to this repo or reach out to [me on Discord](https://discord.gg/SGhQzj5tyz)!

## Who is RHINO?

RHINO is a professionally managed, highly available validator service. Earn rewards and help secure networks by staking your tokens with RHINO. We operate across the Cosmos, Helium and APTOS ecosystems. Read more at [https://rhinostake.com](https://rhinostake.com).
