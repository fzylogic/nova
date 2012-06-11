Description
===========
Placeholder for the OpenStack Compute service `Nova` as part of the OpenStack `Essex` reference architecture using Chef. The http://github.com/opscode/openstack-chef-repo will contain documentation for using this cookbook in the context of a full OpenStack deployment.

The major components of Nova need to be separated into distinct recipes to enable moving them from a single box to multiple. A very incomplete list of likely initial recipes are things like scheduler, controller, compute, api, network and volume. The intention is to make it modular so databases, hypervisors, block storage and anything else can be replaced relatively easily.

Recipes
=======

License and Author
==================

Author:: Matt Ray (<matt@opscode.com>)

Copyright 2012 Opscode, Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

