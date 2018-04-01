
# Install ssl guna Let’s encrypt free cert

Dapatkan Cert bundle di sslforfree.com
ikut arahan (guna manually configure)
dah dapat 3 file (private.key, ca_bundle.crt,certificate.crt) convert kepada pkcs12 (pfx) guna openssl
openssl pkcs12 -export -out c:/Users/aziri/certificate.pfx -inkey private.key -in certificate.crt -certfile ca_bundle.crt

-refer : https://www.ssl.com/how-to/create-a-pfx-p12-certificate-file-using-openssl/
Next guna command pada keytool 
keytool -importkeystore -srckeystore c:/Users/aziri/certificate.pfx -srcstoretype pkcs12 
-destkeystore c:/Users/aziri/aziricert.jks -deststoretype JKS
Buka fail {tomcat dir}/conf/server.xml configure
	<Connector port="443" maxHttpHeaderSize="8192" maxThreads="150" minSpareThreads="25" maxSpareThreads="75" enableLookups="false" disableUploadTimeout="true" acceptCount="100" scheme="https" secure="true" SSLEnabled="true" clientAuth="false" sslProtocol="TLS" keyAlias="server" keystoreFile="c:/Users/aziri/aziricert.jks" keystorePass="your_keystore_password" />
restart tomcat
