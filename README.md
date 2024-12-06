# Cyberbro

A simple application that extracts your IoCs from garbage input and checks their reputation using multiple services.
Inspired by [Cybergordon](https://cybergordon.com/) and [IntelOwl](https://github.com/intelowlproject/IntelOwl).

This project aims to provide a simple and efficient way to check the reputation of your observables using multiple services, 
without having to deploy a **complex** solution.

![GitHub stars](https://img.shields.io/github/stars/stanfrbd/cyberbro?style=social)
![GitHub issues](https://img.shields.io/github/issues/stanfrbd/cyberbro)
![License](https://img.shields.io/github/license/stanfrbd/cyberbro)
![example branch parameter](https://github.com/stanfrbd/cyberbro/actions/workflows/jobs.yml/badge.svg)

![cyberbro_extended](https://github.com/user-attachments/assets/0485e283-2d79-4c62-85eb-304ed0b1550d)

# Features

* **Supports garbage input**: paste your raw logs, IoC, fanged IoC... and they will be parsed using regex.
* Check if an observable (IP, hash, domain, URL) is malicious using VirusTotal, AbuseIPDB, IPInfo, Spur.us, IP Quality Score, MDE, Google Safe Browsing, Shodan, Abusix, Phishtank (and more to come)...
* Comprehensive report with search and filter features (type, country, risk, detection, proxy/VPN).
* Uses multithreading to speed up the process (articially limited with `time.sleep()` because of free API usage).
* Performs a reverse DNS lookup.
* Checks ICANN RDAP for domain information.
* Checks abuse contacts for a IP / URL / domain (Abusix).
* Provides the ability to export the results to a CSV file and an Excel file.
* Checks if the observable has been seen on the Microsoft Defender for Endpoint (MDE) platform (your tenant).
* Uses a proxy if needed.
* Stores the results in a SQLite database.
* Provides a history of the analysis.
* Easily retrieve observable in analysis with the search function in history (highlighted results).

# Getting Started

* To get started, clone the repository

```bash
git clone https://github.com/stanfrbd/cyberbro
cd cyberbro
```

## Edit the config file (mandatory)

```
cp secrets-sample.json secrets.json
```

* Fill values (including proxy if needed) in the `secrets.json` file.

```json
{
    "virustotal": "token_here",
    "abuseipdb": "token_here",
    "ipinfo": "token_here",
    "google_safe_browsing": "token_here",
    "proxy_url": "",
    "mde_tenant_id": "tenant_here",
    "mde_client_id": "client_id_here",
    "mde_client_secret": "client_secret_here",
    "ip_quality_score": "token_here",
    "shodan": "token_here"
}
```

* To get API keys, refer to the official documentation of the services.
* MDE is NOT free, you can skip it if you don't have an account (unchecked by default).

> **Warning:** It is possible to change the config from the GUI using [http://127.0.0.1:5000/config](http://127.0.0.1:5000/config), but this endpoint is disabled by default because it is not protected. This endpoint is useful if you want to change the config without restarting the app. To activate it, set `app.config['CONFIG_PAGE_ENABLED'] = True` at the beginning of `app.py`. **This is not recommended for public or team use, because they will be able to see your API keys.**

# Launch the app

## Lazy and easy - use docker

```bash
docker compose up # use -d to run in background and use --build to rebuild the image
```

* Go to http://127.0.0.1:5000 and Enjoy.

> Don't forget to edit the `secrets.json` before building the image.

## The old way

* Clone the repository and install the requirements.

You might want to create a [`venv`](https://docs.python.org/3/library/venv.html) before installing the dependencies.

```bash
pip install -r requirements.txt
```

* Run the app with `gunicorn` (clean mode).

```bash
gunicorn -w 1 -b 0.0.0.0:5000 app:app
```

* Run the app with in development mode.

```bash
python3 app.py
```

# Screenshots

<details>
<summary>See all screenshots</summary>

![image](https://github.com/user-attachments/assets/72af5afe-d738-4b73-9c14-ee8db4713356)

![image](https://github.com/user-attachments/assets/e3dd9d26-8bd2-42df-b5b7-1b828e62f6c3)

![Capture d’écran_14-11-2024_93554_cyberbro stan local](https://github.com/user-attachments/assets/eced18ef-cab1-4056-9f59-323cf91bef3c)

![Capture d’écran_14-11-2024_93537_cyberbro stan local](https://github.com/user-attachments/assets/3afe3b1f-a7c3-4c7b-bb32-42ebf6a3f1a6)

</details>

![image](https://github.com/user-attachments/assets/479f1fc6-65df-41fe-93a6-4bf54c19a435)

# Security

**Disclaimer**: this is still a development server, not intended for production. \
Some misconfigurations may lead to **security issues**.

# API and third-party services

* [VirusTotal](https://developers.virustotal.com/v3.0/reference)
* [AbuseIPDB](https://docs.abuseipdb.com/)
* [IPInfo](https://ipinfo.io/developers)
* [Google Safe Browsing](https://developers.google.com/safe-browsing)
* [IP Quality Score](https://www.ipqualityscore.com/)
* [Microsoft Defender for Endpoint](https://docs.microsoft.com/en-us/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-for-endpoint-api)
* [Shodan](https://developer.shodan.io/)
* [Spur.us](https://spur.us/)
* [Abusix](https://abusix.com/)
* [Phishtank](https://www.phishtank.com/)
* [OpenRDAP](https://openrdap.org/api)
* [ICANN](https://lookup.icann.org/)

# License

```
        DO WHAT THE FUCK YOU WANT TO PUBLIC LICENSE 
                    Version 2, December 2004 

 Copyright (C) 2004 Sam Hocevar <sam@hocevar.net> 

 Everyone is permitted to copy and distribute verbatim or modified 
 copies of this license document, and changing it is allowed as long 
 as the name is changed. 

            DO WHAT THE FUCK YOU WANT TO PUBLIC LICENSE 
   TERMS AND CONDITIONS FOR COPYING, DISTRIBUTION AND MODIFICATION 

  0. You just DO WHAT THE FUCK YOU WANT TO.
```

