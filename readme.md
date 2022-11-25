## Resources

### Introduction material

You will be asked for this take-home assignment to develop samples using **Open Enclave** (C++ SDK).

We advise you to do the following things to get started:

1. Install Open Enclave for [Ubuntu 18.04](https://github.com/openenclave/openenclave/blob/master/docs/GettingStartedDocs/install_oe_sdk-Ubuntu_18.04.md)
2. Have a look at the [**simulation mode**](https://github.com/openenclave/openenclave/blob/master/docs/GettingStartedDocs/install_oe_sdk-Simulation.md)
3. Have a look at the “[Helloworld](https://github.com/openenclave/openenclave/tree/master/samples/helloworld)” sample and build it.
4. Do not forget to add this to your *.bashrc* file before compiling
    
    ```bash
    . /opt/openenclave/share/openenclave/openenclave
    ```
    
    You will need to use the following command to run in simulation mode: 
    
    …
    

## Protecting Applications and Data In Use

### Abstract

Today, data is often encrypted at rest in storage and in transit across the network, but not while in use in memory. Organizations that handle sensitive data such as **Personally Identifiable Information** (PII), financial data, or health information need to mitigate threats that target the confidentiality and integrity of either the application or the data in system memory.

In this webinar, experts from the **Confidential Computing Consortium** (CCC) will define Confidential Computing, discuss how businesses are using Confidential Computing today, and review the ecosystem of solutions and open-source projects available to enable applications to make use of Confidential Computing.

### **Key [Topics](https://youtu.be/LdN3R7zDuaA)**

- The Confidential Computing definition and comparison to related technologies
- Key properties of Trusted Execution Environments (TEEs) to look for
- Threats mitigated by Confidential Computing technologies
- Utilization paradigms: using application SDKs vs. runtime deployment systems
- The ecosystem available to support Confidential Computing application development
- Common real-world use cases for Confidential Computing

## Exercise: Making a guessing game

We get that this is a fairly simple exercise and probably one of the first things we do when learning to program, but here, we’re going to do it a bit differently.

In a usual guessing game, the program randomly generates a secret number that will be guessed by the user's inputs, usually using the CLI. This is interesting as it simulates a kind of lottery where the user has to guess the correct number. However, we see that in practice this lottery is rigged because the person organizing the lottery has to access to the secret and could leak it to someone else.

We propose in this sample here to build an “**unbiased” lottery** in the sense that the secret number to be guessed will be generated inside the enclave. This way, no one will be able to cheat and everyone will have to guess it randomly instead of trying to peek directly at the value.

There will be a simple interface: the host will create an enclave for the guessing game, and the secret number will be generated inside the enclave and **MUST NOT** be available directly to the outside world through any endpoint. However, the user’s input will be forwarded to the enclave which will output true if it is equal to the secret, and false otherwise. The host will then provide relevant messages to communicate the results.

You can imagine the guessing game to have the following flow :

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bc45a752-a1c5-408f-9fc1-846922e2602d/Untitled.png)

What you will need to do:

- A host program will ask a prompt to the user, in this prompt, the user will write a number and then this number will be sent to the enclave for a checkup.
- **Make sure as well that the enclave will initiate properly the number in its own memory**, and that the enclave will give a simple answer saying if it’s true or not.
- Once a good answer is found, **make sure to exit the program properly and terminate the enclave properly as well**.
    - As a bonus, you can try to make the enclave “lock itself”, and reject any further call from the host. You will be asked about your method to do it and why this method specifically.
- Please make sure that the project will compile either with a Makefile or a CMakeLists.txt and run in simulation mode. We recommend providing a Makefile.
