Download Link: https://assignmentchef.com/product/solved-cs642-homework4
<br>
This homework assignment needs you to understand vulnerabilities in 5 target programs. The first 4 are required; if you do the 5th you can earn extra credit. You may pair up for this home work (but it’s not a requirement). No extra credit for doing it alone. Click here to download HW4 files:<u> HW4.zip.</u>

Prerequisites

For this project, you are going to use a virtual machine configured with Debian stable (“Lenny”), with ASLR (address space layout randomization) turned off. We provide basic VM images for Oracle VirtualBox.

<ul>

 <li>Download Oracle’s Virtual Box: <a href="https://vvww.virtualbox.org/wiki/Downloads">https://vvww.virtualbox.org/wiki/Downloads</a><u> </u><u>(</u><a href="https://www.virtualbox.org/wiki/Downloads)">https://www.virtualbox.org/wiki/Downloads)</a></li>

 <li>Download<u> a virtual machine description file.</u></li>

 <li>Download<u> a virtual disk image file.</u></li>

</ul>

Environment Setup

<ul>

 <li>The user name and password are ‘user’ and ‘user’.</li>

 <li>The root name and password are ‘root’ and ‘root’.</li>

</ul>

SSH Configuration

It might be easier to work on the VM over SSH from the guest — easier to do copy-paste commands. Here are some guidelines in case you want to use SSH. (You are free to use the native VM environment or SSH.)

Step 1: Enable Port Forwarding Feature for VM

You will have to enable port forwarding feature to access VM from any terminal using SSH.

On the VirtualBox application window where VM is listed, right click VM listed and click<u> (settings).</u> In (Network, tab, under<u> (Adapter</u> 1<sup></sup>, select<u><sub> `</sub></u><u>NAT)</u> in<u> (Attached to</u> option.

UnderAcrianced click (Port Forwarding which open a window to set port forwarding option. Add an entry there with following fields

Name                    Protocol               1-lost IP                        Host Port                    Guest IP                     Guest Port

4/3/2020                                                                                                                                                                               HW4

SSH                       TCP                      0.0.0.0                   2222                                                   22

Step 2: Using SSH to Access VM and SCP to Transfer Files/Folders

Save the settings in step 1 and restart your VM.

Now sshinto the VM from terminal using the following command

ssh -p 2222 <a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="3f4a4c5a4d7f0e0d08110f110f110e">[email protected]</a>

You can also SCP file/folder into VM using the following command

<table>

 <tbody>

  <tr>

   <td width="723">scp -P 2222 file <a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="d0a5a3b5a290e1e2e7fee0fee0fee1">[email protected]</a>:—/scp -r -P 2222 folder <a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="ec999f899eacdddedbc2dcc2dcc2dd">[email protected]</a>:—/d</td>

  </tr>

 </tbody>

</table>

The Targets

The `targets/ directory contains the source code for the vulnerable targets, along with a<u> riakefiie)</u> for building them.

Your exploits should assume that the compiled target programs are installed setuid-root in<u> /tmp)</u> —

&gt; , /tmp/target0 „ ,/tmp/target1<sub>)</sub>, etc.

To build the targets, change to the targets/ directory and type             on the command line; the

,Makefile will take care of building the targets. To install the target binaries in , run:

make install

To make the target binaries setuid-root, run:

su

make setuid

exit # to get out of the root shell

Once you’ve run :make setuid<sup>‘</sup> use exit to return to your user shell.

Keep in mind that it’ll be easier to debug the exploits if the targets aren’t setuid. (See below for more on debugging.) If an exploit succeeds in getting a user shell on a non-setuid target in<u> (/tmp</u> , it should succeed in getting a root shell on that target when it is setuid. (But be sure to test that way, too, before submitting your solutions!)

The Exploits

The<u> (sT:doits/</u> ‘contains skeleton source for the exploits which you are to write, along with a Make<sup>–</sup>le for building them. Also included is ,shellcode. h<sub>)</sub>, which gives Aleph One’s shellcode (code which leads a vulnerable target to a shell).

4/3/2020                                                                                                                      HW4

The Assignment

You are to write exploits for vulnerable targets, with one exploit per target.

<ol>

 <li>The goal of sploit0 is different from the rest of the exploits. Take a look at c , the output is “Grade = F” for any string (&lt;20 bytes) you pass. Your goal as an attacker is to hijack the control flow of to print “Grade = A”. Use sploit0. c . to generate and pass a “string” that is going toaid you in obtaining the desired grade, which is A obviously.</li>

 <li>The rest of the exploits (sploite through sploit4 ), when run in the virtual machine with its target installed setuid-root in<u> (mp</u> , should yield a root shell (</li>

</ol>

<sub>x</sub><u> /bin/sh</u> )).

<ol start="3">

 <li>For full credit you must provide an explanation in the sploit[0-4].txt</li>

 <li>We will grade each of your exploits implementation on a zero or all basis. So make sure your code works before submission!</li>

</ol>

Once again, (spioite-: are required;<u> (sploit4</u> is extra credit.

Hints

Read the Phrack articles suggested below. Read Aleph One’s paper carefully, in particular.

To understand what’s going on, it is helpful to run code through gdb. See the GDB tips section below. Make sure that your exploits work within the provided virtual machine.

Start early! Theoretical knowledge of exploits does not readily translate into the ability to write working exploits. target0 is relatively simple and the other problems are quite challenging.

GDB Tips

Notice the (disassemble) and<u>Ftepi</u> commands.

You may find the command useful to examine memory (and the different ways you can print the contents such as , /a , /i after 01<sub>)</sub>). The<sub> L</sub>info register command is helpful in printing out the contents of registers such as el:1 and e sT’.

A useful way to run gdb is to use the          and     command line flags; for example, the command gdb

-e sploit3 -s /tmp/target3 in the VM tells gdb to execute sploit3 and use the symbol file in<u> target3].</u> These flags let you trace the execution of the ,targej after the sploit’s memory image has been replaced with the target’s through the execve system call.

When running gdb using these command line flags, you should follow the following procedure for setting breakpoints and debugging memory:

<ol>

 <li>Tell gdb to notify you on exec(), by issuing the command<sub> :</sub>catch exec<sup>‘</sup></li>

 <li>Run the program. gdb will execute the sploit until the execve syscall, then return control to you</li>

 <li>Set any breakpoints you want in the target</li>

 <li>Resume execution by telling gdb (continue ‘ (or just ).</li>

</ol>

4/3/2020                                                                                                                                                                               HW4

If you wish, you can instrument the target code with arbitrary assembly using the _asm_ () pseudofunction, to help with debugging. Be sure, however, that your final exploits work against the unmodified targets, since these we will use these in grading.

Warnings

Aleph One gives code that calculates addresses on the target’s stack based on addresses on the exploit’s stack. Addresses on the exploit’s stack can change based on how the exploit is executed (working directory, arguments, environment, etc.); during grading, we do not guarantee to execute your exploits exactly the same way bash does. You must therefore hard-code target stack locations in your exploits. You should *not* use a function such as get_sp() in the exploits you hand in.

(In other words, during grading the exploits may be run with a different environment and different working directory than one would get by logging in as user, changing directory to (-inw4ispioits , and running . /sploitl , etc.; your exploits must work even so.)

Your exploit programs should not take any command-line arguments.

Submission

You need to submit:

<ol>

 <li>The source code for your exploits ( sploit0 . c through sploit3 . c and/orc ).</li>

 <li>ID: this include both you and your partner’s wisc emails and names.</li>

 <li>The explanation for your exploits(txt through sploit3 .txt and/or sploit4.txt ) to explain how your exploit works: what is the bug in the corresponding target, how you exploit it, and where the various constants in your exploit come from. If you don’t explain, you won’t get full credits even if your code works.</li>

</ol>

As a team, only one person should submit the homework. That person should compress all the files into one zip file, name it with his/her own netlD.

Suggested Readings

Basic readings:

<ul>

 <li>Aleph One,<u> Smashing the stack for fun and  profit </u><u>(</u><a href="https://insecure.org/stf/smashstack.html)">https://insecure.org/stf/smashstack.html)</a></li>

 <li>blexim,<u> Basic Integer Overflows </u><u>(</u><a href="http://phrack.org/issues/60/10.html)_,">http://phrack.org/issues/60/10.html)_,</a> Phrack 60 #0x10.</li>

 <li>Gera and Riq,<u> Advances in Format String Exploiting</u><u> (</u><a href="http://phrack.org/isbues/59/..html)">http://phrack.org/isbues/59/..html)</a> , Phrack 59 #0x04.</li>

 <li>klog,<u> </u><u>. </u><u>Frame Pointer Overwrite </u><u> (</u><a href="http://phrack.org/issues/55/8.html)_,">http://phrack.org/issues/55/8.html)_,</a> Phrack 55 #08.</li>

 <li>Anonymous,<u> Once Upon a free()…</u><u> (</u><a href="http://phrack.org/issues/57/9.html)">http://phrack.org/issues/57/9.html)</a> , Phrack 57 #0x09.</li>

</ul>

Advanced readings:

<ul>

 <li>Bulba and Kil3r,<u> Bypassing StackGuard and StackShield </u><u>(</u><a href="http://phrack.org/issues/56/5.html)_,">http://phrack.org/issues/56/5.html)_,</a> Phrack 56 #0x05.</li>

</ul>

<a href="https://canvas.wisc.edu/courses/190368/assignments/801571">https://canvas.wisc.edu/courses/190368/assignments/801571</a>                                                                                                                                                                                                          4/5

4/3/2020                                                                                                                                                                                HW4

<ul>

 <li>Silvio Cesare,<u> Shared Library Call Redirection via ELF PLT Infection </u><u>(</u><a href="http://www.phrack.org/archives/issues/56/7.txt)">http://www.phrack.org/archives/issues/56/7.txt)</a> , Phrack 56 #0x07.</li>

 <li>Michel Kaempf,<u> vudo </u><u>– </u><u>An Object Superstitiously Believed to Embody Magical Powers </u><u>(</u><a href="http://phrack.org/issues/57/8.html)_,">http://phrack.org/issues/57/8.html)_,</a> Phrack 57 #0x08.</li>

</ul>




HW4 Rubric

Criteria

sploit0 explanation

sploit0 correct implementation sploitl explanation

sploitl correct implementation sploit2 explanation

sploit2 correct implementation sploit3 explanation

sploit3 correct implementation sploit4 explanation

sploit4 correct implementation




Total Points: 120.0


