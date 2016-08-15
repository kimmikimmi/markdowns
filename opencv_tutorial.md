#OpenCV tutorial

### 1. 이미지 읽기 


~~~
#include "opencv2/highgui/highgui.hpp"
#include <iostream>

using namespace cv;
using namespace std;

int main( int argc, const char** argv )
{
    Mat img = imread("/Users/Jaden/Documents/Cpp/OpenCVTest/OpenCVTest/myPic.JPG", CV_LOAD_IMAGE_UNCHANGED); //read the image data in the file "MyPic.JPG" and store it in 'img'
    
    if (img.empty()) //check whether the image is loaded or not
    {
        cout << "Error : Image cannot be loaded..!!" << endl;
        //system("pause"); //wait for a key press
        return -1;
    }
    
    namedWindow("MyWindow", CV_WINDOW_AUTOSIZE); //create a window with the name "MyWindow"
    imshow("MyWindow", img); //display the image which is stored in the 'img' in the "MyWindow" window
    
    waitKey(0); //wait infinite time for a keypress
    
    destroyWindow("MyWindow"); //destroy the window with the name, "MyWindow"
    
    return 0;
}
~~~

위의 코드는 간단하게 이미지를 읽는 소스코드이다.

Mat 타입의 이미지는 지정해 준 PATH로 부터의 이미지를 읽어와 img 에 저장한다.

그 후 조건문은 예외처리.. 파일이름이나 경로가 틀린 경우일 것이다.

그리고 nameWindow는 name이 MyWindow인 윈도우를 하나 생성하고
image를 보여주는 imShow함수를 통해 MyWindow에 img를 디스플레이 한다.

waitKey함수를 통해 키가 눌려지기를 기다리고
그 후 window를 파괘한다!!

	
	동영상 read후 캡쳐하는 예제
	#include "opencv2/highgui/highgui.hpp"
	#include <iostream>

	using namespace cv;
	using namespace std;

	int main(int argc, char* argv[])
	{
    	VideoCapture cap("/Users/Jaden/Desktop/talkv_high.mp4"); // open the video file 	for reading
    
    	if ( !cap.isOpened() )  // if not success, exit program
    	{
        	cout << "Cannot open the video file" << endl;
        	return -1;
    	}
    
    	//cap.set(CV_CAP_PROP_POS_MSEC, 300); //start the video at 300ms
    
    	double fps = cap.get(CV_CAP_PROP_FPS); //get the frames per seconds of the 	video
    
    	cout << "Frame per seconds : " << fps << endl;
    
	    namedWindow("MyVideo",CV_WINDOW_AUTOSIZE); //create a window called "MyVideo"
    
    	while(1)
    	{
        	Mat frame;
        
	        bool bSuccess = cap.read(frame); // read a new frame from video
        
    	    if (!bSuccess) //if not success, break loop
        	{
            	cout << "Cannot read the frame from video file" << endl;
	            break;
    	    }
        
        	imshow("MyVideo", frame); //show the frame in "MyVideo" window
        
	        if(waitKey(30) == 27) //wait for 'esc' key press for 30 ms. If 'esc' key is pressed, break loop
	        {
    	        cout << "esc key is pressed by user" << endl;
        	    break;
	        }
    	}
    
	    return 0;
    
	}
///////////////////////////////////////////////////////


##4 히스토 그램으로 화소 세기
1. 영상 히스토그램 계싼
2. 영상 모습을 변경하는 룩업 테이블 적용
3. 영상 히스토그램 평활화
4. 특정 영상 내용을 검출하기 위한 히스토그램 역투영
5. 객체를 찾는 평균 이동 알고리즘 사용
6. 영상 비교를 이용한 유사 영상 검색
7. 적분 영상으로 화소세기

###소개

	영상은 다양한 화소값(컬러)으로 이루어진다. 히스토그램을 사용하는 방법과 영상의 모습을 변경하기 위해 히스토그램을 사용하는 방법을 배운다. 영상의 내용을 특성화하고, 영상 내의 특정 객체나 질감을 검출할 때 히스토그램을 사용
	할 수도 있다. 4장에서는 이런 기술 중 일부를 제시한다.

###히스토그램 계산 
	



