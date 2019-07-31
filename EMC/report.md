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

### 7/29/2019
Last week, Wei and I completed and connected each component.
Sammer helped us to clean up the changes. I took a look at the changes. Started to test.
And For the topn changes feature, I updated the configuration for the demo. Then rebuilt the PR.
It is interesting the unit test coverage drop to below 75% even if I didn't change any code. So I added more unit test to pass the validation.

7/30
Made a optimization, made the montor and task scanner sepelty, and Monsly I was debuging. 
Basicly, made current code can pass old MeteringVTFs.

Stand UP: https://Dell.zoom.us/j/5522588246

15621
