# almalinux-deploy

An EL to AlmaLinux migration tool.


## Usage

In order to convert your EL8 operating system to AlmaLinux do the following:

1. Make a backup of the system. We didn't test all possible scenarios so there
   is a risk that something goes wrong. In such a situation you will have a
   restore point.
2. Disable Secure Boot because AlmaLinux doesn't support it yet
   ([almbz#3](https://bugs.almalinux.org/view.php?id=3)). Detailed instructions
   for bare metal hardware can be found
   [here](https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/disabling-secure-boot#disable-secure-boot).
   Instructions for VMWare are available
   [here](https://docs.vmware.com/en/VMware-vSphere/6.7/com.vmware.vsphere.security.doc/GUID-898217D4-689D-4EB5-866C-888353FE241C.html).
3. Download the [almalinux-deploy.sh](almalinux-deploy.sh) script:
   ```shell
   $ curl -O https://raw.githubusercontent.com/AlmaLinux/almalinux-deploy/master/almalinux-deploy.sh
   ```
4. Run the script and check its output for errors:
   ```shell
   $ sudo bash almalinux-deploy.sh
     ...
     Migration to AlmaLinux is completed
   ```
5. Ensure that your system was successfully converted:
   ```shell
   # check release file
   $ cat /etc/redhat-release 
   AlmaLinux release 8.3 (Purple Manul)
   
   # check that the system boots AlmaLinux kernel by default
   $ sudo grubby --info DEFAULT | grep AlmaLinux
   title="AlmaLinux (4.18.0-240.el8.x86_64) 8"
   ```
6. Thank you for choosing AlmaLinux!


## Roadmap

* [x] CentOS 8 support.
* [ ] Write debug information to a log file for failed migration analysis.
* [x] Oracle Linux 8 support.
* [x] RHEL 8 support.
* [ ] DirectAdmin control panel support.
* [x] cPanel control panel support.
* [ ] Plesk control panel support (blocked from Plesk side).
* [ ] Cover all common scenarios with tests.
* [ ] Add OpenNebula support to Molecule test suite.


## Get Involved

Any contribution is welcome:

* Find and [report](https://github.com/AlmaLinux/almalinux-deploy/issues) bugs.
* Submit pull requests with bug fixes, improvements and new tests.
* Test it on different configurations and share your thoughts in
  [discussions](https://github.com/AlmaLinux/almalinux-deploy/discussions).

Technology stack:

* The migration script is written in [Bash](https://www.gnu.org/software/bash/).
* We use [Bats](https://github.com/bats-core/bats-core) for unit tests.
* Functional tests are implemented using
  [Molecule](https://github.com/ansible-community/molecule),
  [Ansible](https://github.com/ansible/ansible) and
  [Testinfra](https://github.com/pytest-dev/pytest-testinfra). Virtual machines
  are powered by [Vagrant](https://www.vagrantup.com/) and
  [VirtualBox](https://www.virtualbox.org/).

To run the functional tests do the following:

1. Install Vagrant and VirtualBox.
2. Install requirements from the requirements.txt file.
3. Run `molecule test --all` in the project root.


## License

Licensed under the GPLv3 license, see the [LICENSE](LICENSE) file for details.
