# redirect-http-to-https-in-iis
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <system.webServer>
        <httpErrors errorMode="Custom" existingResponse="Replace">
            <remove statusCode="404" subStatusCode="-1" />
            <error statusCode="404" path="/" responseMode="ExecuteURL" />
        </httpErrors>
        
        // start
        <rewrite>
          <rules>
              <rule name="http to https" stopProcessing="true">
                  <match url="(.*)" />
                  <conditions>
                      <add input="{HTTPS}" pattern="^OFF$" />
                  </conditions>
                  <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" />
              </rule>
          </rules>
      </rewrite>
      // end
      
    </system.webServer>
</configuration>
