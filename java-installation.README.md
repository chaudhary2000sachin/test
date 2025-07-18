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

  <img width="960" height="326" alt="Image" src="https://github.com/user-attachments/assets/14f898f8-64db-4c0e-b3f1-f0f4b4053a04" />

---

### Step 2: Check Existing Java Installation

```bash
java -version
```

 <img width="732" height="196" alt="Image" src="https://github.com/user-attachments/assets/b1ef78d9-2c0f-4a43-a46c-10e8dc61a910" />

> If Java is installed, you'll see the version details. If not, proceed to the next step.

---

### Step 3: Install OpenJDK

#### For Java 11 (LTS):

```bash
sudo apt install openjdk-11-jdk -y
```

  <img width="732" height="140" alt="Image" src="https://github.com/user-attachments/assets/2e8885e2-8cb4-49bf-add1-40bd8a0e41ae" />
  
#### For Java 17 (Newer LTS):

```bash
sudo apt install openjdk-17-jdk -y
```
   <img width="732" height="208" alt="Image" src="https://github.com/user-attachments/assets/96358b77-a13a-47be-a5e0-949f3dd48b35" />
  
  
#### For JRE only (runtime environment):

```bash
sudo apt install openjdk-11-jre -y
```

 <img width="691" height="143" alt="Image" src="https://github.com/user-attachments/assets/a29f3d69-f4f7-44a1-83df-58f773719997" />

---

### Step 4: Verify Installation

```bash
java --version  # Check Java
javac --version # Check compiler (JDK)
```

  <img width="760" height="126" alt="Image" src="https://github.com/user-attachments/assets/16694e67-ba6c-41b1-b1c0-3af65118608a" />

---

### Step 5: Set Default Java Version (If Multiple Installed)

```bash
sudo update-alternatives --config java
```
  <img width="1063" height="274" alt="Image" src="https://github.com/user-attachments/assets/7ccc7cad-e6d8-4220-a905-1bde9346cec0" />

> Select your preferred version from the list.

---

### Step 6: Set JAVA_HOME Environment Variable

Find Java installation path:

```bash
sudo update-alternatives --config java
```

  <img width="748" height="192" alt="Image" src="https://github.com/user-attachments/assets/eb8a4bc9-8c5c-4497-aee8-b5b17d6e2ab8" />

Example path: `/usr/lib/jvm/java-11-openjdk-amd64/bin/java`

Edit environment file:

```bash
sudo nano /etc/environment
```

Add this line (use your actual path without `/bin/java`):

```text
JAVA_HOME="/usr/lib/jvm/java-11-openjdk-amd64"
```

  <img width="945" height="100" alt="Image" src="https://github.com/user-attachments/assets/3e6e63f6-52a5-4ef1-a36b-d34b12b08884" />

Reload:

```bash
source /etc/environment
```

Verify:

```bash
echo $JAVA_HOME
```

  <img width="492" height="90" alt="Image" src="https://github.com/user-attachments/assets/da6e3cc0-18a2-4cd2-8cb9-f91ed6bceee8" />

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

    <img width="492" height="122" alt="Image" src="https://github.com/user-attachments/assets/7283ad1a-5489-4205-89bd-4e674d70583a" />

2. **Compile and Run:**

    ```bash
    javac HelloWorld.java
    java HelloWorld
    ```

    <img width="492" height="77" alt="Image" src="https://github.com/user-attachments/assets/7ad9f165-ccac-4ddf-8624-58940b17c3c8" />
   
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
