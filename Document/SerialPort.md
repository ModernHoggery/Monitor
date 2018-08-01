## Serial Port ##

### Windows API ###
- CreateFile(): Open a file to access the serial port.
- GetCommState(): Get the configuration of current port and save it to DCB.
- SetCommState(): Use DCB to set the port configuration.
- SetCommTimeouts(): Timeout about operation(read/write).
- ReadFile(): Read form buffer.
- WriteFile(): Write to buffer.
- SetCommMask(): Listen to communication events.
- WaitCommEvent(): Wait for communication events.
- CloseHandle()

#### CreateFile() ####
	
	HANDLE CreateFile(LPCTSTR lpFileName,
					  DWORD dwDesiredAccess,
					  DWORD dwShareMode,
					  LPSECURITY_ATTRIBUTES lpSecurityAttributes,
					  DWORD dwCreationDistribution,
					  DWORD dwFlagsAndAttributes,
					  HANDLE hTemplateFile);
	
Parameters description
- lpFileName: 要打开的文件名称。对串口通信来说就是COM1或COM2。
- dwDesiredAccess: 读写模式设置。此处应该用GENERIC_READ及GENERIC_WRITE。
- dwShareMode: 串口共享模式。此处不允许其他应用程序共享，应为0。
- lpSecurityAttributes: 串口的安全属性，应为0，表示该串口不可被子程序继承。
- dwCreationDistribution: 创建文件的性质，此处为OPEN_EXISTING.
- dwFlagsAndAttributes: 属性及相关标志，这里使用异步方式应该用FILE_FLAG_OVERLAPPED。
- hTemplateFile: 此处为0。

Function description
若文件打开成功，串口即可使用了，该函数返回串口的句柄，以后对串口操作时即可使用该句柄。

Example

	HANDLE hComm=CreateFile("COM1",						//串口号
							GENERIC_READ|GENERIC_WRITE,	//允许读写
							0,							//通讯设备必须以独占方式打开
							NULL,						//无安全属性
							OPEN_EXISTING,				//通讯设备已存在
							FILE_FLAG_OVERLAPPED,		//异步I/O
							0);							//通讯设备不能用模板打开
	
