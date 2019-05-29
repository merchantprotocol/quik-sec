quik-sec (Quick Security) 
--
Command Line Module For Magento 2 Security


## Monitoring files

**Find all files changed within the last 15 days**
```
find ./ -type f -mtime -15
```

**Use Git to check for changed files**
This is not sufficient enough. It will not track the temporary directories like `pub/media` which is also an uploads directory set to 777. We will need to build something for our own protection.
```
git status
```

**Search for command commands**
```
find . -type f -name '*.php' | xargs grep -l "eval *(" --color
find . -type f -name '*.php' | xargs grep -l "base64_decode *(" --color
find . -type f -name '*.php' | xargs grep -l "gzinflate *(" --color
find . -type f -name '*.php' | xargs grep -l "str_rot13 *(" --color
find . -type f -name '*.php' | xargs egrep -i "(mail|fsockopen|pfsockopen|stream_socket_client|exec|system|passthru|eval|base64_decode) *\("
find . -type f -name '*.php' | xargs egrep -i "preg_replace *\((['|\"])(.).*\2[a-z]*e[^\1]*\1 *," --color
```

```
find . -type f -name '*.php' | xargs grep base64_ | less
find . -type f -name '*.php' | xargs grep base64_ > results.txt
```

**Search Apache Files**
```
find . -type f -name '\.htaccess' | xargs grep -i auto_prepend_file;
find . -type f -name '\.htaccess' | xargs grep -i auto_append_file;
find . -type f -name '\.htaccess' | xargs grep -i http;
```

**Search just for changed files lately**
```
find /home/*/public_html/ -type f -mtime -7 -maxdepth 4 -exec egrep -q “eval\(|exec\(|gzinflate\(|base64_decode\(|str_rot13\(|gzuncompress\(|rawurldecode\(|strrev\(|ini_set\(chr|chr\(rand\(|shell_exec\(|fopen\(|curl_exec\(|popen\(|x..x..” {} \; -print > /tmp/suspected-malware.txt
```

## Directory

- Check for symlinks
- Check for public directories
- Check for publicly accessible zip files
- Check for Installed programs

## Modsec

- Set the default magento modsec files
- Check modsec rules
- Check status
- whitelist IPs
- blacklist IPs
- enable/disable rules
- enable/disable urls

## selinux

- Check status
- Check file settings
- Set file settings

## Logs

- 90 days of logs stored on the server
- 365 days of logs archived on S3
