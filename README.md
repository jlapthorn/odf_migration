# AWS Environment

Order a blank AWS Open environment from [RHPDS](https://catalog.demo.redhat.com/)


**_NOTE:_**  To make life simple deploy into us-east-2

## Configure credentials

```aws configure --profile rfj2t```

Enter your AWS_ACCESS_KEY_ID and 
AWS_SECRET_ACCESS_KEY.

Set your AWS profile

```export AWS_PROFILE=rfj2t```

Check the credentials work 

```
aws sts get-caller-identity 
{
    "UserId": "AIDA6BHKFR4TXDWAXZTBF",
    "Account": "964711255847",
    "Arn": "arn:aws:iam::964711255847:user/open-environment-rfj2t-admin"
}
```
# Deploy Openshift

Download 'oc' client and 'openshift-installer' from [Red Hat Console](https://console.redhat.com/openshift/downloads)


Run the installation program

```
openshift-install create cluster --dir=ocp4
? SSH Public Key /var/home/lapthorn/.ssh/id_ed25519.pub
? Platform aws
INFO Credentials loaded from the "rfj2t" profile in file "/var/home/lapthorn/.aws/credentials" 
? Region us-east-2
? Base Domain sandbox3017.opentlc.com
? Cluster Name cluster-rfj2t
? Pull Secret [? for help] *******************************************************************************************************************************************************************
```

You can watch cluster deploy

```
export KUBECONFIG=ocp4/auth/kubeconfig
watch 'oc get co'
```

Once complete update the machineset yaml files with the new values

```
sed -i s/cluster-XXXXX-YYYYY/cluster-rfj2t-c8x4q/g' <file>
```

