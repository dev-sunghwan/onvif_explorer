# ONVIF Explorer

ONVIF Explorer is a Flask-based web application for testing ONVIF SOAP commands through a browser GUI.

Enter camera connection details, load a WSDL URL, choose an operation, fill in the dynamically generated parameter form, and inspect both the parsed JSON result and the raw SOAP XML exchange. I built it as a practical developer and QA tool for quickly checking ONVIF behavior without needing a full certification workflow.

![ONVIF Explorer screenshot](docs/screenshot.png)

> [Korean documentation (README_ko.md)](README_ko.md)

## Why this tool?

Existing ONVIF tools solve adjacent problems, but they are not ideal for quick interactive command testing:

- **ODM (ONVIF Device Manager)** is useful for browsing devices and streams, but not for invoking arbitrary operations and inspecting raw responses.
- **ODTT (ONVIF Device Test Tool)** is aimed at conformance testing rather than day-to-day debugging.

ONVIF Explorer fills that gap by making arbitrary ONVIF operations directly testable from a lightweight browser interface.

| | ODM | ODTT | ONVIF Explorer |
|---|---|---|---|
| Interactive SOAP command test | no | no | yes |
| Raw SOAP XML visible | no | no | yes |
| Any ONVIF operation on demand | no | no | yes |
| ONVIF profile detection | no | yes | yes |
| Complexity | low | high | low |
| Target user | general users | certification engineers | developers / QA engineers |

## Quick start

### Option 1: `run.bat` on Windows

```text
Double-click run.bat
```

### Option 2: Manual setup

```bash
git clone https://github.com/dev-sunghwan/onvif_explorer.git
cd onvif_explorer
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
python app.py
```

Open `http://127.0.0.1:5000` in your browser.

## Core features

- connection test through `GetDeviceInformation`
- ONVIF profile detection through `GetServices`
- preset support for common ONVIF services plus custom WSDL URLs
- dynamic operation forms generated from XSD metadata
- raw request and response XML inspection
- command history and last-response-value reuse for faster follow-up operations

## Supported service areas

- device management
- media and media2
- PTZ
- imaging
- events and analytics
- device I/O
- recording, search, and replay
- provisioning and thermal services
- access control, door control, and credential services

## Project structure

```text
onvif_explorer/
├── app.py
├── config.py
├── onvif_client/
│   ├── wsdl_loader.py
│   ├── type_introspector.py
│   ├── command_executor.py
│   ├── serializer.py
│   └── profile_checker.py
├── templates/
└── static/
```

## Tech stack

- Python 3
- Flask
- zeep
- lxml
- Bootstrap 5
- Vanilla JavaScript

## Roadmap

- command execution history with save and replay
- raw SOAP XML direct-send mode
- richer auto-fill flows for `Set*` operations from previous responses
