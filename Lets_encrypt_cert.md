
# Install ssl guna Let’s encrypt free cert
<ol type=a>
<li>Dapatkan Cert bundle di sslforfree.com</li>
<li>ikut arahan (guna manually configure)</li>
<li>dah dapat 3 file (private.key, ca_bundle.crt,certificate.crt) convert kepada pkcs12 (pfx) guna openssl
<br>openssl pkcs12 -export -out c:/Users/aziri/certificate.pfx -inkey private.key -in certificate.crt -certfile ca_bundle.crt</li>
*openssl dalam folder C:\Program Files (x86)\GnuWin32\bin
  
<br>-refer : https://www.ssl.com/how-to/create-a-pfx-p12-certificate-file-using-openssl/</li>
<li>Next guna command pada keytool </li>
*keytool dalam folder {{lucee folder}}\jdk\bin
<br>keytool -importkeystore -srckeystore c:/Users/aziri/certificate.pfx -srcstoretype pkcs12 
-destkeystore c:/Users/aziri/aziricert.jks -deststoretype JKS</li>
<li>Buka fail {tomcat dir}/conf/server.xml configure
<br>	&LT;Connector port="443" maxHttpHeaderSize="8192" maxThreads="150" minSpareThreads="25" maxSpareThreads="75" enableLookups="false" disableUploadTimeout="true" acceptCount="100" scheme="https" secure="true" SSLEnabled="true" clientAuth="false" sslProtocol="TLS" keyAlias="server" keystoreFile="c:/Users/aziri/aziricert.jks" keystorePass="your_keystore_password" /&GT;</li>
<li> Configure Cipher and TLS - Untk dapat rating A<br>
&LT;Connector port="443" protocol="org.apache.coyote.http11.Http11NioProtocol"
maxThreads="150" SSLEnabled="true" sslEnabledProtocols="TLSv1,TLSv1.1,TLSv1.2" 
ciphers="ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA256"
SSLHonorCipherOrder="true" SSLDisableCompression="true" scheme="https" secure="true"
clientAuth="false" sslProtocol="TLS"
keyAlias="namakeyalias_anda" keystoreFile="lokasikeystore"
keystorePass="passkeystore" 
/&GT;"
</li>

<li>restart tomcat</li>
</ol>
