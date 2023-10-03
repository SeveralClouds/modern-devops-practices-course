# SAST
Static application security testing (SAST), or static analysis, is a testing methodology that analyzes source code to find security vulnerabilities that make your organization’s applications susceptible to attack. SAST scans an application before the code is compiled. It’s also known as white box testing.

## What problems does SAST solve?
SAST takes place very early in the software development life cycle (SDLC) as it does not require a working application and can take place without code being executed. It helps developers identify vulnerabilities in the initial stages of development and quickly resolve issues without breaking builds or passing on vulnerabilities to the final release of the application.

## Why is SAST an important security activity? 
Developers dramatically outnumber security staff. It can be challenging for an organization to find the resources to perform code reviews on even a fraction of its applications. A key strength of SAST tools is the ability to analyze 100% of the codebase. Additionally, they are much faster than manual secure code reviews performed by humans.

## What tools can be used for SAST?
Together we will practice how to use [Trivy](https://aquasecurity.github.io/trivy/v0.45/), [Sonar](https://www.sonarsource.com/) and [Sync](https://snyk.io/)

## Sync
Snyc offers multiple security solutions:
- **Snyc Code** \
Snyk Code works in the IDEs and SCMs where the developers build and review code and provides fast, actionable, and meaningful results to fix issues in real-time.

- **Snyk Open Source** \
Snyk Open Source allows you to find and fix vulnerabilities in the open source libraries used by your applications. It also allows you to find and address licensing issues in (or caused by) these open source libraries.

- **Snyk Container** \
Snyk Container provides tools and integrations to quickly find and fix vulnerabilities. This allows you to create images that have security built-in from the start.

- **Snyk IaC** \
With Snyk Infrastructure as Code (IaC), you can secure cloud infrastructure configurations before and after deployment.

Together we will focus on Snyc Code and how to get immidiate feedback on the code we write. We can integrate Snyk to our development experience using [IDE-based plugins](https://snyk.io/platform/ide-plugins/).

Another approach would be to allow Snyk to access your GitHub account and get the code from there to perform a scan.

## Trivy
Trivy offers one service - "Trivy scan" which covers:
- Container Image
- Filesystem
- Git Repository (remote)
- Virtual Machine Image
- Kubernetes
- AWS

### Scan container images with Trivy
We are going to practice how to scan container images with Trivy. 

Clone the following repository
```
git clone https://github.com/devopshobbies/docker-templates.git
```
Enter the `08-C++` directory
```
cd docker-templates/08-C++
```
Build the image with Docker
```
docker build -t cpp:1.0 . 
```
Install trivy CLI and then run
```bash
trivy image cpp:1.0
```
Let us now scan a public image from DockerHub
```bash
trivy image python:3.4-alpine
```

## Sonar

## Further reading
- [Sonar docs](https://docs.sonarsource.com/sonarqube/latest/)
- [Sync docs](https://docs.snyk.io/)
