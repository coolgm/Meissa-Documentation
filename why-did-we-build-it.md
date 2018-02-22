# Why Did We Build It? #

I had the task to make a research and think of a way to solve the problem. I read everything I could find for a couple of days, besides all of the solutions I know from the companies I worked for in the past. The truth is that for seven years the way how people execute their tests almost haven’t changed. 
Additionally, to my research we asked our followers a similar question in our survey: “Do you run your tests in parallel if YES how?”. Their answers were almost identical to what I read.

Approach      |Percent        
------------- | ------------- 
Unit test framework + Selenium grid  | 56.25%
CI tool as jobs and slaves  | 6.25%
Custom solution | 18.75%
Custom solution | 18.75%

The most common practice is as previously mentioned to run your tests in parallel based on the machine cores and to leverage on the Selenium Grid if we are talking about UI tests. 
However, this solution has a couple of drawbacks. For example, most of the native runners can run tests in parallel only if they are in separate projects/containers/libraries. Meissa can run tests without additional attributes/annotations/configurations added to your source code. Using it make the onboarding of the parallel tests execution easier and faster.
If you already use the in-parallel feature of your native runner- excellent. You can use it side by side with Meissa. The tests will be run with the same speed but in addition to that you will have all of the other Meissa's benefits, and most importantly you will be able to distribute them on multiple machines. 
Some popular solutions for testing environments now utilise Docker containers. One of my favourites is Selenoid. It is a Selenium Grid on steroids that gives you clean installations of specific browsers each time in dedicated containers. It is excellent for WebDriver tests if you test on Firefox, Chrome or Opera.  
How it differs from Meissa? Well, it is not a test runner. You still need a way to execute your tests in parallel if you want to run your tests simultaneously. I considered it during my research. However, there were a couple of limitations which stopped us from using it. The tool doesn't use containers for InternetExplorer and Edge. It doesn't support Appium and running desktop apps. It is built primarily for the major browsers. Of course, it is open-source, and you can create new images on top of the existing ones, but for me, it is too much effort to make it work for these scenarios.
Most of the points are valid for the standard Selenium grid and its tuned versions such as Jsonwired-Grid, Gridrouter, Selenograph. They are no test runners they just give you browsers/devices configurations. If you run your tests on one process even if you have 100 hub nodes, your tests will be executed one by one. So, you can use these tools together with Meissa to run the tests distributed.
Because of the lack of tooling, some people use their CI systems to execute their tests. The usual practice is to mark each test with attribute/annotation such as Machine1, Machine2 and then use the slave/build capability of the CI tool to run them on these machines separately. However, for me this is unacceptable since the ‘balancing’ of the tests is manual and the whole test execution time is equal to the time of the slowest slave’s sub-run. Moreover, when you add or remove tests, you need to calculate that time yourself. With Meissa, the whole process happens automatically without modifications of the tests source code, and the runner produces a single test results file.
Most of the time I like the Microsoft tools. In my previous companies, we used MS test agents, but they have a couple of flaws. Unpredictability how the tests are balanced. They are hard to setup and troubleshoot. And the documentation is missing almost entirely. Last but not least they can run tests only on the Windows platform. And if you cancel the build the machines can be left in an inconsistent state with open browsers and so on.
Meissa is cross-platform and simplified to maximum including everything you need in a single CLI. Moreover, it has most essential features of the MS distributed tests runner but can handle adequately any cancellations and execution issues.
As you can see from the survey, many people don’t have another way but building their tool. I don’t like the idea of reinventing the wheel every time. So we decided that we will develop our tool but share it with the rest of the world. This is why Meissa is open-source.
The last problem that I saw in most solutions, even the open-sourced ones, is that most of them don't give you an easy way to add your logic. I needed to execute a piece of code in various points of the whole process. Because of that Meissa is based on two types of plugins. There is a plugin for each different test technology that you use to execute your tests- MSTest, NUnit, JavaScript, Java. The second type gives you a simple interface to write your plugin and running your code each time during the processes happening in the runner or test agents. For example, for Bellatrix, we built a plugin for cleaning the state of all browsers.
