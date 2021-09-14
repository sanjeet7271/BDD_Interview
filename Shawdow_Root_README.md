# Shadow Root
## DOM structure below
![image](https://user-images.githubusercontent.com/45819133/133214432-4eb09619-1850-41f9-82d1-5b4f0f62a85f.png)

    According to the Image, there are 3 shadow-roots in the given DOM structure. Each shadow DOM resides in another shadow DOM. Input field is available in the third shadow DOM.
    => First we have to locate attached element of first shadow-root which is **“settings-ui”**.
      => WebElement attachedElement1 = driver.findElement(By.tagName("settings-ui"));
    Then we can locate the first shadow-root:
      => WebElement shadowRoot1 = (WebElement) ((JavascriptExecutor)driver).executeScript("return arguments[0].shadowRoot", attachedElement1);
      
    From the first shadow-root we can locate and access the attached element of second shadow-root:
      => WebElement attachedElement2 = shadowRoot1.findElement(By.cssSelector("cr-toolbar"));
      
    Likewise we can access the elements of third shadow-DOM
      => WebElement shadowRoot2 = (WebElement) ((JavascriptExecutor) driver).executeScript("return arguments[0].shadowRoot",attachedElement2);
    // Access third shadow-root 
      => WebElement attachedElement3 = shadowRoot2.findElement(By.cssSelector("cr-toolbar-search-field"));
      => WebElement shadowRoot3 = (WebElement) ((JavascriptExecutor) driver).executeScript("return arguments[0].shadowRoot",attachedElement3);
     
    After correctly locating third shadow-root, we can input the word to the search input field:
        // Input "password" to search input field 
        => shadowRoot3.findElement(By.cssSelector("input")).sendKeys("password");

