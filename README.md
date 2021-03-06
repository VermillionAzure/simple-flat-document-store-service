# Simple Flat Document Store Service

This is an example REST service for my UH Manoa talk on 11/16/2018.

## Setup

### Linux

You need to have a copy of JVM 9, and install maven.
Also, install `jq`, `git` and `vim` for good measure

### Install Homebrew on Mac

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

### Install Java on Mac

```bash
brew update
brew tap caskroom/cask
```

### Linux: Install Additional Dependencies

```bash
sudo apt install default-jdk
sudo apt install maven
sudo apt install maven jq git vim
```

### Mac: Install Additional Dependencies

```bash
brew install maven
brew install maven jq git vim
```

## Agenda

- Short introduction
- Workshop
- Distributed design problem
- Q&A

## Test Commands

```bash
curl -v -X POST localhost:8080/documents-random
# Keep track of the resulting DOCUMENT_ID

# If you have jq, you can also pipe the output to make it all pretty
curl -v -X GET localhost:8080/documents/$DOCUMENT_ID | jq .

# Add a new attribute: "test-data" : "hi there"
curl -v -X PUT localhost:8080/documents/$DOCUMENT_ID?test-data=hi+there

# Get the document again, but save to "example-data.json"
curl -v -X GET localhost:8080/documents/$DOCUMENT_ID > example-data.json

# Edit the file here
vi example-data.json

# Put a new version of the document up.
curl -v -X PUT -H 'Content-Type: application-json' -d @example-data.json localhost:8080/documents/$DOCUMENT_ID

# Verify that it changed
curl -v -X GET localhost:8080/documents/$DOCUMENT_ID | jq .
```

## Shortlist of important dependencies

- Maven (build system)
- JAX-RS (impl: Jersey 2.x)
- Jackson (JSON serialization)
- SLF4J/Log4j 2.x (logging)
- JUnit/Mockito (testing)
