#This project is based on two dedicated self-trained models. For model-related information, please refer to the face_emotion and speech_emotion folders.
#Project Introduction
	To run this project, two devices are required, one for deploying the API server and one for running the test program to verify that the API is available.

#Copy the following files to the working directory:
	expert_judgment_system.py - expert judgment system

	health_api_server.py - API server

	improved_model.onnx - voice emotion recognition model

	face_emotion_model.onnx - facial emotion recognition model

	test_integration.py -api call test code

#Dependency installation:
	pip install numpy librosa onnxruntime opencv-python flask werkzeug requests

#Configuration:
	Modify the health_api_server.py file before running (make sure the model path is correct)
	voice_model_path="/home/pi/emotion_analysis/improved_model.onnx"
	face_model_path="/home/pi/emotion_analysis/face_emotion_model.onnx"

#Usage:
	clone files: git lfs clone https://github.com/Evan2001ok/health_system_api.git
 
	Run health_api_server.py on the first device
 
	Run test_integration.py on the second device
 
	Run the command on the second device
 
	python test_integration.py --api_url http://localhost:5000/api --voice /path/to/test/audio.wav --face /path/to/test/image.jpg


 #Judgment system's core logic:

#Standardization: 
	Converts different emotion formats (like "female_angry" or "Angry") to standard categories (like "angry").

#Emotion fusion:

	If only one source available (voice or face), use that emotion
	If both match, use that shared emotion
	If conflicting, prioritize negative emotions (angry > fearful > sad > disgusted > surprised > neutral > calm > happy)


#Response generation: 
	Provides appropriate comfort messages and practical suggestions based on the final emotional assessment.

#Efficiency features: 
	Uses a 60-second cache to avoid reprocessing identical inputs and allows adjustable weighting between voice and face inputs.


