**Volume resources**  
Files or directories on the root file system \(except under `/sys`, `/dev`, or `/var`\)\. These include:  
+ Folders or files used to read or write information across Greengrass Lambda functions \(for example, `/usr/lib/python2.x/site-packages/local`\)\.
+ Folders or files under the host's /proc file system \(for example, `/proc/net` or `/proc/stat`\)\. Supported in v1\.6 or later\. For additional requirements, see [Volume resources under the /proc directory](#lra-proc-resources)\.
To configure the `/var`, `/var/run`, and `/var/lib` directories as volume resources, first mount the directory in a different folder and then configure the folder as a volume resource\.
When you configure volume resources, you specify a *source* path and a *destination* path\. The source path is the absolute path of the resource on the host\. The destination path is the absolute path of the resource inside the Lambda namespace environment\. This is the container that a Greengrass Lambda function or connector runs in\. Any changes to the destination path are reflected in the source path on the host file system\.  
Files in the destination path are visible in the Lambda namespace only\. You can't see them in a regular Linux namespace\.

**Device resources**  
Files under `/dev`\. Only character devices or block devices under `/dev` are allowed for device resources\. These include:  
+ Serial ports used to communicate with devices connected through serial ports \(for example, `/dev/ttyS0`, `/dev/ttyS1`\)\.
+ USB used to connect USB peripherals \(for example, `/dev/ttyUSB0` or `/dev/bus/usb`\)\.
+ GPIOs used for sensors and actuators through GPIO \(for example, `/dev/gpiomem`\)\.
+ GPUs used to accelerate machine learning using on\-board GPUs \(for example, `/dev/nvidia0`\)\.
+ Cameras used to capture images and videos \(for example, `/dev/video0`\)\.
`/dev/shm` is an exception\. It can be configured as a volume resource only\. Resources under `/dev/shm` must be granted `rw` permission\.

AWS IoT Greengrass also supports resource types that are used to perform machine learning inference\. For more information, see [Perform machine learning inference](ml-inference.md)\.