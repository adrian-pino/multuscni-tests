# There is available a daemonset that cleans MultusCNI leftovers. This is useful in case of updating the Multus image or in case of experiencing a weird behaviour
# E.g: Pod with additional interface can't be deployed stating that "the interface X is already present".

# References:
# https://github.com/k8snetworkplumbingwg/multus-cni/issues/461
# https://github.com/vmware-tanzu/community-edition/pull/2728/commits/9d142764c40fae781a93eb0b975b281d60fd29c0#diff-b3bcfc2239a31ce402e523af40621d56be9deea35afe73f1c45d594bb1fc472f
