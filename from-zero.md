# From Zero

## Prerequisites

See the 3scale toolbox image in the Red Hat Ecosystem Catalog. You must have a Red Hat registry service account. The examples in this topic assume that you have Podman installed.

## Install Procedure

Log in to the Red Hat Ecosystem Catalog:
~~~
$ podman login registry.redhat.io
Username: ${REGISTRY-SERVICE-ACCOUNT-USERNAME}
Password: ${REGISTRY-SERVICE-ACCOUNT-PASSWORD}
Login Succeeded!
~~~
Pull the toolbox container image:
~~~
$ podman pull registry.redhat.io/3scale-amp2/toolbox-rhel8:3scale2.13
~~~
Verify the installation:
~~~
$ podman run registry.redhat.io/3scale-amp2/toolbox-rhel8:3scale2.13 3scale help
~~~

## Environment Setup

Create personal access tokens and set an environment variable for ease of use with the demo.

1. Log into your source 3scale instance
1. Go to Account Settings > Personal > Tokens
1. Click 'Add Access Token'
    1. Provide a descriptive name for the token
    1. For the purposes of the demo select all 4 'Scope' checkboxes
    1. Set the 'Permissions' to 'Read & Write'
    1. Click 'Create Access token'
    1. Save this value somewhere safe, it will only be displayed this one time
1. On your server create an environment variable called SOURCE
    ~~~
    export SOURCE="https://<TOKEN>@<TENANT>-admin.<WILDCARD_DOMAIN>"
    ~~~
1. Repeate Steps 1-3 on the destination 3scale instance
1. Create a second environment variable called DEST
    ~~~
    export DEST="https://<TOKEN>@<TENANT>-admin.<WILDCARD_DOMAIN>"
    ~~~

## Alias the toolbox command

For shorthand, create an alias that contains the needed podman options for ease of use during the demo.

~~~
$ alias toolbox='podman run -u root -v $PWD:/tmp:Z -w=/tmp registry.redhat.io/3scale-amp2/toolbox-rhel8:3scale2.13'
~~~

This will mount the current user director as /tmp inside the container and set the container user's working directory to /tmp. The :Z flag tells podman to relable the volume's content to match the label inside the container, which is a simple way to satisfy SELinux.

You should now be able to verify your setup with these commands using the new alias:

~~~
$ toolbox 3scale help
$ toolbox ls -al
~~~

## Next Steps

Now that you have a working instance of the 3scale toolbox available to you, proceed to [Querying remote 3scale instances](querying-remotes.md).