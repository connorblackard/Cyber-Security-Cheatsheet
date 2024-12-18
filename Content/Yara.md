## Yara
### Usage

- Scanning a file: `yara64 yara-rules-extended.yar c:\Windows\System32\cmd.exe`
- Compiling a rules file: `yarac64 yara-rules-extended.yar compiled_yara.yac`
- Scanning a file with compiled rules: `yara64 -C compiled_yara.yac c:\windows\System32\cmd.exe`
    - Must run on the same version of yara that compiled the file
- Creating an index.yar file: `Get-ChildItem *.yar | ForEach-Object { 'include "{0}"' -f $_.Name } | Out-File index.yar -Encoding ascii`

### Rules

- [https://yarahq.github.io/](https://yarahq.github.io/)
- [https://github.com/Neo23x0/signature-base](https://github.com/Neo23x0/signature-base)
- [https://github.com/elastic/protections-artifacts/tree/main/yara](https://github.com/elastic/protections-artifacts/tree/main/yara)

Additional Resources:
- [https://github.com/InQuest/awesome-yara](https://github.com/InQuest/awesome-yara)

*** 
[Return to home page](../README.md)