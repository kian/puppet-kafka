# Change log

## 2.0.1 (unreleased)

* TBD


## 2.0.0 (April 09, 2014)

IMPROVEMENTS

* Simplify how this module is configured in Hiera, at the expense of breaking backwards compatibility by removing the
  feature to run multiple broker instances on the same machine.
* Introduces `config.pp`.
* The functionality of the previous `broker.pp` code was split into `install.pp`, `config.pp`, and `service.pp`.
  Parameters are now exclusively defined through `init.pp`, with defaults in `params.pp`.
* Adds more unit tests.

BACKWARDS INCOMPATIBILITY

* Remove support for running multiple Kafka broker instances on the same box.
    * As part of this change the functionality of the defined type `kafka::broker` was merged into `kafka::service`.
* Remove `$kafka::global_config_map` `$kafka::broker::config_map` parameters, which have been superceded by
  `$kafka::config_map`.
* Default value of `$log_dirs` changed from `['/app/kafka-broker-0']` to `['/app/kafka/log']`
* The broker ID index suffix was removed from various configuration and log files.  Examples:
    * `server-0.properties` becomes `server.properties`.
    * `log4j-0.properties` becomes `log4j.properties`.
    * `daemon-gc-0.log` becomes `daemon-gc.log`.
    * `state-change-0.log` becomes `state-change.log`.
    * And so on.
* Default value of `$tmpfs` changed from `/tmpfs-0` to `/tmpfs`.
* The supervisord service name does not include the broker ID anymore because we do not support multiple broker
  instances per target machine.  For instance, the default service name is changed from `kafka-broker-0` to
  `kafka-broker`.


## 1.0.7 (April 09, 2014)

IMPROVEMENTS

* Add `$kafka::global_config_map` to facilitate sharing Kafka config settings between broker instances.


## 1.0.6 (April 08, 2014)

IMPROVEMENTS

* Remove `puppetlabs/stdlib` from `Modulefile` to decouple us from PuppetForge.


## 1.0.5 (March 25, 2014)

IMPROVEMENTS

* Add experimental support to write Kafka (data) log files to a tmpfs mount.  See the new class parameters
  `$tmpfs_manage` (default: false), `$tmpfs_path`, and `$tmpfs_size` in `broker.pp`.  Note that you want to use tmpfs
  only in rare scenarios.


## 1.0.4 (March 24, 2014)

IMPROVEMENTS

* Add `compile` test for `kafka::broker`.


## 1.0.3 (March 17, 2014)

IMPROVEMENTS

* Add `$user_manage` and `$group_manage` parameters.
* Add more unit tests.


## 1.0.2 (March 14, 2014)

IMPROVEMENTS

* Initial support for testing this module.
    * A skeleton for acceptance testing (`rake acceptance`) was also added.

BACKWARDS INCOMPATIBILITY

* Change default value of `$package_ensure` from "latest" to "present".
* Puppet module fails if run on an unsupported platform.  Currently we only support the RHEL OS family.

BUG FIXES

* Properly generate broker configuration when multiple directories are specified for `$log_dirs`.


## 1.0.1 (March 11, 2014)

IMPROVEMENTS

* Recursively create directories defined via `$log_dirs` if needed.


## 1.0.0 (February 25, 2014)

* Initial release.

