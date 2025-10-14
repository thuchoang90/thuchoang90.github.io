---
layout: post
title: Install VLSI-CAD tools on Ubuntu (24.04)
categories: Tutorial
tags: VLSI Linux Tutorial
---

## I. Preparation
Install some dependencies:
```shell
$ sudo apt install ksh csh zsh patchelf xvfb
```
Make changes to **YOUR** `~/.bashrc` according to the [example](/assets/sources/other/bashrc).<br/>
In the example, watch from the mark `# VLSI-CAD TOOLS` *<ins>to the end</ins>*.<br/>
Make sure to put the correct installation folder to those `export ...` .

The **bin-PATH** and **HOME-PATH** are two different things and serve different purposes.<br/>
You can change the **bin-PATH** names, but please keep the **HOME-PATH** names because the tool's environment needs those exact **HOME-PATH** names.

## II. Install CADENCE Tools
### II. 1) Installation
- **Step 1:** After downloading all the data, unzip all the tarballs.

- **Step 2:** If there are multi-part tarballs (like `...1of4`, `...2of4`, etc.), extract each tarball, and then merge all the folders into one.<br/>
You can run it by the terminal: `$ mv <name>_*/* .`

- **Step 3:** To run the installation GUI: `$ IScape/iscape/bin/iscape.sh`

- **Step 4:** On the GUI, select the `Local directory/Media install` and browse to the `CDROM1` folder in the merged folder in *step 2*.

- **Step 5:** Follow the GUI, choose the installation folder, start, wait -> done.<br/>
It is best to wait for the GUI and do nothing; don't interact with other terminals; the GUI is quite fragile!

- **Step 6:** If there are many versions, install the LOWEST (or OLDEST) version FIRST.

- **Step 7:** If there are Base, Hotfix, and Update on the SAME VERSION, the install sequence should be: Base -> Hotfix -> Update.<br/>
Please DON'T install Hotfix/Update in a separate folder with the Base.

- **Step 8:** After the installation, you can remove the `install/` and `installData/` folders to restore some spaces.

### II. 2) About the OA_HOME
All the Cadence tools require an `OA_HOME` .<br/>
Each tool sometimes carries its own local `oa_...` folder (not always).

We need to look for those local `oa_...` folders and choose the one with the latest `linux_rhel...` in its `lib/` .<br/>
Usually, **INNOVUS** or **IC** will have the latest version.

When you decided which `oa_...` folder to use,<br/>
-> put the correct **PATH** to the `OA_HOME` in the `~/.bashrc` .<br/>
-> put the correct `OA_UNSUPPORTED_PLAT` in the `~/.bashrc`, too.<br/>
The `OA_UNSUPPORTED_PLAT` must match the name `linux_rhel...` in the `$OA_HOME/lib/` folder.<br/>
<ins>*Note:*</ins> The suffix `_64` must be removed from the `OA_UNSUPPORTED_PLAT` .
   
Finally, open the `$OA_HOME/bin/sysname` and change the 1st line from `#!/bin/sh` to `#!/bin/bash` .

### II. 3) CADENCE Tool List
After installed, to check if the tool works, try to run the following:
```shell
   $ ASSURA/bin/assura
   $ CONFRML/bin/lec_64
   $ DDI/bin/genus
   $ DDI/bin/innovus
   $ DDI/bin/joules
   $ GENUS/bin/genus
   $ IC23/bin/virtuoso
   $ IC618/bin/virtuoso
   $ ICADV/bin/virtuoso
   $ INNOVUS/bin/innovus
   $ JasperGold/bin/jaspergold
   $ LIBERATE/bin/liberate
   $ MVS/bin/lpa
   $ PEGASUS/bin/pegasus
   $ PVS/bin/pvs
   $ QUANTUS/bin/quantus
   $ SIGRITY/tools/bin/3dworkbench
   $ SPB/bin/XScale
   $ SPECTRE/bin/spectre
   $ SSV/bin/tempus
   $ STRATUS/bin/stratus
   $ XCELIUM/tools/bin/xrun
```
As long as the tool opens (maybe complains about the license), then you are fine.<br/>
If the tool shows errors (mostly related to those .so files) and does not open, then you have to try to fix the errors.

## III. Install MENTOR GRAPHICS Tools
### III. 1) Installation
- **Step 1:** Untar all the tarballs.

- **Step 2:** Run the `.exe`, `.bin`, `.mib`, or `.aol` directly and follow the guide in the terminal.<br/>
(for **calibre** tool, choose the `aok...` version if Ubuntu)

- **Step 3:** After the installation, you can remove the `_msidata/` and `install.aol/` folders to restore some spaces.

### III. 2) Fix Calibre Error
After installed, when you're trying to run the **calibre** and get this error:
```shell
   Invalid operating system environment, VENDOR=unknown OS VERSION=24
```
This means the tool checked your OS version and said it doesn't support the OS.<br/>
-> Follow these steps to bypass the check:

- **Step 1:** Check this website: [https://calibre.mentorcloudservices.com/docs/Calibre_OS_Roadmap.htm](https://calibre.mentorcloudservices.com/docs/Calibre_OS_Roadmap.htm)<br/>
For example, if you previously installed the `aok...` version, you now have to 'trick' the tool into thinking that your machine is a RedHat 8 version.

- **Step 2:** In the **calibre** installation path: `$ vi pkgs/icv_calenv/pvt/calibre_host_info`<br/>
<ins>At the end</ins> of the file, write these two lines in:
```shell
   OS_VENDOR='redhat'
   OS_MAJOR_REV='8'
```
In the calibre's installation folder, there is a folder named **tmp** or **temp**.<br>
That is a symbolic link, and it has to be true.<br>
If you see it is showing red, means the link is broken. -> You have to correct it.

Usually, the **tmp** folder in Ubuntu filesystem is at **/tmp**.<br>
So, do the following to re-correct the link:
```shell
   $ rm tmp
   $ sudo ln -s /tmp tmp
```

### III. 3) MENTOR GRAPHICS Tool List
After installed, to check if the tool works, try to run the following:
```shell
   $ 0-in/linux_x86_64/bin/0in
   $ AMSV/amsv/bin/afs
   $ Calibre/bin/calibre
   $ DFT/bin/dftadvisor
   $ LeonardSpectrum/bin/Linux/spectrum
   $ ModelSim/bin/vsim
   $ Pyxis/bin/da_ic
   $ QuestaSim/bin/vlib
```
As long as the tool opens (maybe complains about the license), then you are fine.<br/>
If the tool shows errors (mostly related to those .so files) and does not open, then you have to try to fix the errors.

## IV. Install SYNOPSYS Tools
### IV. 1) Installation
- **Step 1:** Go to the `synopsys_installer/` folder and run the `.run` file.<br/>
It'll self-extract into a series of files. The `setup.sh` is the one we need.

- **Step 2:** Open the installation GUI by running that `setup.sh` .<br/>
<ins>*Note:*</ins> the `Site ID Number` = `000` is ok.

- **Step 3:** Browse to each folder, set the target installation folder, install, wait -> done.<br/>
<ins>*Note 1:*</ins> The download folder (containning those .spf files) and the destination folder must be different; the GUI wants that.<br/>
-> In my experience, I set the destination folder = `.../Synopsys/` while my download folder = `.../Synopsys/toolname/` .<br/>
<ins>*Note 2:*</ins> You might have to re-run the `setup.sh` GUI after each installation.
   
- **Step 4:** If you see an error about **OVERLAY**, another tool must be installed first.<br/>
<ins>*Note:*</ins> The versions of the required TOOL and the OVERLAY TOOL must match in order to continue with the installation.

### IV. 2) SYNOPSYS Tool List
After installed, to check if the tool works, try to run the following:
```shell
   $ customcompiler/W-2024.09/bin/custom_compiler
   $ finesim/Q-2020.03-SP1/bin/finesim
   $ formality/W-2024.09/bin/fm_shell
   $ fpga/U-2023.03/bin/synplify_pro
   $ fusioncompiler/W-2024.09/bin/fc_shell
   $ fusioncompiler/W-2024.09/bin/icc2_lm_shell
   $ fusioncompiler/W-2024.09/bin/lm_shell
   $ hercules/B-2008.09-SP5-1/bin/amd64/hercules
   $ hsim/Q-2020.03-SP2/hsimplus/bin/hsim
   $ hspice/W-2024.09-1/hspice/bin/hspice
   $ icc/W-2024.09/bin/icc_shell
   $ icc2/W-2024.09/bin/icc2_shell
   $ icv_workbench/V-2023.09-SP2/bin/linux64/icvwb
   $ icvalidator/W-2024.09-2/bin/icv64
   $ idq/R-2020.09-SP4/linux64/iddq/bin/ipro
   $ library_compiler/W-2024.09/bin/lc_shell
   $ milkyway/W-2024.09/bin/linux64/Milkyway
   $ nanotime/V-2023.12-SP5/bin/nt_shell
   $ primelib/T-2022.03-1/bin/primelib
   $ primerail/M-2017.06-SP3/bin/pr_shell
   $ primesim/T-2022.06-SP2-2/bin/primesim
   $ primetime/U-2022.12-SP5-4/bin/pt_shell
   $ primewave/W-2024.09/bin/primewave
   $ primewavereliability/W-2024.09/bin/primewave_reliability
   $ quantumatk/W-2024.09-SP1/bin/quantumatk
   $ quickcap/W-2024.09/bin/quickcap
   $ raphael/T-2022.03/bin/raphael
   $ raphael_fx/T-2022.03-SP1/bin/raphael_fx
   $ rtl_architect/T-2022.03-SP1/bin/rtl_shell
   $ sentaurus/W-2024.09/bin/qtx
   $ sentaurus_explorer/W-2024.09/bin/spx
   $ slitho/U-2022.12/bin/slitho
   $ slitho_pwa/U-2022.12/bin/pwa
   $ spxviewer/W-2024.09/bin/spx_routeview
   $ spyglass/V-2023.12/SPYGLASS_HOME/bin/spyglass
   $ starrc/V-2023.12-SP5/bin/starrc_shell
   $ syn/W-2024.09/bin/dc_shell
   $ taurus/S_2021.06/bin/medici
   $ tetramax/R-2020.09-SP4/bin/tmax2
   $ vcs/W-2024.09/bin/vcs
   $ vc_static/S-2021.09-SP2-4/bin/vc_static_shell
   $ verdi/T-2022.06-SP1-1/bin/verdi
   $ waveview/W-2024.09-2/bin/wv
   $ xa/W-2024.09-1/bin/xa
```
As long as the tool opens (maybe complains about the license), then you are fine.<br/>
If the tool shows errors (mostly related to those .so files) and does not open, then you have to try to fix the errors.

## V. Fix .so Error
### V. 1) Fix Missing .so Files
Fix the missing or wrong `<name>.so.<number>` file:

- **Step 1:** Check if the `<name>.so.<number>` or the `<name>.so` in the system or not.<br/>
The check command: `$ whereis <name>.so.<number>` or: `$ whereis <name>.so`<br/>
-> If not found, proceed to *step 2*.<br/>
-> If found, create a symbolic link and link it back to the `/usr/lib/` folder.<br/>
The link command: `$ ln -s /path/to/filename /usr/lib/<name>.so.<number>`

- **Step 2:** If the `<name>.so.<number>` or `<name>.so` file cannot be found by `whereis`, then try to `apt install` it first.<br/>
The apt install command: `$ sudo apt-get install <name>` or: `$ sudo apt-get install <name><number>`<br/>
<ins>*Note:*</ins> The `<name>` is usually all <ins>de-capitalized</ins>, and <ins>NO dot</ins> `.` in between the `<name>` and the `<number>` .<br/>
-> If the apt package or the exact version is unavailable, proceed to *step 3*.

- **Step 3:** In this step, you have to download the `<name>.so.<number>` manually. Go to this website: [https://pkgs.org/](https://pkgs.org/)<br/>
Search for the full name of `<name>.so.<number>` . Pick either **Solus** or **FreeBSD/NetBSD**.<br/>
Beware of the 32-bit or 64-bit version, pick the one you need. Download it, untar it.<br/>
Beware of the link files, after untar, always use `ll` to check, not `ls` -> So you can see where the link is going to.<br/>
Copy only the content file (*NOT* the link file) to the `/usr/lib/` folder.<br/>
Then, go to the `/usr/lib/` folder and re-create the link file by: `$ sudo ln -s <raw file> <name>.so.<number>` .

- **Step 4:** If the error still exists and says `ELF32` or `ELF64` wrong, you copied the wrong 32/64-bit version.<br/>
-> Repeat *step 3* and download the corrected ones.

### V. 2) Other Errors
- **Problem 1:** If the error says something about `undefined symbol`, for example:
```shell
   undefined symbol: ucal_openTimeZones_50
```
Maybe it's still about the missing .so file, let's `grep -r` and see if something comes up: `$ grep -r ucal_openTimeZones_50` :
```shell
   grep: tools.lnx86/lib/cdnslibicui18n.so.50.1.2: binary file matches
   grep: tools.lnx86/lib/64bit/cdnslibicui18n.so.50.1.2: binary file matches
   grep: tools.lnx86/Qt/v5/64bit/lib/libcdsQt5Core.so.5.15.9: binary file matches
```
In this case, it means you're missing the `cdnslibicui18n.so` file.<br/>
-> So, let's repeat from the *step 1* in the <ins>*previous section*</ins>.

- **Problem 2:** If these kind of errors show up: `operator`, `unexpected`, `syntax error`; for example:
```shell
   test: unexpected operator
   Syntax error: redirection unexpected
   Syntax error: "(" unexpected
   [: 0: unexpected operator
   /bin/sh: 0: Illegal option -h
```
Then, this is about the bash-script environment.<br/>
Open the run file, change the 1st line from `#!/bin/sh` to `#!/bin/bash` and try again.

- **Problem 3:** If the error says something about `GLIBC`, it could be very serious or still about some missing .so files.<br/>
Take a closer look at the error message. If it said something like this:
```shell
   tools.lnx86/lib/64bit/<name>.so.<number>: version `GLIBC_X.X' not found (required by ...)
```
Look closely at the **PATH** of the `<name>.so.<number>` file, and you'll see it uses its own local lib of `tools.lnx86/lib/64bit/`, not the system's lib like `/usr/...` or `/lib/...` .<br/>
Maybe the system doesn't have that `<name>.so.<number>` file -> The tool is trying to use its own local version, which is causing the problem.<br/>
To know for sure, try `whereis` the `<name>.so.<number>` and check if the system has it or not. -> This means you're repeating the *step 1* in the <ins>previous section</ins>.

- **Problem 4:** Same as the previous problem, however, this time, the **PATH** of the `<name>.so.<number>` DO belongs to the system's lib. For example:
```shell
   /lib/x86_64-linux-gnu/<name>.so.<number>: version `GLIBC_X.X' not found (required by ...)
```
Yeah, in this case, this is serious. Mismatching **GLIBC** between the tool and its host is a horror for any Linux dev.<br/>
Just a sanity check, let's still do a `$ whereis <name>.so.<number>` .<br/>

If the `<name>.so.<number>` is there, properly linked, but the error persists, then you're left with only one option: <ins>upgrade</ins> or <ins>downgrade</ins> the **GLIBC** (which is not recommended anywhere).<br/>

**GLIBC** *IS* the Kernel. Messing with it could destroy your OS, so do it at your own risk.<br/>
When you're ready, check the [Install VLSI-CAD Tools with GLIBC_Problem](/tutorial/2025/03/10/Install-VLSI-tools-GLIBC-problem) guide.

### V. 3) Backup Solution
**NOTE:** This solution is a backup and not recommended because tricking the VLSI-CAD tools this way could lead to unforeseen problems.<br/>
Sometimes, it causes problems for other tools, not even the VLSI-CAD tools.

You can create a 'fake' **redhat-release** file by: `$ sudo vi /etc/redhat-release`<br/>
Then, write this line:
```shell
   CentOS Linux release 8.<sub-version>.<date> (Core)
```
For the `<sub-version>` and `<date>`, check this website: [https://access.redhat.com/articles/3078](https://access.redhat.com/articles/3078)<br/>
The `<date>` is a 4-digit number: first 2-digit for year, and last 2-digit for month.

For example, if you want to pick the RedHat 7.0 version, then:
```shell
   CentOS Linux release 7.0.1406 (Core)
```
If you want to pick the RedHat 8.0 version, then:
```shell
   CentOS Linux release 8.0.1905 (Core)
```
If you want to pick the RedHat 8.10 version, then:
```shell
   CentOS Linux release 8.10.2405 (Core)
```
