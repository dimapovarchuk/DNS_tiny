# DNS_tiny_ubuntu_server

apt-get update 

apt-get install build-essential 

 <img width="416" alt="image" src="https://user-images.githubusercontent.com/52627259/222768514-4878e2d7-f5a1-4037-ad52-633c121f4bed.png">


mkdir -p /package 

chmod 1755 /package 

cd /package 

wget http://cr.yp.to/daemontools/daemontools-0.76.tar.gz 

 <img width="449" alt="image" src="https://user-images.githubusercontent.com/52627259/222769029-e27c39ad-317b-4acc-b91c-45563f53f37c.png">


gunzip daemontools-0.76.tar 

tar -xpf daemontools-0.76.tar 

rm -f daemontools-0.76.tar 

cd admin/daemontools-0.76 

 
<img width="461" alt="image" src="https://user-images.githubusercontent.com/52627259/222769185-fb6186ce-c0fc-488c-85fc-fbdd77548fa4.png">

 

package/install 

cd compile 

nano error.h 

 <img width="382" alt="image" src="https://user-images.githubusercontent.com/52627259/222769355-22300a98-9c04-4da8-b8a6-6b69b3299ce3.png">


cd /usr/local/src 

wget http://cr.yp.to/ucspi-tcp/ucspi-tcp-0.88.tar.gz 

 <img width="470" alt="image" src="https://user-images.githubusercontent.com/52627259/222769482-a8db5a20-9b13-45d4-bcca-9d69d7725b14.png">


gunzip ucspi-tcp-0.88.tar 

tar -xf ucspi-tcp-0.88.tar 

cd ucspi-tcp-0.88 

 

make 

make setup check 

 

mkdir packages 

cd packages 

wget http://cr.yp.to/djbdns/djbdns-1.05.tar.gz 

 <img width="464" alt="image" src="https://user-images.githubusercontent.com/52627259/222769626-2ccf050f-612f-480c-9f67-05852824b051.png">


tar -xzf djbdns-1.05.tar.gz 

cd djbdns-1.05/  

echo gcc -O2 -include /usr/include/errno.h > conf-cc  

make  

make setup check 

 

/usr/sbin/useradd -s /bin/false tinydns 

/usr/sbin/useradd -s /bin/false dnslog 

 <img width="464" alt="image" src="https://user-images.githubusercontent.com/52627259/222769798-befbc8b4-34ff-4bec-ad49-bf885ee5b01d.png">


tinydns-conf tinydns dnslog /etc/tinydns 127.0.0.1 

ln -s /etc/tinydns /etc/service 

sleep 5 

svstat /service/tinydns 

 <img width="385" alt="image" src="https://user-images.githubusercontent.com/52627259/222769914-97c0f61c-d6aa-4138-93a9-22ae4e1787b8.png">


/usr/sbin/useradd -s /sbin/nologin -d /dev/null dnscache 

dnscache-conf dnscache dnslog /etc/dnscache 192.168.1.16 

 
<img width="463" alt="image" src="https://user-images.githubusercontent.com/52627259/222770055-c3a82984-59d2-4ddb-976b-a321b01d3823.png">

 

ln -s /etc/dnscache /etc/service 

sleep 5 

svstat /service/dnscache 

 <img width="449" alt="image" src="https://user-images.githubusercontent.com/52627259/222770148-832c3182-75cd-448d-91f9-3b2255c3a0d8.png">


mkdir /etc/dnscache/root/ip 

touch 192.168 

dig google.com 

 <img width="461" alt="image" src="https://user-images.githubusercontent.com/52627259/222770240-e0ecfe0c-db1c-405d-80a5-94a813a0aaaa.png">


svc -t /service/dnscache 

 <img width="457" alt="image" src="https://user-images.githubusercontent.com/52627259/222770333-7e77a654-abb1-4570-970b-444dc6a583fe.png">


dig povarchuk.com @127.0.0.53 

 <img width="377" alt="image" src="https://user-images.githubusercontent.com/52627259/222770420-43c430f4-4544-463b-8b12-d585baf3288c.png">


Dig mail.povarchuk.com @127.0.0.53 

 <img width="356" alt="image" src="https://user-images.githubusercontent.com/52627259/222770504-9b7b0700-1fda-4eba-8e92-0df9f904a686.png">


dig -x 192.168.1 @127.0.0.53 

 <img width="454" alt="image" src="https://user-images.githubusercontent.com/52627259/222770572-8db12729-7cd6-4f48-bf93-374a243cd4bd.png">


tinydns-get any povarchuk.com 127.0.0.53 

 <img width="355" alt="image" src="https://user-images.githubusercontent.com/52627259/222770665-cdab9ab1-42ee-402f-aae5-12a1a98cdb42.png">


tinydns-get ptr 1.168.192.in-addr.arpa 127.0.0.53 

 <img width="464" alt="image" src="https://user-images.githubusercontent.com/52627259/222770778-3def1aa4-ac3e-4d26-96ef-33fa95a0de72.png">
 DNS_tiny_ubuntu_server
