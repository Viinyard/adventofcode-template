# Advent Of Code Template


## Prerequisites

- [Java 21](https://www.oracle.com/java/technologies/downloads/#java21)
- [Maven 3.9.9](https://maven.apache.org/download.cgi)

## Build

Clic on [`Use this template`](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template#creating-a-repository-from-a-template) and clone the repository.

Then, build the project with the following command:

```shell
  mvn clean install
```

## Setting up the project

### Customize the project

If you want to customize the project, and change the group id for example, you can change group id in the pom.xml file:

```xml
  <groupId>dev.vinyard.adventofcode</groupId>
```
If you do this you also need to change the package name in the BluePrinter environment.xml file to keep it working:

```xml
  <property key="PACKAGE">dev/vinyard/adventofcode</property>
```
All the generated files will be created in the new package.

### Setting up the environment

To get the Advent of Cope scrapper plugin to work, you need to set up your session id :

You can set your session id in your environment variables:

<details><summary><b>How to get my session id</b></summary>

1. Go to the [Advent of Code](https://adventofcode.com/) website.
2. Connect to your account.
3. Open the developer tools of your browser.
4. Go to the `Application` tab.
5. In the `Cookies` section, you will find a cookie named `session`.
6. Copy the value of the cookie.

</details>

<details><summary><b>Show instruction for Linux or macOS</b></summary>

```shell
  export AOC_SESSION_ID=your_session_id
```

</details>

<details><summary><b>Show instruction for Windows</b></summary>

You have to go to the environment variables and add a new one with the name `AOC_SESSION_ID` and the value `your_session_id`.

</details>

Or you can set it in the BluePrinter environment.xml file:

```xml
  <property key="SESSION_ID">your_session_id</property>
```

> [!CAUTION]
> Be careful not to share your session id with anyone, don't commit it in your repository.

### Configure your repository

1. Allow github action to create pull requests on your repository:
   - Go to your repository settings.
   - Go to the `Actions` tab.
   - Go to the `General` section.
   - Check the `Workflow permissions` checkbox.
     - Check `Read and write permissions`
     - Check `Allow GitHub Actions to create and approve pull requests`

2. Add your session_id in your secrets:
   - Go to your repository settings.
   - Go to the `Secrets and variables` tab.
   - Go to the `Actions` section.
   - Clic on `New repository secret`.
   - Add a new secret with the name `AOC_SESSION_ID` and the value `your_session_id`.

3. Create a Personal Access Token (PAT) for the workflow:
   - Fine-grained [Personal Access Token (PAT)](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token) with `contents: write` and `pull-requests: write` scopes.
   - Go to your account settings.
   - Go to the `Developer settings` tab.
   - Go to the `Personal access tokens` section.
   - Go to the `Fine-grained token` section.
   - Create a new token with the `contents: write` and `pull-requests: write` scopes and copy the token.
   - Go to your repository settings.
   - Go to the `Secrets and variables` tab.
   - Go to the `Actions` section.
   - Clic on `New repository secret`.
   - Add a new secret with the name `PAT` and the value `your_personal_access_token`.

That's it, you are ready to generate your solutions with Github Actions. Solutions will be generated in a brand new branch and a pull request will be created.

## How to use

### Generate a solution

To generate the next solution of the year for Advent of Code, run the following command:

```shell
  mvn blueprinter:blueprint@next-solution 
```

To generate a specific solution for Advent of Code, run the following command:

```shell
  mvn blueprinter:blueprint@solution -Dyear=2023 -Dday=1 -Dpart=1
```

> [!IMPORTANT]
> To generate a new pull request with the solution, you need to have your GitHub environment set up

1. On your repository, go to the `Actions` tab.
2. Go to the `All workflows` section.

You will see 3 workflows:
- `Generate antlr4 based Solution of the Day` : This workflow generates the solution for today's day.
- `Generate Next antlr4 based Solution` : This workflow generates the next unimplemented solution of the year. If you haven't implemented any solution yet, it will generate the first one.
- `Maven Build` : This workflow builds the project, generates the README.md file, and pushes the changes to the repository.

## Getting started

Once you have generated the solution, you can implement the code in the generated files.

1. You can find the antlr4 grammar in the `src/main/antlr4` directory.
2. You can find the solution in the `src/main/java` directory
   - You have one ASD file for the antlr4 grammar for the day
   - And one solution file for each part of the day.
3. Go to the `src/test/java` directory to initialize the first test result.
4. The first test from the `test.txt` is not automatically generated, you need to copy it from the Advent of Code website and paste it in the second argument of the `testSolution` method in the test file.
5. You can run the tests, and begin to implement the solution until all tests pass.
6. Once the first test passes, you can try to paste the result of the second test as your puzzle answer in the advent of code website.
7. Don't forget to paste it in the expected result of the second test in the test file.
8. Now you can refactor your code to make it more efficient, and run the tests to check if everything is still working.
9. Push your changes to your repository, and the workflow will generate the README.md file with the result of the tests and benchmarks.

> [!IMPORTANT]
> Automated generation of the README.md is disabled by default, because it erase the actual content of the README.md file.
> You can enable it by uncomment the `on:` section in the `.github/workflows/build.yml` file.

```yaml
on: 
   pull_request:
   push:
     branches:
       - master
```

> [!TIP]
> You can find a lot of examples of resolved solutions in my repository [adventofcode](https://github.com/Viinyard/adventofcode).

