# honeycombLX2
Reference for Honeycomb LX2 Board Config / Development

The attached files are tested for use with kernel-5.14.0-70.17.1.el9_0.src.rpm.

- Note that the sed line is tagging the kernel with a custom build ID so it's not confused with the original RHEL package. You can use whatever you like there.
- The wiki in this repo has the specific kernel options that were enabled. Nothing else was changed, disabled, or adjusted from the RHEL9 default. 

Download kernel-5.14.0-70.17.1.el9_0.src.rpm from RedHat
rpm -Uvh kernel-5.14.0-70.17.1.el9_0.src.rpm
cp kernel-aarch64-rhel.config ~/rpmbuild/SOURCES
cp kernel-local ~/rpmbuild/SOURCES
sed 's/# define buildid .local/%define buildid .honeycomb/g' -i ~/rpmbuild/SPECS/kernel.spec
rpmbuild -bb --with baseonly --without debuginfo kernel.spec
