# Install OpenShift 4.x

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

I usually extract the install program to `~/deploy/MM-DD` or something like that.


1) Run the installer, debug log level is helpful to figure out issues that may
crop up.
2) When prompted pick `/home/devel/jesusr/.ssh/libra.pub`

```
[jesusr@transam 0718]$ ./openshift-install create cluster  --log-level debug

? SSH Public Key  [Use arrows to move, type to filter, ? for more help]
  /home/devel/jesusr/.ssh/id_rsa.fedora.pub
  /home/devel/jesusr/.ssh/id_rsa.jmrodri.pub
  /home/devel/jesusr/.ssh/id_rsa.pub
> /home/devel/jesusr/.ssh/libra.pub
  <none>
```

3) Pick the AWS Platform.

```
? Platform  [Use arrows to move, type to filter]
> aws
```

4) Use one of the east regions, I usually use **us-east-1 (N. Virginia)**

```
? Platform aws
? Region  [Use arrows to move, type to filter, ? for more help]
  eu-west-2 (London)
  eu-west-3 (Paris)
  sa-east-1 (São Paulo)
> us-east-1 (N. Virginia)
  us-east-2 (Ohio)
  us-west-1 (N. California)
  us-west-2 (Oregon)
```

5) Use `devcluster.openshift.com`

```
? Region us-east-1
DEBUG       Generating "Base Domain"...
DEBUG listing AWS hosted zones
? Base Domain  [Use arrows to move, type to filter, ? for more help]
> devcluster.openshift.com
  eap-qe-cluster59.fw.rhcloud.com
  eap-qe-cluster60.fw.rhcloud.com
  eap-qe-cluster61.fw.rhcloud.com
  vmware.devcluster.openshift.com
```

6) Use your id plus the date, something like `zeus0718`

```
? Base Domain devcluster.openshift.com
DEBUG       Fetching "Cluster Name"...
DEBUG         Fetching "Base Domain"...
DEBUG         Reusing previously-fetched "Base Domain"
DEBUG       Generating "Cluster Name"...
? Cluster Name [? for help]
```

7) Paste in the long secret that includes token from `registry.svc.ci.openshift.org`

```
? Cluster Name zeus0718
DEBUG       Fetching "Pull Secret"...
DEBUG       Generating "Pull Secret"...
? Pull Secret [? for help]
```

This directory will contain your `kubeconfig` and details on how to login to the console log (tail -n 5 .openshift_install.log)
`export KUBECONFIG=/home/jaboyd/deploy/05-06-163240/auth/kubeconfig`  where 05-06-163240 is the directory where I extract the install to.

## Destroying a cluster

Come back to the same directory and run `./openshift-install destroy cluster  --log-level debug`
