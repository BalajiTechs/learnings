Useful Equinox OSGi commands
ss (Ex: osgi> ss)
This command can be used to list all the existing bundles in the OSGi environment. Bundle ID, State and Bundle symbolic name of all the bundles are shown.

start <bundle-id> (Ex: osgi> start 16)
This command can be used to start a particular bundle. If it can’t be started, reasons are printed on the console.

stop <bundle-id> (Ex: osgi> stop 16)
This command can be used to stop a particular bundle. If it can’t be stopped, reasons are printed on the console.

b <bundle-id> (Ex: osgi> b 16)
This can be used to print all the meta data related to this bundle. That includes imported packages, exported packages, host bundle, required bundles etc.

diag <bundle-id> (Ex: osgi> diag 16)
This can be used to diagnose a particular bundle. It will show you the list of missing imported packages.

headers <bundle-id> (Ex: osgi> headers 16)
This can be used to list the headers for a particular bundle.

packages <package-name> (Ex: osgi> packages org.wso2.foo)
This can be used to list all the bundles which use the given package.

install file:<file-path> (Ex: osgi> install file:/home/temp/bundle1.jar)
This can be used to install a bundle into running OSGi environment. After installing, use ‘start’ command to activate the bundle.

uninstall <bundle-id> (Ex: osgi> uninstall 16)
This can be used to remove a bundle from the OSGi environment.

active (Ex: osgi> active)
This can be used to list all active bundles in the current instance.

refresh (Ex: osgi> refresh)
This can be used to refresh the system. All the package resolutions are refreshed when this is executed. Always refresh the system after uninstalling a bundle as a best practice.
Note : <bundle-symbolic-name> also can be used instead of <bundle-id> in above commands which uses <bundle-id> as a parameter.
