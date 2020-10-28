The CI/CD paradigm is hyped as the next step in designing a software system that needs to deliver results. CI stands for Continuous Integration, and CD for Continuous Deployment or Continous Delivery.

Its main objective is the automation of engineers' repetitive work and reducing the need to handle dull and detailed processes. CI is about automated tests (including linting and format), and CD about building and deployment (*e.g.* deployment to dev branch).

## CI
Continuous Integration uses automation tools to build and test code after each merge as seamlessly as possible.

Developers should merge with the main code as often as possible, ensuring compatiblity of commited code on the go and software consistency. Before the merge, automated tests will be run to make sure it meets the standards and contains no errors.

The key component is the test environment. Aumotated code testing helps spotting the most serious bugs at early stages of software delivery.

## CD
CD can stand for Continuous Delivery or Continuous Deployment. They both focus working in fast iterations and delivering small batches of code to apply to the app. The differences mostly come down to when the code goes to production.

Both approaches can be mixed or merged in different ways, *e.g.* apps are interally tested in-house (Continuous Delivery) to be polished before released in a Continous Deployment format.

### Continuous Delivery
Focus on keeping the code ready to deploy at any given time: all the sets of features are ready to go, and the lastest build is ready to be delivered at any given time.

CD is challeging the traditional means of releasing code, opting to make new releases available on demand. With smaller batches released, the code becomes more bug-resistant.

It does not define what and when the code will be released for production.

### Continuous Deployment
Has the idea of constant and automted production deployment of every change done to the code. The changes are ideally automated without human intervention.

This approach works well in a internal corporate apps, where the user and the tester are the same person.

It focus on putting all the changes straight into production.

## Software used in CI/CD processes
There are two different categories of CI/CD software:
1. __Installable software__ → apps or services we can install in our computer or remote machine. *e.g.* Jenkins, TeamCity
2. __SaaS__ → apps or services with web interface provided by an external company. *e.g.* CircleCI, Azure DevOps.

What category to choose depends on the app's requirements, the organization's budget and policies, and other factors.

For more information on how to setup a simple CI/CD process with CircleCI, go [here](https://blog.logrocket.com/from-front-end-developer-to-a-devops-an-intro-to-ci-cd-7a8a8713fb34/).

# Keywords
__pipeline__ → a scenario with a action and reaction we can automate by using scripts or some other machinery.

__trigger__ → kickstart that initiates a particular pipeline. *e.g.* code repository trigger, runs tests when a new pull request has been published.

# Sources
[What is CI/CD - all you need to know – codilime](https://codilime.com/what-is-ci-cd-all-you-need-to-know/)\
[What do you need to know about CI/CD as a front end developer – Reddit](https://www.reddit.com/r/Frontend/comments/b72gty/what_do_you_need_to_know_about_cicd_as_a_front/?sort=top)\
[From frontend developer to a DevOps: An intro to CI/CD](https://blog.logrocket.com/from-front-end-developer-to-a-devops-an-intro-to-ci-cd-7a8a8713fb34/)