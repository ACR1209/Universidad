Is a group of processes run in isolation. All processes **must** be able to run in a shared [[Kernel|kernel]].  Each container has its own set of *namespaces*

A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another. A [[Docker]] container image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings.

![[Pasted image 20230803150750.png]]

The containers differ from a [[Virtual Machine|VM]] because they are a trimmed down version of the OS, this is why the containers are faster. 