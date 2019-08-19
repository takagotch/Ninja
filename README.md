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
    
    verify(context).addCookie(cookieCaptor.capture());
    assertEquals("value", session_1.get("key"));
    
    Cookie cookie = cookieCaptor.getValue();
    
    Session session_2 = createNewSession();
    when(context.getCookie("NINJA_SESSION")).thenReturn(cookie);
    session_2.init(context);
    assertFalse(session_2.isEmpty);
    assertEquals("value", session_2.get("key"));
    
    when(ninjaProperties.getOrDie(NinjaConstant.applicationSecret))
      .thenReturn(SecretGenerator.generatedSecret());
    encryption = new CookieEncryption(ninjaProperties);
    
    Session session_3 = createNewSession();
    session_3.init(context);
    assertTrue(session_3.isEmpty());
  }
  
  private Session roundTrip(Session sessionCookie1) {
    sessionCookie1.save(context);
    
    verify(context, atLeastOnce()).addCookie(cookieCaptor.capture());
    
    when(context.getCookie("NINJA_SESSION")).thenReturn(cookieCaptor.getValue());
    
    Session sessionCookie2 = createNewSession();
    sessionCookie2.init(context);
    return sessionCookie2;
  }
  
  private Session createNewSession() {
    return new SessionImpl(crypto, encryption, ninjaProperties, clock);
  }
  
  private String captureFinalCookie(Session sessionCookie) {
    sessionCookie.save(context);
    
    verify(context, atLeastOnce()).addCookie(cookieCaptor.capture());
    
    String cookieValue = cookieCaptor.getValue().getValue();
    String cookieValuWithoutSign = cookieValue.substring(cookieValue.indexOf("-") + 1);
    
    if (encrypted) {
      cookieValueWithoutSign = encryption.decrypt(cookieValueWithoutSign);
    }
    
    return cookieValueWithoutSign;
  }
}


```

```
```

```
```


