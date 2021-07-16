# TradingBot-Alive

## Dependencies
### Dev-Ops
Required:
- `Anaconda`: Package management
Optional:
- `docker`: For continuous deployment.

### Framework
Required:
- `freqtrade`

## Setting up Env
0. Preparing the project root. Remember to clone recursively as we are using submodules
```powershell
git clone --recurse-submodules https://github.com/Alive24/TradingBot-Alive
```
Note: Since this point, the appropriate working directory would be mentioned in the comments by `@` (e.g. `@projectRoot`)
1. Create Anaconda Environment
```powershell
# @projectRoot/freqtrade
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
3. Update pip and dependencies.
```powershell
pip install --upgrade pip
pip install -e .
```
## Generate default user folder and configuration file (might not be necessary)
```Powershell
# @projectRoot
# Step 1 - Initialize user folder
freqtrade create-userdir --userdir user_data
# Step 2 - Create a new configuration file
freqtrade new-config --config config.json
```
### Optional Initializations (Recommended for learning)
```shell
freqtrade install-ui
```
- Note: Try downgrading urllib3 if raises `ValueError: check_hostname requires server_hostname`.
```shell
pip install urllib3==1.25.11 -i http://pypi.douban.com/simple --trusted-host pypi.douban.com
```

## Starting the project
Note:Replace `SampleStrategy` with the name of your strategy.
```powershell
# @projectRoot
freqtrade trade --config config.json --strategy SampleStrategy
```
## Configuration Guide
https://www.freqtrade.io/en/stable/configuration/

## Strategy Guide
https://www.freqtrade.io/en/stable/strategy-customization/

## Informative Notes:
1. If the submodules are not recursively cloned, use `git submodule update --recursive` to manually update the submodules.
