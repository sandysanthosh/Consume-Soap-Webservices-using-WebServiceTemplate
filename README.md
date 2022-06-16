#### WebserviceTemplate:


SOAPConnector class extends WebServiceGatewaySupport which basically injects one interface with internal 
implementation of **WebServiceTemplate** which is available by getWebServiceTemplate() method.

We will use this WebServiceTemplate to invoke the SOAP service.

This class also expects one injected spring bean called **Marshaller** and **Unmarshallerwhich** will be provided by a configuration class which we will see next.


#### pom.xml:

```
<plugin>
  <groupId>org.jvnet.jaxb2.maven2</groupId>
  <artifactId>maven-jaxb2-plugin</artifactId>
  <version>0.13.2</version>
  <executions>
    <execution>
      <goals>
        <goal>generate</goal>
      </goals>
    </execution>
  </executions>
  <configuration>
    <generatePackage>com.example.howtodoinjava.schemas.school</generatePackage>
    <generateDirectory>${project.basedir}/src/main/java</generateDirectory>
    <schemaDirectory>${project.basedir}/src/main/resources/wsdl</schemaDirectory>
    <schemaIncludes>
      <include>*.wsdl</include>
    </schemaIncludes>
  </configuration>
</plugin> 

```


#### SOAPConnector.java:

```

package com.example.howtodoinjava.springbootsoapclient;
 
import org.springframework.ws.client.core.support.WebServiceGatewaySupport;
 
public class SOAPConnector extends **WebServiceGatewaySupport** {
 
  public Object callWebService(String url, Object request){
    return getWebServiceTemplate().marshalSendAndReceive(url, request);
  }
}

```

#### configuration.java:

```

@configuration
public class config{

@Bean
public Jaxb2Marshaller marshaller(){

Jaxb2Marshaller marshaller = new Jaxb2Marshaller();

marshaller.setContextPath("com.example.howtodoinjava.schemas.school");

return marshaller;

}




```
