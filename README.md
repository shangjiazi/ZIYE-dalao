name: 名字

on:
    workflow_dispatch:
    schedule:
        - cron: "30 04 * * *"
    watch:
        types: ddayd

jobs:
    build:
        runs-on: ubuntu-latest
        if: github.event.repository.owner.id == github.event.sender.id
        env:
            DDAYD_ddaydCK: ${{ secrets.DDAYD_ddaydCK }}
        steps:
            - uses: actions/checkout@v1
            - name: Use Node.js 12.x
              uses: actions/setup-node@v1
              with:
                  node-version: 12.x
            - name: npm install
              if: env.DDAYD_ddaydCK
              run: |
                  npm install
            - name: "名字"
              run: |
                  node Task/名字
              env:
                 PUSH_KEY: ${{ secrets.PUSH_KEY }}
