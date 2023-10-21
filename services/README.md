Shared Helm Charts
==================

The services described in helm charts in this folder should be installed
once per beamline or accelerator domain. At present these are only versioned
via the appVersion and Version fields in Chart.yaml and these values should
be updated manually when changing these charts.

Current charts are:

- shared: sets up the PVCs that all IOCs may use. These should be set up
  once and not deleted as they hold data for IOCs. All of the PVCs have
  a folder hierarchy with the names of IOCs at the root.

  - autosave data: for IOCs that support autosave. This is separate from IOC
    helm charts so that it can survive deletion and re-creation of an IOC.

  - opis: all the OPI files for engineering screens that an IOC supplies are
    saved here. This is stored in a single PVC so that the opis service
    can publish them over http for access by an OPI client.

- opis: installs the web server that shares the engineering screens published
  by each IOC. The structure is two deep only: IOC names as folders at the root
  containing all the IOCs OPI files in a flat list.