# Tetration ACI Annotator

This python script pulls the information from APIC about every known IP and sends it to Tetration as an annotation.  Currently the following fields can be pushed:

#### Enabled by Default
* **ACI Bridge Domain** *(bd)*
* **ACI VRF** *(vrf)*
* **ACI Tenant** *(tenant)*
* **ACI Application Profile** *(app)*
* **ACI End Point Group** *(epg)*
* **ACI Attached Interface** *(intf)*
* **ACI Leaf** *(leaf)*

#### Disabled by Default
* **ACI MAC** *(mac)*
* **ACI Last Endpoint Move Time Stamp** *(ts)*
* **ACI EPG DN** *(epg_dn)*

This script is a derivative of the ACI End Point Tracker that is part of the ACI Toolkit.  Instead of pushing the endpoint details to a MySQL database, it pushes those details to the Tetration API:  [ACI Endpoint Tracker](https://acitoolkit.readthedocs.io/en/latest/endpointtracker.html) 


# Dependencies
ACI Toolkit is a dependency to running the script.  You can find installation instructions here: [Github: ACI Toolkit](https://github.com/datacenter/acitoolkit/blob/master/docs/source/endpointtracker.rst)

The following required packages can be installed via pip.
```
pip install tetpyclient pylru
```
# Usage

All of the arguments can be provided via the command line arguments, Environment Variables, or via interactive prompts when launching the script.

```
python3 annotations.py --help

optional arguments:
  -h, --help            show this help message and exit
  --tet_url TET_URL     Tetration API URL (ex: https://url) - Can
                        alternatively be set via environment variable
                        "ANNOTATE_TET_URL"
  --tet_creds TET_CREDS
                        Tetration API Credentials File (ex:
                        /User/credentials.json) - Can alternatively be set via
                        environment variable "ANNOTATE_TET_CREDS"
  --apic_url APIC_URL   APIC URL (ex: https://url) - Can alternatively be set
                        via environment variable "ANNOTATE_APIC_URL"
  --frequency FREQUENCY
                        Frequency to pull from APIC and upload to Tetration
  --tenant TENANT       Tetration Tenant Name - Can alternatively be set via
                        environment variable "ANNOTATE_TENANT"
  --apic_pw APIC_PW     APIC Password - Can alternatively be set via
                        environment variable "ANNOTATE_APIC_PW"
  --apic_user APIC_USER
                        APIC Username - Can alternatively be set via
                        environment variable "ANNOTATE_APIC_USER"
```

To change the annotations that are being sent to Tetration, edit the following line at the top of the script.  Order is not important.

```
config['annotations'] = ['bd','tenant','vrf','app','epg','intf','leaf']
```