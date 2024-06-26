# BDD Interview
 ## Cucumber Examples
    Feature: Account Holder withdraws cash
    Scenario: Account has sufficient funds
     Given the account balance is $100
       And the card is valid
       And the machine contains enough money  
      When the Account Holder requests $20
      Then the ATM should dispense $20
       And the account balance should be $80
       And the card should be returned

 ## Enlist the files needed in the Cucumber framework
      i.) Feature File: It has plain text descriptions of single or numerous test situations.
         Keywords like Then, When, Background, Scenario Outline, Feature, And, But, and so on are used in the tests. As a result, it's a file that keeps track of features 
         and their descriptions.
      ii.) Step Definition File: It has the extension .java. It essentially acts as a translator between the test scenario steps provided in the feature file and the automation
          code. Cucumber searches the step definition file and executes the relevant functions that are assigned to that step when it runs a step described in the feature file
      iii.) TestRunner: .java is the file extension for this file. It connects the feature file and the step definition file. It allows the user to run one or more feature files
            at the same time. It contains the locations of the step definition and feature files.
 ## Annotations in Cucumber
       i.) Feature: The Feature keyword's aim is to collect relevant scenarios and provide a high-level description of a software feature.
       ii.) Rule: The Rule keyword is used to express a single business rule that should be followed. It adds to the information about a feature.
       iii.) Example: This is a practical illustration of a business rule. It comprises a series of steps.
       iv.) Background: A background helps you to give the situations that follow it some context. It can have one or more Given steps, which are executed prior to each scenario
            but after any Before hooks.
       v.) Given: It specifies the requirements for running the test.
                Example: Given I have an account on facebook.
       vi.) When: It establishes the starting point for any test scenario.
                  Example: When I log in to facebook.
       vii.) Then: It contains the expected result of the test which is to be executed.
                  Example: Then registration should be successful.
       viii.) And: Between any two statements, it gives the logical AND condition. AND can be combined with the GIVEN, WHEN, and THEN statements.
                Example: When I enter my account number AND CVV. 
       ix.) But: It denotes a logical OR relationship between two propositions. OR can be combined with the GIVEN, WHEN, and THEN statements.
                Example: Then I should be logged in BUT I must enter the OTP.
        x.) Scenario: Scenario is a fundamental Gherkin structure. Every scenario begins with the keyword "Scenario:" (or a localized version of it) and ends with a scenario
             title. Every feature can have one or more scenarios, each of which has one or more steps. 
        xi.) Scenario Outline: Consider the situation when we need to run a test scenario multiple times. Assume we need to ensure that the login feature is functional for
             all types of subscribers.

  ## Hooks in Cucumber
      i.) Hooks are code blocks that execute before or after each Cucumber scenario in the execution cycle
      ii.) Certain preconditions, such as executing the program, creating a database connection, preparing the test data, and so on, may be required in some cases. There are also
           several postconditions to be fulfilled, such as ending the database connection, closing the browser, refreshing test data, and logging out of the program. Cucumber
           handles all of these situations with the use of hooks.
      iii.) The methods @Before and @After can be used to define hooks anywhere in the project or step definition layers. Before hook is executed before any other test situations,
            and after the hook is executed after all test scenarios have been completed
  
  ##  In a feature file, what is the maximum number of scenarios?
        A feature file in Cucumber can include a maximum of 10 scenarios. This quantity can differ from one project to the next and from one organization to the next.
        It's advisable to keep the number of scenarios in the feature file to a minimum
        
  
  ## Runner File
       @RunWith(Cucumber.class)
       @CucumberOptions(
               features =  {
                       "src/test/java/com/features/fpos/admin",
               },
               glue = {
                       "com.stepdefinitions"
               },
               monochrome = true,
               tags =  {
                       "@fpos_smoke"
               },
               plugin = {"pretty",
                       "html:target/cucumber",
                       "json:target/cucumber-report/cucumber.json",
                       "json:target/cucumber.json",
                       "com.aventstack.extentreports.cucumber.adapter.ExtentCucumberAdapter: target/report.html"}
       )
       
      
## How to execute test cases parallel in BDD
Answer : "https://cucumber.io/docs/guides/parallel-execution/"

## Data-Table
  Cucumber Data Tables can be used to add multiple parameters in Step Definition in a tabular form rather than putting all the parameters in the Gherkin statement
  Depending on the table shape, we can use one of the following collections:
  1. List<List<String>> table
  2. List<Map<String, String>> table
  3. Map<String, String> table
  4. Map<String, List<String>> table
  5. Map<String,Map<String,String>> table

   1. Table into List of a List of Strings:
      | firstName | lastName | age |
      | Thomas    | Brown | 30 |
      | Perry     | Wilson | 26 |
      | Ashley    | William | 27 |
      Code:
      @When("User enters valid credentials")
    public void entersValidCredential(DataTable dataTable) throws InterruptedException{
        System.out.println("Credentials Entered");
        List<List<String>> signUpForm = dataTable.asLists(String.class);
        String userName = signUpForm.get(0).get(0);
        String passWord = signUpForm.get(0).get(1);
        driver.findElement(By.name("username")).sendKeys(userName);
        driver.findElement(By.name("password")).sendKeys(passWord);
        driver.findElement(By.xpath("//*[@class='oxd-form']/div[3]/button")).submit();
    }

   2. Table into List of Maps
      @InValidCredential
  Scenario: Login with invalid credential - Header with Single Row
  Given User is on HRMLogin page
  Then User enters invalid credentials and Login will be unsuccessful with error message
    | Username  | Password   | ErrorMessage        |
    | Admin1    | admin123!$ | Invalid credentials |

Code:
  @Then("User enters invalid credentials and Login will be unsuccessful with error message")
    public void entersInvalidCredential(DataTable userTable) throws InterruptedException {
        System.out.println("Enter Credentials");
        List<Map<String, String>> user = userTable.asMaps(String.class, String.class);
        String userName = user.get(0).get("Username");
        System.out.println("Username :" + userName);
        driver.findElement(By.name("username")).sendKeys(userName);
 
        String passWord = user.get(0).get("Password");
        System.out.println("Password :" + passWord);
        driver.findElement(By.name("password")).sendKeys(passWord);
 
        driver.findElement(By.xpath("//*[@class='oxd-form']/div[3]/button")).submit();
 
        String errorMessage = user.get(0).get("ErrorMessage");
        String actualErrorMessage = driver.findElement(By.xpath("//*[@class='orangehrm-login-error']/div[1]/div[1]/p")).getText();
        System.out.println("Actual Error Message :" + actualErrorMessage);
        Assert.assertTrue(actualErrorMessage.equalsIgnoreCase(errorMessage));
 
    }

 
