Download Link: https://assignmentchef.com/product/solved-cs1632-exercise3
<br>
For this assignment, you and a partner will write a systems-level, automatedblack-box tests for the Reddit website using the Selenium IDE. Specifically,we are going to test the r/cats subreddit at:

https://www.reddit.com/r/cats/

It was chosen because it is a nice safe subreddit which is policed pretty well. Besides, it’s cats.

First, let’s start by adding the Selenium IDE browser extension for your webbrowser by selecting “Chrome Download” or “Firefox Download” on the belowwebsite:

https://www.selenium.dev/selenium-ide/

Then, open Selenium IDE by clicking on the newly created browser extension withthe “Se” symbol. You should see a pop up window that looks very similar to theone shown on the lecture slides.

## Task 1: Write test cases

Write a test case for each requirement listed in[requirements.md](requirements.md). Name each test case same as therequirement name (e.g. FUN-TITLE). I’m asking you to do this for the purposesof GradeScope autograding. Normally, you would use a more descriptive name.

Remember, each test must end with an assertion! The list of availableassertions and other commands are available at:

https://www.selenium.dev/selenium-ide/docs/en/api/commands

### Tips for Writing assertions for each Test

You will want to use the below commands and assertions to test each of the requirements:

FUN-TITLE: “assert title”

FUN-JOIN-BUTTON-EXISTS – “assert text”

FUN-SIGNUP-LINK – “store attribute” followed by “assert”. You will be storingthe attribute value to a Selenium variable and asserting on the value of thatvariable. Now there is a defect in Selenium IDE with the “store attribute”command where the target selector button is disabled when it should be enabled.A work around is to enter a command such as “assert text” or “click” whichallows you to use the target selector, fill in the locator string using it, andthen revert to “store attribute”. As I said, while Selenium web driver is verymature, Selenium IDE is a work in progress. &#x1f642;

FUN-SEARCH-SMELLY-CAT – “assert text”

FUN-RULE-3 – “assert text”

FUN-RULES-11-ITEMS – “assert element present” for the 11th item; “assert element not present” for the locator for the 12th item.

**Hint:** If you are really stuck, there is a solution project file [RedditCats Solution.side](Reddit%20Cats%20Solution.side) that you can open fromSelenium IDE. Take a peek but don’t loiter!

### Other Tips

Sometimes your test case will not work as expected. Here are a few hints on how to debug a problem:

1. Check the Log window at the bottom of the Selenium IDE. It will tell youwhich step failed for what reason (in red).

1. Select the test step that failed in the main test case window, and thenselect the Reference tab at the bottom pane of the IDE. It will displayusage instructions for that command. Remember always, the first argument goesto the Target field and the second argument goes to the Value field, regardlessof command.

1. Sometimes the target component of a test step is the problem. The selectorbutton tries to generate a locator string as best it can using xpath, cssselector, or id tag. But it is not fool proof. The problem is, the web pagemay change ever so slightly on the next page load (e.g. due to a new post, or anew comment) and then the locator will stop working. You will notice thatthere is a small down arrow at the end of the target text box. If you click onthat arrow, you will see alternative locator strings to the current string.Select the one that looks specific enough to be able to point to the target butalso general enough to not change between page loads. You do need to try thisout several times to get a feel of what a good locator string is. Here is anin-depth discussion about locators:

https://www.selenium.dev/documentation/en/getting_started_with_webdriver/locating_elements/#element-selection-strategies

1. Sometimes you can use an XPATH position locator string to check that anelement exists at an expected location (“assert element present”) or doesnot exist (“assert element not present”). But to do this, you have to selectthe XPath position locator string in the drop-down list of optional strings inthe Target field.

1. For those of you who are working in groups, you will be working on the sameshared .side project file. So it is especially important that your pullbefore opening the project file and push immediately after you have modifiedand saved the project file. Otherwise, you may get merge conflicts. Mergingconflicts is possible by using the technique I went over with the[Using_Git](https://github.com/wonsunahn/CS1632_Fall2020/blob/master/lectures/Using_Git.pdf)slides, but it’s best to avoid it.

## Task 2: Add test cases to test suite and save project

1. Choose “Test Suites” from the left panel drop down menu.

1. There will already be a “Default Suite” there with possibly one or more tests.

1. Right click on “Default Suite”, or click on the vertical-3-dot context menu button, and select “Rename” and rename to “RedditCats”.

1. Right click on “RedditCats”, or click on the vertical-3-dot context menubutton, and select “Add tests”. Make sure all tests are checked as shown inthe below figure. Press on the “Select” button.

&lt;img alt=”Test Suite” src=test-suite-selection.png width=700&gt;

1. Click on the “Save project” button on the top right corner that looks like afloppy disk. Save to file name “Reddit Cats.side” in the exercise root folder.

## Task 3: Export test suite to JUnit class

Once you are done writing your Selenium test suite, let’s try exporting the testsuite in Selenium IDE to a Java JUnit test class.

Follow these instructions:

1. Right click on “RedditCats”, or click on the vertical-3-dot context menubutton, and select “Export”.

1. Select “Java JUnit” in the list of language options and optionally check“Include step descriptions as a separate comment” to generate more detailedcomments. Leave other boxes unchecked.

1. Save the resulting file into “RedditCatsTest.java”.

You can now run the RedditCatsTest JUnit class using the provided[TestRunner.java](TestRunner.java) using one of the following scripts:

* If you are running Windows:“`cd Windowsrun.bat“`* If you are running Mac:“`cd Macrun.sh“`* If you are running Linux:“`cd Linuxrun.sh“`

Note that the script only works if you have Chrome version 85 installed on yourcomputer (the most recent version as of today). If you have a differentversion of Chrome, you may have to update the chromedriver.exe (orchromedriver) in your respective OS folder (Windows / Mac / Linux) bydownloading a new Chrome Web Driver from:

https://chromedriver.chromium.org/downloads

Your Chrome version can be obtained by clicking on the vertical-3-dot menu atthe top right corner of your browser, then Help &gt; About Google Chrome.

If things go properly, you will see the Chrome browser pop up repeatedly foreach test case, perform the actions, and close. In the command line, youshould see “ALL TESTS PASSED”, which is printed by TestRunner if there are nofailures.

There are multiple reasons why you would want to export to JUnit:

1. You may have a pre-existing testing framework in JUnit (or Python Pytest, orJavaScript Mocha, etc). And you may want to merge the Selenium IDE testingscript to the language and framework of your choice.

1. Exporting to JUnit really gives you a good sense of what’s happening underthe covers (in terms of the actual calls to the WebDriver). Also, if thereis a test case that is particularly hard to nail down just by using SeleniumIDE, you can touch it up in the form of exported Java code.

1. Selenium IDE also gives the option to export your JUnit test directly to aSelenium Grid which can run the test cases in parallel. This can allow youto utilize a server farm to finish your testing very quickly, although we willnot explore this option today.

### Tips for JUnit + Selenium problem solving

1. Often problems that are not apparent in the Selenium IDE commands become apparent in the Java code. Read the Java code to detect problems.

1. If you want to run your Selenium tests on Eclipse using the “Run JUnit” feature, you will have to also add this line to the beginning of the @Before setUp() method:“`System.setProperty(“webdriver.chrome.driver”, “Windows/chromedriver.exe”);“`Or whatever the path is to your OS compatible chromedriver.

1. One common problem with Selenium is that it takes a long time for certain web pages or web elements to load and if Selenium proceeds with testing immediately after opening a page, the tests will fail. So Selenium provides APIs to allow you to wait until an event happens (e.g. the element is loaded). All the details about which APIs to use on which situations is in the page:

https://www.selenium.dev/documentation/en/webdriver/waits/

For your purposes, an implicit wait setting at the beginning should be enough. Insert the following line in the @Before setUp() method:“`driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);“`In order to use that line, you will need to also import this library:“`import java.util.concurrent.TimeUnit;“`What that does is: for every step, if the corresponding element is missing, it inserts an implicit wait of 10 seconds before signaling a failure.

1. Another common problem is that depending on the browser window size, certain elements may disappear. For example, the Reddit site would hide the “rules” bar on the right hand side if the windows is too narrow. One way to solve this is to uniformly set the window size at the setUp() method so that all your tests will have the correct size:“`driver.manage().window().setSize(new Dimension(1200, 800));“`And remove all calls to setSize in your test cases.

1. Lastly, there is a quirk with the Reddit website that I only found out recently. The following two websites are very different websites:* https://www.reddit.com/r/cats/* https://www.reddit.com//r/cats/You’d be surprised! Make sure you are accessing the former and not the latter.

## Submission

Each pairwise group will submit the exercise *once* to GradeScope, by *onemember* of the group. The submitting member will press the “View or editgroup” link at the top-right corner of the assignment page after submission toadd his/her partner, as usual.

When you are done, submit your github repository to GradeScope at the “Exercise3 GitHub” link. Once you submit, GradeScope will run the autograder to gradeyou and give feedback. If you get deductions, fix your code based on thefeedback and resubmit. Repeat until you don’t get deductions.

You can either create a GitHub repository just for Exercise 3 and then submitthat. Or, you may just directly upload files. If you choose the latteroption, please make sure you upload the “Reddit Cats.side” and“RedditCatsTest.java” files.

My solution test cases are stored as the [Reddit CatsSolution.side](Reddit%20Cats%20Solution.side) file afore mentioned. Comparewith your test cases and see if you implemented them correctly. It is in JSONformat so you should be able to open it with a text editor and trace it withyour eyes, if that’s what you prefer.

## GradeScope Feedback

The GradeScope autograder works in 2 phases:

1. **RedditCatsTest on https://www.reddit.com/r/cats**: This tests yourRedditCatsTest.java file on the cats subreddit as originally intended. Allof your tests should pass.

1. **RedditCatsTest on https://www.reddit.com/r/dogs**: This tests yourRedditCatsTest.java file on the dogs subreddit, repeating the same steps butfor a different webpage. Now some tests should pass but some should fail.Specifically, FUN-JOIN-BUTTON-EXISTS and FUN-SEARCH-SMELLY-CAT should pass andthe rest shold fail.

You may be curious how I was able to run the tests on the GradeScope docker images when they most likely don’t have displays to render the Chrome browser. The Chrome webdriver, as well as other webdrivers, can be run in “headless” mode. That is, the tests can be performed inside the web engine without having to actually display the page. This is very common practice since in a work setting, testers will be running tests on server machines or even on the cloud in docker images like I did. If you need to do this in the future, you can achieve this by passing options when creating the Chrome webdriver:

“`ChromeOptions options = new ChromeOptions();options.addArguments(“–headless”);options.addArguments(“–disable-dev-shm-usage”); // overcome limited resource problemsdriver = new ChromeDriver(options);“`

## Resources

These links are the same ones posted at the end of the slides:

* Selenium IDE Command Reference:https://www.selenium.dev/selenium-ide/docs/en/api/commands