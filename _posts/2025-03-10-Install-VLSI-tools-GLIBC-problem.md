---
layout: post
title: Install VLSI-CAD tools with GLIBC problem
categories: Tutorial
tags: VLSI Linux Tutorial
---

<ins>**WARNING:**</ins> Like I said, this solution could destroy your OS if you're not careful enough.<br/>
Reinstalling OS and all the VLSI-CAD tools is not fun. So, do it at your own risk.

## I. Main Solution
- **Step 1:** First of all, check your GLIBC version:
```shell
   $ ldd --version
```
Example print-out:
```shell
   ldd (Ubuntu GLIBC 2.39-0ubuntu8.4) 2.39
```
I'm using Ubuntu 24.04, and according to this, my GLIBC version is `2.39` .<br/>
-> This means `2.39` is not working. So we have to downgrade it (or upgrade it, we don't know yet).

- **Step 2:** Note on the **run file** in the `bin/` folder vs. the *executable* **ELF file**:<br/>
The **run file** in a tool's `bin/` is usually a **.sh file** to set the environment. It will eventually call to the actual *executable* **ELF file**, but it is *NOT* the **ELF file**.<br/>
-> To know where the **ELF file** is, the easiest way is to run the **run file**. -> The true **PATH** to the **ELF file** will shown in the error.<br/>
-> The `$ objdump` command in the next step must point to the *executable* **ELF file**, *NOT* the **run file**.

- **Step 3:** Sometimes the error says which version it is looking for, and sometimes it just says `GLIBC_PRIVATE` .<br/>
-> Regardless of what it said, even if it stated which version, don't believe it yet.<br/>
We need to check it manually. The check command:
```shell
   $ objdump -T /path/to/the/executable/ELF/file | grep GLIBC_ | sed 's/.*GLIBC_\([.0-9]*\).*/\1/g' | sort -Vu
```
Example print-out:
```shell
   2.2.5
   2.3
   2.3.2
   2.3.3
   2.3.4
   2.4
   2.6
   2.7
   2.11
```
According to this example, the minimum required GLIBC version is `2.11` .<br/>
-> Combined with the previous information in *step 1*, we now know we have to *DOWNGRADE* the GLIBC to the range: `2.39` > **wanted-version** >= `2.11`.

<ins>*Note 1:*</ins> Downgrade or upgrade depends on what information you get from *steps 1 and 3*. In my example, this will be a downgrade, but it might be an upgrade on your machine.

<ins>*Note 2:*</ins> Remember, you checked only the *executable* **ELF file**. However, there may be more run/lib files behind, and they could request a more recent version of GLIBC.<br/>
-> So, don't downgrade it too far, and if you have to upgrade it, upgrade only the requested version (not the latest).

- **Step 4:** You need to decide which GLIBC version you want. Check the source: https://launchpad.net/ubuntu/+source/glibc/

From the website, we have `2.41` (*the latest*), `2.39` (*Ubuntu24.04*), `2.35` (*Ubuntu22.04*), `2.31` (*Ubuntu20.04*), `2.27` (*Ubuntu18.04*), and so on.

Let's say, I know my tool was released around 2020. -> So, `2.31` (*Ubuntu20.04*) sounds reasonable. Let's do that first. -> And if that doesn't work, we'll try `2.27` (*Ubuntu18.04*), and so on.<br/>

Just note which version you want to get; you don't need to download anything (yet).

- **Step 5:** Download the Ubuntu .iso image from the website: https://ubuntu.com/download/alternative-downloads

From the previous step, we have already chosen *Ubuntu20.04* (with GLIBC version `2.31`). -> So let's download that **Ubuntu 20.04LTS** .iso image.

To mount the .iso file, usually just double-click is enough.<br/>
Then, go to the .iso mounted folder and navigate to the `casper/` folder.<br/>
There, you will find the `filesystem.squashfs` file.<br/>
-> Open a new terminal from there, then do this to unsquash it to your `Downloads/` folder:
```shell
   $ sudo unsquashfs -d ~/Downloads/unsquashfs filesystem.squashfs
```
This will unsquash all the .iso disc data to your `~/Downloads/unsquashfs` folder.<br/>
Finally, let's copy that data to our system in `/usr/`; let's say, `/usr/glibc-2.31` :
```shell
   $ sudo cp -rf ~/Downloads/unsquashfs/usr /usr/glibc-2.31
```
After this, you can now run the tool with overridden `$PATH` and `$LD_LIBRARY_PATH` .

- **Step 6:** Before running the tool with `/usr/glibc-2.31/` , we need to modify the **ELF file**'s *linker-PATH*.

Because we're going to mess with the **ELF file**, it's better to save the *original* **ELF file** to *another* **ELF file**. For example: `$ cp ./finesim ./finesim.bak`

To change the **ELF file**'s *linker-PATH*, use the command:
```shell
   $ patchelf --set-interpreter <linker-PATH> <filename>
```
For example:
```shell
   $ patchelf --set-interpreter /usr/glibc-2.31/lib/x86_64-linux-gnu/ld-linux-x86-64.so.2 ./finesim
```
<ins>*Note:*</ins> This `patchelf --set-interpreter` must point to the *executable* **ELF file**, *NOT* the **run rile**.

- **Step 7:** Finally, we can run the tool with `/usr/glibc-2.31/` . To do that, simply run the *executable* **ELF file** (*NOT* the **run file**) with overridden `$PATH` and `$LD_LIBRARY_PATH`, like this:
```shell
   $ PATH=/usr/glibc-2.31/bin LD_LIBRARY_PATH=/usr/glibc-2.31/lib/x86_64-linux-gnu ./finesim
```
<ins>*Note:*</ins> This `./finesim` is the *executable* **ELF file**, *NOT* the **run file**.

Previously, the error is like this:
```shell
   ./finesim: /lib/x86_64-linux-gnu/libpthread.so.0: version `GLIBC_PRIVATE' not found (required by ./finesim)
```
Now, the error looks like this:
```shell
   ./finesim: /usr/glibc-2.31/lib/x86_64-linux-gnu/libc.so.6: version `GLIBC_2.33' not found (required by /lib/libncurses.so.5)
```
It is working. The `libc.so.6` is already at the correct location at `/usr/glibc-2.31/lib/x86_64-linux-gnu/` . So, it's not about the `libc.so.6` .<br/>
-> In the above example, `libncurses.so.5` is the one that is missing in the `/usr/glibc-2.31/` folder.<br/>
To deal with the missing .so files, follow the next step.

- **Step 8:** For the missing .so files in the `/usr/glibc-2.31/lib/x86_64-linux-gnu/` , first, let's do a quick check and search for a similar name in the `/usr/glibc-2.31/` (*NOT* in the `lib/x86_64-linux-gnu/`) folder:
```shell
   $ cd /usr/glibc-2.31/
   $ find . -name "<name>.so*"
```
Sometimes, the missing .so files are still in the `/usr/glibc-2.31/` , just not in the `lib/x86_64-linux-gnu/` one.

If that is the case, simply create a symbolic link in the `/usr/glibc-2.31/lib/x86_64-linux-gnu/` .<br/>
The command: `$ sudo ln -s <source file> <destination file>`

If a similar .so file is not found in `/usr/glibc-2.31/` , let's check the apt package in the next step.

- **Step 9:** Go to this website: https://packages.ubuntu.com/

Select the *released* Ubuntu version you want to download. In my case, it is **focal (20.04LTS)** because I chose the GLIBC version `2.31` from **Ubuntu20.04** in *step 4*.

Scroll down and hit **"All packages"** to display everything (this will take a while to load).

Like the error shown in the example (in *step 7*), the package I want to download is `libncurses.so.5` . -> So, I search for the name `libncurses5` .<br/>
-> For `libncurses5` , I found **"libncurses5 (6.2-0ubuntu2.1 ..."** seems good. -> So, let's take it as an example.

When you go to the package page, you can see the **"[list of files]"** to confirm that the file you're looking for is there.<br/>
-> Once you're ready, select the link that fits your **"Architecture"** (in my case, *amd64*), and it'll lead you to the download page.

On the download page, look for <ins>**3 info**</ins>: the *mirror link*, the *subdirectory*, and the *.deb filename*.<br/>
-> Then, you can download it by:
```shell
   $ wget <mirror link>/<subdirectory>/<the .deb filename>
```
For example:
```shell
  $ wget security.ubuntu.com/ubuntu/pool/universe/n/ncurses/libncurses5_6.2-0ubuntu2.1_amd64.deb
```
After downloading, DO NOT install it, just EXTRACT. The extract command:
```shell
   $ dpkg-deb -x <the .deb filename> <folder name>
```
For example:
```shell
  $ dpkg-deb -x libncurses5_6.2-0ubuntu2.1_amd64.deb libncurses5
```
In the next step, do not copy *just one* .so file.<br/>
Because those .so files are usually linked, let's copy <ins>*every*</ins> .so files there.<br/>
To do that, use this command:
```shell
   $ find <folder name> -name "*.so*" -exec sudo cp '{}' <destination folder> ';'
```
For example:
```shell
   $ find libncurses5/ -name "*.so*" -exec sudo cp '{}' /usr/glibc-2.31/lib/x86_64-linux-gnu/ ';'
```
That's done. Let's try to run the tool again.

This time, it gets a new error:
```shell
   ./finesim: /lib/libtinfo.so.5: version `NCURSES_TINFO_5.6.20061217' not found (required by /usr/glibc-2.31/lib/x86_64-linux-gnu/libncurses.so.5)
```
Take a closer look, and you'll see that the `libncurses.so.5` is already at the correct location of `/usr/glibc-2.31/lib/x86_64-linux-gnu/` .<br/>
-> So, it's not about the `libncurses.so.5` -> `libtinfo.so.5` is the one that is missing.

You know what to do next: repeat the <ins>*previous step*</ins> and <ins>*this step*</ins> again, rinse and repeat until all the problems are gone.

- **Step 10:** Once the *executable* **ELF file** (*NOT* the **run file**) can run with the overridden `$PATH` and `$LD_LIBRARY_PATH` , you can make it permanent in two ways:

a) The easiest way is to modify the `~/.bashrc` , put in `alias` which records the whole command `PATH=... LD_LIBRARY_PATH=... /path/to/the/executable/ELF/file` . For example:
```shell
   alias finesim='PATH=/usr/glibc-2.31/bin LD_LIBRARY_PATH=/usr/glibc-2.31/lib/x86_64-linux-gnu/ ~/VLSI-CAD/Synopsys/finesim/Q-2020.03-SP1/finesim/platform/linux64/finesim'
```
-> This is the fastest way. However, it could miss some environment settings set up by the **run file**.

b) Therefore, the safe way is to modify the **run file** itself.<br/>
Because the **run file** is actually a **.sh file**, it will eventually call the *executable* **ELF file** somewhere in its content.

-> We have to find those places and replace them `<command>` with `PATH=... LD_LIBRARY_PATH=... <command>`.<br/>
This takes more effort but is the safest option.

## II. Backup Solution
**NOTE:** This solution was abandoned because later, I discovered that downloading the Ubuntu .iso image and then unsquash it is faster than this solution.

However, this solution has an advantage.<br/>
-> This solution allows you to rebuild an *OLDER* version of GLIBC with the *NEWER* version of GCC/Binutils/Linux, while downloading the .iso image can only give you the *OLDER* version of <ins>everything</ins>.<br/>
-> This is why I keep this solution as a backup here.

Repeat the same *steps 1 to 4* as in the <ins>other solution</ins>, then:

- **Step 5:** Besides the *GLIBC* version, you also need other information such as *Linux* version, *GCC* version, and *binutils* version of your machine.<br/>
-> By default, you WILL want to keep other things as same as your running machine.<br/>
-> That would be perfect. So, let's do that.

To check your Linux version:
```shell
   $ uname -a
```
Example print-out:
```shell
   Linux thuc-UEC 6.11.0-17-generic
```
To check your binutils version:
```shell
  $ ld -v
```
Example print-out:
```shell
   GNU ld (GNU Binutils for Ubuntu) 2.42
```
To check your GCC version:
```shell
  $ gcc --version
```
Example print-out:
```shell
  gcc (Ubuntu 13.3.0-6ubuntu2~24.04) 13.3.0
```
So, we have the following information: *Linux* `6.11.0`, *Binutils* `2.42`, and *GCC* `13.3.0` .<br/>
-> Note all of that, we're moving to the actual action.

- **Step 6:** We'll use the **crosstool-ng** tool.<br/>
Its GibHub: https://github.com/crosstool-ng/crosstool-ng<br/>
and its docs: https://crosstool-ng.github.io/docs/

Basically, this is the tool that allows you to create a custom root filesystem.<br/>
-> It'll build the whole thing, a whole package, all as one.<br/>
-> Less headache about mismatched versions between *GCC*, *GLIBC*, *binutils*, *Linux*, etc.

To make:
```shell
   $ git clone https://github.com/crosstool-ng/crosstool-ng
   $ cd crosstool-ng/
   $ mkdir install
   $ cd install/
   $ export CT_PREFIX=$(pwd)
   $ mkdir src
   $ cd ../
   $ ./bootstrap
   $ ./configure --prefix=$CT_PREFIX --enable-local
   $ make
   $ ./ct-ng x86_64-unknown-linux-gnu
   $ ./ct-ng menuconfig
```
After this, a GUI will come up. -> We need to modify several things in `menuconfig` :

a) Select `Paths and misc options`<br/>
-> Modify the `Local tarballs directory` from `${HOME}/src` to `${CT_PREFIX}/src`<br/>
-> `Exit` back outside.

b) Select `Operating System`<br/>
-> Select `Version of linux`<br/>
-> Pick the one that is EQUAL or OLDER than the one you choose in the previous step.<br/>
-> `Exit` back outside.

c) Select `Binary utilities`<br/>
-> Select `Version of binutils`<br/>
-> Pick the one that you choose in the previous step.<br/>
-> `Exit` back outside.

d) Select `C-library`<br/>
-> Select `Version of glibc`<br/>
-> Pick the one that you choose in the previous step.<br/>
-> `Exit` back outside.

e) Select `C compiler`<br/>
-> Select `Version of gcc`<br/>
-> Pick the one that you choose in the previous step.<br/>
-> `Exit` back outside.

Done, `Save` and `Exit` the GUI.

Final step, build it:
```shell
   $ env -u LD_LIBRARY_PATH time ./ct-ng build CT_JOBS=`nproc`
```
This gonna take a while.

- **Step 7:** When the build is completed, the files you want are in: `install/x86_64-unknown-linux-gnu/x86_64-unknown-linux-gnu/sysroot`

Let's copy them to, like, `/usr/glibc-2.31` :
```shell
   $ sudo cp -rf install/x86_64-unknown-linux-gnu/x86_64-unknown-linux-gnu/sysroot /usr/glibc-2.31
```
Now, you can run your tool with the overridden `$PATH` and `$LD_LIBRARY_PATH` .

<ins>*Note:*</ins> If you want to rebuild the **crosstool-ng**, just remove the `install/` and `.build/` folders and start again.

The rest of this solution repeats the same *steps 6 to 10* as in the <ins>other solution</ins>, with some differences:

a) The *linker-PATH* `ld-linux-x86-64.so.2` is in the `/usr/glibc-2.31/lib/` folder, *NOT* in the `/usr/glibc-2.31/lib/x86_64-linux-gnu/` folder as in the <ins>other solution</ins>.

b) For the `$PATH` and `$LD_LIBRARY_PATH` , they should point to:
```shell
   PATH=/usr/test/usr/bin          #(instead of PATH=/usr/glibc-2.31/bin as in the other solution)
   LD_LIBRARY_PATH=/usr/test/lib   #(instead of LD_LIBRARY_PATH=/usr/glibc-2.31/lib/x86_64-linux-gnu as in the other solution)
```
