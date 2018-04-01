
# Install ssl guna Let’s encrypt free cert

<li>Dapatkan Cert bundle di sslforfree.com</li>
<li>ikut arahan (guna manually configure)</li>
<li>dah dapat 3 file (private.key, ca_bundle.crt,certificate.crt) convert kepada pkcs12 (pfx) guna openssl
<br>openssl pkcs12 -export -out c:/Users/aziri/certificate.pfx -inkey private.key -in certificate.crt -certfile ca_bundle.crt</li>

<br>-refer : https://www.ssl.com/how-to/create-a-pfx-p12-certificate-file-using-openssl/</li>
<li>Next guna command pada keytool </li>
<br>keytool -importkeystore -srckeystore c:/Users/aziri/certificate.pfx -srcstoretype pkcs12 
-destkeystore c:/Users/aziri/aziricert.jks -deststoretype JKS</li>
<li>Buka fail {tomcat dir}/conf/server.xml configure
<br>	<Connector port="443" maxHttpHeaderSize="8192" maxThreads="150" minSpareThreads="25" maxSpareThreads="75" enableLookups="false" disableUploadTimeout="true" acceptCount="100" scheme="https" secure="true" SSLEnabled="true" clientAuth="false" sslProtocol="TLS" keyAlias="server" keystoreFile="c:/Users/aziri/aziricert.jks" keystorePass="your_keystore_password" /></li>
<li>restart tomcat</li>
