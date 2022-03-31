# nest-mailer
Automate mailing the [Nested-Linux](https://github.com/techgrounds/linux-nester) access details through GMail API.

# Preperations before running
## Requirements
Access to a Desktop. This app requires web authentication and cannot function inside a CLI only environment.
The following needs to be installed:
 - Python 3.10
 - Python Virtual Environment `pip3 install venv`

## Clone
Clone this repository with:
- `git clone https://github.com/techgrounds/nest-mailer`

## Retrieving input
- Get the CSV-output-file from [Linux-Nester](https://github.com/techgrounds/linux-nester). 
- Note down the public IP of your LXD instance.

## Get your secret
For security reasons the client_secret-json isn't included with the GitHub repository. To get the secret head over to the google cloud console with your TechGrounds account. The console can be found [here](https://console.cloud.google.com/apis/credentials?hl=nl&project=default-333121). Download the `Py-Nest-Mailer` keys and place it in the `secrets`-folder.

Be careful of committing this secret into the repository. The `.gitignore`-file does have ignore rules, delete the credentials afterward sending out your mail.

### What happens when this gets public
The secret is setup for internal use only. And users need to authenticate to actually use our API access. So nothing much. We could get flooded with login attempts, which could incur a charge. It is just better to be safe.

## Activate Venv, Download Python dependencies
Use the following commands to setup your virtual python environment:
```sh
python3 -m venv .venv
```

| On Linux do:             | In Windows PowerShell do:      |
|--------------------------|--------------------------------|
| `. ./.venv/bin/activate` | `.\.venv\Scripts\Activate.ps1` |

Finish with:
```sh
python3 -m pip install -r requirements.txt
```

# Execution
To run the script use the following command:
```
python3 mailer.py [INPUT_CSV_PATH] [LXD_HOST_IP] [SECRET_JSON_PATH]
```

- INPUT_SCV_PATH: Path to the CSV-file that [Linux-Nester](https://github.com/techgrounds/linux-nester) generated
- LXD_HOST_IP: The public IP address of your LXD Host
- SECRET_JSON_PATH: [Instructions](#Get-your-secret)

This script will open a browser window which allows you to authenticate with your Google account. Make certain you use a TechGrounds account as non other will work.

## The script interrupted?
This script has no mechanism to resume after a failed run. You can 'resume' the script by removing the entries from the input file that has been send correctly before the script failed.