# Windows - custom prompt batch file


```bat
@echo off
:: Temporary system path at cmd startup
TITLE PROFILE SET FOR %USERNAME% ON %COMPUTERNAME% - %USERNAME% - %DATE% %TIME%
::MODE CON:cols=150 lines=55
::call conSize 140 65 140 9999

::Background Black + ForeGround Red
::COLOR 0C  
::Background LightAqua + ForeGround Black
::color B0
color 70
cls

:: Add to path by command
:: SET ORACLE_HOME=C:\Oracle\product\12.1.0\client_64bit
::SET FFMPEG_HOME=C:\D\APP\ffmpeg
::set PATH=%ORACLE_HOME%\BIN;C:\D\APP\DIG\bin;C:\D\APP\MinGW\bin;%FFMPEG_HOME%\bin;%PATH%
:: Commands
	
:: Lists wtih out Header
:: List Just Directories
:: List Both Directories & Files
:: List Short Names


:: DOSKEY sublime=sublime_text $*  
:: Common directories

DOSKEY chromecache=cd/d "%LOCALAPPDATA%\Google\Chrome\User Data\Default"
DOSKEY desktop=cd "C:\Users\%USERNAME%\Desktop"
DOSKEY alias=doskey /macros:all
DOSKEY bash="C:\Program Files\Git\git-bash.exe" --cd-to-home
DOSKEY lp=dir *.py* /b
DOSKEY batch=cd /d "C:\D\APP\Dropbox\BATCH"
DOSKEY research=cd %USERPROFILE%\Dropbox\Research\
DOSKEY sq=call "C:\D\APP\Dropbox\BATCH\env.listsql.cmd"
DOSKEY sq1=call "C:\D\APP\Dropbox\BATCH\env.listsql1.cmd"
DOSKEY ba=call "C:\D\APP\Dropbox\BATCH\env.listbatch.cmd"
DOSKEY reload=call "C:\D\APP\Dropbox\BATCH\reload.cmd"
DOSKEY aconda=%windir%\System32\cmd.exe "/K" D:\APP\Anaconda3\Scripts\activate.bat D:\APP\Anaconda3
DOSKEY env1=activate carnd-term1
DOSKEY mydesk=ping xxxx -t

setlocal enabledelayedexpansion
SET "TAB=      "
echo %TAB%:::::PATH VARIABLE CONSISTS BELOW :::::
echo %TAB%:::::TO MAKE ANY SPECIFIC VAR APPEAR BEFORE IN LIST - UPDATE PATH VAR ::::: 
set themes=%PATH%
set x=0
set result=0
for %%a in ("%themes:;=" "%") do (
  set /A result=!result! + 1
  set PATHVAR=%%~a
  if defined PATHVAR echo [!result!.] %%~a
)
endlocal

doskey /macros:all

cd /d "C:\Users\%USERNAME%"
REM cd /d "D:\APP\Anaconda3"
REM conda info --envs

ipconfig /all | FINDSTR "IPv4 Mask Servers"

set dircmd=/ogne
REM prompt [$p]$_$g
prompt %DATE:~-10% %TIME:~0,8% [$p]$_$g
GOTO:eof

```
