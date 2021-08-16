## BDD Interview
  # Enlist the files needed in the Cucumber framework
      i.) Feature File: It has plain text descriptions of single or numerous test situations.
         Keywords like Then, When, Background, Scenario Outline, Feature, And, But, and so on are used in the tests. As a result, it's a file that keeps track of features 
         and their descriptions.
      ii.) Step Definition File: It has the extension .java. It essentially acts as a translator between the test scenario steps provided in the feature file and the automation
          code. Cucumber searches the step definition file and executes the relevant functions that are assigned to that step when it runs a step described in the feature file
      iii.) TestRunner: .java is the file extension for this file. It connects the feature file and the step definition file. It allows the user to run one or more feature files
            at the same time. It contains the locations of the step definition and feature files.
