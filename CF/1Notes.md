What do you think?
humble
The past couple of days
In the first couple of days
In the next couple of days


# Q
## Provide Quesions, Give to Manager, Provide proposal for optimize team

- What’s something I should to start doing? 

- Are there any skills that you’d like me to acquire in the short term?

- Could you please point me to some starting material?

- Have you had any chance to have a talking with my per-manager？

- Where is our new cube location, when?

- Would we have a mentor to help us to ramp up?

- Would you please let me know what is your specific expectations for me?

SMB/NFS/FSP



- Are you satisfied with your performance so far?

- After we deliver the AR, do you think I can go to fix he customer issues with Rohit & Sameer. I would like to learn how fix customer issues.

- I saw S will provide her PR to team slack channel, let all the team members to review her PR. Do you thin we should do the same thing?

- How is our team doing and what could we do to better reach our objectives?
  
- AM drop plan change

- A suggest. If you could ask us project details randomly, (NO periodically), probability can make our work more efficient.

- Maybe inters need more help from S




Hi, I am Fan Zhou graduated from WSU. have been in EMC for the past almost 1 year, have been working on a number of new features in the metering service in Java. I have been working on embedded system in C for two years in China. 
Hopefully my experience can help our team in future.

I have been reading the wiki from isilone such as one file system, and reviewing C language which can help me to start the new tasks quickly. And spend some time to help pre-team to finish the new feature which was impled by us. 

All,
 
I am really looking forward to getting the opportunity to work with each of you and have you join our team.  I was hoping to have the opportunity to get you all together this week to give a brief introduction to my current team.  Unfortunately timing didn’t quite work out due to training and a folks out on PTO.  Because I will be out in training for 2.5 days next week, I will be setting up 1:1s for each of you mid to late next week.  Additionally, I will take the opportunity to have a sync up with your manager to ensure there is a clear transition plan/hand-off between us in completing current team commitments/deliverables.  In preparation for our 1:1 discussion next week, I’d like you to think about the following questions to gather your thoughts on what you’d like me to know about you:


We can certainly provide you with visa instructions, but first, we would like to confirm certain details. Please provide the following information so that we can evaluate your specific situation, and provide you with the most accurate instructions. 

- Provide the Consulate you will visit: 
  - Shanghai China
- Date of departure and duration of stay:
  - Departure from USA: 10/6/2019  Come back to USA: 10/25/2019 (If I can get my VISA stamp successfully)
- Your official job title, and worksite:
  - Software Development Engineer II.  Seattle 
- Current job duties:
  - I have bean reorganized to another team which is working on file access protocol of isilon few weeks ago.
- Manager’s name & email address:
  - Leslie Nguyen   Leslie.Nguyen@dell.com
- Manager’s job title:
  - Manager 2, Software Engineering
- Copy of your most recent pay statement:
  - Please find my pay statement of attachment.
- Copy of your most recent passport, visa, and approval notice:
  - Please find mymost recent passport, visa, and approval notice of attachment.

Also, has there been any significant change to your job description, functions, or location since the filing of your last petition?

Thanks,


Administrative Processing


Do you think I can do ramp up with Wei together since we believe it will be more efficient for us. if so could you please add me and Wei to a channel? 

remotedev-fzhou.west.isilon.com




 I-129 申请批件 (petition) 或 I-797 通过凭证 (Notice of Action) 的条码编号


 DS-160 confirmation page with barcode.
 Interview appointment letter confirming that the interview was booked through the correct service.
 A 2 inch by 2 inch passport-type photograph taken within the past six months against a white background.
 Visa application fee receipt.
 Your email address.
 Current letter of employment (instructions to obtain provided).
 Original H-1B approval notice, Form I-797 Notice of Action (previously sent).
 Certified copy of H-1B petition filed with USCIS, including petitioner support letter and Labor Condition Application.
 Original or certified copies of complete academic credentials and, if applicable, foreign credentials evaluation.
 W-2 statements for all years you have been employed in the U.S.
2, Shanghai Visa Instructions
 All paystubs from the current calendar year.
 Names and current phone numbers of the personnel managers at your present and previous places of employment
in the U.S.
 Copies of all previously issued U.S. immigration documents (if applicable).
 All prior passports that contain U.S. visas (if applicable).
 Passport with at least six months of validity remaining and at least one blank page.
 Appointment letter confirming you booked your appointment through this service
http://www.ustraveldocs.com/cn/cn-niv-appointmentschedule.asp



Creating your vCluster (this might take a while).
build: b.master.320r
created: '2019-09-16T18:27:31.577930+00:00'
expires: '2019-09-23T18:27:31.576612+00:00'
id: 717282
ips: [10.224.39.210, 10.224.39.211, 10.224.39.212, 10.224.39.213]
location: rdu1
logs: https://ducttape.west.isilon.com:443/api/v2.0/clusters/717282/logs
name: fzhou-kvwxoo6
notes: ''
owner: fzhou
provider: VCENTER
state: OK                
type: ONEFS
vms: [DTRDUONEFS506497, DTRDUONEFS506498, DTRDUONEFS506499]
isi network subnets modify groupnet0.subnet0 --sc-service-addr 10.224.39.213

dig @fzhou-dns.west.isilon.com fzhou.west.isilon.com

Do you plan to have a call or would like me to go to your office?

mount fzhou.west.isilon.com:/path/to/onefs/source/code/on/local/workstation




mount remotedev-fzhou.west.isilon.com://ifs/home/fzhou/onefs /mnt/sourcs

sudo vim /etc/exports

/ifs/home/fzhou/onefs 0.0.0.0/255.0.0.0(rw,sync,no_subtree_check,all_squash,anonuid=4397,anongid=1000)

sudo chmod -R o+rx /ifs/home/fzhou/onefs


   cribsbiox.west.isilon.com:/ifs/home/fzhou /mnt/source nfs intr,rw,rsize=32768,wsize=32768,tcp 0 0
mount /mnt/source


make isi-isilon OVERRIDE=isilon/bin/isi_smartconnect
make isi-isilon OVERRIDE=isilon/bin/isi_flexnet
make isi-isilon OVERRIDE=isilon/lib/isi_flexnet

make isi-isilon OVERRIDE=isilon/isilon/lib/isi_flexnet/