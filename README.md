# vlmcsd is a replacement for Microsoft's KMS server.

> It contains vlmcs, a KMS test client, mainly for debugging purposes, that also can "charge" a genuine KMS server designed to run on an always-on or often-on device, e.g. router, NAS Box, ...intended to help people who lost activation of their legally-owned licenses, e.g. due to a change of hardware (motherboard, CPU, ...)
  
> vlmcsd is not a one-click activation or crack tool intended to activate illegal copies of software (Windows, Office, Project, Visio)

## Info / About this docker
Docker based in Alpine OS with vlmcsd compiled from "source" (Wind4 GitHub)

## Usage:

server side:

* run `docker build -t gucs/vlmcsd .` to build image
* run `docker-compose up` to start container

windows client side:

* run `skmgr.vbs -skms 10.0.0.7` to set kms server
* run `skmgr.vbs -ato` to activate

docker compose logs of my computer

```
Creating network "dockervlmcsd_default" with the default driver
Creating dockervlmcsd_vlmcsd_1 ... done
Attaching to dockervlmcsd_vlmcsd_1
vlmcsd_1  | 2018-04-17 08:30:47: Listening on [::]:1688
vlmcsd_1  | 2018-04-17 08:30:47: Listening on 0.0.0.0:1688
vlmcsd_1  | 2018-04-17 08:30:47: vlmcsd private build started successfully
vlmcsd_1  | 2018-04-17 08:31:43: IPv4 connection accepted: 172.23.0.1:38940.
vlmcsd_1  | 2018-04-17 08:31:43: <<< Incoming KMS request
vlmcsd_1  | 2018-04-17 08:31:43: Protocol version                : 4.0
vlmcsd_1  | 2018-04-17 08:31:43: Client is a virtual machine     : No
vlmcsd_1  | 2018-04-17 08:31:43: Licensing status                : 2 (OOB grace)
vlmcsd_1  | 2018-04-17 08:31:43: Remaining time (0 = forever)    : 43200 minutes
vlmcsd_1  | 2018-04-17 08:31:43: Application ID                  : 55c92734-d682-4d71-983e-d6ec3f16059f (Unknown)
vlmcsd_1  | 2018-04-17 08:31:43: SKU ID (aka Activation ID)      : 620e2b3d-09e7-42fd-802a-17a13652fe7a (Unknown)
vlmcsd_1  | 2018-04-17 08:31:43: KMS ID (aka KMS counted ID)     : ca87f5b6-cd46-40c0-b06d-8ecd57a4373f (Unknown)
vlmcsd_1  | 2018-04-17 08:31:43: Client machine ID               : c0ece1f0-ea45-4568-a519-a680cd960f29
vlmcsd_1  | 2018-04-17 08:31:43: Previous client machine ID      : 129fa978-efe4-4c67-8401-3f46d95a0d26
vlmcsd_1  | 2018-04-17 08:31:43: Client request timestamp (UTC)  : 2018-04-17 08:31:44
vlmcsd_1  | 2018-04-17 08:31:43: Workstation name                : win2k8r2
vlmcsd_1  | 2018-04-17 08:31:43: N count policy (minimum clients): 5
vlmcsd_1  | 2018-04-17 08:31:43: >>> Sending response, ePID source = randomized at program start
vlmcsd_1  | 2018-04-17 08:31:43: Protocol version                : 4.0
vlmcsd_1  | 2018-04-17 08:31:43: KMS host extended PID           : 03612-00206-479-326298-03-1058-14393.0000-0072017
vlmcsd_1  | 2018-04-17 08:31:43: Client machine ID               : c0ece1f0-ea45-4568-a519-a680cd960f29
vlmcsd_1  | 2018-04-17 08:31:43: Client request timestamp (UTC)  : 2018-04-17 08:31:44
vlmcsd_1  | 2018-04-17 08:31:43: KMS host current active clients : 50
vlmcsd_1  | 2018-04-17 08:31:43: Renewal interval policy         : 10080
vlmcsd_1  | 2018-04-17 08:31:43: Activation interval policy      : 120
vlmcsd_1  | 2018-04-17 08:31:43: IPv4 connection closed: 172.23.0.1:38940.
```

## Server Usage:
> $ docker run -d -p 1688:1688 --restart=always --name vlmcsd mikolatero/vlmcsd

## To view docker log:
Now (thanks to embii74) vlmcsd process send logs to docker.
> $ docker logs vlmcsd (change 'vlmcsd' with the docker's name)

## Client
### Windows
>slmgr.vbs -upk  
>slmgr.vbs -ipk XXXXX-XXXXX-XXXXX-XXXXX-XXXXX  
>slmgr.vbs -skms DOCKER_IP  
>slmgr.vbs -ato  
>slmgr.vbs -dlv  

### Office x86
>cd \Program Files (x86)\Microsoft Office\Office16  
>cscript ospp.vbs /sethst:DOCKER_IP  
>cscript ospp.vbs /inpkey:xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
>cscript ospp.vbs /act  
>cscript ospp.vbs /dstatusall  

### Office x86_64
>cd \Program Files\Microsoft Office\Office16  
>cscript ospp.vbs /sethst:DOCKER_IP  
>cscript ospp.vbs /inpkey:xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
>cscript ospp.vbs /act  
>cscript ospp.vbs /dstatusall  

## Sources
> https://forums.mydigitallife.info/threads/50234-Emulated-KMS-Servers-on-non-Windows-platforms  
https://github.com/Wind4/vlmcsd

## GVLK keys
> Windows: https://technet.microsoft.com/en-us/library/jj612867(v=ws.11).aspx  
> Office 2013: https://technet.microsoft.com/en-us/library/dn385360.aspx  
> Office 2016: https://technet.microsoft.com/en-us/library/dn385360(v=office.16).aspx

## Docker Link
> https://hub.docker.com/r/mikolatero/vlmcsd/
