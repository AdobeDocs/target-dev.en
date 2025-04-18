---
keywords: client care, cname, certificate program, canonical name, cookies, certificate, amc, adobe managed certificate, digicert, domain control validation, dcv, client care2
description: Work with [!UICONTROL Adobe Client Care] to implement CNAME (Canonical Name) support in [!DNL Adobe Target] to handle ad-blocking issues.
title: How Do I Use CNAME in Target?
feature: Privacy & Security
exl-id: 5709df5b-6c21-4fea-b413-ca2e4912d6cb
---
# CNAME and Target

Instructions for working with [!DNL Adobe Client Care] to implement CNAME (Canonical Name) support in [!DNL Adobe Target]. Use CNAME to handle ad blocking issues or ITP-related (Intelligent Tracking Prevention) cookie policies. With CNAME, calls are made to a domain owned by the customer rather than a domain owned by Adobe.

## Request CNAME support in Target

1. Determine the list of hostnames you need for your SSL certificate (see FAQ below).

1. For each hostname, create a CNAME record in your DNS pointing to your regular [!DNL Target] hostname `clientcode.tt.omtrdc.net`. 

   For example, if your client code is "cnamecustomer" and your proposed hostname is `target.example.com`, your DNS CNAME record looks similar to:

   ```
   target.example.com.  IN  CNAME  cnamecustomer.tt.omtrdc.net.
   ```
   
   >[!WARNING]
   >
   >Adobe's certificate authority, DigiCert, cannot issue a certificate until this step is complete. Therefore, Adobe cannot fulfill your request for a CNAME implementation until this step is complete.

1. [Fill out this form](assets/FPC_Request_Form.xlsx) and include it when you [open an Adobe Client Care ticket requesting CNAME support](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html?#reference_ACA3391A00EF467B87930A450050077C):

   * [!DNL Adobe Target] client code:
   * SSL certificate hostnames (example: `target.example.com target.example.org`):
   * SSL certificate purchaser (Adobe is highly recommended, see FAQ): Adobe/customer
   * If the customer is purchasing the certificate, also known as "Bring Your Own Certificate" (BYOC), fill out these additional details:
      * Certificate organization (example: Example Company Inc):
      * Certificate organizational unit (optional, example: Marketing):
      * Certificate country (example: US):
      * Certificate state/region (example: California):
      * Certificate city (example: San Jose):

1. If Adobe is purchasing the certificate, Adobe works with DigiCert to purchase and deploy your certificate on Adobe's production servers.

   If the customer is purchasing the certificate (BYOC), Adobe Client Care sends you the certificate signing request (CSR). Use the CSR when purchasing the certificate through your certificate authority of choice. After the certificate is issued, send a copy of the certificate and any intermediate certificates to Adobe Client Care for deployment.

   Adobe Client Care notifies you when your implementation is ready.

1. Update the `serverDomain` [documentation](../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#serverdomain) to the new CNAME hostname and set `overrideMboxEdgeServer` to `false` [documentation](../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#overridemboxedgeserver) in your at.js configuration.

## Frequently Asked Questions

The following information answers frequently asked questions about requesting and implementing CNAME support in Target:

### Can I provide my own certificate (Bring Your Own Certificate or BYOC)?

You can provide your own certificate. However, Adobe does not recommend this practice. Management of the SSL certificate lifecycle is easier for both Adobe and you if Adobe purchases and controls the certificate. SSL certificates must be renewed every year. Therefore, Adobe Client Care must contact you every year to obtain a new certificate in a timely manner. Some customers can have difficulty producing a renewed certificate in a timely manner. Your [!DNL Target] implementation is jeopardized when the certificate expires because browsers refuse connections.

>[!WARNING]
>
>If you request a [!DNL Target] bring-your-own-certificate CNAME implementation, you are responsible for providing renewed certificates to Adobe Client Care every year. Allowing your CNAME certificate to expire before Adobe can deploy a renewed certificate results in an outage for your specific [!DNL Target] implementation.

### How long until my new SSL certificate expires?

All Adobe-purchased certificates are valid for one year. See [DigiCert's article on 1-year certificates](https://www.digicert.com/blog/position-on-1-year-certificates) for more information.

### What hostnames should I choose? How many hostnames per domain should I choose?

Target CNAME implementations require only one hostname per domain on the SSL certificate and in the customer's DNS. Adobe recommends one hostname per domain. Some customers require more hostnames per domain for their own purposes (testing in staging, for example), which is supported.

Most customers choose a hostname like `target.example.com`. Adobe recommends following this practice, but the choice is ultimately yours. Do not request a hostname of an existing DNS record. Doing so causes a conflict and delays time to resolution of your [!DNL Target] CNAME request.

### I already have a CNAME implementation for Adobe Analytics, can I use the same certificate or hostname?

No, [!DNL Target] requires a separate hostname and certificate.

### Is my current implementation of [!DNL Target] impacted by ITP 2.x?

Apple Intelligent Tracking Prevention (ITP) version 2.3 introduced its CNAME Cloaking Mitigation feature, which is able to detect [!DNL Target] CNAME implementations and reduces the cookie's expiration to seven days. Currently [!DNL Target] has no workaround for ITP's CNAME Cloaking Mitigation. For more information about ITP, see [Apple Intelligent Tracking Prevention (ITP) 2.x](../before-implement/privacy/apple-itp-2x.md).

### What kind of service disruptions can I expect when my CNAME implementation is deployed?

There is no service disruption when the certificate is deployed (including certificate renewals). 

However, after you change the hostname in your [!DNL Target] implementation code (`serverDomain` in at.js) to the new CNAME hostname (`target.example.com`), web browsers treat returning visitors as new visitors. Returning visitors' profile data is lost because the previous cookie is inaccessible under the old hostname (`clientcode.tt.omtrdc.net`). The previous cookie is inaccessible due to browser security models. This disruption occurs only on the initial cut-over to the new CNAME. Certificate renewals do not have the same effect because the hostname doesn't change.

### What key type and certificate signature algorithm is used for my CNAME implementation?

All certificates are RSA SHA-256 and keys are RSA 2048-bit, by default. Key sizes larger than 2048-bit should be requested explicitly through [!UICONTROL Customer Care]. 

### How can I validate that my CNAME implementation is ready for traffic?

Use the following set of commands (in the macOS or Linux command-line terminal, using bash and curl >=7.49):

1. Copy and paste this bash function into your terminal, or paste the function into your bash startup script file (usually `~/.bash_profile` or `~/.bashrc`) so the function is available across terminal sessions:

   ```
   function adobeTargetCnameValidation {
     local hostname="$1"
     
     if [ -z "$hostname" ]; then
       echo "ERROR: no hostname specified"
       return 1
     fi
     
     local service="Adobe Target CNAME implementation"
     local edges="41 42 44 45 46 47 48"
     local edgeDomain="tt.omtrdc.net"
     local edgeFormat="mboxedge%d%s.$edgeDomain"
     local poolDomain="pool.data.adobedc.net"
     local shards=5
     local shardsFoundCount=0
     local shardsFound=""
     local shardsFoundOutput=""
     local curlRegex="subject:.*CN=|expire date:|issuer:"
     local curlValidation="SSL certificate verify ok"
     local curlResponseValidation='"OK"'
     local curlEndpoint="/uptime?mboxClient=uptime3"
     local url="https://$hostname$curlEndpoint"
     local sslShopperUrl="https://www.sslshopper.com/ssl-checker.html#hostname=$hostname"
     local success="✅"
     local failure="🚫"
     local info="🔎"
     local rule="="
     local horizontalRule="$(seq ${COLUMNS:-30} | xargs printf "$rule%.0s")"
     local miniRule="$(seq 5 | xargs printf "$rule%.0s")"
     local curlVersion="$(curl --version | head -1 | cut -d' ' -f2)"
     local curlVersionRequired=7.49
     local edgeCount="$(wc -w <<< "$edges" | tr -d ' ')"
     local cnameExists=""
     local endToEndTestSucceeded=""
     
     for region in IRL1 IND1 SIN OR SYD VA TYO; do
       local currShard="${region}-${poolDomain}"
       local curlResult="$(curl -vsm20 --connect-to "$hostname:443:$currShard:443" "$url" 2>&1)"
       
       if grep -q "$curlValidation" <<< "$curlResult"; then
         shardsFound+=" $currShard"
         
         if grep -q "$curlResponseValidation" <<< "$curlResult"; then
           shardsFoundCount=$((shardsFoundCount+1))
           shardsFoundOutput+="\n\n$miniRule $success $hostname [edge shard: $currShard] $miniRule\n"
         else
           shardsFoundOutput+="\n\n$miniRule $failure $hostname [edge shard: $currShard] $miniRule\n"
         fi
         
         shardsFoundOutput+="$(grep -E "$curlRegex" <<< "$curlResult" | sort)"
         
         if ! grep -q "$curlResponseValidation" <<< "$curlResult"; then
           shardsFoundOutput+="\nERROR: unexpected HTTP response from this shard using $url"
         fi
       fi
     done
     
     echo
     echo "$horizontalRule"
     echo
     echo "$service validation for hostname $hostname:"
     
     local dnsOutput="$(dig -t CNAME +short "$hostname" 2>&1)"
     if grep -qFi ".$edgeDomain" <<< "$dnsOutput"; then
       echo "$success $hostname passes DNS CNAME validation"
       cnameExists=true
     else
       echo -n "$failure $hostname FAILED DNS CNAME validation -- "
       if [ -n "$dnsOutput" ]; then
         echo -e "$dnsOutput is not in the subdomain $edgeDomain"
       else
         echo "required DNS CNAME record pointing to <target-client-code>.$edgeDomain not found"
       fi
     fi
     
     for region in IRL1 IND1 SIN OR SYD VA TYO; do
       local curlResult="$(curl -vsm20 --connect-to "$hostname:443:${region}-pool.data.adobedc.net:443" "https://$hostname$curlEndpoint" 2>&1)"
       
       if grep -q "$curlValidation" <<< "$curlResult"; then
         if grep -q "$curlResponseValidation" <<< "$curlResult"; then
           echo -en "$success $hostname passes TLS and HTTP response validation for region $region"
           if [ -n "$cnameExists" ]; then
             echo
           else
             echo " -- the DNS CNAME is not pointing to the correct subdomain for ${service}s with Adobe-managed certificates" \
               "(bring-your-own-certificate implementations don't have this requirement), but this test passes as configured"
           fi
           endToEndTestSucceeded=true
         else
           echo -n "$failure $hostname FAILED HTTP response validation for region $region --" \
             "unexpected response from $url -- "
           if [ -n "$cnameExists" ]; then
             echo "DNS is NOT pointing to the correct shard, notify Adobe Client Care"
           else
             echo "the required DNS CNAME record is missing, see above"
           fi
         fi
       else
         echo -n "$failure $hostname FAILED TLS validation for region $region -- "
         if [ -n "$cnameExists" ]; then
           echo "DNS is likely NOT pointing to the correct shard or there's a validation issue with the certificate or" \
             "protocols, see curl output below and optionally SSL Shopper ($sslShopperUrl):"
           echo ""
           echo "$horizontalRule"
           echo "$curlResult" | sed 's/^/    /g'
           echo "$horizontalRule"
           echo ""
         else
           echo "the required DNS CNAME record is missing, see above"
         fi
       fi
     done
     
     if [ "$shardsFoundCount" -ge "$edgeCount" ]; then
       echo -n "$success $hostname passes shard validation for the following $shardsFoundCount edge shards:"
       echo -e "$shardsFoundOutput"
       echo
       
       if [ -n "$cnameExists" ] && [ -n "$endToEndTestSucceeded" ]; then
         echo "$horizontalRule"
         echo ""
         echo "  For additional TLS/SSL validation, see SSL Shopper:"
         echo ""
         echo "    $info  $sslShopperUrl"
         echo ""
         echo "  To check DNS propagation around the world, see whatsmydns.net:"
         echo ""
         echo "    $info  DNS A records:     https://whatsmydns.net/#A/$hostname"
         echo "    $info  DNS CNAME record:  https://whatsmydns.net/#CNAME/$hostname"
       fi
     else
       echo -n "$failure $hostname FAILED shard validation -- shards found: $shardsFoundCount," \
         "expected: $edgeCount"
       echo ""
     fi
     
     echo
     echo "$horizontalRule"
     echo
   }
   
   ```

1. Paste this command (replacing `target.example.com` with your hostname):

   ```
   adobeTargetCnameValidation target.example.com
   ```

   If the implementation is ready, you see output like below. The important part is that all validation status lines show `✅` rather than `🚫`. Each Target edge CNAME shard should show `CN=target.example.com`, which matches the primary hostname on the requested certificate (additional SAN hostnames on the certificate aren't printed in this output).

   ```
   $ adobeTargetCnameValidation target.example.com
   
   ==========================================================
   
   Adobe Target CNAME implementation validation for hostname target.example.com:
   ✅ target.example.com passes DNS CNAME validation
   ✅ target.example.com passes TLS and HTTP response validation for region IRL1
   ✅ target.example.com passes TLS and HTTP response validation for region IND1
   ✅ target.example.com passes TLS and HTTP response validation for region SIN
   ✅ target.example.com passes TLS and HTTP response validation for region OR
   ✅ target.example.com passes TLS and HTTP response validation for region SYD
   ✅ target.example.com passes TLS and HTTP response validation for region VA
   ✅ target.example.com passes TLS and HTTP response validation for region TYO
   ✅ target.example.com passes shard validation for the following 7 edge shards:
   
   ===== ✅ target.example.com [edge shard: IRL1-pool.data.adobedc.net] =====
   *  expire date: Feb 20 23:59:59 2026 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: IND1-pool.data.adobedc.net] =====
   *  expire date: Feb 20 23:59:59 2026 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: SIN-pool.data.adobedc.net] =====
   *  expire date: Feb 20 23:59:59 2026 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: OR-pool.data.adobedc.net] =====
   *  expire date: Feb 20 23:59:59 2026 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: SYD-pool.data.adobedc.net] =====
   *  expire date: Feb 20 23:59:59 2026 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: VA-pool.data.adobedc.net] =====
   *  expire date: Feb 20 23:59:59 2026 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: TYO-pool.data.adobedc.net] =====
   *  expire date: Feb 20 23:59:59 2026 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ==========================================================  
   
   For additional TLS/SSL validation, see SSL Shopper:
   
       🔎  https://www.sslshopper.com/ssl-checker.html#hostname=target.example.com  
   
   To check DNS propagation around the world, see whatsmydns.net:
   
       🔎  DNS A records:     https://whatsmydns.net/#A/target.example.com
       🔎  DNS CNAME record:  https://whatsmydns.net/#CNAME/target.example.com 
   
   ```

>[!NOTE]
>
>If this validation command fails on DNS validation but you've already made the necessary DNS changes, you might need to wait for your DNS updates to fully propagate. DNS records have an associated [TTL (time-to-live)](https://en.wikipedia.org/wiki/Time_to_live#DNS_records) that dictates cache expiration time for DNS replies of those records. As a result, you might need to wait at least as long as your TTLs. You can use the `dig target.example.com` command or [the G Suite Toolbox](https://toolbox.googleapps.com/apps/dig/#CNAME) to look up your specific TTLs. To check DNS propagation around the world, see [whatsmydns.net](https://whatsmydns.net/#CNAME).

### How do I use an opt-out link with CNAME

If you are using CNAME, the opt-out link should contain the "client=`clientcode` parameter, for example:
`https://my.cname.domain/optout?client=clientcode`.

Replace `clientcode` with your client code, then add the text or image to be linked to the [opt-out URL](privacy/privacy.md).

## Known limitations

* QA mode is not sticky when you have CNAME and at.js 1.x because it is based on a third-party cookie. The workaround is to add the preview parameters to each URL you navigate to. QA mode is sticky when you have CNAME and at.js 2.x.
* When using CNAME, it becomes more likely that the size of the cookie header for [!DNL Target] calls increase. Adobe recommends keeping the cookie size under 8 KB.
