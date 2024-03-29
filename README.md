# Dogged


## Overview
```Dogged``` represents a central place where we maintain information relating to getting [REX-Ray](https://github.com/emccode/rexray) into upstream Container Engine and Runtime projects.  The goal here is to provide a storage abstraction layer that can understand underlying infrastructure and storage aspects of an instance and issue the necessary control plane calls to get storage created and attached to a Container.  With this done, it should allow for composeability of the Volume feature to the general Container eco-system.

By using ```REX-Ray``` we greatly simplify how storage is managed and expose storage services at the most granular level which can enable Container and Persistence use cases further.

## Docker 1.7+
In future releases we are working on ensuring that Volume Drivers can use a remote API endpoint.  This involves abstracting the current Volume Driver implementation.  See the [PR](https://github.com/docker/docker/pull/13924) where this work is highlighted.

## Docker 1.7
This release brought to the table Volume Drivers. See the [post](http://blog.emccode.com/2015/06/22/volume-drivers-arrive-at-dockcon/) speaking about the project REX-Ray and it's native support for this feature.  


## Docker 1.4.1
Here we continued work on an existing branch that brought "Container Volumes" as proper entities into the Docker object model.  We further enhanced this a bit and added direct calls to Dogged for Volume related functionality.

This allows you to issue commands like ```docker volume create``` or ```docker volume snapshot``` which creates actual volumes on underlying storage or virtualization platforms and removes then

See the EMC {code} video playlist for Dogged and REX-Ray related videos [here](https://www.youtube.com/playlist?list=PLbssOJyyvHuWiBQAg9EFWH570timj2fxt).

Notice the [docker-1.4.1-dev-volumes-dogged](https://github.com/clintonskitson/docker/tree/docker-1.4.1-dev-volumes-dogged) branch that can be reviewed.

This is purely a proto-type as the Volume functionality is not currently in 1.6.  Now that we have a working prototype, we are hoping for broader feedback to help steer the Container Data Volume discussions.

### Commands

      docker volume ls - List volumes that have been created in Docker
      docker volume inspect - Inspect a specific volume
      docker volume create - Create a Container Data Volume
      docker volume rm - Remove a Container Data Volume
      docker volume snapshot ls
      docker volume snapshot create - Create a snapshot of a Container Data Volume
      docker volume snapshot rm - Remove a snapshot of a Container Data Volume
      docker volume snapshot cp - Copy a snapshot between regions

### Run it!

You can download the experimental Docker binary from the releases.  Load this up on a CentOS7 release (this is what we developed against, but it should work against others).

#### EC2 Example

      export AWS_ACCESS_KEY=access_key AWS_SECRET_KEY="secret_key"
      export REXRAY_STORAGEDRIVERS=ec2 (optional, but used now)
      docker-1.4.1-dev -dD --storage-driver=devicemapper
      docker volume create --name=datavol --size=50 --volumetype=io1 --iops=1000
      docker run -ti -v datavol:/data --name=persistent ubuntu


## Sub-Modules
We are leveraging sub-modules here to bring the gather the work from other repos centrally.

## State
Actively looking for other Container eco-system projects to embed REX-Ray into.  This work will further enhance the object model to ensure we have the proper abstraction, arhcitecture, and interface structure.



Licensing
---------
Licensed under the Apache License, Version 2.0 (the “License”); you may not use this file except in compliance with the License. You may obtain a copy of the License at <http://www.apache.org/licenses/LICENSE-2.0>

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an “AS IS” BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.

Support
-------
Please file bugs and issues at the Github issues page. For more general discussions you can contact the EMC Code team at <a href="https://groups.google.com/forum/#!forum/emccode-users">Google Groups</a> or tagged with **EMC** on <a href="https://stackoverflow.com">Stackoverflow.com</a>. The code and documentation are released with no warranties or SLAs and are intended to be supported through a community driven process.
