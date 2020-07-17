# PyTrack - The Python eYe Tracking Library

### Overview

PyTrack is a python-based pupil-tracking library. The library tracks eye movements with commodity hardware, such as a laptop webcam, and gives a real-time stream of eye coordinates.  It provides the functionality of eye-tracking and blink detection and encapsulates these in a generic interface that allows clients to use these functionalities in a variety of use-cases. 

The goal has been to make the library generic. A user can provide any interface: a static image, text, video, and call upon PyTrack to capture eye-movement data. The default is to measure eye-movement data captured by a live camera feed, a saved video file can also be used as input.PyTrack can optionally save audio and video as an aid to debugging and development. 

Use PyTrack to develop applications that can be controlled by eye movements or blinks. Or use it to track eye movements as an aid to medical diagnostics.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Overall Design
PyTrack has three modules - EyeTracking, AudioVideo recording, and the main interface (along with the data handling class). 
The EyeTracking module is the core of the library that performs eye tracking and blink detection. This module is responsible for accessing the webcam to track eyes and write it to a CSV. <br>
AudioVideo Recording module records audio and video.<br>
The third module is the primary interface to PyTrack - The PyTrackRunnerClass. This class provides the user with an interface to execute the functionalities of the library. The user can specify the UI, the eye-tracking functionality, the destination folder and exploit the functions of this library by using various combinations with the following call-

`pytrack_runner(UI = False,`<br>
` UI_file_name = “User_ImageUI_EscExit”,` <br>
`pupilTracking = False,`<br>
`blinkDetection = False,` <br>
`video_source = 0,` <br>
`eyeTrackingLog = True,`<br>
`eyeTrackingFileName = ‘EyeTrackLog’,` <br>
`videoRecorder = False,` <br>
`videoName = ‘video’,` <br>
`audioRecorder = False,` <br>
`audioName = ‘audio’,` <br>
`syncAudioVideo = False,` <br>
`destinationPath = ‘/Output’)`
The user can set flags to run the combination of these functionalities.

UI (bool, optional): This parameter enables the user to run UI. Default: False.

UI_file_name(str, optional): This parameter takes the file name of the UI. 
Default: “User_ImageUI_EscExit”.

pupilTracking(bool, optional): This parameter enables the user to run pupil tracking. 
Default: False.

blinkDetection(bool, optional): This parameter enables the user to run blink detection. 
Default: False.

video_source(int/str, optional): This parameter takes either device index or a video file as input. Default: 0.

eyeTrackingLog(bool, optional): This parameter enables the user to generate a CSV of pupil tracking/ blink detection. Default: True.

eyeTrackingFileName(str, optional): This parameter takes the file name for the CSV. 
Default: ‘EyeTrackLog’.

videoRecorder(bool, optional): This parameter enables the user to record video. 
Default: False.

videoName(str, optional): This parameter enables the user to specify the filename with which
the recorded video is to be saved. Default: ‘video’.

audioRecorder(bool, optional): This parameter enables the user to record audio. 
Default: False.

audioName(str, optional): This parameter enables the user to specify the filename with which the recorded audio is to be saved. Default: ‘audio’.

syncAudioVideo(bool, optional): This parameter enables the user to synchronize audio and video together. This functionality requires a ffmpeg executable file in the working directory to complete the syncing process. Default: False.

destinationPath(str, optional): The parameter enables the user to specify the location of the output files. Default:  ‘/Output’.

### The Data Handling Class
The Data Handling class is responsible for handling the real-time pupil locations and blinks dynamically. This class implements a queue that the user has access to get the eye location or the blink details dynamically. This functionality gives the user the freedom to use eye-tracking data in real-time as per their wish. The user can use the following functions to handle the data:

add_data(data): This function allows the user to add data to the dynamic queue.
get_data(): This function returns the data elements of the queue.
is_empty(): This function checks if the queue is empty.
search_element(key): This function is used to search if a specified key

To make this clear, a basic example that makes use of the library to track the eyes of the user reading a text UI is described below.
`pytrack_runner(UI = True,`<br> 
`UI_file_name = “Ex_1_SampleTextUI”,`<br>
`pupilTracking = True,`<br>
`eyeTrackingLog = True,`<br> 
`eyeTrackingFileName = ‘User_1’)`

This example uses the pupil tracking functionality of the library. This example tracks the eyes of the user as the user reads the text displayed on the screen. The text UI is specified by the user. The user can set the destination path. In this case, as the destination path is not specified, the pupil coordinates CSV will be stored in the default 'Output' folder.

For more examples refer to our [Github repository](link).

Library requirements: 
The library needs dlib’s shape_predictor_68_face_landmarks.dat file to be located in the EyeTracking folder. The library also needs FFmpeg executable file in the working directory for the audio-video syncing to work.

UI requirements:
The library can run any UI developed in python. The user needs to ensure that the UI has the main function. The library takes the name of the UI as input and runs the main function in it.






