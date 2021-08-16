# BDD Interview
  ## Enlist the files needed in the Cucumber framework
      i.) Feature File: It has plain text descriptions of single or numerous test situations.
         Keywords like Then, When, Background, Scenario Outline, Feature, And, But, and so on are used in the tests. As a result, it's a file that keeps track of features 
         and their descriptions.
      ii.) Step Definition File: It has the extension .java. It essentially acts as a translator between the test scenario steps provided in the feature file and the automation
          code. Cucumber searches the step definition file and executes the relevant functions that are assigned to that step when it runs a step described in the feature file
      iii.) TestRunner: .java is the file extension for this file. It connects the feature file and the step definition file. It allows the user to run one or more feature files
            at the same time. It contains the locations of the step definition and feature files.
 ## Annotations in Cucumber
       i.) Given: It specifies the requirements for running the test.
                Example: Given I have an account on facebook.
       ii.) When: It establishes the starting point for any test scenario.
                  Example: When I log in to facebook.
       iii.) Then: It contains the expected result of the test which is to be executed.
                  Example: Then registration should be successful.
       iv.) And: Between any two statements, it gives the logical AND condition. AND can be combined with the GIVEN, WHEN, and THEN statements.
                Example: When I enter my account number AND CVV. 
       v.) But: It denotes a logical OR relationship between two propositions. OR can be combined with the GIVEN, WHEN, and THEN statements.
                Example: Then I should be logged in BUT I must enter the OTP.
