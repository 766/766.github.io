---
layout: post
title: GCP开通了香港机房，小伙伴们赶紧试试吧
category: 技术
tags: gcp
keywords: gcp,google,kvm
---

## 创建

还是老套路 菜单选择----->Compute Engine-------->VM实例---------->创建实例

如图所示
![](/assets/img/gcp/1.png)

然后就是填写一些配置信息，注意一下图中标记的地方就可以了

![](/assets/img/gcp/2.png)

点击创建按钮，如果不出意外会出现下图的提示

![](/assets/img/gcp/3.png)

**接下来将是关键步骤，将决定创建的成败！**

首先我们创建一个子网

![](/assets/img/gcp/4.png) 点击 创建 VPC 网络

1 配置信息

名称随意，但必须符合规范（名称必须以小写字母开头，后面最多可跟 63 个小写字母、数字或连字符，但不能以连字符结尾）

说明可写可不写，反正我没写

2 写子网信息

名称可以和上面一样

区域选择 asia-east2

IP地址范围填写示例即可 10.0.0.0/9

没有提及的不用管

点击创建

![](/assets/img/gcp/5.png)

回到实例创建，填写完配置信息之后**不不不不不不不不不要**点创建按钮，点击 等效 REST 或命令行 中的命令行

然后会出现如下命令
```
gcloud beta compute --project=true-subject-218011 instances create instance-4 --zone=us-east1-b --machine-type=n1-standard-1 --subnet=default --network-tier=PREMIUM --maintenance-policy=MIGRATE --service-account=xxxxxxxxx-compute@developer.gserviceaccount.com --scopes=https://www.googleapis.com/auth/devstorage.read_only,https://www.googleapis.com/auth/logging.write,https://www.googleapis.com/auth/monitoring.write,https://www.googleapis.com/auth/servicecontrol,https://www.googleapis.com/auth/service.management.readonly,https://www.googleapis.com/auth/trace.append --image=debian-9-stretch-v20181011 --image-project=debian-cloud --boot-disk-size=10GB --boot-disk-type=pd-standard --boot-disk-device-name=instance-4  
```

把--subnet=default  修改一下，改成刚才我们创建子网填写的名称比如我的是haha，修改完后的命令如下
```
gcloud beta compute --project=true-subject-218011 instances create instance-4 --zone=us-east1-b --machine-type=n1-standard-1 --subnet=haha --network-tier=PREMIUM --maintenance-policy=MIGRATE --service-account=xxxxxxxx-compute@developer.gserviceaccount.com --scopes=https://www.googleapis.com/auth/devstorage.read_only,https://www.googleapis.com/auth/logging.write,https://www.googleapis.com/auth/monitoring.write,https://www.googleapis.com/auth/servicecontrol,https://www.googleapis.com/auth/service.management.readonly,https://www.googleapis.com/auth/trace.append --image=debian-9-stretch-v20181011 --image-project=debian-cloud --boot-disk-size=10GB --boot-disk-type=pd-standard --boot-disk-device-name=instance-4 
```

**提醒一下，不要copy我的命令** 因为配置的需求可能不同

然后点击 在CLOUD SHELL 中运行，会打开一个命令行终端，复制上面修改过的命令，然后敲回车，等命令执行成功就可以看到我们的实例已经创建成功了，还有显示IP


接下来就是各种科学配置咯，跟之前一样 不再赘述
