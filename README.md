# UnRoamify
Automatic and manual Active Directory roaming profiles deleting tool

<blockquote>
Copyright 2018, Alexandru-David Deaconu

Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:

1. Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.

2. Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.

3. Neither the name of the copyright holder nor the names of its contributors may be used to endorse or promote products derived from this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
</blockquote>



About UnRoamify
Version 0.1

UnRoamify is an application that you can use to take ownership of folders and delete those folders. You aknowledge that by using this application, there is a potential risk of data loss, so use it at your own risk. I am not responsible for anything that happens to anyone or to anything from the use of this application. 


I made UnRoamify to delete roaming profiles of Active Directory users (hence the name). This tool is an automated equivalent of making batch files (or running commands directly into CMD or PowerShell as Administrator) with:


"takeown /f  P:ath/to/profiles/username.folder /r /d y"

"icacls P:/ath/to/profiles/username.folder /grant administrators:F /t"

"rd P:/ath/to/profiles/username.folder /S /Q"


But instead of you writing the name of every user, you just push a button and it does it for you. READ THE INSTRUCTIONS ! IT'S VERY IMPORTANT YOU GET TO KNOW HOW THE APP WORKS BEFORE YOU USE IT IN PRODUCTION (PLEASE HAVE COMMON SENSE !).

You can find this app on Github @ <to be filled with link>




Disclaimer: I am not a professional programmer and I am very aware that what I did is mostly spaghetti code, so again, use it at your own risk.


UnRoamify has a few modes in which it deletes profiles. You have the nuclear options with which you delete all profiles after you upgraded all Windows versions in the domain. You also got a manual deletion to help you with deleting corrupted profiles.


As for the automatic deletion, there are 2 options, both only work if you use in AD Profile Path the nomenclature \\server\profiles$\%username%: one in which UnRoamify compares the folders on the server with the usernames in AD , or one in which UnRoamify compares the name of the folders with the name found in the profile path in AD. Both have their drawbacks (also mentioned in the instructions): if you use "Delete by Profile", UnRoamify does an AD query in which it can only get by default a maximum number of 1000 users (I think you can modify it somehow, haven't read into it). If you have more than 1000 users in AD, it may delete all the users that weren't returned in the query. If you use "Delete by User" UnRoamify will check profile by profile to see if the name of the folder matches a username in AD, if it doesn't, it deletes it. The problem is when the username got renamed, but maintained the old username in the profile path, in which case, this option deletes the roaming folder even if it is being used.




Story Time (you can ignore this, it's just ramble)
I was wasting a lot of time writing 3 commands for every user's profile I had to delete (sometimes having to delete more than 10 users at once) and also wait for each command to finish, so first I made a C# program that was reading a .txt file with the name of the users that needed to have their roaming profiles deleted and creating a batch file with the commands mentioned above for each user. Then I wanted to create a log file with every user it deleted (just to be sure it did it). The initial program was just a Console Application and had the paths hard-coded into it, so I thought that if I ever needed to change the path to the roaming profiles or change the place where I put my log file, then I had to rebuild the application. Also, if someone else needed to use the application and do those changes, maybe he or she didn't have the source code or the knowledge to modify it. I did the original application to make my job at that time easier and it was working very well, but I was also a sutdent in my Bachelor of Science Degree, the time was passing and I had to make my Bachelor Thesis. This was the point where I decided to create another application based on the old one and make it "more elegant", by using only .NET, instead of using batch files and also give the users the option to customize the application for their setups. As I made great use of this application and I know how boring and error prone repetitive tasks are, I decided to make UnRoamify open source after I had finished my Bachelor's Degree, so that everyone can enjoy it (or lose their jobs to automatization). If you wonder about me, yes, I got my BS.

