# installing-CUDA-and-NVIDIA-driver
packages installation for ubuntu 

Note:All the following described installation methods have been implemented and completed sucessfully on my desktop(ubuntu) or notebook(ubuntu)! Without doubt, I aslo saw errors confusing me and ended up with falling before because it is new to me !And it really wasted time i think!Now I get it and know how to install them more efficiently and simply with NO MISTAKE! I hope it is hopeful to you!

1> installing CUDA( CUDA Toolkit v10.0.130 as an example)

Here are two methods:
  1)Package Manager installation:This method is very simple.Moreover,you need not NVIDIA-drive as prerequisite.Make sure you download correct RPM or Deb packages for you system.More details seen at https://docs.nvidia.com/cuda/index.html
  
  2)Runfile installation:Although NVIDIA official website recommended to use above method I prefer to choose this method.The .run package has the advantages of working across a wider set of Linux distributions and uninstalling and reinstalling it easily(via 
$ sudo /usr/local/cuda-10.0/bin/uninstall_cuda_10.0.pl).You can choose needful applications or packeges which the package contains.For example.If you need not NVIDIA-driver just  unselect it.
   steps:
   One: execute Pre-installation action in https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#pre-installation-actions
    
    1.1. Verify You Have a CUDA-Capable GPU
 
      $ lspci | grep -i nvidia
I
    1.2. Verify You Have a Supported Version of Linux

      $ uname -m && cat /etc/*release

    1.3. Verify the System Has gcc Installed

       $ gcc --version

    1.4. Verify the System has the Correct Kernel Headers and Development Packages Installed

     $ uname -r

        RHEL/CentOS 
           $ sudo yum install kernel-devel-$(uname -r) kernel-headers-$(uname -r)
        Fedora
           $ sudo dnf install kernel-devel-$(uname -r) kernel-headers-$(uname -r)
        OpenSUSE/SLES
           $ uname -r
           3.16.6-2-default
           $ sudo zypper install kernel-<variant>-devel=<version>
        Ubuntu
          $ sudo apt-get install linux-headers-$(uname -r)
          
     1.5. Download the NVIDIA CUDA Toolkit
        The NVIDIA CUDA Toolkit is available at http://developer.nvidia.com/cuda-downloads.
 
 Two:
  2.1 The Nouveau drivers are loaded if the following command prints anything:
      $ lsmod | grep nouveau
     
   To install the Display Driver, the Nouveau drivers must first be disabled. Each distribution of Linux has a different
  method for disabling Nouveau.
 
  Fedora
     Create a file at /usr/lib/modprobe.d/blacklist-nouveau.conf with the following contents:
         blacklist nouveau
         options nouveau modeset=0
     Regenerate the kernel initramfs:
         $ sudo dracut --force
     Run the below command:
         $ sudo grub2-mkconfig -o /boot/grub2/grub.cfg
     Reboot the system.
  
  RHEL/CentOS
      Create a file at /etc/modprobe.d/blacklist-nouveau.conf with the following contents:
         blacklist nouveau
         options nouveau modeset=0
      Regenerate the kernel initramfs:
         $ sudo dracut --force
  OpenSUSE
     Create a file at /etc/modprobe.d/blacklist-nouveau.conf with the following contents:
        blacklist nouveau
        options nouveau modeset=0
     Regenerate the kernel initrd:
        $ sudo /sbin/mkinitrd
  Ubuntu
     Create a file at /etc/modprobe.d/blacklist-nouveau.conf with the following contents:
        blacklist nouveau
        ptions nouveau modeset=0
     Regenerate the kernel initramfs:
        $ sudo update-initramfs -u
 2.2 Reboot into text mode (runlevel 3)
    shutdown graphical interface 
        $ sudo init 3
    Change to text mode(tty1)
        Ctrl+Alt+F1
    Verify that the Nouveau drivers are not loaded
        $ lsmod | grep nouveau
    Run the installer and follow the on-screen prompts (remember that do not select NVIDIA driver which may causes login errors)
        $ sudo sh cuda_<version>_linux.run
    reboot
        $ reboot

Three: Environment Setup and verify the installation
 
 3.1  To add this path to the PATH variable
     $ export PATH=/usr/local/cuda-10.0/bin${PATH:+:${PATH}}
     The LD_LIBRARY_PATH variable (64bit)
     $ export LD_LIBRARY_PATH=/usr/local/cuda-10.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
  3.2 verify the installation
     $nvcc -V
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2018 NVIDIA Corporation
Built on Tue_Jan_10_13:22:03_CDT_2018
Cuda compilation tools, release 10.0, V10.0.130

END

  
  
   



