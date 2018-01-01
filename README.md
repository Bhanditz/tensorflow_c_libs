https://www.tensorflow.org/install/install_c

# Installing TensorFlow for C

TensorFlow provides a C API defined in [c_api.h](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/c/c_api.h), which is suitable for building bindings for other languages. The API leans towards simplicity and uniformity rather than convenience.
Supported Platforms

You may install TensorFlow for C on the following operating systems:

    Linux
    Mac OS X

Installation

Take the following steps to install the TensorFlow for C library and enable TensorFlow for C:

    Decide whether you will run TensorFlow for C on CPU(s) only or with the help of GPU(s). To help you decide, read the section entitled "Determine which TensorFlow to install" in one of the following guides:
        Installing TensorFlow on Linux
        Installing TensorFlow on Mac OS

    Download and extract the TensorFlow C library into /usr/local/lib by invoking the following shell commands:

     TF_TYPE="cpu" # Change to "gpu" for GPU support
     OS="linux" # Change to "darwin" for Mac OS
     TARGET_DIRECTORY="/usr/local"
     curl -L \
       "https://storage.googleapis.com/tensorflow/libtensorflow/libtensorflow-${TF_TYPE}-${OS}-x86_64-1.4.0.tar.gz" |
       sudo tar -C $TARGET_DIRECTORY -xz

    The tar command extracts the TensorFlow C library into the lib subdirectory of TARGET_DIRECTORY. For example, specifying /usr/local as TARGET_DIRECTORY causes tar to extract the TensorFlow C library into /usr/local/lib.

    If you'd prefer to extract the library into a different directory, adjust TARGET_DIRECTORY accordingly.

    In Step 2, if you specified a system directory (for example, /usr/local) as the TARGET_DIRECTORY, then run ldconfig to configure the linker. For example:

    sudo ldconfig

    If you assigned a TARGET_DIRECTORY other than a system directory (for example, ~/mydir), then you must append the extraction directory (for example, ~/mydir/lib) to two environment variables. For example:

     export LIBRARY_PATH=$LIBRARY_PATH:~/mydir/lib # For both Linux and Mac OS X
     export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:~/mydir/lib # For Linux only
     export DYLD_LIBRARY_PATH=$DYLD_LIBRARY_PATH:~/mydir/lib # For Mac OS X only

Validate your installation

After installing TensorFlow for C, enter the following code into a file named hello_tf.c:

#include <stdio.h>
#include <tensorflow/c/c_api.h>

int main() {
  printf("Hello from TensorFlow C library version %s\n", TF_Version());
  return 0;
}

Build and Run

Build hello_tf.c by invoking the following command:

gcc hello_tf.c

Running the resulting executable should output the following message:

a.out
Hello from TensorFlow C library version number

Troubleshooting

If building the program fails, the most likely culprit is that gcc cannot find the TensorFlow C library. One way to fix this problem is to specify the -I and -L options to gcc. For example, if the TARGET_LIBRARY was /usr/local, you would invoke gcc as follows:

gcc -I/usr/local/include -L/usr/local/lib hello_tf.c -ltensorflow

If executing a.out fails, ask yourself the following questions:

    Did the program build without error?
    Have you assigned the correct directory to the environment variables noted in Step 3 of Installation?
    Did you export those environment variables?

If you are still seeing build or execution error messages, search (or post to) StackOverflow for possible solutions.

Except as otherwise noted, the content of this page is licensed under the Creative Commons Attribution 3.0 License, and code samples are licensed under the Apache 2.0 License. For details, see our Site Policies. Java is a registered trademark of Oracle and/or its affiliates.

Last updated November 2, 2017.

