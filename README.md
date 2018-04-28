# TSThread
Simple thread wrapper. Tested on Windows, Android, OSX, iOS.

## Setup

Add the header and source files to your project.

## Sample Usage


```cpp
#include "TSThread.h"

TSConditionVariable printedStuff;

class BufferingThread : public TSThread
{
public:
    std::string name()
    {
        return "background thread";
    }
    
    void run()
    {
        printf ("hello from a background thread\n");
        printedStuff.notify();
    }
};

void testThreads() 
{
    TSMutex waitingForPrintedStuff;
    BufferingThread bufferingThread;

    waitingForPrintedStuff.lock();
    bufferingThread.start();
    printedStuff.wait(waitingForPrintedStuff);
    printf("hello from parent thread\n");
    waitingForPrintedStuff.unlock();
}
```