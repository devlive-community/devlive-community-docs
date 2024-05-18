[TOC]

Many Ambari users use RedHat Satellite or Spacewalk to manage Operating System repositories in their cluster. The general process to configure Ambari to work with your Satellite or Spacewalk infrastructure is to:

1. Ensure you have created channels for the [public repositories]($AccessingClouderaRepositories) that correspond to the products you intend to use.
2. Ensure the created channels are available on all machines in the cluster.
3. Install the Ambari Server and start it.
4. Before starting a cluster install, update Ambari so it knows not to delegate repository management to Satellite or Spacewalk, and use the appropriate channel names when installing or upgrading packages.

    > Please have the names of your channels on hand before proceeding.


### Next Step

[Configuring Ambari to use RedHat Satellite or Spacewalk]($ConfiguringAmbariToUseRedHatSatelliteOrSpacewalk)
