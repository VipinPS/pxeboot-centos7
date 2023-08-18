# pxeboot-centos7

# Installing Packages #
```yum install net-utils httpd vsftpd xinetd syslinux tftp-server dhcp*```

# Setting up software packages and directories #
``mount -o loop  /dev/cdrom /var/lib/tftpboot/centos7
ln -sf /var/lib/tftpboot/centos7 /var/www/html/centos7
cp -v /usr/share/syslinux/{pxelinux.0,menu.c32,memdisk,mboot.c32,chain.c32} /var/lib/tftpboot
mkdir /var/lib/tftpboot/pxelinux.cfg
mkdir /var/www/html/installer
chmod -R 755 /var/www/html/centos7 /var/www/html/installer``

# Copy config files #
cp -v ./default /var/lib/tftpboot/pxelinux.cfg
cp -v ./pxe.conf /etc/httpd/conf.d/
cp -v ./anaconda-ks.cfg /var/www/html/installer/
cp -v ./tftp /etc/xinetd.d/tftp
cp -v ./dhcpd.conf /etc/dhcp/dhcpd.conf

# Restart required services #
systemctl restart httpd
systemctl restart vsftpd
systemctl restart tftp
systemctl restart xinetd
