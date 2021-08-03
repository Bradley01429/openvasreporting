# OpenVAS Reporting:  

[![License](https://img.shields.io/github/license/TheGroundZero/openvasreporting.svg)](https://github.com/TheGroundZero/openvasreporting/blob/master/LICENSE)
![Known Vulnerabilities](https://snyk.io/test/github/TheGroundZero/openvasreporting/badge.svg?targetFile=requirements.txt)

A tool to convert [OpenVAS](http://www.openvas.org/) XML into reports with the ability to supply a Nmap output file to use for hostname lookups. This repo has been forked from https://github.com/TheGroundZero/openvasreporting. Commit hash: (https://github.com/TheGroundZero/openvasreporting/commit/fe25b8359933df57c2129c2b1babde966d741f18)

![Report example screenshot](docs/_static/img/OpenVASreporting.png?raw=true)

## Requirements

 - [Python](https://www.python.org/) version 3
 - [XlsxWriter](https://xlsxwriter.readthedocs.io/)
 - [Python-docx](https://python-docx.readthedocs.io)

## Installation

    # Install Python3 and pip3
    # Clone repository 
    git clone https://github.com/Bradley01429/openvasreporting
    # Open cloned to repository
    # Run command below to install the required python packages
    pip3 install -r requirements.txt
    # Install module (not required when running from repo base folder)
    pip3 install .

## Usage

    python3 -m openvasreporting -i [OpenVAS xml file(s)] [-o [Output file]] [-f [Output format]] [-l [minimal threat level (n, l, m, h, c)]] [-t [docx template]]

### Parameters

| Short param | Long param     | Description                    | Required | Default value                              |
| :---------: | :------------- | :----------------------------- | :------: | :----------------------------------------- |
| -i          | --input        | Input file(s)                  | YES      | n/a                                        |
| -o          | --output       | Output filename                | No       | openvas_report                             |
| -f          | --format       | Output format                  | No       | xlsx                                       |
| -l          | --level        | Minimal level                  | No       | n                                          |
| -t          | --template     | Docx template                  | No       | openvasreporting/src/openvas-template.docx |
| -nh         | --nmaphostname | Nmap file containing hostnames | No       | n/a                                        |

## Examples

### Create Excel report from 1 OpenVAS XML report using default settings

    python3 -m openvasreporting -i openvasreport.xml -f xlsx

### Create Excel report from 1 OpenVAS XML report using default settings nmap file for hostnames

    python3 -m openvasreporting -i openvasreport.xml -f xlsx -nh NmapResult.txt

### Create Excel report from multiple OpenVAS reports using default settings

    # Wildcard select
    python3 -m openvasreporting -i *.xml -f xlsx
    # Selective
    python3 -m openvasreporting -i openvasreport1.xml -i openvasreport2.xml -f xlsx

### Create Word report from multiple OpenVAS reports, reporting only threat level high and up, use custom template

    python3 -m openvasreporting -i *.xml -o docxreport -f docx -l h -t "/home/user/myOpenvasTemplate.docx"

### Example contents of nmap input file to use for hostnames instead of openvas reported values
    Nmap scan report for AAA.co.uk (192.171.1.12)
    Nmap scan report for BBB.co.uk (10.254.240.175)
    Nmap scan report for CCCC.test.local (10.254.230.10)

## Result

The final report (in Excel format) will then look something like this:

![Report example screenshot - Summary](docs/_static/img/screenshot-report.png?raw=true)
![Report example screenshot - ToC](docs/_static/img/screenshot-report1.png?raw=true)
![Report example screenshot - Vuln desc](docs/_static/img/screenshot-report2.png?raw=true)

Worksheets are sorted according to CVSS score and are colored according to the vulnerability level.
