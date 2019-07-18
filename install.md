# Install Service Catalog into OpenShift 4.x

## Download the installer

Locate good builds here:  https://openshift-release.svc.ci.openshift.org/

Use the **Download the installer** link to get the correct installer binary to
install the latest code.

Click the linux installer, should be something like
`openshift-installer-linux-4.1...tar.gz`. Extract to a desired directory.


Use builds from:

**4.1.x-x.ci**: You want to test code that hasn't been built by OCP yet<br/>
**4.1.x-x.nightly**: You want to test code that customers will get if we shipped today.

## Get the auth secret

   * Get auth secret from https://cloud.redhat.com/openshift/install
   * Search for **Pull Secret**
   * Click **Download Pull Secret**.  It will look something like:

```
{"auths":{"cloud.openshift.com":{"auth":"b3BlbnNoaWZ0LXJlbGVhc2UtZGV2K2phYm95ZHJlZGhhdGNvbTFkdHlqZTBzbXpqNGljZHNqNHdvcXRqZ3l4azoyNU5LSzVaR1gyVTZMSVIyWVJKT0lCWlZCNUM1RjJNN0VJWTRLMlMwNENMTlpLRURQMjRIRTlBRU9LVTVRSkcx","email":"jaboyd@redhat.com"},"quay.io":{"auth":"b3BlbnNoaWZ0LXJlbGVhc2UtZGV2K2phYm95ZHJlZGhhdGNvbTFkdHlqZTBzbXpqNGljZHNqNHdvcXRqZ3l4azoyNU5LSzVaR1gyVTZMSVIyWVJKT0lCWlZCNUM1RjJNN0VJWTRLMlMwNENMTlpLRURQMjRIRTlBRU9LVTVRSkcx","email":"jaboyd@redhat.com"},"registry.connect.redhat.com":{"auth":"NTE5MzUzMzZ8dWhjLTFEdFlqRTBzTXpqNEljZHNqNFdvcXRKR1lYazpleUpoYkdjaU9pSlNVelV4TWlKOS5leUp6ZFdJaU9pSXhaR1JpWm1abU1URmhNV0kwWm1JMlltWm1OekprWVRSbVlqUXlZMlF3TlNKOS5PYW9zTERkc0F0S25wR2xWSlpMU3VTTExSUzJmb1dKeFRKQnF5Y2Z0OGU5WlFLOGMzT3hzdXVNSzNMY1FWLXFKTVN4Q2dBYUdJanBwSXkzQVpkYi1iNUw1R2djU3lPLVpyeWxFblJnZGtkQlBaNzk4cU0xcHNxajkyVGxaejJ6OWZBcW9PSTVWbTZIZU10cF92NHczeUkyZF9KMnc1MjAzVC1iRDVGX2NLd3dBU0dpdXdyZ3BLV09vWjhvNjdRV2U0V0U5Nnc5ZEpNYV9tQnVlYnVHRjN4NGQxdEl5ck1KMXNHNnk3SkplRlBUNnI0Q3Ewc1NpcXBVTGc5TnVYNllIZUdYY1BNQUtXdDZZZDZOUnJwZi1NWTVXV3lWZW1RR204SWFwWVVqLU5XbDhVa2plZ2hpNDRyYUs3dG9DTEktNklTZXJHTUxaTnQzam4wNmF3UzRFVTN1dWxzd1VFaV9QdEVNLUZ4RDVNYmxycnpNUGhCN1d0UTFLaXh2U3lxdUY0Qk9FZ0hPSko5Z2pzWWEwcU10dUx1TVJyVUZVd0dBdElETDhzd2h1c0F1ZjRwaDlLOEhmT3FYR2J5MjcyTl91SnBHLV9IRjhnMmlOLWVvbEcwRjNXTG9rM0hES0RfX3Zud0d0QllmSjYxZ1NJMWJ5NTA0dFF1NlhKVkR0SmpWVEhQcl9MOUtEU3pxOThCcEFpZTVHNTF3Tlp2UFFMUWZWU0RqMnUwMTdiR3N2RnlBX1p3cHJ3bEhHYkFqRnZQeWhvMndEdGMyMGpVT3lJM2hrQWNTZTI4NkFxTXpjdnprNnh5Tlg3VHhvYW5KeGRSN2xUZjR3eVJtSEYyNVJlTHYySFlpNGJwakRxVU9yUW9Icmd2cFdPZTZnVDJ4SUFad1BlUjlxZmxNdmFBWQ==","email":"jaboyd@redhat.com"},"registry.redhat.io":{"auth":"NTE5MzUzMzZ8dWhjLTFEdFlqRTBzTXpqNEljZHNqNFdvcXRKR1lYazpleUpoYkdjaU9pSlNVelV4TWlKOS5leUp6ZFdJaU9pSXhaR1JpWm1abU1URmhNV0kwWm1JMlltWm1OekprWVRSbVlqUXlZMlF3TlNKOS5PYW9zTERkc0F0S25wR2xWSlpMU3VTTExSUzJmb1dKeFRKQnF5Y2Z0OGU5WlFLOGMzT3hzdXVNSzNMY1FWLXFKTVN4Q2dBYUdJanBwSXkzQVpkYi1iNUw1R2djU3lPLVpyeWxFblJnZGtkQlBaNzk4cU0xcHNxajkyVGxaejJ6OWZBcW9PSTVWbTZIZU10cF92NHczeUkyZF9KMnc1MjAzVC1iRDVGX2NLd3dBU0dpdXdyZ3BLV09vWjhvNjdRV2U0V0U5Nnc5ZEpNYV9tQnVlYnVHRjN4NGQxdEl5ck1KMXNHNnk3SkplRlBUNnI0Q3Ewc1NpcXBVTGc5TnVYNllIZUdYY1BNQUtXdDZZZDZOUnJwZi1NWTVXV3lWZW1RR204SWFwWVVqLU5XbDhVa2plZ2hpNDRyYUs3dG9DTEktNklTZXJHTUxaTnQzam4wNmF3UzRFVTN1dWxzd1VFaV9QdEVNLUZ4RDVNYmxycnpNUGhCN1d0UTFLaXh2U3lxdUY0Qk9FZ0hPSko5Z2pzWWEwcU10dUx1TVJyVUZVd0dBdElETDhzd2h1c0F1ZjRwaDlLOEhmT3FYR2J5MjcyTl91SnBHLV9IRjhnMmlOLWVvbEcwRjNXTG9rM0hES0RfX3Zud0d0QllmSjYxZ1NJMWJ5NTA0dFF1NlhKVkR0SmpWVEhQcl9MOUtEU3pxOThCcEFpZTVHNTF3Tlp2UFFMUWZWU0RqMnUwMTdiR3N2RnlBX1p3cHJ3bEhHYkFqRnZQeWhvMndEdGMyMGpVT3lJM2hrQWNTZTI4NkFxTXpjdnprNnh5Tlg3VHhvYW5KeGRSN2xUZjR3eVJtSEYyNVJlTHYySFlpNGJwakRxVU9yUW9Icmd2cFdPZTZnVDJ4SUFad1BlUjlxZmxNdmFBWQ==","email":"jaboyd@redhat.com"}}}
```

   * Save this off.
   * Navigate to https://api.ci.openshift.org/console and login
   * In the header, next to your name, click on the `(?)`
   * Select **Command Line Tools**
   * Select **Copy to Clipboard**

    ```
    oc login https://api.ci.openshift.org --token=n2kw5cpba3szQoNmL3zJMGebggAD-olcpiBPM9WmGHc
    ```

   * Login to registry, passing in your secret. The registry auth will be
     appended:

```
[jaboyd@jboyd service-catalog (master)]$ oc registry login --to=/path/to/pull-secret
info: Using registry public hostname registry.svc.ci.openshift.org
```
   * To make pasting the secret to the installer easier, remove the newlines:
```
cat /path/to/pull-secret | tr -d '\n' > pull-secret.json
```

some more discussion is here:

>
> https://coreos.slack.com/archives/CEKNRGF25/p1555518885441800
>
> OK! I finally had a successful launch after ~ a week, with a payload from https://openshift-release.svc.ci.openshift.org  If anyone else is having issues read this (launching w/ non-interactive install-config):
> 1) go to https://api.ci.openshift.org/console copy/paste the oc login cmd - now you're logged in to ci cluster.
> 2) oc registry login --to /path/where/you/want/your/pull-secret/dropped
> 3) copy the registry.svc.ci.openshift.org auth from your pull-secret into your ~/installdir/install-config.yaml. like so:
> pullSecret: '{"auths": {"registry.svc.ci.openshift.org": {"auth": "blahblah"}}}'
> 4) download installer for particular release from https://openshift-release.svc.ci.openshift.org (I used the oc adm release extract --tools registry.svc.ci.openshift.org/ocp/release:4.0.0-0.ci-2019-04-17-133604 from today )
> 5) tar xvf the installer there ^^
> 6) run /path/to/openshift-install create cluster --dir ~/installdir
> this worked for me, finally, after a week or so of failed installs (probably bc I missed some emails, but if you're like me...)
>


## Install the cluster

I usually extract the install program to ~/deploy/MM-DD or something like that.

```
jaboyd@jboyd 0515]$ ./openshift-install create cluster  --log-level debug

? SSH Public Key  [Use arrows to move, type to filter, ? for more help]
  /home/jaboyd/.ssh/id_rsa.pub
  /home/jaboyd/.ssh/jaboyd@redhat.com-id_rsa.pub
  /home/jaboyd/.ssh/libra.pub
# pick /home/jaboyd/.ssh/libra.pub

? Platform  [Use arrows to move, type to filter]
# pick AWS

? Platform aws
? Region  [Use arrows to move, type to filter, ? for more help]
  eu-west-2 (London)
  eu-west-3 (Paris)
  sa-east-1 (São Paulo)
> us-east-1 (N. Virginia)
  us-east-2 (Ohio)
  us-west-1 (N. California) us-west-2 (Oregon)
? Region us-east-1

us-east-1 or use-east-2 work


DEBUG       Generating "Base Domain"...
DEBUG listing AWS hosted zones
? Base Domain  [Use arrows to move, type to filter, ? for more help]
> devcluster.openshift.com
  eap-qe-ocp41-cluster10.fw.rhcloud.com
  eap-qe-ocp41-cluster12.fw.rhcloud.com
  eap-qe-ocp41-cluster7.fw.rhcloud.com
  installer.devcluster.openshift.com
  kwills-cluster.fw.rhcloud.com
  kwills1-cluster.fw.rhcloud.com
? Base Domain devcluster.openshift.com

I always use devcluster.openshift.com



DEBUG       Fetching "Cluster Name"...
DEBUG         Fetching "Base Domain"...
DEBUG         Reusing previously-fetched "Base Domain"
DEBUG       Generating "Cluster Name"...
? Cluster Name [? for help] jaboyd0515

I always use jaboyd and MMDD.


? Cluster Name jaboyd0515
DEBUG       Fetching "Pull Secret"...
DEBUG       Generating "Pull Secret"...
? Pull Secret [? for help]

paste in the long secret that includes token from registry.svc.ci.openshift.org


This directory will contain your kubeconfig and and details on how to login to the console log (tail -n 5 .openshift_install.log)
export KUBECONFIG=/home/jaboyd/deploy/05-06-163240/auth/kubeconfig    where 05-06-163240 is the directory where I extract the install to.


Destoring a cluster is similar:

come back to the same directory and run `./openshift-install destroy cluster  --log-level debug`
```


==============
I usually locate the latest good nightly such as 4.1.0-0.nightly-2019-05-15-151517, click on it to get to that build's details, then click "Download the installer", potentially wait for a minute or two for tools to be staged, then click on the linux installer like openshift-client-linux-4.1.0-0.nightly-2019-05-15-151517.tar.gz to download.  Extract to a desired directory



from Clayton email (4/15/2018 subject "ATTN: Clarifying "what to install"")

Last week the emails about how to install weren't clear enough as mentioned to me by folks :)

ALL DEVELOPERS, QE, AND INTERNAL TESTING SHOULD INSTALL THE PRODUCT BY:
--------------
Use the "Download the installer" link from https://openshift-release.svc.ci.openshift.org to get the correct installer binary to install the latest code.

Building the installer manually and running installs from it is not a supported path for customers and should only be tested by the installer team and people hacking the installer.

Bugs opened from origin-release will be ignored

Use builds from:

4.0.0-0.ci: You want to test code that hasn't been built by OCP yet
4.0.0-0.nightly: You want to test code that customers will get if we shipped today.

We will send an update when we have the 4.1.0 named variants of these working (will be the same code, just still cutting things over)

Install team developers:
-----------------
Can continue building the installer locally, but the location we publish origin to has been updated to registry.svc.ci.openshift.org/origin/release:v4.1 and this is only if you are hacking the installer.


-----------------------------------------


Get auth secret from https://cloud.redhat.com/openshift/install
search for "Step 2" and click "Copy pull secret".  It will look something like

{"auths":{"cloud.openshift.com":{"auth":"b3BlbnNoaWZ0LXJlbGVhc2UtZGV2K2phYm95ZHJlZGhhdGNvbTFkdHlqZTBzbXpqNGljZHNqNHdvcXRqZ3l4azoyNU5LSzVaR1gyVTZMSVIyWVJKT0lCWlZCNUM1RjJNN0VJWTRLMlMwNENMTlpLRURQMjRIRTlBRU9LVTVRSkcx","email":"jaboyd@redhat.com"},"quay.io":{"auth":"b3BlbnNoaWZ0LXJlbGVhc2UtZGV2K2phYm95ZHJlZGhhdGNvbTFkdHlqZTBzbXpqNGljZHNqNHdvcXRqZ3l4azoyNU5LSzVaR1gyVTZMSVIyWVJKT0lCWlZCNUM1RjJNN0VJWTRLMlMwNENMTlpLRURQMjRIRTlBRU9LVTVRSkcx","email":"jaboyd@redhat.com"},"registry.connect.redhat.com":{"auth":"NTE5MzUzMzZ8dWhjLTFEdFlqRTBzTXpqNEljZHNqNFdvcXRKR1lYazpleUpoYkdjaU9pSlNVelV4TWlKOS5leUp6ZFdJaU9pSXhaR1JpWm1abU1URmhNV0kwWm1JMlltWm1OekprWVRSbVlqUXlZMlF3TlNKOS5PYW9zTERkc0F0S25wR2xWSlpMU3VTTExSUzJmb1dKeFRKQnF5Y2Z0OGU5WlFLOGMzT3hzdXVNSzNMY1FWLXFKTVN4Q2dBYUdJanBwSXkzQVpkYi1iNUw1R2djU3lPLVpyeWxFblJnZGtkQlBaNzk4cU0xcHNxajkyVGxaejJ6OWZBcW9PSTVWbTZIZU10cF92NHczeUkyZF9KMnc1MjAzVC1iRDVGX2NLd3dBU0dpdXdyZ3BLV09vWjhvNjdRV2U0V0U5Nnc5ZEpNYV9tQnVlYnVHRjN4NGQxdEl5ck1KMXNHNnk3SkplRlBUNnI0Q3Ewc1NpcXBVTGc5TnVYNllIZUdYY1BNQUtXdDZZZDZOUnJwZi1NWTVXV3lWZW1RR204SWFwWVVqLU5XbDhVa2plZ2hpNDRyYUs3dG9DTEktNklTZXJHTUxaTnQzam4wNmF3UzRFVTN1dWxzd1VFaV9QdEVNLUZ4RDVNYmxycnpNUGhCN1d0UTFLaXh2U3lxdUY0Qk9FZ0hPSko5Z2pzWWEwcU10dUx1TVJyVUZVd0dBdElETDhzd2h1c0F1ZjRwaDlLOEhmT3FYR2J5MjcyTl91SnBHLV9IRjhnMmlOLWVvbEcwRjNXTG9rM0hES0RfX3Zud0d0QllmSjYxZ1NJMWJ5NTA0dFF1NlhKVkR0SmpWVEhQcl9MOUtEU3pxOThCcEFpZTVHNTF3Tlp2UFFMUWZWU0RqMnUwMTdiR3N2RnlBX1p3cHJ3bEhHYkFqRnZQeWhvMndEdGMyMGpVT3lJM2hrQWNTZTI4NkFxTXpjdnprNnh5Tlg3VHhvYW5KeGRSN2xUZjR3eVJtSEYyNVJlTHYySFlpNGJwakRxVU9yUW9Icmd2cFdPZTZnVDJ4SUFad1BlUjlxZmxNdmFBWQ==","email":"jaboyd@redhat.com"},"registry.redhat.io":{"auth":"NTE5MzUzMzZ8dWhjLTFEdFlqRTBzTXpqNEljZHNqNFdvcXRKR1lYazpleUpoYkdjaU9pSlNVelV4TWlKOS5leUp6ZFdJaU9pSXhaR1JpWm1abU1URmhNV0kwWm1JMlltWm1OekprWVRSbVlqUXlZMlF3TlNKOS5PYW9zTERkc0F0S25wR2xWSlpMU3VTTExSUzJmb1dKeFRKQnF5Y2Z0OGU5WlFLOGMzT3hzdXVNSzNMY1FWLXFKTVN4Q2dBYUdJanBwSXkzQVpkYi1iNUw1R2djU3lPLVpyeWxFblJnZGtkQlBaNzk4cU0xcHNxajkyVGxaejJ6OWZBcW9PSTVWbTZIZU10cF92NHczeUkyZF9KMnc1MjAzVC1iRDVGX2NLd3dBU0dpdXdyZ3BLV09vWjhvNjdRV2U0V0U5Nnc5ZEpNYV9tQnVlYnVHRjN4NGQxdEl5ck1KMXNHNnk3SkplRlBUNnI0Q3Ewc1NpcXBVTGc5TnVYNllIZUdYY1BNQUtXdDZZZDZOUnJwZi1NWTVXV3lWZW1RR204SWFwWVVqLU5XbDhVa2plZ2hpNDRyYUs3dG9DTEktNklTZXJHTUxaTnQzam4wNmF3UzRFVTN1dWxzd1VFaV9QdEVNLUZ4RDVNYmxycnpNUGhCN1d0UTFLaXh2U3lxdUY0Qk9FZ0hPSko5Z2pzWWEwcU10dUx1TVJyVUZVd0dBdElETDhzd2h1c0F1ZjRwaDlLOEhmT3FYR2J5MjcyTl91SnBHLV9IRjhnMmlOLWVvbEcwRjNXTG9rM0hES0RfX3Zud0d0QllmSjYxZ1NJMWJ5NTA0dFF1NlhKVkR0SmpWVEhQcl9MOUtEU3pxOThCcEFpZTVHNTF3Tlp2UFFMUWZWU0RqMnUwMTdiR3N2RnlBX1p3cHJ3bEhHYkFqRnZQeWhvMndEdGMyMGpVT3lJM2hrQWNTZTI4NkFxTXpjdnprNnh5Tlg3VHhvYW5KeGRSN2xUZjR3eVJtSEYyNVJlTHYySFlpNGJwakRxVU9yUW9Icmd2cFdPZTZnVDJ4SUFad1BlUjlxZmxNdmFBWQ==","email":"jaboyd@redhat.com"}}}

Save this off.  Navigate to https://api.ci.openshift.org/console login, then in the header, next to your name, click on the "?" and then select "Command Line Tools".    Select "Copy to Clipboard"

oc login https://api.ci.openshift.org --token=n2kw5cpba3szQoNmL3zJMGebggAD-olcpiBPM9WmGHc

followed by

[jaboyd@jboyd service-catalog (master)]$ oc registry login --to=-
info: Using registry public hostname registry.svc.ci.openshift.org
{
  "auths": {
    "registry.svc.ci.openshift.org": {
      "auth": "dXNlcjpuMmt3NWNwYmEzc3pRb05tTDN6Sk1HZWJnZ0FELW9sY3BpQlBNOVdtR0hj"
    }
  }
}



copy the returned auth info and merge it into auths from above at the end.  My end result is


{"auths":{"cloud.openshift.com":{"auth":"b3BlbnNoaWZ0LXJlbGVhc2UtZGV2K2phYm95ZHJlZGhhdGNvbTFkdHlqZTBzbXpqNGljZHNqNHdvcXRqZ3l4azoyNU5LSzVaR1gyVTZMSVIyWVJKT0lCWlZCNUM1RjJNN0VJWTRLMlMwNENMTlpLRURQMjRIRTlBRU9LVTVRSkcx","email":"jaboyd@redhat.com"},"quay.io":{"auth":"b3BlbnNoaWZ0LXJlbGVhc2UtZGV2K2phYm95ZHJlZGhhdGNvbTFkdHlqZTBzbXpqNGljZHNqNHdvcXRqZ3l4azoyNU5LSzVaR1gyVTZMSVIyWVJKT0lCWlZCNUM1RjJNN0VJWTRLMlMwNENMTlpLRURQMjRIRTlBRU9LVTVRSkcx","email":"jaboyd@redhat.com"},"registry.connect.redhat.com":{"auth":"NTE5MzUzMzZ8dWhjLTFEdFlqRTBzTXpqNEljZHNqNFdvcXRKR1lYazpleUpoYkdjaU9pSlNVelV4TWlKOS5leUp6ZFdJaU9pSXhaR1JpWm1abU1URmhNV0kwWm1JMlltWm1OekprWVRSbVlqUXlZMlF3TlNKOS5PYW9zTERkc0F0S25wR2xWSlpMU3VTTExSUzJmb1dKeFRKQnF5Y2Z0OGU5WlFLOGMzT3hzdXVNSzNMY1FWLXFKTVN4Q2dBYUdJanBwSXkzQVpkYi1iNUw1R2djU3lPLVpyeWxFblJnZGtkQlBaNzk4cU0xcHNxajkyVGxaejJ6OWZBcW9PSTVWbTZIZU10cF92NHczeUkyZF9KMnc1MjAzVC1iRDVGX2NLd3dBU0dpdXdyZ3BLV09vWjhvNjdRV2U0V0U5Nnc5ZEpNYV9tQnVlYnVHRjN4NGQxdEl5ck1KMXNHNnk3SkplRlBUNnI0Q3Ewc1NpcXBVTGc5TnVYNllIZUdYY1BNQUtXdDZZZDZOUnJwZi1NWTVXV3lWZW1RR204SWFwWVVqLU5XbDhVa2plZ2hpNDRyYUs3dG9DTEktNklTZXJHTUxaTnQzam4wNmF3UzRFVTN1dWxzd1VFaV9QdEVNLUZ4RDVNYmxycnpNUGhCN1d0UTFLaXh2U3lxdUY0Qk9FZ0hPSko5Z2pzWWEwcU10dUx1TVJyVUZVd0dBdElETDhzd2h1c0F1ZjRwaDlLOEhmT3FYR2J5MjcyTl91SnBHLV9IRjhnMmlOLWVvbEcwRjNXTG9rM0hES0RfX3Zud0d0QllmSjYxZ1NJMWJ5NTA0dFF1NlhKVkR0SmpWVEhQcl9MOUtEU3pxOThCcEFpZTVHNTF3Tlp2UFFMUWZWU0RqMnUwMTdiR3N2RnlBX1p3cHJ3bEhHYkFqRnZQeWhvMndEdGMyMGpVT3lJM2hrQWNTZTI4NkFxTXpjdnprNnh5Tlg3VHhvYW5KeGRSN2xUZjR3eVJtSEYyNVJlTHYySFlpNGJwakRxVU9yUW9Icmd2cFdPZTZnVDJ4SUFad1BlUjlxZmxNdmFBWQ==","email":"jaboyd@redhat.com"},"registry.redhat.io":{"auth":"NTE5MzUzMzZ8dWhjLTFEdFlqRTBzTXpqNEljZHNqNFdvcXRKR1lYazpleUpoYkdjaU9pSlNVelV4TWlKOS5leUp6ZFdJaU9pSXhaR1JpWm1abU1URmhNV0kwWm1JMlltWm1OekprWVRSbVlqUXlZMlF3TlNKOS5PYW9zTERkc0F0S25wR2xWSlpMU3VTTExSUzJmb1dKeFRKQnF5Y2Z0OGU5WlFLOGMzT3hzdXVNSzNMY1FWLXFKTVN4Q2dBYUdJanBwSXkzQVpkYi1iNUw1R2djU3lPLVpyeWxFblJnZGtkQlBaNzk4cU0xcHNxajkyVGxaejJ6OWZBcW9PSTVWbTZIZU10cF92NHczeUkyZF9KMnc1MjAzVC1iRDVGX2NLd3dBU0dpdXdyZ3BLV09vWjhvNjdRV2U0V0U5Nnc5ZEpNYV9tQnVlYnVHRjN4NGQxdEl5ck1KMXNHNnk3SkplRlBUNnI0Q3Ewc1NpcXBVTGc5TnVYNllIZUdYY1BNQUtXdDZZZDZOUnJwZi1NWTVXV3lWZW1RR204SWFwWVVqLU5XbDhVa2plZ2hpNDRyYUs3dG9DTEktNklTZXJHTUxaTnQzam4wNmF3UzRFVTN1dWxzd1VFaV9QdEVNLUZ4RDVNYmxycnpNUGhCN1d0UTFLaXh2U3lxdUY0Qk9FZ0hPSko5Z2pzWWEwcU10dUx1TVJyVUZVd0dBdElETDhzd2h1c0F1ZjRwaDlLOEhmT3FYR2J5MjcyTl91SnBHLV9IRjhnMmlOLWVvbEcwRjNXTG9rM0hES0RfX3Zud0d0QllmSjYxZ1NJMWJ5NTA0dFF1NlhKVkR0SmpWVEhQcl9MOUtEU3pxOThCcEFpZTVHNTF3Tlp2UFFMUWZWU0RqMnUwMTdiR3N2RnlBX1p3cHJ3bEhHYkFqRnZQeWhvMndEdGMyMGpVT3lJM2hrQWNTZTI4NkFxTXpjdnprNnh5Tlg3VHhvYW5KeGRSN2xUZjR3eVJtSEYyNVJlTHYySFlpNGJwakRxVU9yUW9Icmd2cFdPZTZnVDJ4SUFad1BlUjlxZmxNdmFBWQ==","email":"jaboyd@redhat.com"},"registry.svc.ci.openshift.org":{"auth":"dXNlcjpuMmt3NWNwYmEzc3pRb05tTDN6Sk1HZWJnZ0FELW9sY3BpQlBNOVdtR0hj"}}}


some more discussion is here:

https://coreos.slack.com/archives/CEKNRGF25/p1555518885441800

OK! I finally had a successful launch after ~ a week, with a payload from https://openshift-release.svc.ci.openshift.org  If anyone else is having issues read this (launching w/ non-interactive install-config):
1) go to https://api.ci.openshift.org/console copy/paste the oc login cmd - now you're logged in to ci cluster.
2) oc registry login --to /path/where/you/want/your/pull-secret/dropped
3) copy the registry.svc.ci.openshift.org auth from your pull-secret into your ~/installdir/install-config.yaml. like so:
   pullSecret: '{"auths": {"registry.svc.ci.openshift.org": {"auth": "blahblah"}}}'
4) download installer for particular release from https://openshift-release.svc.ci.openshift.org (I used the oc adm release extract --tools registry.svc.ci.openshift.org/ocp/release:4.0.0-0.ci-2019-04-17-133604 from today )
5) tar xvf the installer there ^^
6) run /path/to/openshift-install create cluster --dir ~/installdir
this worked for me, finally, after a week or so of failed installs (probably bc I missed some emails, but if you're like me...) 


I usually extract the install program to ~/deploy/MM-DD or something like that.

jaboyd@jboyd 0515]$ ./openshift-install create cluster  --log-level debug

? SSH Public Key  [Use arrows to move, type to filter, ? for more help]
  /home/jaboyd/.ssh/id_rsa.pub
  /home/jaboyd/.ssh/jaboyd@redhat.com-id_rsa.pub
  /home/jaboyd/.ssh/libra.pub
pick /home/jaboyd/.ssh/libra.pub

? Platform  [Use arrows to move, type to filter]
pick AWS

? Platform aws
? Region  [Use arrows to move, type to filter, ? for more help]
  eu-west-2 (London)
  eu-west-3 (Paris)
  sa-east-1 (São Paulo)
> us-east-1 (N. Virginia)
  us-east-2 (Ohio)
  us-west-1 (N. California)
  us-west-2 (Oregon)
? Region us-east-1

us-east-1 or use-east-2 work


DEBUG       Generating "Base Domain"...
DEBUG listing AWS hosted zones
? Base Domain  [Use arrows to move, type to filter, ? for more help]
> devcluster.openshift.com
  eap-qe-ocp41-cluster10.fw.rhcloud.com
  eap-qe-ocp41-cluster12.fw.rhcloud.com
  eap-qe-ocp41-cluster7.fw.rhcloud.com
  installer.devcluster.openshift.com
  kwills-cluster.fw.rhcloud.com
  kwills1-cluster.fw.rhcloud.com
? Base Domain devcluster.openshift.com


I always use devcluster.openshift.com



DEBUG       Fetching "Cluster Name"...
DEBUG         Fetching "Base Domain"...
DEBUG         Reusing previously-fetched "Base Domain"
DEBUG       Generating "Cluster Name"...
? Cluster Name [? for help] jaboyd0515

I always use jaboyd and MMDD.


? Cluster Name jaboyd0515
DEBUG       Fetching "Pull Secret"...
DEBUG       Generating "Pull Secret"...
? Pull Secret [? for help]

paste in the long secret that includes token from registry.svc.ci.openshift.org


This directory will contain your kubeconfig and and details on how to login to the console log (tail -n 5 .openshift_install.log)
export KUBECONFIG=/home/jaboyd/deploy/05-06-163240/auth/kubeconfig    where 05-06-163240 is the directory where I extract the install to.


Destoring a cluster is similar:

come back to the same directory and run `./openshift-install destroy cluster  --log-level debug`
