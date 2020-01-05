# Ubuntu18 : Installing Eclipse Script


```sh
######## INSTALLING ECLIPSE ON UBUNTU STEPS - SCRIPT###################################
cd /tmp
sudo apt purge --auto-remove cmake
sudo -E add-apt-repository -y ppa:george-edison55/cmake-3.x
sudo -E apt-get update
sudo apt-get -y install cmake
sudo apt-get -y install build-essential

cd /tmp
wget -O eclipse-cpp-neon-R-linux-gtk-x86_64.tar.gz http://eclipse.mirror.triple-it.nl/technology/epp/downloads/release/neon/R/eclipse-cpp-neon-R-linux-gtk-x86_64.tar.gz
tar -xzf /tmp/eclipse-cpp-neon-R-linux-gtk-x86_64.tar.gz -C /opt/
chown -R sysadmin: /opt/eclipse/
rm /usr/bin/eclipse42
touch /usr/bin/eclipse42
echo "#!/bin/sh" >>/usr/bin/eclipse42
echo "export ECLIPSE_HOME="/opt/eclipse"" >>/usr/bin/eclipse42
echo "$ECLIPSE_HOME/eclipse "$@"" >>/usr/bin/eclipse42
chmod +x /usr/bin/eclipse42
rm /usr/share/applications/eclipse42.desktop
touch /usr/share/applications/eclipse42.desktop
echo "[Desktop Entry]" >> /usr/share/applications/eclipse42.desktop
echo "Encoding=UTF-8" >> /usr/share/applications/eclipse42.desktop
echo "Name=Eclipse" >> /usr/share/applications/eclipse42.desktop
echo "Comment=Eclipse IDE" >> /usr/share/applications/eclipse42.desktop
echo "Exec=eclipse42" >> /usr/share/applications/eclipse42.desktop
echo "Icon=/opt/eclipse/icon.xpm" >> /usr/share/applications/eclipse42.desktop
echo "Terminal=false" >> /usr/share/applications/eclipse42.desktop
echo "Type=Application" >> /usr/share/applications/eclipse42.desktop
echo "Categories=GNOME;Application;Development;IDE;" >> /usr/share/applications/eclipse42.desktop
echo "StartupNotify=true" >> /usr/share/applications/eclipse42.desktop
#
#How to download and install prebuilt OpenJDK packages
#JDK 8

export myosversion=$(for f in $(find /etc -type f -maxdepth 1 \( ! -wholename /etc/os-release ! -wholename /etc/lsb-release -wholename /etc/\*release -o -wholename /etc/\*version \) 2> /dev/null); do echo ${f:5:${#f}-13}; done;)
if [ "$myosversion" == "debian" ]; then
{
echo "Found Ubuntu"
} 
elif [ "$myosversion" == "redhat" ]
then
{
echo "Found RedHat"
} 
else {
echo "Unrecognized"
}
fi

if [ "$myosversion" == "debian" ]; then
{
#Debian, Ubuntu, etc.#On the command line, type:sudo apt-get -y install openjdk-8-jdk
# If error run sudo dpkg --configure -a
#The openjdk-8-jre package contains just the Java Runtime Environment. If you want to develop Java programs then please install the openjdk-8-jdk package.
}
if [ "$myosversion" == "redhat" ]; then
{
#Fedora, Oracle Linux, Red Hat Enterprise Linux, etc.#On the command line, type:
su -c "yum install java-1.8.0-openjdk"
#The java-1.8.0-openjdk package contains just the Java Runtime Environment. If you want to develop Java programs then install the java-1.8.0-openjdk-devel
#
# After installing OpenJDK
#Open Eclipse as Root
#CheckUpdates by setting /root/workspace as dir
#After udpating quit and then Open Eclipse as <normal-user>
}

```
