# History #
Now it is time for the story how our company solved the problem. To understand more completely the reason why we created the tool, I need to tell you what we need to test.
Our company specializes in building test automation framework and tooling for web, mobile, desktop and API. It is not a visual application rather than set of C# libraries and other tools to speed up writing of tests scripts. My believe is that when you build a testing tool you need to make sure that it is covered with lots of tests.
For example for the web part, we support 8 different browsers, the five major ones and three headless. The web library uses WebDriver in its core but adds many capabilities on top of it so we have lots of tests related to Selenium grid mode and all integrations with the cloud providers. 
We have tons of other logic that needs to be tested so we ended up for this moment with over 4500 UI tests. I skip here all of the unit tests since they execute super fast. Actually most of the UI tests are quite fast too since we use Bellatrix to test itself. But even this way if we execute them sequentially on a single machine it takes more than 16 hours to execute them.

![16 hours Bellatrix Build](https://i.imgur.com/TrYcNWk.png)

We need to be able to deliver updates a few times a day so this was unacceptable. 
![4 hours Bellatrix Build](https://i.imgur.com/YpH0u84.png)
Now with Meissa, we execute them for under 4 hours. 
