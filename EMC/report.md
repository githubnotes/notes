### 7/26/2019
Yesterday completed the scanner major functions which are creating GSM and monitoring whether trigger recon,
Sameer reviewed te changes in persion, then I  made few changes.
And connect each MeteringProcesshanders of GSM
Today am going to think about how to throttle /'θrɑtl/ the scanners

### 7/27/2019
Put in the necessary configuration to throttle the scanners

Had a brief dicuession about scanner throttle with Ger and Yas who are from Blob team.
Basically, introduce my scanners task type to them first. The scanners only scan and update a key on a dt. 
Then they introduced common scanner throttles in ECS to me. We choosed a appropriate /əˈproprɪt/ one to my scanners.

Wei mergerd my pr, We reviewed the code together. We did a few minor changes.

And Did minor things for TOP N buckets. Basically, I changed the configuration then builded the PR again. Somehow the test coverage beacome 74%. It was over then 75%. Maybe the pipline team is changing the alg. Anyway, will provide more unit tests.
