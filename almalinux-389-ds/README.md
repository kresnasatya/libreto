1. Run command below to build image.

docker build -t kresnasatya/almalinux-389ds:1.0 .

2. Run container command below.

docker run -itd -p 9090:9090/tcp -p 389:389/tcp -p 636:636/tcp --name=almalinux9-389-ds --privileged kresnasatya/almalinux-389ds:1.0 /usr/sbin/init

3. Open terminal in container (step 2) then run command below.

/usr/bin/systemctl start firewalld \
&& /usr/bin/firewall-cmd --permanent --add-service={ldap,ldaps} \
&& /usr/bin/firewall-cmd --permanent --add-port=9090/tcp \
&& /usr/bin/firewall-cmd --permanent --add-port=389/tcp \
&& /usr/bin/firewall-cmd --permanent --add-port=636/tcp \
&& /usr/bin/systemctl enable --now cockpit.socket \
&& /usr/bin/systemctl start --now cockpit.socket

4. Reset password root with command below.

passwd root

5. Open cockpit ui in browser with URL localhost:9090

6. For next step, please open this Google Docs link: https://docs.google.com/document/d/1JKNjKeH-dv-tkSUS-R7z-ggn8DJ0_UNfncVaNz_ykW0/edit?usp=sharing