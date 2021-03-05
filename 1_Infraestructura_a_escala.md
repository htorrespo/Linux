<!-- https://link-springer-com.ezproxy.unal.edu.co/chapter/10.1007/978-1-4842-0511-2_1 -->
# Managing Large-Scale Infrastructure

This chapter is about the issues that come up in infrastructure management at a large scale. Mission-critical decisions such as infrastructure architecture, and decisions on matters such as licensing and support, are all part of infrastructure design. When managing a small infrastructure, many of these issues do not have the same criticality as they do in a large enterprise. A scalable architecture is an important foundation for a successful, large infrastructure.

Infrastructure management can be divided into two components: application deployment and infrastructure architecture. First we review application deployment and then look at different infrastructure architecture models. We also review the components that make up a scalable infrastructure.

## Application Deployment
From design to production, a scalable infrastructure enables developers to code, test, and deploy applications quickly. The traditional deployment model has not been effective at speeding up the design-to-production pipeline. Figure 1-1 shows the traditional deployment model where a major hurdle to reaching production is testing. After developers have written code, they pass it to a quality assurance (or QA) team that tests the code manually and sends it back to the development team for fixing. After the fixes are complete, the code is tested again. When the tests pass, the code is sent to staging. Staging is a replica of production. After the code passes through staging, the operations team deploys the code to production using a change management process. This entire process for a single line of change in code might take two to four weeks.
Open image in new windowFigure 1-1.
Figure 1-1.

Traditional design-to-production model
Realizing that this model is not a very effective one, a newer model came into existence—that of continuous integration and continuous delivery (CI/CD). With this model, as soon as unit testing is complete and code is checked into the source code repository, the CI/CD pipeline kicks in. The pipeline consists of an automated build system, using tools such as Jenkins ( http://jenkins-ci.org ). The build system takes the code and builds it, outputting a compiled binary. The binary can then be taken and installed into production in an automated manner (Figure 1-2).

Open image in new windowFigure 1-2.

Figure 1-2. Continuous integration and continuous delivery

The CI/CD pipeline automates as many tests as possible to gain confidence in the code. In addition, it performs a complete build of the software system and ensures the code that has been checked in does not cause anything to break. Any failure has to be investigated by a developer. There are numerous software products that can help implement a CI/CD pipeline, including the following:

- Jenkins ( http://jenkins-ci.org )

- CruiseControl ( http://cruisecontrol.sourceforge.net )

- Buildbot ( http://buildbot.net )

## Software Development Automation

Software development automation is the process of automating as many components of software development as possible. The goal of software development automation is to minimize the time between when a developer checks in code to the time a product is in the hands of an end user or is being used in production. Without software development automation there is a significant delay in getting software products to end users. There are various components of software development automation, a few of them are listed in the following sections, along with the tools that can help accomplish the automation needed.

### Build Automation

Build automationis the process of automating the immediate tasks that need to happen after a developer checks in code. This process includes actually building the code. The build is triggered on a check-in by the developer. Some of the features of build automation are as follows:

- Frequent builds to catch problems with code sooner than later

- Incremental build management, an attempt to build modules and then integrate them

- Build acceleration, so that a large code base does not slow down the build

- Build status reporting and failure detection

Some of the tools that can help with build automation are the following:

- Gradle ( http://www.gradle.org )

- Apache Ant ( http://ant.apache.org )

- Apache Maven ( http://maven.apache.org )

- Gnu Make ( http://www.gnu.org/software/make/ )

### Software Configuration Management

Software configuration management (SCM) is an integral component of software development automation. A few questions that need to be answered in software configuration management are

- Which source code management system do we use?

- How do we do code branches?

- What kind of revisions in software will we support?

Anything that has to do with managing the actual code itself is considered part of SCM. The following is a list of some of the tools that can help with the source code control part of SCM:

- Git ( http://git-scm.com )

- SVN ( https://subversion.apache.org )

- Mercurial ( http://mercurial.selenic.com )

SCM is more of a process than a selection of tools, and includes questions about how to manage branches, versions, merging, and code freeze, and should be answered with policy rather than a product.

### Continuous Integration

There can be many different components of a large software project. After a developer checks in code, it has to be integrated with the rest of the code base. It is not feasible for one developer to work on integrating his or her components with all other components. Continuous integration (CI) ensures all different components of code are eventually merged into one mainline that can then be built and a complete product released. The components of an effective CI are as follows:

    The CI process should start automatically with a successful build of code.

    Developers should commit code frequently to catch issues early.

    The CI build should be self-testing.

    The CI build should be fast.

An example of a CI process is that of a web services application divided into a PHP front end and a Java back end with MariaDB as a database. Any change on the PHP front-end code should trigger a full CI pipeline build that also builds Java and does a full test that includes database calls.

### Continuous Delivery

So far, we have automated builds using build automation, we have integrated our code with other components using CI, and we have now arrived at the final step of continuous delivery (CD). CD is the process of getting code out to production as soon as a successful CI is complete. This is one of the most crucial steps in software development; a botched CD can cause an outage in your environment. The output of CI can be packaged binary. Software that can help with CD includes the following:

- Gnu AutoConf ( https://www.gnu.org/software/autoconf/ )

- Go ( http://www.go.cd )

- Chef ( https://www.getchef.com/chef/ )

- SaltStack ( http://www.saltstack.com )

The output of a CI pipeline can be a war file in case of Java or a tar.gz file or a package that is based on your production distribution. The CD process has to take this output and get in on a running production server. This should be done within the scope of release management.
Change Management

Change control plays a very important role in effective infrastructure management. Change management is the process of reviewing, approving, and executing changes relating to infrastructure components. To operate at a large scale, there has to be an effective change management process. The process should not be that of rubber-stamping changes without reviewing them. It also should not be so burdensome that engineers become wary of changes as a result of the burden required in getting changes pushed out.
Changes can be classified into the following categories:

- Low risk

- Medium risk

- High risk

A low-risk change is one that does not affect an infrastructure’s uptime. An example is adding a few comments to code in a production environment and deploying them to production. It is possible the software engineer will forget to add the appropriate blocks of code that denote a comment, but this causes, at most, build failure, not the failure of the application. Hence, this type of change can be classified as low risk.

A medium-risk change can be classified as something that might potentially affect production. An example is adding a new virtual machine to a load balancer group. A misconfiguration on the load balancer might knock out the entire cluster; however, these chances are low because the change is not modifying the existing servers behind the load balancer.

An example of a high-risk change is upgrading an entire application to a new version of the code base, with significant changes in it. This certainly affects production because it involves code changes, and it involves the entire application cluster.

An organization should have published policies on what types of changes fall into the low-, medium-, and high-risk categories. No one should be allowed to make changes to production without following the change process in place.

Regardless of the type of change, medium to large organizations have a change control board that reviews changes, either daily or a few times a week. The board approves changes that are then executed by engineers. Changes may not be allowed during certain times of the year. If you are working for an online retailer, then no changes may be allowed to the infrastructure during the holiday season in an effort to minimize anything that affects sales. In the United States, a “freeze” might go into effect starting November 1 and lasting until January 5, because during this time a lot of online retail shopping happens for the holiday season.

A question may arise regarding how change control integrates into CI/CD or into the model where code is pushed to production in an automated manner as soon as it is ready. There are times when the CI/CD model should be placed on hold, such as during the freeze period for online retailers. During other times, software itself can integrate with a change control system so that all changes are documented, even if they are pushed out automatically. In addition, large-scale changes such as upgrading the entire code base should perhaps be reviewed and supervised by a team of engineers, instead of allowing it to be fully automated.
