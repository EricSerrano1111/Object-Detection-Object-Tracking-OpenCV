\[cite:# Object Detection & Object Tracking with OpenCV in Python 

## Description
This project implements vision techniques for facial detection but also for both detecting and tracking humans with video data.  3] An image preprocessing pipeline is developed to process images for testing. A Deep Neural Network (ResNet-10 via Caffe) is then utilized to test for facial detection using three test static images. A Haar Cascade Full Body Classifier is then utilized to demonstrate object detection and tracking. A video pipeline processes the video feed, applies bounding boxes to detect pedestrians walking in an intersection, and updates a live Heads-Up Display (HUD) counter. This video is compiled and exported for viewing once the pipeline completes its execution. As an experiment, the facial detection Deep Neural Network is tested against the same video using the same pipeline process. To summarize, the Deep Neural Network is a clear domain mismatch for the pedestrian detection task as the Haar Cascade Full Body Classifier vastly outperforms. In other words, this demonstrates the importance of aligning model architecture with environmental data constraints when considering real world applications.

## Getting Started

### Dependencies:
* Python 3.10.13
* OpenCV 4.13.0
* Matplotlib
* Current Web Browser
* Jupyter Notebook

### Installing
* **Anaconda:** https://www.anaconda.com/download (Python, Scikit-Learn & Jupyter Notebook)
* **Pandas:** https://pandas.pydata.org/pandas-docs/stable/getting_started/install.html
* **OpenCV:** Run `pip install opencv-python` in your terminal or Anaconda Prompt to ensure the computer vision libraries and pre-trained cascades are available locally.
* **Deep Neural Network (DNN) Models:** To utilize the ResNet-10 facial detection model, you must download the pre-trained architecture (`deploy.prototxt`) and weights (`res10_300x300_ssd_iter_140000.caffemodel`). If automated script downloads fail due to server protections, navigate to the official OpenCV GitHub repository in your web browser, download these two files manually, and place them directly into your project's `notebook/` directory. 

## Executing Program
1. Structure directory by creating a central notebook folder to hold the .ipynb file and downloads or model outputs.
2. A central data folder is then to be created to hold static test images along with the validation video.
3. Launch Anaconda, change your file directory if needed to the newly structured project directory by execting `cd` (followed by the directory).
4. Then launch Jupyter Notebook by executing the command `jupyter notebook`.
5. Run the cell in the sequence they are set up from top to bottom.
6. Once the video pipeline cells are executed, check the project directory to open the notebook folder and view the processed frame by frame video outputs.

### Program Setup Reference
The following table:

| Directory Structure | File Folders | Description |
| :--- | :--- | :--- |
| CoreProjectFolder/ | `notebook/` | .ipynb file, DNN models, and, or model outputs. |
| | `data/` | Static test images and validation video. |

## Expected Results
The Deep Neural Network (ResNet-10 via Caffe) will show the confidence scores of the facial detection results below based on the parameters set. 

![Soccer Team](/images/img1.png)

The two images below were acquired from a free online image resource platform. Unlike the soccer team image their file type was different but more importantly their image resolution quality was 8K.

![Family Photo](/images/img2.png)

This image was chosen as an edge case as the one individual is looking away completely but the toy figures in the center of the photo have human features. The model successfully captured the only forward-looking face.

![Music Booth](/images/img3.png)

The facial detection model failed spectacularly to successfully detect the faces in the test video. The neural network created many false positives and only captured a single face despite experimenting with the parameters.

![Family Photo](/images/img5.png)

The Haar Cascade Full Body Classifier on the other hand performed well at both detecting human objects and tracking them across a majority of the video.

![Pedestrians](/images/img4.png)

## Help / Issue Log
* **Issue 1:** Bounding boxes and HUD text were drawn multiple times per frame, creating a glitchy output video.
  * **Resolution:** Corrected the indentation of `cv2.putText` and `out.write(frame)` to ensure they execute at the frame level, rather than inside the `for` loop iteration for every detected body. 

* **Issue 2:** `(-215:Assertion failed) !empty() in function 'detectMultiScale'` which likely indicates the `haarcascade_fullbody.xml` file is missing or the path is incorrect.
  * **Resolution:** Utilized `os.path.join(cv2.data.haarcascades, 'haarcascade_fullbody.xml')` to securely fetch the file from OpenCV's offline installation directory rather than relying on an external GitHub HTTP request.

* **Issue 3:** High-resolution 8K test images resulted in invisible bounding boxes.
  * **Resolution:** Implemented a resolution-normalization pipeline using `cv2.resize` with `cv2.INTER_AREA` interpolation to downscale inputs to a maximum width of 1200px prior to inference, preventing Matplotlib rendering compression.

* **Issue 4:** Automated DNN download scripts fail with `RemoteDisconnected` or similar connection errors. 
  * **Resolution:** GitHub's aggressive anti-bot protections often block basic Python `urllib` requests. To bypass this, manually download the required `.caffemodel` and `.prototxt` files directly through your web browser and place them in the core project folder's notebook directory.

## TODO
* Implement a Deep Learning Object Detection model (e.g., MobileNet-SSD or YOLOv8) to compare accuracy and occlusion-handling capabilities against the legacy Haar Cascade.
* Refactor the frame-processing while loop into a modular Python function to easily ingest dynamic video paths.

## Authors
* Lead Developer – Eric Serrano

## Version History
* 0.1 – Initial Release 

## License
The MIT License (MIT)
Copyright (c) 2026 Eric Serrano

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.