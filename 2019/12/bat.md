## 批量停止脚本
```
::::::::::::::批量停止脚本::::::::::::::::::
@echo off & setlocal EnableDelayedExpansion
echo ::::::::::::::::::::::::::::::::::::
jps -l
jps -l>scipt.txt

set /a j=1
for /f "delims=," %%i in (scipt.txt) do (
set con=%%i
echo !con!

set EXISTS_FLAG=false
echo !con!|find ".Jps">nul&&set EXISTS_FLAG=true
echo !EXISTS_FLAG!
if !EXISTS_FLAG!==true (
echo 这行内容符合筛选的标准
set str="aa bb cc"
for /f "tokens=*" %%v in (%str%) do (
echo %%v
) 
) else (
echo 不符合标准
)
echo ****************************************
)
:::::::::::::::::::::::::::::::::::::::::::::::::
```