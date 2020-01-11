# Issues encountered with bitbucket

Based on the error message you posted, looks like this is a problem with Visual Studio. I found a solution in the Visual Studio forum, you could try this: 

1. Delete this folder (backing it up in case you need to restore it):
```
C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\Common7\IDE\CommonExtensions\Microsoft\TeamFoundation\Team Explorer\Git
```
2. Uninstall all versions of Git via Control Panel / Uninstall a program.
3. Run the Visual Studio 2017 installer and modify the install to remove Git For Windows.
4. Download the latest version of Git and install it.
5. Run the Visual Studio 2017 installer again and modify the install to add Git For Windows again.
