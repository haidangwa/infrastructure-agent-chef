# newrelic-infra Cookbook CHANGELOG

This file is used to list changes made in each version of the `newrelic-infra` cookbook.

## 0.12.4 (2023-03-22)

* Removed keep_existing property from archive_file (@akashgoel92)
* Uses `remote_file` to download an integration with a remote source URL and maintain a local path with `archive_file` when the installation method is tarball (@haidangwa)

## 0.12.3 (2022-08-31)
- Update gpg key path by @rogercoll in #120

## 0.12.2 (2022-01-10)
- removed chef-workstation_21.7.524-1_amd64.deb file from the root of the cookbook

## 0.12.1 (2021-09-08)

FEATURES:

* The minimum supported Centos version is now 7.0 instead of 5.0.
## 0.12.0 (2021-08-02)

BREAKING CHANGES:

* The minimum supported Chef version is now 15+ instead of 12.5+.
* Removed `poise_service` and `poise_archive` dependencies, `agent_linux.rb` rewritten to use Chef resources instead.
* Change of creation of config file and it's location - removed `agent.yaml` and changed it to `newrelic.yml` in `/etc`.

## 0.11.0 (2019-07-04)

FEATURES:

* Add support for Amazon Linux 2.

IMPROVEMENTS:

* Add support for disabling the removal of quotes in the generated
  integration definition and config files.

## 0.10.0 (2019-05-27)

FEATURES:

* Add support for installing the agent in different linux architecture from the
  tarballs.

## 0.9.0 (2019-03-29)

IMPROVEMENTS:

* *Breaking change*: Add support for installing individual integrations. The role
  switches from the deprecated `newrelic-infra-integrations` package (which
  only included 5 integrations), to the `nri-*` individual integration
  packages. The `host_integrations` changes from a bool to a list specifying
  the names of `nri-*` integration packages to install.


## 0.8.1 (2018-11-16)

IMPROVEMENTS:

* Fix upstart config reload when running inside a Centos6 docker container

## 0.8.0 (2018-11-16)

IMPROVEMENTS:

* Add support for Centos/RHEL 5

## 0.7.2 (2018-08-24)

BUG FIXES:

* Add support for Ubuntu 18.04 (bionic)
* Fix case where `false` values were not added to configuration
* Change `require_chef_omnibus` to `product_version` in Test Kitchen config to avoid deprecation message

## 0.7.1 (2018-05-31)

BUG FIXES:

* Remove duplicate constant warning

IMPROVEMENTS:

* Update Fauxhai OS versions for tests

## 0.7.0 (2018-05-21)

IMPROVEMENTS:

* Make Yum repositories default to `:create` action instead of `[:add, :makecache]`

## 0.6.0 (2018-03-13)

FEATURES:

* SLES support

## 0.5.1 (2018-02-25)

IMPROVEMENTS:

* Pattern match on later versions of Amazon Linux

## 0.5.0 (2018-01-17)

FEATURES:

* Add `retries` attribute for packages

## 0.4.0 (2017-11-12)

FEATURES:

* Windows support

## 0.3.3 (2017-11-06)

BUG FIXES:

* Travis deploy was not honoring the chefignore file

## 0.3.2 (2017-11-06)

IMPROVEMENTS:

* Cookbook is automatically deployed to [Chef Supermarket](https://supermarket.chef.io/cookbooks/newrelic-infra)

## 0.3.1 (2017-10-23)

IMPROVEMENTS:

* Add .kitchen.dokken.yml to allow Test Kitchen tests in Docker
* Add .travis.yml to run tests in Travis CI
* Typo fixes
* Change "LWRP" to "custom resource" in documentation
* Automatically deploy with Travis CI to supermarket

## 0.3.0 (2017-10-18)

BREAKING CHANGES:

* The minimum supported Chef version is now 12.15+ instead of 12.14+.
* The prefix name for custom on-host integrations has been changed to use the name of the Chef resource instead of the integration name since the New Relic Infrastructure API does not accept prefix names with `.`'s.

FEATURES:

* Add `sensitive` to all configuration file resources as well as associated unit testing for the `sensitive` property.

BUG FIXES:

* Remove the use of `Hash#compact`, which only works with Ruby >= 2.4. No versions of Chef 12.x ship with a version of Ruby this new. Replace with monkey patched method `Hash.delete_blank` ([#18](https://github.com/newrelic/infrastructure-agent-chef/issues/18)).
* Modify the generated YAML configuration files to generate a format that is compatible with the Infrastructure agent's Go YAML parser ([#19](https://github.com/newrelic/infrastructure-agent-chef/issues/19)).

## 0.2.0 (2017-10-16)

FEATURES:

* Add `sensitive` to agent configuration file resource

## 0.1.0 (2017-10-12)

NOTE: Versions prior to 0.1.0 were not tagged or released on the [Chef supermarket](https://supermarket.chef.io).

BREAKING CHANGES:

* *Attribute namespace changed:* The top-level attribute key was changed from `newrelic-infra` to `newrelic_infra` in order to be used as both strings and symbols.
* Only `chef-client` versions `>= 12.14` are supported.
* Lots of attribute changes to help simplify configuration generation. See [README.md](README.md) for more details.

FEATURES:

* **Testing added:** Unit and integration tests added. See the [CONTRIBUTING][3] guide for more details.
* **newrelic\_infra\_integration LWRP added:** An LWRP for installing and configuring custom New Relic Infrastructure on-host integrations. Custom integrations can also be installed using by including the default recipe and the appropriate attributes.
* **New Relic On-Host integrations:** Added the capability to install and configure the New Relic provided on-host integrations. See the [README.md](README.md) for more details on what attributes to set.

IMPROVEMENTS:

* Updated the apt and YUM repository resources to use metaprogramming. This allows all properties available for each of the respective resources to be available as attributes.
* Resolved all Rubocop and Foodcritic violations.
