# honeycombLX2
Reference for Honeycomb LX2 Board Config / Development

The attached files are intended for use with kernel-5.14.0-70.17.1.el9_0.src.rpm.

General build process -

rpm -Uvh kernel-5.14.0-70.17.1.el9_0.src.rpm
cp kernel-aarch64-rhel.config ~/rpmbuild/SOURCES
cp kernel-local ~/rpmbuild/SOURCES
sed 's/# define buildid .local/%define buildid .honeycomb/g' -i ~/rpmbuild/SPECS/kernel.spec
rpmbuild -bb --with baseonly --without debuginfo kernel.spec
