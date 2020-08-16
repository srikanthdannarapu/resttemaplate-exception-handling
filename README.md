You have to create a class that implements ResponseErrorHandler and then use an instance of it to set the error handling of your rest template:
```java
public class MyErrorHandler implements ResponseErrorHandler {
  @Override
  public void handleError(ClientHttpResponse response) throws IOException {
    // your error handling here
  }

  @Override
  public boolean hasError(ClientHttpResponse response) throws IOException {
     ...
  }
}

[...]

public static void main(String args[]) {
  RestTemplate restTemplate = new RestTemplate();
  restTemplate.setErrorHandler(new MyErrorHandler());
}
```
Also, Spring has the class DefaultResponseErrorHandler, which you can extend instead of implementing the interface, in case you only want to override the handleError method.

```java
public class MyErrorHandler extends DefaultResponseErrorHandler {
  @Override
  public void handleError(ClientHttpResponse response) throws IOException {
    // your error handling here
  }
}
```
Take a look at its source code to have an idea of how Spring handles HTTP errors.

https://github.com/spring-projects/spring-framework/blob/master/spring-web/src/main/java/org/springframework/web/client/DefaultResponseErrorHandler.java