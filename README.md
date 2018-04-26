# TSThread
Simple thread wrapper. Tested on Windows, Android, OSX, iOS.
 
## Sample Usage

```cpp
TSConditionVariable printedStuff;

class BufferingThread : public TSThread
{
public:
    std::string name();
    void run()
	{
		printf ("hello from a background thread\n");
		printedStuff.notify();
	}
};

void testThreads() {
	TSMutex waitingForPrintedStuff;
	BufferingThread bufferingThread;

	waitingForPrintedStuff.lock();
	bufferingThread.start();
	printedStuff.wait(waitingForPrintedStuff);
	printf("hello from parent thread\n");
	waitingForPrintedStuff.unlock();
}
```