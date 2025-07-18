# Java Installation Guide for Linux (Debian/Ubuntu)

> **A comprehensive step-by-step guide for installing Java on Debian/Ubuntu-based Linux systems.**

---

## Table of Contents

1. [Introduction](#introduction)
2. [Scope](#scope)
3. [Prerequisites](#prerequisites)
4. [Procedure](#procedure)
    - [Step 1: Update System Packages](#step-1-update-system-packages)
    - [Step 2: Check Existing Java Installation](#step-2-check-existing-java-installation)
    - [Step 3: Install OpenJDK](#step-3-install-openjdk)
    - [Step 4: Verify Installation](#step-4-verify-installation)
    - [Step 5: Set Default Java Version](#step-5-set-default-java-version)
    - [Step 6: Set JAVA_HOME Environment Variable](#step-6-set-java_home-environment-variable)
    - [Step 7: Test with a Simple Program](#step-7-test-with-a-simple-program)
5. [Notes](#notes)
6. [Conclusion](#conclusion)
7. [Contact](#contact)
8. [References](#references)

---

## Introduction

This guide provides a clear and concise workflow for installing Java on Debian/Ubuntu-based systems. Java is a widely used programming language and installing it correctly ensures smooth development and execution of Java applications.

---

## Scope

This guide covers:

- Installation of OpenJDK (Java Development Kit) and JRE (Java Runtime Environment).
- Setting up the JAVA_HOME environment variable.
- Compiling and running a basic Java program for validation.

---

## Prerequisites

- A Debian/Ubuntu-based Linux system
- User privileges to run commands with `sudo`
- Internet connection for downloading packages

---

## Procedure

### Step 1: Update System Packages

```bash
sudo apt update && sudo apt upgrade -y
```

---

### Step 2: Check Existing Java Installation

```bash
java -version
```

> If Java is installed, you'll see the version details. If not, proceed to the next step.

---

### Step 3: Install OpenJDK

#### For Java 11 (LTS):

```bash
sudo apt install openjdk-11-jdk -y
```

#### For Java 17 (Newer LTS):

```bash
sudo apt install openjdk-17-jdk -y
```

#### For JRE only (runtime environment):

```bash
sudo apt install openjdk-11-jre -y
```

---

### Step 4: Verify Installation

```bash
java --version  # Check Java
javac --version # Check compiler (JDK)
```

---

### Step 5: Set Default Java Version (If Multiple Installed)

```bash
sudo update-alternatives --config java
```
> Select your preferred version from the list.

---

### Step 6: Set JAVA_HOME Environment Variable

Find Java installation path:

```bash
sudo update-alternatives --config java
```

Example path: `/usr/lib/jvm/java-11-openjdk-amd64/bin/java`

Edit environment file:

```bash
sudo nano /etc/environment
```

Add this line (use your actual path without `/bin/java`):

```text
JAVA_HOME="/usr/lib/jvm/java-11-openjdk-amd64"
```

Reload:

```bash
source /etc/environment
```

Verify:

```bash
echo $JAVA_HOME
```

---

### Step 7: Test with a Simple Program

1. **Create HelloWorld.java:**

    ```java
    public class HelloWorld {
        public static void main(String[] args) {
            System.out.println("Java works on Linux!");
        }
    }
    ```

2. **Compile and Run:**

    ```bash
    javac HelloWorld.java
    java HelloWorld
    ```

> **Output:**  
> `Java works on Linux!`

---

## Notes

- Ensure you install the correct version of Java as per your application requirements.
- Use `sudo` carefully, especially when editing system environment files.
- JAVA_HOME is essential for many Java-based tools and frameworks.
- If you have multiple versions of Java, always check and set the default as needed.

---

## Conclusion

Following this guide will set up Java efficiently on your Debian/Ubuntu system. With Java correctly installed, you are ready to develop and run Java applications seamlessly.

---

## Contact

**Sachin Kumar**  
Email: [chaudhary2000sachin@gmail.com](mailto:chaudhary2000sachin@gmail.com)

---

## References

| Title        | Link |
|--------------|------|
| Official Java Download Options | [https://www.java.com/en/download/help/download_options.html](https://www.java.com/en/download/help/download_options.html) |
| GeeksforGeeks Java Install Guide | [https://www.geeksforgeeks.org/linux-unix/download-install-java-windows-linux-macos/](https://www.geeksforgeeks.org/linux-unix/download-install-java-windows-linux-macos/) |
| Oracle Java SE Installation Overview | [https://docs.oracle.com/en/java/javase/17/install/overview-jdk-installation.html](https://docs.oracle.com/en/java/javase/17/install/overview-jdk-installation.html) |

---
