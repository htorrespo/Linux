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
Figure 1-2.

Continuous integration and continuous delivery
