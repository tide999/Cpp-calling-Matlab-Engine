## **step 1**<br>
 ![step 1](https://github.com/Rogerbin/Cpp-calling-Matlab-Engine/blob/master/m1.png)
 ![step 1](https://github.com/Rogerbin/Cpp-calling-Matlab-Engine/blob/master/m2.png)<br>
**_1_** 中添加 **D:\MATLAB7\bin\win32<br>**
**_2_** 中添加 **D:\MATLAB7\extern\include<br>**
**_3_** 中添加 **D:\MATLAB7\extern\lib\win32\microsoft\msvc71<br>**

 
#linker 添加:
>**libmx.lib<br>**
**libmex.lib<br>**
**libeng.lib<br>**
**libmat.lib<br>**

 ![step 2](https://github.com/Rogerbin/Cpp-calling-Matlab-Engine/blob/master/m3.png)<br>

_示例程序_：***main.cpp***
##Code
	#include <engine.h>
	#include <iostream>
	#include <string>
	#include <cmath>
	
	#pragma comment( lib, "libmx.lib" ) 
	#pragma comment( lib, "libmex.lib" )
	#pragma comment( lib, "libeng.lib" )
	#pragma comment (lib, "libmat.lib")
	
	using namespace std;
	
	int main()
	{
		Engine *m_pEngine;
		m_pEngine = engOpen(NULL);
		engSetVisible(m_pEngine,0);//设置Matlab command 不显示
	
		if (m_pEngine == NULL)
		{
			cout << "Error: Not Found"
		        << endl;
		            exit(1);
		}
	
		const int arraysize=1000;
		const double deg=.0174;
		double SinArray[arraysize];
	
		for(int i=0;i<arraysize;i++)
		{
			SinArray[i]=sin(i*deg);
		}
		cout<<"example";
		mxArray* SIN =mxCreateDoubleMatrix(arraysize,1,mxREAL);
		memcpy((void*)mxGetPr(SIN),(void*)SinArray,sizeof(double)*arraysize);
		engPutVariable(m_pEngine,"sinegraph",SIN);
		engEvalString(m_pEngine,"figure('units','normalized','outerposition',[0 0 1 1])");
		engEvalString(m_pEngine,"plot(sinegraph),");
		system("pause");
		engClose(m_pEngine);
	}
