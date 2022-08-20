# SolidRun Honeycomb LX2 with RHEL 9
Reference for using Red Hat Enterprise Linux 9 with the Honeycomb LX2 Board.

The attached files are tested for use with kernel-5.14.0-70.17.1.el9_0.src.rpm.

- The sed line below is just tagging the kernel with a custom build ID so it's not confused with the original RHEL package. You can use whatever you like there.
- The wiki in this repo has the specific kernel options that were enabled. Nothing else was changed, disabled, or adjusted from the RHEL9 default. 

### Kernel Build Process
```
yum install yum-utils
yumdownloader --source kernel (downloads kernel src RPM from RedHat)
rpm -Uvh kernel-5.14.0-70.17.1.el9_0.src.rpm
cp kernel-aarch64-rhel.config ~/rpmbuild/SOURCES
cp kernel-local ~/rpmbuild/SOURCES
sed 's/# define buildid .local/%define buildid .honeycomb/g' -i ~/rpmbuild/SPECS/kernel.spec
rpmbuild -bb --with baseonly --without debuginfo kernel.spec
```

### Useful References
- [I need to build a custom kernel](https://webcache.googleusercontent.com/search?q=cache:81CW9A9VGTsJ:https://wiki.centos.org/HowTos/Custom_Kernel+&cd=1&hl=en&ct=clnk&gl=us)
- [Building a custom kernel/Source RPM](https://fedoraproject.org/wiki/Building_a_custom_kernel/Source_RPM)
- [SolidRun HoneyComb/Clearfog ARM Workstation Up-and-running](https://carlosedp.medium.com/solidrun-honeycomb-arm-up-and-running-56b3de896143)
- [Discord thread on kernel options](https://discord.com/channels/620838168794497044/665456384971767818/993157487643590776)
- [Fedora Aarch64 on the SolidRun HoneyComb LX2K](https://fedoramagazine.org/fedora-aarch64-on-the-solidrun-honeycomb-lx2k/)
- [Rocking a 16 core ARM workstation for data analysis and NAS – HoneyComb LX2K](https://mightynotes.wordpress.com/2020/02/29/rocking-a-16-core-arm-workstation-for-data-analysis-and-nas-honeycomb-lx2k/)
- [LX2160A Software](https://solidrun.atlassian.net/wiki/spaces/developer/pages/197494345/LX2160A+Software#using-the-built-in-nics)
