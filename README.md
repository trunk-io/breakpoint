![GitHub Breakpoint](https://github.com/trunk-io/breakpoint/assets/1265982/8a38229b-80d8-4752-bcf2-a7e86e94342b)
Hosts the code for the Trunk Breakpoint GitHub Action. To get beta access, [sign-up here](https://www.ci-debugger.io?ref=README)

## Overview

Trunk CI Debugger (beta invite required) is available at [app.trunk.io](https://app.trunk.io). With a sprinkling of code you can enable live debugging of your CI actions enabling real-time diagnosis, troubleshooting, and of course debugging of your otherwise ephemeral CI job.

## How does it work?

At its most basic - the trunk ci debugger wraps the execution of whatever command you give it. This allows the debugger to break `on_enter` before running your command and `on_exit` after your command completes. This wrapper connects to the Trunk Service to determine in real time based on the conditional rules whether to trigger a breakpoint or continue execution.

## Usage

<!-- start usage -->

```yaml
- uses: trunk-io/breakpoint@v1
  with:
    # Name of the conditional breakpoint
    breakpoint-id: ""

    # Command to run inside the breakpoint. For example if you want to debug
    # a unit test - this would be the command you execute to run your unit test.
    run: ""

    # Trunk API token used to communicate with trunk web services. The token
    # enables the trunk ci debugger to run conditional breakpoint evaluation
    # and support live debugging of your GitHub action
    trunk-token: ""

    # Organization connected to the provided trunk-token.
    org: ""
```

<!-- end usage -->

### What happens a breakpoint is triggered?

Upon triggering, the execution of your CI run will be paused and the system will attempt to notify someone that a breakpoint has been triggered. In practice when working with a pull request for example, this can be a Slack notification to the author of the PR, or a posting of a comment to the PR thread on GitHub.

The notification will include a link to connect to the debugging session and provides authenticated users with direct access to the machine that is being held.

### What can I do during a debug session?

Anything! When connected over a debug session, you have live access to the terminal that is running your CI job; you are connecting to the live instance that is being used to run your job.

Besides running any normal shell command from the session, the debugger provides a set of command line tooling to further assist your debugging session.

| command         | what does it do                                                                                                                                             |
| :-------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| retry           | runs the provided command again. upon retry the exit code of the breakpoint will be overwritten.                                                            |
| getexit         | returns the current exit code that will be returned when the debugging session terminates (by default this is the exit code of the user provided command)   |
| setexit {value} | overwrites the current exit code of the session with a user provided value. use this to change a failing execution into a passing execution (or vice versa) |
| download {file} | downloads the provided file to your local machine                                                                                                           |
| continue        | resumes execution; returns the current exit code, and allows CI process execution to proceed                                                                |

To start using CI Debugger, [sign-up here](https://www.ci-debugger.io?ref=README)
