# Packer

**Contents** [TL;DR] | [Overview] | [Getting started] | [Usage] | [Next steps] | [Contributing] | [Resources]  

This repository contains common [Packer] helper tools and sample templates of [Visual Studio], [Docker], [IIS] and [SQL Server] on [Windows] and [Ubuntu], building virtual machine images and [Vagrant] boxes for [VirtualBox], [Hyper-V] and [AWS], provisioned with [Chef].

## TL;DR

- [Vagrant boxes] ready to use for virtualizing the development and hosting scenarios.
- [Blog] with an overview of the why, how and what of Packer.
- [Virtual workstations] for automating the configuration of your development environment.

[TL;DR]: #tldr

## Overview

**Contents** [Operating systems] | [Development] | [Hosting]  

> **Note** This section covers the details of the published [Vagrant boxes] this repository builds. See the [Getting started] section to build your own virtual machine images. See [this blog][Blog] for more background and motivation and [virtual workstations] for samples of automating the configuration of your development environment.  

This repository contains [Packer] sample template for the following virtualization scenarios:

- [Operating systems] for generic experiments with [Windows] and [Ubuntu].
- [Development] using [Visual Studio].
- [Hosting] using [Docker], [IIS] and [SQL Server].

The virtual machine images and [Vagrant] boxes are built for [VirtualBox], [Hyper-V] - supporting [nested virtualization] - and [AWS], and are provisioned using [Chef].

> **Note** All the components, including the core operating systems, share the following characteristics:
> 
> * They are based on their publicly available versions. You might need to provide your own license(s) (for example, a valid Windows or Visual Studio license) to start or keep using them after their evaluation periods expire.
> * They are installed using their latest available versions. The latest patches (for example, all the Windows Updates) are applied as well.
> * Unless noted otherwise, they are installed using the default configuration options.

[Overview]: #overview

[Vagrant boxes]: https://app.vagrantup.com/gusztavvargadr/
[Blog]: https://bit.ly/wdywttt5
[Virtual workstations]: https://github.com/gusztavvargadr/workstations/

[Packer]: https://www.packer.io/
[Vagrant]: https://www.vagrantup.com/
[VirtualBox]: https://www.virtualbox.org/
[Hyper-V]: https://en.wikipedia.org/wiki/Hyper-V
[Nested virtualization]: https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/user-guide/nested-virtualization
[AWS]: https://aws.amazon.com/
[Chef]: https://www.chef.sh/

### Operating systems

The following Vagrant boxes can be used for generic expirments on the respective platforms.

They contain the core operating system with the minimum configuration required to make Vagrant work, and some of the commonly used tools installed and options configured for easier provisioning. All the other Vagrant boxes below are based on these configurations as well.

[Operating systems]: #operating-systems

#### Windows

- [**Windows 10 Enterpise**][w10e]
- [**Windows Server 2016 Standard**][w16s]
- [**Windows Server 2016 Standard Core**][w16sc]

[Windows]: #windows

[w10e]: https://app.vagrantup.com/gusztavvargadr/boxes/w10e/
[w16s]: https://app.vagrantup.com/gusztavvargadr/boxes/w16s/
[w16sc]: https://app.vagrantup.com/gusztavvargadr/boxes/w16sc/

#### Ubuntu

- [**Ubuntu 16 Server**][u16s]

[Ubuntu]: #ubuntu

[u16s]: https://app.vagrantup.com/gusztavvargadr/boxes/u16s/

### Development

The following Vagrant boxes can be used for development scenarios including setting up [virtual workstations].

They contain the respective development tools with the common configuration and are based on the core [operating systems].

[Development]: #development

#### Visual Studio

- [Windows 10 Enterpise, Docker Community, **Visual Studio 2017 Community**][w10e-dc-vs17c]

[Visual Studio]: #visual-studio

[w10e-dc-vs17c]: https://app.vagrantup.com/gusztavvargadr/boxes/w10e-dc-vs17c/

### Hosting

The following Vagrant boxes can be used for hosting scenarios.

They contain the respective hosting tools with the default configuration are based on the core [operating systems].

[Hosting]: #hosting

#### Docker

- [Windows 10 Enterpise, **Docker Community**][w10e-dc]
- [Windows Server 2016 Standard, **Docker Enterprise**][w16s-de]
- [Windows Server 2016 Standard Core, **Docker Enterprise**][w16sc-de]
- [Ubuntu 16 Server, **Docker Community**][u16s-dc]

[Docker]: #docker

[w10e-dc]: https://app.vagrantup.com/gusztavvargadr/boxes/w10e-dc/
[w16s-de]: https://app.vagrantup.com/gusztavvargadr/boxes/w16s-de/
[w16sc-de]: https://app.vagrantup.com/gusztavvargadr/boxes/w16sc-de/
[u16s-dc]: https://app.vagrantup.com/gusztavvargadr/boxes/u16s-dc/

#### IIS

- [Windows Server 2016 Standard, **IIS**][w16s-iis]

[IIS]: #iis

[w16s-iis]: https://app.vagrantup.com/gusztavvargadr/boxes/w16s-iis/

#### SQL Server

- [Windows Server 2016 Standard, **SQL Server 2014 Developer**][w16s-sql14d]
- [Windows Server 2016 Standard, **SQL Server 2017 Developer**][w16s-sql17d]

[SQL Server]: #sql-server

[w16s-sql14d]: https://app.vagrantup.com/gusztavvargadr/boxes/w16s-sql14d/
[w16s-sql17d]: https://app.vagrantup.com/gusztavvargadr/boxes/w16s-sql17d/

## Getting started

> **Note** The rest of this document covers the details of building virtual machine images and Vagrant boxes, and assumes that you are familiar with the basics of [Packer]. If that's not the case, it's recommended that you take a quick look at its [getting started guide][PackerGettingStarted].  

> **Note** Building the Packer templates have been tested on Windows hosts only, but they are supposed to run on any other platform as well, given that the actual virtualization provider (e.g. VirtualBox) supports it. [Let me know][Contributing] if you encounter any issues and I'm glad to help.  

Follow the steps below to install the required tools:

1. Install [Packer][PackerInstallation].
1. Install the [Chef Development Kit][ChefDKInstallation].
1. Install the tools for the virtualization provider you want to use.
    - **VirtualBox** Install [VirtualBox][VirtualBoxInstallation].
    - **Hyper-V** Enable [Hyper-V][HyperVEnabling].
    - **AWS** Install the [AWS Command Line Interface][AWSCLIInstallation] and [configure a profile][AWSCLIProfile].

You are now ready to build a virtual machine image and a Vagrant box.

> **Note** It is recommended to set up [caching for Packer][PackerCaching], so you can reuse the downloaded resources (e.g. OS ISOs) across different builds. Make sure you have a bunch of free disk space for the cache and the build artifacts.  

[Getting started]: #getting-started

[PackerGettingStarted]: https://www.packer.io/intro/getting-started/install.html
[PackerInstallation]: https://www.packer.io/docs/install/index.html
[ChefDKInstallation]: https://downloads.chef.io/chefdk/
[VirtualBoxInstallation]: https://www.virtualbox.org/wiki/Downloads/
[HyperVEnabling]: https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v
[AWSCLIInstallation]: https://aws.amazon.com/cli/
[AWSCLIProfile]: http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html
[PackerCaching]: https://www.packer.io/docs/other/environment-variables.html#packer_cache_dir

## Usage

**Contents** [Building base images] | [Building images for distribution] | [Chaining builds further] | [Testing] | [Cleaning up]

This repository uses some [custom wrapper scripts][SourceCoreCake] using [Cake] to generate the Packer templates and the related resources (e.g. the unattended install configuration) required to build the virtual machine images. Besides supporting easier automation, this approach helps with reusing parts of the templates and the
related resources, and makes chaining builds and creating new configurations quite easy.

[Usage]: #usage

[SourceCoreCake]: src/core/cake/
[Cake]: http://cakebuild.net/

### Building base images

Clone this repo [including the submodules][GitCloneRecursive], and navigate to the root directory of the clone using PowerShell. Type the following command to list all the available templates you can build:

```powershell
PS> .\ci.ps1 [info]
```

The output will be contain the section `packer-info` with the list of the templates:

```
...
========================================
packer-info
========================================
Executing task: packer-info
w10e-virtualbox-core: Info
w10e-virtualbox-sysprep: Info
w10e-hyperv-core: Info
w10e-hyperv-sysprep: Info
w10e-dc-virtualbox-core: Info
w10e-dc-virtualbox-sysprep: Info
w10e-dc-hyperv-core: Info
w10e-dc-hyperv-sysprep: Info
...
w16s-virtualbox-core: Info
w16s-virtualbox-sysprep: Info
w16s-hyperv-core: Info
w16s-hyperv-sysprep: Info
w16s-amazon-sysprep: Info
w16s-dc-virtualbox-core: Info
w16s-dc-virtualbox-sysprep: Info
w16s-dc-hyperv-core: Info
w16s-dc-hyperv-sysprep: Info
w16s-iis-virtualbox-core: Info
w16s-iis-virtualbox-sysprep: Info
w16s-iis-hyperv-core: Info
w16s-iis-hyperv-sysprep: Info
...
```

You can filter this further to list only the templates for a given virtual machine image type. For example, to list the templates based on the `Windows Server 2016 Standard` image, invoke the `info` command with the `w16s` argument:

```powershell
PS> .\ci.ps1 info w16s
```

You can use this filtering with all the `ci.ps1` commands below as well. It selects all the templates which contain the specified argument as a substring, so you can filter for components (`w10e`, `w16s`, `iis`, etc.) or providers (`virtualbox`, `hyperv`, `amazon`) easily.  

The output will contain only the matching templates:

```
...
========================================
packer-info
========================================
Executing task: packer-info
w16s-virtualbox-core: Info
w16s-virtualbox-sysprep: Info
w16s-hyperv-core: Info
w16s-hyperv-sysprep: Info
...
```

This means that this configuration supports building some base images (`virtualbox-core`, `hyperv-core`) mainly for reusing them in other configurations, and also boxes for distribution (`virtualbox-sysprep`, `hyperv-sysprep`). Under the hood, the `sysprep` configurations will simply start from the output of the `core` ones, so build times can be reduced significantly.

Now, invoke the `restore` command with the name of the template you want to build to create the resources required by Packer. For example, for VirtualBox, type the following command:

```powershell
PS> .\ci.ps1 restore w16s-virtualbox-core
``` 

This will create the folder `build/w16s/virtualbox-core` in the root of your clone with all the files required to invoke the Packer build. This setup is self-contained, so you can adjust the parameters manually in `template.json` or the other resources and / or even copy it to a different machine and simply invoke `packer build template.json` there. Most of the time though, you just simply want to build as it is, as the templates are already preconfigured with some reasonable defaults. This can be done of course with the build script as well:

```powershell
PS> .\ci.ps1 build w16s-virtualbox-core
```

This will trigger the Packer build process, which usually requires only patience. Depending on the selected configuration, a few minutes or hours later, the build output will be created, in this case in the `build/w16s/virtualbox-core/output` directory in the root of your clone. Virtual machine images like this can be directly used with the respective virtualization provider or Vagrant on the host machine.

[Building base images]: #building-base-images

[GitCloneRecursive]: https://stackoverflow.com/a/4438292

### Building images for distribution

As mentioned above, based on Packer's support for starting builds from some virtualization providers' native image format, builds can reuse the output of a previous build. To build and image which can be distributed (e.g. after applying [Sysprep] as well), type the following command:

```powershell
PS> .\ci.ps1 build w16s-virtualbox-sysprep
```

Note that this will include restoring the build folder with the template and the related resources automatically, and then invoking the build process in a single step. It will also reuse the output of the `w16s-virtualbox-core` build, so it does not need to do the same steps for a Vagrant box the original build already included (e.g. the core OS installation itself, installing Windows updates, etc.). Once the build completes, the native image and the Vagrant box will be available in the `build/w16s/virtualbox-sysprep/output` folder.

The same approach works for Hyper-V as well:

```powershell
PS> .\ci.ps1 build w16s-hyperv-core
PS> .\ci.ps1 build w16s-hyperv-sysprep
```

As you can expect, for these samples the build artifacts will be created in the `builds/w16s` folder as well, this time under the `hyperv-sysprep/output` subfolder. You can use the standard options to [distribute them][VagrantDistribute] to be consumed in Vagrant.

[Building images for distribution]: #building-images-for-distribution

[Sysprep]: https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation
[VagrantDistribute]: https://www.vagrantup.com/docs/boxes/base.html#distributing-the-box

### Chaining builds further

Similarly to the process above, you can use build chaining to build more complex boxes. For example, the configuration for `Windows Server 2016 Standard` with `IIS` can be built like this:

```powershell
PS> .\ci.ps1 build w16s-virtualbox-core
PS> .\ci.ps1 build w16s-iis-virtualbox-core
PS> .\ci.ps1 build w16s-iis-virtualbox-sysprep
```

As in the previous `w16s` sample, for this configuration the `w16s-iis-virtualbox-core` build will start from the output of `w16s-virtualbox-core` instead of starting with the core OS installation. Chanining builds like this has no limitations, so you can use this approach to build images with any number of components very effectively.

Note that the script can invoke the build of the dependencies automatically, so for the previous example you can simply type:

```powershell
PS> .\ci.ps1 build w16s-iis-virtualbox-sysprep --recursive=true
```

This will in turn invoke the `restore` and `build` stages for the `w16s-virtualbox-core` and `w16s-iis-virtualbox-core` images as well. By default, `restore` and `build` is skipped if the output from a previous build exists. You can force the build to run again using the `rebuild` command instead, which will `clean` the build directories first.

Again, this works for Hyper-V as well:

```powershell
PS> .\ci.ps1 build w16s-iis-hyperv-sysprep --recursive=true
```

Similarly, this will in turn build the `w16s-hyperv-core` and `w16s-iis-hyperv-core` images first if they are missing.

[Chaining builds further]: #chaining-builds-further

### Testing

To help testing the build results, the reposiory contains a simple [Vagrantfile] to create virtual machines using directly the build outputs.

For example, to test the `w16s` configuration, from the root of your clone you can type the following command to use the box files in the `build\w16s` folder:

```powershell
PS> vagrant up w16s-local
```

This will import the locally built Vagrant box with the name `w16s-local` and will use that to spin up a new virtual machine for testing.

When working with multiple virtualization providers, you can specify which one to use for each test machine [using the command line][VagrantCLIUpProvider], or [define your preferences globally][VagrantPreferredProviders].

You can use the standard Vagrant commands to [clean up the boxes][VagrantCLIBox] after testing.

[Testing]: #testing

[Vagrantfile]: Vagrantfile
[VagrantCLIUpProvider]: https://www.vagrantup.com/docs/cli/up.html#provider-x
[VagrantPreferredProviders]: https://www.vagrantup.com/docs/other/environmental-variables.html#vagrant_preferred_providers
[VagrantCLIBox]: https://www.vagrantup.com/docs/cli/box.html

### Cleaning up

Though the `build` folders are excluded by default from the repository, they can consume significant disk space. You can manually delete the folders, but the build script provides support for this as well:

```
PS> .\ci.ps1 clean w16s-iis-virtualbox-sysprep
```

Using the filtering, to clean up the artifacts of all the VirtualBox builds, you can type:

```powershell
PS> .\ci.ps1 clean virtualbox
```

Omitting this parameter will apply the command to all the templates, so the following command will clean up everything:

```powershell
PS> .\ci.ps1 clean
```

> **Note** The `clean` command removes only the Packer build templates and artifacts, the eventually imported Vagrant boxes and virtual machines need to be removed manually.  

[Cleaning up]: #cleaning-up

## Next steps

Take a look at the repository of [virtual workstations] to easily automate and share your development environment configurations using the Vagrant boxes above.

[Next steps]: #next-steps

## Contributing

<!--
> **Note** This section assumes you are familiar with the basics of [Chef]. If that's not the case, it's recommended that you take a quick look at its [getting started guide][ChefGettingStarted].

TODO: custom template and build
-->

Feedback, please - [issues] or [pull requests] are welcome and are greatly appreciated. Chek out the [milestones] for the list of planned releases.

[Contributing]: #contributing

[Issues]: https://github.com/gusztavvargadr/packer/issues/
[Pull requests]: https://github.com/gusztavvargadr/packer/pulls/
[Milestones]: https://github.com/gusztavvargadr/packer/milestones/ 

## Resources

This repository could not exist without the following great tools:

- [Packer]
- [Vagrant]
- [VirtualBox]
- [Hyper-V]
- [AWS]
- [Chef]

This repository borrows awesome ideas and solutions from the following sources:

- [Matt Wrock]
- [Jacqueline]
- [Joe Fitzgerald]
- [Boxcutter]
- [Bento]

[Resources]: #resources

[Matt Wrock]: https://github.com/mwrock/packer-templates/
[Jacqueline]: https://github.com/jacqinthebox/packer-templates/
[Joe Fitzgerald]: https://github.com/joefitzgerald/packer-windows/
[Boxcutter]: https://github.com/boxcutter/windows/
[Bento]: https://github.com/chef/bento/
