---
layout: default
title: Quick Start Guide
nav_order: 2
---
<details markdown="block">
  <summary>
    Table of Contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

# Quick Start Guide

## Intended Audience

This guide is intended for anyone who wants to download and install Swirl. 

{: .warning }
As of version 2.6.0, Swirl's start-up process no longer starts `redis`.  You must now have `redis` installed *and running* before starting Swirl.

# Docker Installation

## Prerequisites

* To run Swirl in Docker, you must have the latest [Docker app](https://docs.docker.com/get-docker/) for MacOS, Linux, or Windows installed and running locally.

* Windows users must first install and configure either the WSL 2 or the Hyper-V backend, as outlined in the  [System Requirements for installing Docker Desktop on Windows](https://docs.docker.com/desktop/install/windows-install/#system-requirements).

## Start Swirl in Docker

{: .warning }
Make sure the Docker app is running before proceeding!

* Download [https://raw.githubusercontent.com/swirlai/swirl-search/main/docker-compose.yaml](https://raw.githubusercontent.com/swirlai/swirl-search/main/docker-compose.yaml)

``` shell
curl https://raw.githubusercontent.com/swirlai/swirl-search/main/docker-compose.yaml -o docker-compose.yaml
```

* *Optional*: To enable Swirl's Real-Time Retrieval Augmented Generation (RAG) in Docker, run the following commands from the Console using a valid OpenAI API key:
``` shell
export MSAL_CB_PORT=8000
export MSAL_HOST=localhost
export OPENAI_API_KEY='<your-OpenAI-API-key>'
```

{: .highlight }
Check out [OpenAI's YouTube video](https://youtu.be/nafDyRsVnXU?si=YpvyaRvhX65vtBrb) if you don't have an OpenAI API Key.

* On MacOS or Linux, run the following command from the Console:

``` shell
docker-compose pull && docker-compose up
```

* On Windows, run the following command from PowerShell:

``` shell
docker compose up
```

After a few minutes, the following or similar should appear:

``` shell
docker-redis-1  | 1:C 26 Sep 2023 16:20:10.054 * oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
docker-redis-1  | 1:C 26 Sep 2023 16:20:10.054 * Redis version=7.2.1, bits=64, commit=00000000, modified=0, pid=1, just started
docker-redis-1  | 1:C 26 Sep 2023 16:20:10.054 # Warning: no config file specified, using the default config. In order to specify a config file use redis-server /path/to/redis.conf
docker-redis-1  | 1:M 26 Sep 2023 16:20:10.054 * monotonic clock: POSIX clock_gettime
docker-redis-1  | 1:M 26 Sep 2023 16:20:10.056 * Running mode=standalone, port=6379.
docker-redis-1  | 1:M 26 Sep 2023 16:20:10.056 * Server initialized
docker-redis-1  | 1:M 26 Sep 2023 16:20:10.056 * Ready to accept connections tcp
docker-app-1    | __S_W_I_R_L__2_._6______________________________________________________________
docker-app-1    | 
docker-app-1    | Setting Up SWIRL:
docker-app-1    | Checking Migrations:
docker-app-1    | No changes detected
docker-app-1    | 
docker-app-1    | 
docker-app-1    | Migrating:
docker-app-1    | 
docker-app-1    | Operations to perform:
docker-app-1    |   Apply all migrations: admin, auth, authtoken, contenttypes, django_celery_beat, sessions, swirl
docker-app-1    | Running migrations:
docker-app-1    |   No migrations to apply.
docker-app-1    | 
docker-app-1    | 
docker-app-1    | Collecting Statics:
docker-app-1    | 
docker-app-1    | 
docker-app-1    | 215 static files copied to '/app/static'.
docker-app-1    | 
docker-app-1    | Ok
docker-app-1    | Command successful!
docker-app-1    | __S_W_I_R_L__2_._6______________________________________________________________
docker-app-1    | 
docker-app-1    | Warning: logs directory does not exist, creating it
docker-app-1    | ParseResult(scheme='redis', netloc='redis:6379', path='/0', params='', query='', fragment='') checked.
docker-app-1    | ParseResult(scheme='redis', netloc='redis:6379', path='/0', params='', query='', fragment='') checked.
docker-app-1    | Start: celery-worker -> celery -A swirl_server worker --loglevel INFO ... Ok, pid: 27
docker-app-1    | Start: celery-beats -> celery -A swirl_server beat --scheduler django_celery_beat.schedulers:DatabaseScheduler ... Ok, pid: 38
docker-app-1    | Updating .swirl... Ok
docker-app-1    | 
docker-app-1    |   PID TTY          TIME CMD
docker-app-1    |    27 ?        00:00:04 celery
docker-app-1    |    38 ?        00:00:03 celery
docker-app-1    | 
docker-app-1    | You are using version 2.6 of Swirl, the current version.
docker-app-1    | Command successful!
docker-app-1    | 2023-09-26 12:20:40,303 INFO     Starting server at tcp:port=8000:interface=0.0.0.0
docker-app-1    | 2023-09-26 12:20:40,303 INFO     HTTP/2 support not enabled (install the http2 and tls Twisted extras)
docker-app-1    | 2023-09-26 12:20:40,303 INFO     Configuring endpoint tcp:port=8000:interface=0.0.0.0
docker-app-1    | 2023-09-26 12:20:40,303 INFO     Listening on TCP address 0.0.0.0:8000
```

* Open this URL with a browser: <http://localhost:8000> (or <http://localhost:8000/galaxy>)

If the search page appears, click `Log Out` at the top, right. The Swirl login page will appear:

![Swirl Login](images/swirl_login-galaxy_dark.png)

* Enter the username `admin` and password `password`, then click `Login`.

* Enter a search in the search box and press the `Search` button. Ranked results appear in just a few seconds:

![Swirl Results No M365](images/swirl_results_no_m365-galaxy_dark.png)

* To view the raw JSON, open <http://localhost:8000/swirl/search/>

The most recent Search object will be displayed at the top. Click on the `result_url` link to view the full JSON Response.

## Notes

{: .warning }
The Docker version of Swirl does *not* retain any data or configuration when shut down!

{: .highlight }
Swirl includes five (5) Google Programmable Search Engines (PSEs) to get you up and running right away. The credentials for these are shared with the Swirl Community.

{: .highlight }
Using Swirl with Microsoft 365 requires installation and approval by an authorized company Administrator. For more information, please review the [M365 Guide](M365-Guide.md) or [contact us](mailto:hello@swirl.today).

# Local Installation

## Prerequisites

{: .warning }
As of version 2.6.0, Swirl's start-up process no longer starts `redis`.  You must now have `redis` installed *and running* before starting Swirl.

### MacOS

* Python 3.11.x with `pip`
    * If necessary, modify the system PATH so that Python runs when you type `python` at the Terminal (not `python3`)
    * [venv](https://docs.python.org/3/library/venv.html) (*optional*)
    * [pyenv](https://github.com/pyenv/pyenv) (*optional*)
* [Homebrew](https://brew.sh/) installed and updated
* Redis installed:
 ``` shell
 brew install redis
 ```
* jq installed:
``` shell
brew install jq
```
* Redis must be running

{: .warning }
Swirl has not yet been validated on Python 3.12.x as some required packages have not yet completed their own 3.12.x upgrades.

### Linux

* Python 3.11.5 or newer ([stable release](https://www.python.org/downloads/)) with `pip`
* Redis and jq installed:
``` shell
sudo apt install jq redis-server -y
```
* Redis must be running

### Windows

{: .warning }
Swirl is *not* supported for local installation or production use on Windows!

### PostgreSQL (optional)

If you wish to use PostgreSQL as a data source or as the Swirl back-end database:

1. Install [PostgreSQL](https://www.postgresql.org/)

2. Modify the system PATH so that `pg_config` from the PostgreSQL distribution is accessible from the command line

3. Install `psycopg2` using `pip`:
``` shell
pip install psycopg2
```

## Install Swirl

* Clone the repo:

``` shell
git clone https://github.com/swirlai/swirl-search
cd swirl-search
```

* To install Swirl on MacOS, execute this command from the Console:

``` shell
./install.sh
```

* To install Swirl on Linux, execute this command from the Console:

``` shell
apt-get update --allow-insecure-repositories -y && apt-get install apt-file -y && apt-file update && apt-get install -y python3-dev build-essential
./install.sh
```

* If there are problems running `install.sh`, proceed manually:

``` shell
pip install -r requirements.txt
python -m spacy download en_core_web_lg
python -m nltk.downloader stopwords
python -m nltk.downloader punkt
```

{: .warning }
Issues with certifications on OS/X? See: [urllib and "SSL: CERTIFICATE_VERIFY_FAILED" Error](https://stackoverflow.com/questions/27835619/urllib-and-ssl-certificate-verify-failed-error/42334357#42334357)

## Setup Swirl

* Execute the following command from the Console to setup Swirl:

``` shell
python swirl.py setup
```

## Install the Galaxy UI

{: .warning }
To install the Galaxy UI, you must have the latest [Docker app](https://docs.docker.com/get-docker/) for MacOS or Linux installed and running locally.

* To install Galaxy, execute the following command the Console (with the Docker app running):

``` shell
./install-ui.sh
```

{: .highlight }
The Galaxy UI components should be installed only *after* running the `./install.sh` and `python swirl.py setup` commands.

## Start Swirl

* Execute the following command from the Console to start Swirl:

``` shell
python swirl.py start
```

## Open the Swirl Homepage (Django)

* Enter this URL into a browser: <http://localhost:8000/swirl/>

The following page should appear:

![Swirl Homepage](images/swirl_frontpage.png)

## Open the Galaxy UI

* Open this URL with a browser: <http://localhost:8000> (or <http://localhost:8000/galaxy/>)

If the search page appears, click `Log Out` at the top, right. The Swirl login page will appear:

![Swirl Login](images/swirl_login-galaxy_dark.png)

* Enter the username `admin` and password `password`, then click `Login`.

* Enter a search in the search box and press the `Search` button. Ranked results appear in just a few seconds:

![Swirl Results](images/swirl_results_no_m365-galaxy_dark.png)

## Notes

{: .warning }
Removing Swirl's `static/` content will also remove the Galaxy UI files! You will need to re-install Galaxy if you have removed Swirl's `static/` directory and then run either `python manage.py collectstatic` or `python swirl.py setup`.

{: .highlight }
Swirl includes five (5) Google Programmable Search Engines (PSEs), complete with shared credentials, to get you up and running right away. These credentials are shared with the Swirl Community.

{: .highlight }
Using Swirl with Microsoft 365 requires installation and approval by an authorized company Administrator. For more information, please review the [M365 Guide](M365-Guide.md) or [contact us](mailto:hello@swirl.today).
