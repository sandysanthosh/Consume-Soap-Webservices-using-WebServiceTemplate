
SOAPConnector class extends WebServiceGatewaySupport which basically injects one interface with internal 
implementation of **WebServiceTemplate** which is available by getWebServiceTemplate() method.

We will use this WebServiceTemplate to invoke the SOAP service.

This class also expects one injected spring bean called **Marshaller** and **Unmarshallerwhich** will be provided by a configuration class which we will see next.


**
SOAPConnector.java**

```

package com.example.howtodoinjava.springbootsoapclient;
 
import org.springframework.ws.client.core.support.WebServiceGatewaySupport;
 
public class SOAPConnector extends **WebServiceGatewaySupport** {
 
  public Object callWebService(String url, Object request){
    return getWebServiceTemplate().marshalSendAndReceive(url, request);
  }
}

```

**configuration.java:
**

```


public class config{

@Bean
public Jaxb2Marshaller marshaller(){

Jaxb2Marshaller marshaller = new Jaxb2Marshaller();

marshaller.setContextPath("com.example.howtodoinjava.schemas.school");

return marshaller;

}




```
