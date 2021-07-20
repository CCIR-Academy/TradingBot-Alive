# TradingBot-Alive

## Dependencies
### Dev-Ops
Required:
- `Anaconda`: Package management
Optional:
- `docker`: For continuous deployment (Not implemented yet).

### Framework
Required:
- `freqtrade`
- `freqUI`

## Setting up Env
0. Preparing the project root. Remember to clone recursively as we are using submodules
```powershell
git clone --recurse-submodules https://github.com/CCIR-Academy/TradingBot-Alive.git
```
Note: Since this point, the appropriate working directory would be mentioned in the comments by `@` (e.g. `@repoRoot`)
1. Create Anaconda Environment
```powershell
# @repoRoot/freqtrade
conda env create -n freqtrade-conda -f environment.yml
#(May take ages and retries)
```
Note: In case the creation process fails, you need to manually remove and reinstall.
```powershell
conda env remove -n freqtrade-conda
```
2. Activate the virtual environment.
```powershell
conda activate freqtrade-conda
```
Note: Only in this environment, `freqtrade` is callable globally.
3. Update pip and dependencies.
```powershell
pip install --upgrade pip
pip install -e .
```
## Generate default user folder and configuration file (might not be necessary)
```Powershell
# @repoRoot
# Step 1 - Initialize user folder
freqtrade create-userdir --userdir user_data
# Step 2 - Create a new configuration file
# Note: You can skip this config creation as the repo contains one in advance with some basic tweaks for the sake of other components; in addition, only a selection of pairs of crytocurrencies have been left..
freqtrade new-config --config config.json
```
Note: Based on the guide from `freqUI`, you may need to adjust the following settings in `config.json`
```json
// Note: Only replace if different, and do not delete.
{
    "stake_amount": 500,
    "dry_run_wallet": 100000,
    "api_server": {
        "enabled": true,
        "listen_ip_address": "127.0.0.1",
        "listen_port": 8081,
        "CORS_origins": ["http://127.0.0.1:8080", "http://localhost:8080"],
        "username": "freqtrader",
        "password": "freqtrader"
    },
}
```

### freqUI Installation
Note: According to the [default installation guide](https://github.com/freqtrade/frequi) for `freqUI`:
> In newer versions (2021.2 and newer), freqUI is builtin to freqtrade, so manual setup of freqUI will no longer be necessary unless you want to modify freqUI.

To install by the builtin approach, use the following code:
```shell
freqtrade install-ui
# Note(Optional): Try downgrading urllib3 if raises `ValueError: check_hostname requires server_hostname`.
pip install urllib3==1.25.11 -i http://pypi.douban.com/simple --trusted-host pypi.douban.com
```
In our learning case, we would rather install `freqUI` manually as we want to modify freqUI; the repo for `freqUI` should have been available as submodule for this project if the project is cloned recursively.
Note: Before setting up `freqUI` with manual installation, make sure you have `Node.js` and `yarn` installed.
- To install `Node.js`, follow the instructions here: https://nodejs.org/en/download/
- To install `yarn` after installing `Node.js`,  follow the instructions here: https://yarnpkg.com/getting-started/install


```powershell
# @repoRoot/frequi
yarn install
# To compile and hot-reloads for development. You may need to do so in another shell instance.
yarn serve
```




## Starting the project
Note:Replace `SampleStrategy` with the name of your strategy.
```powershell
# @repoRoot
freqtrade trade --config config.json --strategy SampleStrategy
```
## Configuration Guide
https://www.freqtrade.io/en/stable/configuration/

## Strategy Guide
https://www.freqtrade.io/en/stable/strategy-customization/

## Informative Notes:
1. If the submodules are not recursively cloned, use `git submodule update --recursive` to manually update the submodules.
2. The default lint options for `freqUI` seems to be too strict with EOF character which may cause errors for `Vue` in rendering. Edit `freqUI/.prettierrc.json` in the following way to get around.
```json
{
    "printWidth": 100,
    "singleQuote": true,
    "trailingComma": "all",
    "files": "./src/**/*.{js,vue,json}",
    "endOfLine": "auto"
}
3. If the stake amount and dry run wallet are not set properly, no trades would be made in some cases, and you may need to manually change them in `config.json`. The default settings provided by the repo has been validated to be a good starting point.