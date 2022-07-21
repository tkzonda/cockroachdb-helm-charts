# Fork informations
This repository is fork of https://github.com/cockroachdb/helm-charts.
It contains changes similar to PR https://github.com/cockroachdb/helm-charts/pull/134

## Publish helm chart process

### prerequisites
1. Download [binary of helm-chart-releaser](https://github.com/helm/chart-releaser/releases) and install in your `/usr/local/bin` 
2. Create [github personal access token](https://github.com/settings/tokens) with permisions to 'write:packages'

### Updating process
1. Switch to `expose-node-locality` branch
2. Make your changes
3. Update `version` field in `cockroachdb/Chart.yaml`
4. Package your chart
   ```bash
   # in repo root dir
   cr package cockroachdb
   ```
5. Upload new release and generate `index.yaml`
   ```bash
   cr upload -t <GITHUB_TOKEN>
   cr index
   ```
   
6. Automatic push index.yaml with `cr index --push` option ends with `panic` error, so we need to do it manually.
   ```bash
   git checkout gh-pages
   cp .cr-index/index.yaml index.yaml
   git add index.yaml
   git commit -m "Release version <VERSION>"
   git push origin gh-pages
   git checkout expose-node-locality
   ```
