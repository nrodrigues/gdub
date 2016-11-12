# What's gradlew?
`gradlew` is a `gradle` / `gradlew` wrapper. Not to be
confused with the [Gradle][] [Wrapper][], `gradlew` uses the Gradle Wrapper on
projects where one is configured, and falls back to use the `gradle` from the
`$PATH` if a wrapper is not available. 

[Gradle]:  http://www.gradle.org
[Wrapper]: http://www.gradle.org/docs/current/userguide/gradle_wrapper.html

# Installation

## Installation with `brew`

```bash
brew install nrodrigues/gradlew/gradlew
```

## Aliasing the `gradle` command
For maximum fidelity add a `gradle` alias to `gradlew` to your shell's configuration
file.

Example *bash*:

```bash
echo "alias gradle=gradlew" >> ~/.bashrc
source ~/.bashrc
```

From now on you can just type `gradle ...` from wherever you are and `gradlew` takes
care of the rest. Happiness ensues!

# Why gradlew?

## The problems with `gradle` and `gradlew`
gdub is a convenience for developers running local Gradle commands and addresses
a few minor shortcomings of `gradle` and `gradlew`'s commandline behaviour.
These are known issues, and they are set to be addressed in future versions of
Gradle. If you are interested in the discussions surrounding them, check out:

  - [Issue Gradle-2429](http://issues.Gradle.org/browse/Gradle-2429)
  - [Spencer Allain's Gradle Forum Post](http://gsfn.us/t/33g0l)
  - [Phil Swenson's Gradle Forum Post](http://gsfn.us/t/39h67)

Here are the issues I feel are most important, and the ones gdub attempts to
address:

### You have to provide a relative path to `build.Gradle`
If you are using the `gradle` command, and you are not in the same directory as
the `build.gradle` file you want to run, you have to provide `gradle` the path.
Depending on where you happen to be, this can be somewhat cumbersome:

```bash
$ pwd
~/myProject/src/main/java/org/project
$ gradle -b ../../../../../build.gradle build
```

With `gradlew`, this becomes:

```bash
$ gradlew build
```

### You have to provide a relative path to `gradlew`
If you are using `gradlew` and you want to run your build, you need to do
something similiar and provide the relative path to the `gradlew` script:

```bash
$ pwd
~/myProject/src/main/java/org/project/stuff
$ ../../../../../../gradlew build
```

Again, with `gradlew` this becomes:

```bash
$ gradlew build
```

### You have a combination of the above problems
I don't even want to type out an example of this, let alone do it on a
day-to-day basis. Use your imagination.

### Typing `./gradlew` to run the Gradle wrapper is kind of inconvenient
Even with tab completion and sitting at the root of your project, you have to
type at least `./gr<tab>`. It gets a bit worse if you happen to have a
`Gradle.properties` file, and with the Gradle wrapper, you have a `gradle`
directory to contend with as well. A simple alias would solve this problem, but
you still have the other (more annoying) issues to contend with.

### You meant to use the project's `gradlew`, but typed `gradle` instead
This can be a problem if the project you are building has customizations to the
Gradle wrapper or for some reason is only compatible with a certain version of
Gradle that is configured in the wrapper. If you know the project uses Gradle,
you may be tempted to just use your own system's Gradle binary. This might be
ok, or it might cause the build to break, but if a project has a `gradlew`, it
is a pretty safe bet you should use it, and not whatever Gradle distribution you
happen to have installed on your system.

# The `gradlew` payoff
Anywhere you happen to be on your project, you can run the Gradle tasks of your
project by typing `gradlew <tasks>`, regardless of whether you use the Gradle Wrapper
in your project or not.

`gradlew` works by looking upwards from your current directory and will run the
nearest `build.Gradle` file with the nearest `gradlew`. If a `gradlew` cannot
be found, it will run the nearest `build.Gradle` with your system's Gradle. This
is probably always what you want to do if you are running Gradle from within a
project's tree that uses the Gradle build system.
