# 1.1 Install Java (OpenJDK)
```bash
sudo apt update
sudo apt search openjdk
sudo apt install openjdk-21-jdk
java --version
update-alternatives --list java
sudo update-alternatives --config java
dpkg --list | grep openjdk
sudo apt remove openjdk-11-jdk
sudo apt autoremove
```

# remove java version
* https://stackoverflow.com/questions/29964042/how-to-remove-old-version-of-java-and-install-new-version
```bash
ls /usr/local/java/
sudo apt-get purge openjdk-\*
```


# find java install path
list installed java versions
```
which java
ls -la /usr/bin/java
readlink -f $(which java)
update-java-alternatives -l
dpkg -l | grep java
```

# delete remove java
* search the entire filesystem `find / -name "java" 2>/dev/null`
```bash
sudo apt remove --purge openjdk-\*
sudo apt remove openjdk-11-jre openjdk-11-jdk
sudo update-alternatives --remove java /path/to/java/bin/java
sudo apt purge 'openjdk*'
sudo apt autoremove
sudo apt autoclean
```
