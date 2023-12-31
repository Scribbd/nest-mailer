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
For security reasons the client_secret-json isn't included with the GitHub repository. To get the secret head over to the google cloud console with your Google Cloud account. Create a project and create a mail secret.

Be careful of committing this secret into the repository. The `.gitignore`-file does have ignore rules, delete the credentials afterward sending out your mail.

### What happens when this gets public
The secret is setup for internal use only. And users need to authenticate to actually use our API access. So nothing much. We could get flooded with login attempts, which could incur a charge. It is just better to be safe.

## Activate Venv, Download Python dependencies
If you are on Windows you can use the `install.ps1` script to prepare your environment for a run.

`.\install.ps1`

Otherwise following these commands to setup your virtual python environment:
| On Linux do:                               | In Windows PowerShell do:                 |
|--------------------------------------------|-------------------------------------------|
| python3 -m venv .venv                      | python -m venv .venv                      |
| `. ./.venv/bin/activate`                   | `.\.venv\Scripts\Activate.ps1`            |
| python3 -m pip install -r requirements.txt | python -m pip install -r requirements.txt |

# Execution
To run the script use the following command:
```
python3 mailer.py [INPUT_CSV_PATH] [LXD_HOST_IP] [SECRET_JSON_PATH]
```

- INPUT_SCV_PATH: Path to the CSV-file that [Linux-Nester](https://github.com/scribbd/linux-nester) generated
- LXD_HOST_IP: The public IP address of your LXD Host
- SECRET_JSON_PATH: [Instructions](#Get-your-secret)

This script will open a browser window which allows you to authenticate with your Google account. Make certain you use a TechGrounds account as non other will work.

## The script interrupted?
This script has no mechanism to resume after a failed run. You can 'resume' the script by removing the entries from the input file that were send correctly before the script failed.
