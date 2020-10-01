# cs101f2020-practical03-solution

## DUE: October 5 by 9:10am

[![Actions Status](../../workflows/build/badge.svg)](../../actions)

## Table of Contents

* [Objectives](#objectives)
* [Introduction](#introduction)
* [Continuous Learning](#continuous-learning)
* [System Commands](#system-commands)
  + [Using Docker](#using-docker)
  + [Using Gradle](#using-gradle)
* [Program Requirements](#program-requirements)
* [Expected Program Output](#expected-program-output)
* [Automated Checks with GatorGrader](#automated-checks-with-gatorgrader)
* [Using GitHub Actions CI](#using-github-actions-ci)
* [Reporting Problems](#reporting-problems)
* [Receiving Assistance](#receiving-assistance)
* [Project Assessment](#project-assessment)


## Objectives

To continue to practice using GitHub to access the files for a course assignment.  
Additionally, to  review  how  to  use  the  your  operating  system  and  software  
development  programs  such  as  a "terminal window" and "Docker Desktop". 
You will also continue to practice using Slack to support communication with the 
technical leaders and the instructor.  Next,  you will learn how to use a test suite 
to guide the repair of a Java program that incorrectly uses nested iteration constructs
to sort arrays, also practicing how to use an automated grading tool to assess your progress.

## Introduction

This assignment requires a programmer to implement and test a Java program,
called `BubbleSort`, that will produce four lines of output. More details about
the source code for a similar program are provided in the discussion of array
sorting in Section 3.1.2 of the textbook. Details about performing a shallow
copy of an array are available in Section 3.6 of the textbook. Please note that
this assignment will also require you to read and extend another Java class that
contains a test suite. The programmer is also responsible for learning how to
run and extend a test suite written in the JUnit testing framework, as explained
in Section 1.9. As verified by
[Checkstyle](https://github.com/checkstyle/checkstyle), the source code for the
`BubbleSort.java` and `TestBubbleSort.java` files must adhere to all of the
requirements in the [Google Java Style
Guide](https://google.github.io/styleguide/javaguide.html).

The source code in the `BubbleSort.java` file must also pass additional tests
set by the [GatorGrader tool](https://github.com/GatorEducator/gatorgrader).
For instance, GatorGrader will check to ensure that `BubbleSort` has `println`
statements that produce exactly four lines of output. GatorGrader will also
check that your program performs the correct sorting of an array. Please note
that you should not copy in a new implementation of `BubbleSort` and instead
work to fix the provided solution. More details about the GatorGrader checks
are included later in this document and in the assignment sheet.

## Continuous Learning

If you have not done so already, please read all of the relevant [GitHub
Guides](https://guides.github.com/) that explain how to use many of the features
that GitHub provides. In particular, please make sure that you have read the
following GitHub guides: [Mastering
Markdown](https://guides.github.com/features/mastering-markdown/), [Hello
World](https://guides.github.com/activities/hello-world/), and [Documenting Your
Projects on GitHub](https://guides.github.com/features/wikis/). Each of these
guides will help you to understand how to use both [GitHub](http://github.com) and
[GitHub Classroom](https://classroom.github.com/).

Students who want to learn more about how to use
[Docker](https://www.docker.com) should review the [Docker
Documentation](https://docs.docker.com/). Students are also encouraged to review
the documentation for their text editor, which is available for text editors
like [Atom](https://atom.io/docs) and [VS
Code](https://code.visualstudio.com/docs). You should also review the [Git
documentation](https://git-scm.com/doc) to learn more about how to use the Git
command-line client. In addition to talking with the instructor and technical
leader for your course, students are encouraged to search
[StackOverflow](https://stackoverflow.com/) for answers to their technical
questions.

To do well on this assignment, you should also review Chapter 3 of the course
textbook, paying close attention to Sections 3.1 and 3.6 and the source code on
page 111. Note that the source code on page 111 does not provide an
implementation of `BubbleSort`. However, it does furnish an implementation of a
sorting algorithm that produces the same output as would a correct
implementation of `BubbleSort`. Please see the course instructor or one of the
student technical leaders if you have questions about any of these reading
assignments.

## System Commands

This project invites students to enter system commands into a terminal window. This assignment uses [Docker](https://www.docker.com) to deliver programs, such as `gradle` and the source code and packages needed to run [GatorGrader](https://github.com/GatorEducator/gatorgrader), to a students' computer, thereby eliminating the need for a programmer to install them on their development workstation. Individuals who do not want to install Docker can optionally install of the programs mentioned in the [Project Requirements](#requirements) section of this document.

### Using Docker

Once you have installed [Docker Desktop](https://www.docker.com/products/docker-desktop), you can use the following `docker run` command to start `gradle grade` as a containerized application, using the [DockaGator](https://github.com/GatorEducator/dockagator) Docker image available on [DockerHub](https://cloud.docker.com/u/gatoreducator/repository/docker/gatoreducator/dockagator).

```bash
docker run --rm --name dockagator \
  -v "$(pwd)":/project \
  -v "$HOME/.dockagator":/root/.local/share \
  gatoreducator/dockagator
```

The aforementioned command will use `"$(pwd)"` (i.e., the current directory) as the project directory and `"$HOME/.dockagator"` as the cached GatorGrader directory. Please note that both of these directories must exist, although only the project directory must contain something. Generally, the project directory should contain the source code and technical writing of this assignment, as provided to a student through GitHub. Additionally, the cache directory should not contain anything other than directories and programs created by DockaGator, thus ensuring that they are not otherwise overwritten during the completion of the assignment. To ensure that the previous command will work correctly, you should create the cache directory by running the command `mkdir $HOME/.dockagator`.

If you are running your program on a Windows Operating System, you should run the following command instead, replacing the word "user" with the username of your machine:

```bash
docker run --rm --name dockagator -v "%cd%":/project -v "C:\Users\user/.dockagator":/root/.local/share gatoreducator/dockagator
```

Here are some additional commands that you may need to run when using Docker:

- `docker info`: display information about how Docker runs on your workstation
- `docker images`: show the Docker images installed on your workstation
- `docker container list`: list the active images running on your workstation
- `docker system prune`: remove many types of "dangling" components from your workstation
- `docker image prune`: remove all "dangling" docker images from your workstation
- `docker container prune`: remove all stopped docker containers from your workstation
- `docker rmi $(docker images -q) --force`: remove all docker images from your workstation

### Using Gradle

Since the above `docker run` command uses a Docker image that, by default, runs `gradle grade` and then exits the Docker container, you may want to instead run the following command so that you enter an "interactive terminal" that will allow you to repeatedly run commands within the Docker container.

In Linux and Mac OS:

```bash
docker run -it --rm --name dockagator \
  -v "$(pwd)":/project \
  -v "$HOME/.dockagator":/root/.local/share \
  gatoreducator/dockagator /bin/bash
```

In Windows OS:

```bash
docker run -it --rm --name dockagator -v "%cd%":/project -v "C:\Users\user/.dockagator":/root/.local/share gatoreducator/dockagator /bin/bash
```

Once you have typed this command, you can use the [GatorGrader tool](https://github.com/GatorEducator/gatorgrader) in the Docker container by typing the command `gradle grade` in your terminal. Running this command will produce a lot of output that you should carefully inspect. If GatorGrader's output shows that there are no mistakes in the assignment, then your source code and writing are passing all of the automated baseline checks. However, if the output indicates that there are mistakes, then you will need to understand what they are and then try to fix them.

You can also complete several important Java programming tasks by using the `gradle` tool. For instance, you can compile (i.e., create bytecode from the program's source code if it is correct) the program using the command `gradle build`. Here are some other commands that you can type:

- `gradle grade`: run the [GatorGrader](https://github.com/GatorEducator/gatorgrader) tool to check your work
- `gradle clean`: clean the project of all the derived files
- `gradle check`: check the quality of the code using Checkstyle
- `gradle build`: create the bytecode from the Java source code
- `gradle run`: run the Java program in the command-line
- `gradle cleanTest`: clean the JUnit test suite of derived files
- `gradle test`: run the JUnit test suite and display the results
- `gradle tasks`: display details about the Gradle system

To run one of these commands, you must be in the main (i.e., "home base") directory for this assignment where the `build.gradle` file is located.

## Program Requirements

Please study the source code of the `BubbleSort` class.  Can you see any obvious ways in which
the  implementation  of  this  sorting  algorithm  is  incorrect?   You  should  run  the  test  suite  called
`TestBubbleSort` that is written in the JUnit testing framework.  Please read each of the tests as they explain, 
in Java source code, the expected behavior of a sorting algorithm.  You should pay particularly close attention 
to the fact that the test cases use the array-based sorting algorithm that is provided by the Java programming 
language to support the testing ofBubbleSort.  Why is  this  a  good  approach  to  testing  a  new  sorting  algorithm?   
You  can  run  the  test  suite  for  the `BubbleSort` class by typing "gradle test" in the terminal.  Did you notice that many of the test
cases do not pass?  Can you identify any common reason why the tests might fail?  Please study the source code of `src/test/java/practicalthree/TestBubbleSort.java` to see if you can find and fix any implementation mistakes in the test suite.  Now how many test cases are passing?

At  this  point,  you  should  notice  that  many  of  the  tests  are  still  failing  and,  when  run,  the program  crashes  after  throwing  a `java.lang.ArrayIndexOutOfBoundsException`.  This means that you will have to examine the source code of `BubbleSort` to determine what mistakes are lurking in its implementation.  Please notice that the two sorting methods - one for type `char` and another for type `int` -  contain several (different) mistakes that you should incrementally fix.  Reading about `BubbleSort` on Wikipedia and reasoning about how the current implementation does not match the algorithm’s expected behavior, which must performa type of “swap”,  should help you to find and repair the defects.  How will you know when the program is correct?  If you are stuck, please ask a technical leader or the instructor. You should keep revising the implementation of BubbleSort’s methods until all of the tests pass.

## Expected Program Output

Typing the command `gradle run` in the terminal window should produce the
following output for the completed version of `Swap`. As long as your
program adheres to all of the requirements for the assignment and passes all of
the verification checks, your version should produce similar output. With that
said, program output may vary according to, for instance, the name of the
programmer and the date on which you ran the program.

```
> Configure project :
Configured GatorGradle 0.4.4

> Task :run
Before: [C, E, B, D, A, I, J, L, K, H, G, F]
After : [A, B, C, D, E, F, G, H, I, J, K, L]
Before: [1, 2, 4, 4, 9, 10, -10, 3, 8, 7, 20, 0]
After : [-10, 0, 1, 2, 3, 4, 4, 7, 8, 9, 10, 20]

BUILD SUCCESSFUL in 940ms
2 actionable tasks: 1 executed, 1 up-to-date
```

Running the command `gradle -q --console plain run` will suppress the display of
Gradle's diagnostic information and produce output like the following.

```
Before: [C, E, B, D, A, I, J, L, K, H, G, F]
After : [A, B, C, D, E, F, G, H, I, J, K, L]
Before: [1, 2, 4, 4, 9, 10, -10, 3, 8, 7, 20, 0]
After : [-10, 0, 1, 2, 3, 4, 4, 7, 8, 9, 10, 20]
```

## Automated Checks with GatorGrader

In addition to meeting all of the requirements outlined in the assignment sheet,
your submission must pass the following checks that
[GatorGrader](https://github.com/GatorEducator/gatorgrader) automatically
assesses:

- Repository has at least 5 commit(s)
- The BubbleSort.java in src/main/java/practicalthree has at least 3 multiple-line Java comment(s)
- The BubbleSort.java in src/main/java/practicalthree has at least 3 of the `System.arraycopy` fragment
- The BubbleSort.java in src/main/java/practicalthree has at least 4 of the `java.util.Arrays.toString` fragment
- The BubbleSort.java in src/main/java/practicalthree has at least 4 of the `println(` fragment
- The BubbleSort.java in src/main/java/practicalthree has exactly 0 of the `Add Your Name Here` fragment
- The BubbleSort.java in src/main/java/practicalthree has exactly 0 of the `TODO` fragment
- The BubbleSort.java in src/main/java/practicalthree has exactly 1 of the `package practicalthree` fragment
- The TestBubbleSort.java in src/test/java/practicalthree has at least 1 multiple-line Java comment(s)
- The TestBubbleSort.java in src/test/java/practicalthree has at least 12 of the `@Test` fragment
- The TestBubbleSort.java in src/test/java/practicalthree has exactly 0 of the `Add Your Name Here` fragment
- The TestBubbleSort.java in src/test/java/practicalthree has exactly 0 of the `TODO` fragment
- The TestBubbleSort.java in src/test/java/practicalthree has exactly 1 of the `package practicalthree` fragment
- The command `gradle -q --console plain run` executes correctly
- The command `gradle build` executes correctly
- The command output has exactly 2 of the `After` fragment
- The command output has exactly 2 of the `Before` fragment
- The command output has exactly 4 lines
- The file BubbleSort.java exists in the src/main/java/practicalthree directory
- The file TestBubbleSort.java exists in the src/test/java/practicalthree directory

If [GatorGrader's](https://github.com/GatorEducator/gatorgrader) automated
checks pass correctly, the tool will produce the output like the following in
addition to returning a zero exit code (which you can access by typing the
command `echo $?`).

```
        ┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
        ┃ Passed 20/20 (100%) of checks for cs101f2020-practical03! ┃
        ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

## Using GitHub Actions CI

This assignment uses [GitHub Actions CI](https://github.com/features/actions) to automatically run [GatorGrader](https://github.com/GatorEducator/gatorgrader) and additional checking programs every time you commit to your GitHub repository. The checking will start as soon as you have accepted the assignment -- thus creating your own private repository. If you do not see either a yellow ● or a green ✔ or a red ✗ in your listing of commits, then please contact the instructor.

## Reporting Problems

If you have found a problem with this assignment's provided source code or documentation, then you can go to the [Computer Science 101 Fall 2020 Practical 03](https://github.com/allegheny-computer-science-101-f2020/practical03-solution) repository and [raise an issue](https://github.com/allegheny-computer-science-101-f2020/practical03-solution/issues). If you have found a problem with the [GatorGrader tool](https://github.com/GatorEducator/gatorgrader) and the way that it checks your assignment, then you can also [raise an issue](https://github.com/GatorEducator/gatorgrader/issues) in that repository. To ensure that your issue is properly resolved, please provide as many details as is possible about the problem that you experienced. If you discover a problem with the assignment sheet for this project, then please raise an issue in the GitHub repository that provides the assignment sheets for your course.

Whenever possible, individuals who find, and use the appropriate GitHub issue tracker to correctly document, a mistake in any aspect of this assignment will receive free [GitHub stickers](https://octodex.github.com/) and extra credit towards their grade for the project.

## Receiving Assistance

If you are having trouble completing any part of this project, then please talk
with either the course instructor or a student technical leader during the
course session. Alternatively, you may ask questions in the Slack workspace for
this course. Finally, you can schedule a meeting during the course instructor's
office hours.

## Project Assessment

The grade that a student receives on this practical assignment is a checkmark grade (0 or 1) and is based on:

- **Percentage of Correct Gatorgrader Checks**: Students will receive 1 if their solution passes at least 80% of GatorGrader checks, otherwise they will receive 0\. Students are encouraged to repeatedly revise their source code in an attempt to get their GitHub Actions CI build to pass.