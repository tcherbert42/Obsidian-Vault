________
02-02-2026 | 09:09
Status: #school 
Tags: #CS-4610 #SoftwareEngineering

# What is **Software Testing**?
A whole life cycle over the whole development phase of your software. 
1. Requirement Analysis
	- What does the customer want?
2. Test Planning
	- How am I going to test the functionalities of the software?
3. Test Case Development
	- Set up test cases
4. Environment Setup
5. Test Execution
6. Test Cycle Closure

### Verification vs Validation
**Verification**: refers to the set of tasks that ensure that software correctly implements a specific function. 
**Validation**: refers to a different set of tasks that ensure that the software that has been built is traceable to customer requirements. 

## Types of Software Testing
Manual Testing 
- White Box
- Black Box
	- Functional testing
		- Unit Testing
		- Integration Testing
	- Nonfunctional testing
- Grey Box
Automation Testing: Tests are executed automatically using automation tools & frameworks

| **Manual Testing**                                                                          | **Automation Testing**          |
| ------------------------------------------------------------------------------------------- | ------------------------------- |
| Tests are performed step by step without the help of tools.                                 |                                 |
| Requires human resources and is time consuming                                              | Faster                          |
| Manual Tests are usually updpated in Excel/Word and test results are not readily available. |                                 |
| Won't have frameworks but may use guidelines, checklists, and strict processes.             | Frameworks: Data driven, Hybrid |
| Manual testing won't be as accurate as there is a possibility of human error                |                                 |

##### Black Box Testing
- Knowledge of internal working structure (Code) is not required for this type of testing. Only GUI (Graphical User Interface) is required for test cases. 
- The approach towards testing includes trial techniques and error guessing method. 

##### White Box Testing
- Knowledge of internal working structure is necessarily required for this type of testing. 
- White Box Testing is proceeded by verifying the system boundaries and data domains inherit in the software as there is no lack of internal coding knowledge. 
- It is simple to discover hidden errors
- The most time-consuming testing process
- Most exhaustive among all three testing. 

##### Grey Box Testing
- Partially knowledge of the internal working structure is required. 
- If the tester has knowledge of coding, then it is proceeded by validating data domains and internal system boundaries of the software. 
- Difficult to discover the hidden error. 
- less time consuming than white box testing
- partially exhaustive

###### Functional Testing 
- It verifies the operations and actions of an application
- It is based on requirements of customer
- It helps to enhance the behavior of the application
- It tests what the product does
- Functional Testing is based on the business requirement 
- Unit Testing, Integration Testing, System Testing. 

###### Nonfunctional Testing
- It verifies the behavior of an application
- It is based on expectations of customer
- It helps to improve the performance of the application
- It describes how the product does
- Non-functional testing is based on the performance requirement
- Performance Testing, Usability Testing, Compatibility Testing. 

Unit Testing
- Definition: Testing individual components or functions in isolation. 
- Objective: Ensure each unit of the software performs as designed. 
- Tools: JUnit, NUnit, pytest, etc. 

Integration Testing
- Definition: Testing interactions between integrated components.
- Objective: Validate the **combined** functionality of interconnected units. 
- Tools: Selenium, JUnit, TestNG, etc

System Testing
- Definition: Testing the complete and integrated software system

Performance Testing:
- Tools: Apache JMeter, LoadRunner, Gatling, etc

Usability Testing:
- Methods: User surveys, User interviews, A/B testing, etc. 

Compatibility Testing:
- Tools: BrowserStack, Sauce Labs, CrossBrowserTesting, etc. 

