# action-deploy2aliyun
> A composite steps for deploy frontend files to aliyun oss.

## usage
1. set secret `gh secret set -f ~/.aliyun/.env.kubebio`
2. use below workflow
```yml
name: deploy2aliyun workflow
on:
  push:
    branches:
      - master
jobs:
  Release:
    name: Release
    runs-on: ubuntu-latest
    env:
      ACCESS_KEY_ID: ${{ secrets.ALIBABACLOUD_ACCESS_KEY_ID }}
      ACCESS_KEY_SECRET: ${{ secrets.ALIBABACLOUD_ACCESS_KEY_SECRET }}
      REGION: ${{ secrets.ALIBABACLOUD_REGION_ID }}

    if: contains(github.event.head_commit.message, '__@production__')
    steps:
      - name: All in one
        uses: afeiship/action-deploy2aliyun@master
        with:
          build_dist: "build"
          oss_bucket: "oss://kubebio-com-web/kubebio.com/assets/test-app-deploy2aliyun/"
```