# How to fix "Docker doesn't support your Windows version. Check documentation for minimum requirements"

This problem is not with Docker itself, it is with Powershell. The fix described below also fixes the problem with "The specified module 'SOME_MODULE_NAME' was not loaded because no valid module file was found in any module directory."

Docker uses Powershell's Hyper-V module to do its business. With Process Monitor, I saw that Docker was trying to get the Hyper-V module at C:\Users\YOUR_USER_NAME\Documents\WindowsPowerShell\Modules. The Hyper-V module is located at C:\Windows\System32\WindowsPowerShell\v1.0\Modules.

So, what I did was (you must be an administrator to do this):
1. Open 2 Windows Explorers: one for C:\Users\YOUR_USER_NAME\Documents\WindowsPowerShell\Modules, one for C:\Windows\System32\WindowsPowerShell\v1.0\Modules.
2. Copy all folders under C:\Users\YOUR_USER_NAME\Documents\WindowsPowerShell\Modules to C:\Windows\System32\WindowsPowerShell\v1.0\Modules.
3. Erase folder C:\Users\YOUR_USER_NAME\Documents\WindowsPowerShell\Modules.
4. Open a command prompt as administrator.
5. Run the following command in order to create a join symbolic link:

mklink /J C:\Users\YOUR_USER_NAME\Documents\WindowsPowerShell\Modules C:\Windows\System32\WindowsPowerShell\v1.0\Modules

That's it.


