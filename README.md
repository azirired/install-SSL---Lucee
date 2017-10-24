# install-SSL---Lucee
Configure SSL pada server Lucee menggunakan Let's Encrypt (free ssl)

SSL Certificate
----------------
1. Pergi ke laman https://www.sslforfree.com/
2. Taip alamat website anda
3. Tekan butang 'Create Free SSL Certificate'
4. Page Free SSL Certificate Validation for "{alamat website anda}" akan dipaparkan
5. Tekan 'Manual Verification. Upload verification files manually to your domain to verify ownership.'
6. Kemudian tekan 'Manually Verify Domain'
7. Ikut arahan yang dipaparkan.
8. Kemudian tekan 'Download SSL Certificate'
9. Laman 'Generating SSL Certificate Securely' akan dipaparkan.
10. Satu zip file yang mengandung SSL cert akan dimuat turun.

Install pada Lucee
------------------
CREATE KEYSTORE FILE
 - Buka cmd
   Taip
    cd {folder Lucee}/jdk/bin
   
   Kemudian taip 
    keytool -genkey -alias tomcat -keyalg RSA
   
   Jawab soalan-soalan yang ditanya dan masukkan password dan taip Y atau Yes
   Satu fail .keystore akan dicreate pada direktori C:\Users\{nama user}\.keystore atau C:Documents and Settings[username]

CONFIGURE TOMCAT - SSL Config
 - Buka direktori 
   {folder lucee}\tomcat\conf
   Cari fail server.xml buka fail dan cari 
    <!--
    <Connector port="8443" protocol="HTTP/1.1" SSLEnabled="true"
        maxThreads="150" scheme="https" secure="true"
        clientAuth="false" sslProtocol="TLS" />
    -->
    Buka komen iaitu delete '<!-- dan --> (rujuk kod dibawah)

    Connector SSLEnabled="true" acceptCount="100" clientAuth="false"
    disableUploadTimeout="true" enableLookups="false" maxThreads="25"
    port="8443" keystoreFile="{lokasi keystore fail}/.keystore" keystorePass="password"
    protocol="org.apache.coyote.http11.Http11NioProtocol" scheme="https"
    secure="true" sslProtocol="TLS" />

TEST
- Start tomcat service 
  Buka bowser dan layari https://localhost:8443
  Page anda sepatutnya berjaya dibuka.
*Default port ssl 443 so boleh tukar 8443 kepada 443 so tak perlu taip :8443 kat hujung url.
