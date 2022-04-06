# LinuxEnvGuideline
for setting linux dev environment when soem program deploys server.

how to set env without root? usually we could use yum install to do most things if you have a root account. but you can not do this cmd when you try to deploy with some things in server which do not have authernation for your personal accout. so record how to download source code and compile it to deploy is important.

the way to add some thing to env

PATH=$PATH:%APPLICATION%\bin
export PATH

LD_LIBARAY_PATH=$LD_LIBRARY_PATH:%APPLICATION%\lib
export LD_LIBRARY_PATH