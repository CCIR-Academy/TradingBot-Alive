# TradingBot-Alive

## Dependencies
### Dev-Ops
`Anaconda`
`docker`: For continuous deployment.

### Framework
`freqtrade`

## Setting up Env
1. Set up `freqtrade` as submodule.
`git submodule add https://github.com/freqtrade/freqtrade.git freqtrade`
2. Create Conda Environment
`cd freqtrade`
`conda env create -n freqtrade-conda -f environment.yml` (May take ages and retries)
3. Activate the virtual environment.
`conda activate freqtrade-conda`
4. Update pip and dependencies.
`python3 -m pip install --upgrade pip`
`python3 -m pip install -e .`

## Initialize the configuration

```Powershell
# Step 1 - Initialize user folder
cd ..
freqtrade create-userdir --userdir user_data

# Step 2 - Create a new configuration file
freqtrade new-config --config config.json
```
### Optional Initializations
`freqtrade install-ui`
- Note: Try downgrading urllib3 if raises `ValueError: check_hostname requires server_hostname`.
`pip install urllib3==1.25.11 -i http://pypi.douban.com/simple --trusted-host pypi.douban.com`

## Configuration Guide
https://www.freqtrade.io/en/stable/configuration/

## Strategy Guide
https://www.freqtrade.io/en/stable/strategy-customization/