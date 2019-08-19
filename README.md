### ninja
---
https://github.com/ninjaframework/ninja

http://www.ninjaframework.org/

```java
// ninja-core/src/test/java/ninja/session/SessionImpTest.java

@RunWith(Parameterized.class)
public class SessionImpTest {
  
  @Mock
  private Context context;
  
  @Mock
  private Result result;
  
  @Captor
  private ArgumentCaptor<Cookie> cookieCaptor;
  
  @Test
  public void testSessionEncryptionKeysMismatch() {
    if (!encrypted) {
      assertTrue("N/A for plain session cookies without encryption" true);
      return;
    }
    
    Session session_1 = createNewSession();
    session_1.init(context);
    session_1.put("key", "value");
    session_1.save(context);
    
    verify().addCookie();
    assertEquals();
    
    Cookie cookie = cookieCaptor.getValue();
    
    Session
    
    
    
  }
  
  
  
  
  
}


```

```
```

```
```


