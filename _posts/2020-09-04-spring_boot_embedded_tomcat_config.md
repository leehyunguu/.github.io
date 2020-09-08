---
title: Spring boot Embedded Tomcat Config
date: 2020-09-04
categories: diary spring-boot
---
인수 가이드에서 Tomcat의 web.xml 설정을 해야했는데, Spring boot 내장 Tomcat에서 Java Config로 적용을 했다.

먼저 Spring boot의 버전에 따라 적용방법이 달랐는데, Spring boot 2 기준으로 개발을 했다.

```java
@Configuration
public class EmbeddedTomcatConfig implements WebServerFactoryCustomizer<TomcatServletWebServerFactory> {

    @Override
    public void customize(TomcatServletWebServerFactory factory) {
        TomcatContextCustomizer tomcatContextCustomizer = context -> {
            SecurityConstraint securityConstraint = new SecurityConstraint();
            securityConstraint.setDisplayName("Forbidden");
            securityConstraint.setAuthConstraint(true);
            SecurityCollection securityCollection = new SecurityCollection();
            securityCollection.addPattern("/*");
            securityCollection.addMethod("PUT");
            securityCollection.addMethod("DELETE");
            securityCollection.addMethod("TRACE");
            securityCollection.addMethod("OPTIONS");
            securityCollection.setName("Forbidden");
            securityConstraint.addCollection(securityCollection);
            context.addConstraint(securityConstraint);

            Wrapper defaultServlet = (Wrapper) context.findChild("default");
            defaultServlet.addInitParameter("readonly", "true");
        };
        factory.addContextCustomizers(tomcatContextCustomizer);
    }
}
```

내용을 설명하자면, 해당 App Url Method 중 PUT, DELETE, TRACE, OPTIONS는 막는다는 내용과, Default Servlet의 Init Parameter중 readonly를 true로 설정한다는 내용이다.

후자의 readonly는 default가 true로 되어있어, 굳이 설정하지 않아도 되지만, 인수 체크리스트에 사용하기 위해 추가했다.

삽질을 많이 하면서 찾아낸 내용이라 기억에 많이 남을 것 같다.
