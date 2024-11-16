This page covers the setup of [Home Assistant](https://www.home-assistant.io/) to deploy in [my](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/external/jellyfin.yaml) docker-compose stack(s).

# Setup

## Initial Setup of Home Assistant

Enter username and password as shown.

Navigate to Settings at the bottom left, Integrations, and add the following:

- Unifi, Unifi Protect
- Honeywell Total Connect Comfort (US)
- National Weather Service (NWS)
  - Select the NWS Integration, Entities, and Enable the following:
    - {METAR}_temperature and {METAR}_humidity
