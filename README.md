# Web3J-Scala Library

<img src='https://docs.web3j.io/_static/web3j.png' align='right' width='15%'>

[![Build Status](https://travis-ci.org/mslinn/web3j-scala.svg?branch=master)](https://travis-ci.org/mslinn/web3j-scala)
[![GitHub version](https://badge.fury.io/gh/mslinn%2Fweb3j-scala.svg)](https://badge.fury.io/gh/mslinn%2Fweb3j-scala)

`web3j-scala` is an idiomatic Scala wrapper around [Web3J](https://www.web3j.io) for Ethereum.
Web3J is a lightweight, reactive, type safe Java and Android library for integrating with nodes on Ethereum blockchains.

## Use As a Library
Add this to your SBT project's `build.sbt`:

    resolvers += "micronautics/scala on bintray" at "http://dl.bintray.com/micronautics/scala"

    libraryDependencies += "com.micronautics" %% "web3j-scala" % "0.1.2" withSources()

Only Scala 2.12 with JDK 8 is supported at present; this is a limitation of the Scala ecosystem as of November 7, 2017.

## Run the demo.Demo Program
The `bin/run` bash script performs all of the following steps:

1. Before running the demo program, start up an Ethereum client if you don’t already have one running, such as `geth`.
   The `bin/runGeth` script invokes `geth` with the following options:
     - The Ethereum data directory is set `.ethereum` within the current directory, which will be created if required.
     - HTTP-RPC is enabled.
     - Ethereum's experimental Whisper message facility is enabled.
     - The Rinkeby test network is used; no actual money will be risked for this test.
     - Inter-process communication will be via a virtual file located at `.ethereum/geth.ipc`.
     - A log file for the `geth` output will be written, or overwritten, in `logs/geth.log`;
       the `log/` directory will be if it does not already exist.
   ```
   $ mkdir logs/
   $ geth \
      #--datadir .ethereum/devnet --dev \      # boots quickly but has no deployed contracts from others
      --datadir .ethereum/rinkeby --rinkeby \  # takes about 15 minutes to boot, but has contracts
      --rpc \
      --fast \
      --ipcpath geth.ipc \
      --verbosity 2 \
      --ws \
      --shh \
      --metrics \
      console
   ```
   You will see the message `No etherbase set and no accounts found as default`.
   Etherbase is the index into `personal.listAccounts` which determines the account to send Ether too.
   You can specify this value with the option `--etherbase 0`.
2. Create the smart contract JVM wrapper by running `CreateSmartContracts` defined in `demo/DemoSmartContracts.scala`.
   If you did not create a log file, then the shell that you used will continuously scroll output as you proceed through these instructions, 
   so type the following into another shell:
   ```
   $ sbt "test:runMain demo.CreateSmartContracts"
   ```
3. Run the demo in `demo/Main.scala`:
   ```
   $ sbt "test:runMain demo.Main"
   ```
   
## Developers
### API Documentation
* [This library's Scaladoc is here](http://mslinn.github.io/web3j-scala/latest/api/com/micronautics/web3j/index.html).

* [The Web3J JavaDoc is here](https://jar-download.com/java-documentation-javadoc.php?a=core&g=org.web3j&v=3.0.2),
  and here is the [Web3J gitter channel](https://gitter.im/web3j/web3j).

### Publishing
1. Update the version string in `build.sbt` and in this `README.md` before attempting to publish to Bintray.
2. Commit changes with a descriptive comment:
   ```
   $ git add -a && git commit -m "Comment here"
   ```
3. Publish a new version of this library, including committing changes and updating the Scaladoc with this command:
   ```
   $ sbt publishAndTag
   ```

### Updating Scaladoc
If you just want to republish the Scaladoc for this project, without creating a new version, use this command:

    $ sbt scaladoc

### Updating Scaladoc and Committing Changes Without Publishing a New Version
This task rebuilds the docs, commits the git repository, and publishes the updated Scaladoc without publishing a new version:

    $ sbt commitAndDoc

## Sponsor
<img src='https://www.micronauticsresearch.com/images/robotCircle400shadow.png' align='right' width='15%'>

This project is sponsored by [Micronautics Research Corporation](http://www.micronauticsresearch.com/),
the company that delivers online Scala training via [ScalaCourses.com](http://www.ScalaCourses.com).
You can learn Scala by taking the [Introduction to Scala](http://www.ScalaCourses.com/showCourse/40),
and [Intermediate Scala](http://www.ScalaCourses.com/showCourse/45) courses.

Micronautics Research also offers Ethereum and Scala consulting.
Please [contact us](mailto:sales@micronauticsresearch.com) to discuss your organization&rsquo;s needs.

## License
This software is published under the [Apache 2.0 License](http://www.apache.org/licenses/LICENSE-2.0.html).