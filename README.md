# boxfuse

Currently under progress


To produce a deliverable, we need to build it from source. This involves compiling sources, processing and copying resources, and probably a few more steps.
The resulting application deliverable (typically a .jar or .war file for JVM-based apps) is
a single immutable unit
built once and stored in an artifact repository
regenerated by the continuous integration system after every change



The application of course doesn't run directly on bare metal. Whether on your laptop or on a server, it requires a stack of software to execute.
A typical server application requires an app server (embedded in the app or not) and a language runtime (like the JVM). The language runtime itself uses various libraries and runs on top of an OS kernel which drives the hardware.




In all but the simplest projects, there are several machines the application needs to run on, organized in multiple environments. The application is gradually promoted from environment to environment. This ensures that what is run in production, is what was tested in test. To achieve this, the same application is pulled from the artifact repository and deployed unchanged to the different machines:

![image](https://user-images.githubusercontent.com/33985509/59183291-f9c96e00-8b6b-11e9-9157-3d26e2a23347.png)



This avoids the classic mistake of building a separate artifact per environment and effectively taking the risk of running something potentially different on all machines.

Yet when we look at the remaining layers of our stack, this is exactly what is happening!

It is the job of the system administrator to ensure that these machines are as identical as possible, yet each is built individually. All changes, patches and upgrades need to be performed on all machines. The sheer complexity of this task and the numerous moving parts make this very difficult to achieve reliably. Even with automated configuration tools and recipes it's easy for some minor detail to slip through the cracks!

So what could potentially go wrong?

Here is just of short list of issues, most of which you will probably already have encountered:

some additional software is missing
a resource (directory, ...) has been created under the wrong name
the wrong version of some software is installed (usually the old one with the bug)
permissions have been set incorrectly
a critical resource (port, ...) is occupied
If these are the risks, then why aren't we holding our systems to the same standards as our applications by applying the same principles for building them?

Why are we still building works of art and snowflake servers when what we need is an army of clones?



Immutable Infrastructure

This is where Immutable Infrastructure comes in.

![image](https://user-images.githubusercontent.com/33985509/59183392-22e9fe80-8b6c-11e9-8077-4e127c188bf8.png)


Instead of assembling just the application, the whole machine is now packaged as a single immutable unit. It contains the entire software stack and it is regenerated by the continuous integration server after every change:



Instead of having to worry about updating many moving parts at all layers, the whole Machine Image is now promoted unchanged from Environment to Environment. Effectively finally making sure that what we run in production is what we tested in test.



![image](https://user-images.githubusercontent.com/33985509/59183412-2d0bfd00-8b6c-11e9-803f-c5eae6bd143f.png)
