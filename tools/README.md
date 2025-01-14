# Tools

## Set Reserve

This command line tool allows you to read and set the Powerwall minimum backup reserve battery level (percentage).

### Setup

```bash
# Install python modules
pip install python-dateutil teslapy

# Login to Tesla account to set up token
python3 set-reserve.py --login
```

This will create the config file, save an auth token so you will not need to login again, and then display the energy site details associated with your Tesla account. It will run in an interactive mode.

```
Config file 'set-reserve.conf' not found

Do you want to create the config now? [Y/n] Y

Tesla Account Setup
-------------------
Email address: your@email.address
Save auth token to: [set-reserve.auth]

Config saved to 'set-reserve.conf'
```

After the config is saved, you will be prompted to login to your Tesla account. This is done by opening the displayed URL in your browser and then logging in.

**NOTE**: After you log in, it will take you to a *404 Page Not Found* error page - do not panic, 
this is what you want.

```
----------------------------------------
Tesla account: your@email.address
----------------------------------------
Open the below address in your browser to login.

<copy URL to browser> e.g.: https://auth.tesla.com/oauth2/v3/authorize?response_type=code...etc.

After login, paste the URL of the 'Page Not Found' webpage below.

Enter URL after login: <paste URL from browser> e.g.: https://auth.tesla.com/void/callback?code=...etc.
```

After you have logged in successfully, the browser will show a 'Page Not Found' webpage. Copy the URL of this page and paste it at the prompt.

Once logged in successfully, you will be shown details of the energy site(s) associated with your account:

```
----------------------------------------
Tesla account: your@email.address
----------------------------------------
      Site ID: 1234567890
    Site name: My Powerwall
     Timezone: Australia/Sydney
    Installed: 2021-04-01 13:09:54+11:00
  System time: 2022-10-13 22:40:59+11:00
----------------------------------------
```

Once these steps are completed, you should not have to login again.

### Usage

* Display Current Battery Reserve Setting

    ```bash
    # Verbose Response
    python3 set-reserve.py --read

    # Abbreviated Response
    python3 set-reserve.py --read -n
    ```

* Set Battery Reserve Setting

    ```bash
    # Set reserve percentage
    python3 set-reserve.py --set 25

    # Set reserve based on current battery level - useful 
    # to pause charging and discharging 
    python3 set-reserve.py --current
    ```

  `READ: Current Battery Reserve Setting: 25% for 2 Powerwalls`

  `SET: Current Battery Reserve Setting: 25% - Response: Updated`


* Cron Job Examples

  See the [cron.sh](cron.sh) example script on how you can use set-reserve.py to optimize your Powerwall usage.
  

## Set Mode

This command line tool allows you to read and set the Powerwall operational mode (self-powered or time-based control).

### Setup

```bash
# Install python modules
pip install python-dateutil teslapy

# Login to Tesla account to set up token
python3 set-mode.py --login
```

This will create the config file, save an auth token so you will not need to login again, and then display the energy site details associated with your Tesla account. It will run in an interactive mode.  See the instructions for the "Set Reserve" tool above.

### Usage

* Display Current Operational Mode

    ```bash
    # Verbose Response
    python3 set-mode.py --read

    # Abbreviated Response
    python3 set-mode.py --read -n
    ```

  `READ: Current Operational Mode: self_consumption with 2 Powerwalls`

* Set Operational Mode

    ```bash
    # Set to Self Powered mode
    python3 set-reserve.py --set self

    # Set to Time-Based Control mode
    python3 set-reserve.py --set time
    ```

### Credit

These tools (set-reserve and set-mode) are based on the the amazing [tesla_history.py](https://github.com/jasonacox/Powerwall-Dashboard/tree/main/tools/tesla-history) tool by Michael Birse (@mcbirse) that imports Tesla cloud history into the [Powerwall-Dashboard](https://github.com/jasonacox/Powerwall-Dashboard).
