# Extension
#include &lt;File.au3>  Local $aRoot[] = ["c:\Apps\Temp\","c:\users\" &amp; @UserName &amp; "AppData\local\"] ; add as much root folders as you want here Local $aFile, $sFile, $sContent, $sDrive, $sDir, $sFileName, $sExtension For $sFolder in $aRoot   ConsoleWrite ($sFolder &amp; @CRLF)   $aFile = _FileListToArrayRec($sFolder, "*.HOD;*.WS", $FLTAR_FILES, $FLTAR_RECUR, Default, $FLTAR_FULLPATH)   If @error Then ContinueLoop   For $i = 1 To $aFile[0]     $sFile = $aFile[$i]     $sContent = FileRead($sFile)     _PathSplit($sFile, $sDrive, $sDir, $sFileName, $sExtension)     If $sExtension = ".HOD" Then       $sContent = StringRegExpReplace($sContent, "(?is)(Host=)(\d+\.\d+\.\d+\.\d+)","$1DNSNAME")     Else       $sContent = StringRegExpReplace($sContent, "(?is)(HostName=)(\d+\.\d+\.\d+\.\d+)","$1DNSNAME")     EndIf     FileWrite($sDrive &amp; $sDir &amp; "New_" &amp; $sFileName &amp; $sExtension, $sContent)   Next Next
