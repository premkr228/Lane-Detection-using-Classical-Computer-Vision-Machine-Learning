# Lane Detection using Classical Computer Vision and Machine Learning

1. Objective of the Project

The objective of this project is to design and implement a lane detection system for road images using only classical computer vision techniques and lightweight machine learning ideas. The focus is strictly on detecting straight lane lines without relying on deep learning models. The system is built and evaluated using a publicly available Kaggle dataset, ensuring reproducibility and fairness. Emphasis is placed on interpretability, computational efficiency, and robustness under common road conditions.

2. Dataset Configuration and Setup

The dataset is sourced directly from Kaggle using the Kaggle API. Proper configuration of the Kaggle environment ensures seamless dataset download and extraction within the notebook. Only valid road scene images are used for testing, and non-road images such as logos are explicitly excluded. This careful selection avoids biased evaluation and ensures that the results reflect realistic driving scenarios.

3. Test Case Selection Strategy

Five representative road images are selected from the dataset to evaluate the lane detection pipeline. These images include variations in perspective, road width, and lighting. Limiting the number of test cases allows for clear qualitative visualization while still demonstrating the consistency and reliability of the approach across different inputs.

4. Overview of the Lane Detection Pipeline

The lane detection system follows a structured, step-by-step pipeline. Each stage contributes to progressively refining the image and isolating lane boundaries. The pipeline consists of grayscale conversion, noise reduction, edge detection, region-of-interest masking, line detection using the Hough Transform, and final lane estimation through statistical averaging.

5. Image Preprocessing

The input RGB image is first converted to grayscale to simplify computation and focus on intensity changes rather than color information. A Gaussian blur is then applied to suppress high-frequency noise, which helps improve edge continuity. This preprocessing step is critical for stabilizing subsequent edge detection results.

6. Edge Detection using Canny Operator

Canny edge detection is used to identify strong intensity gradients corresponding to lane markings. Carefully chosen threshold values strike a balance between sensitivity and noise suppression. This step transforms the image into a sparse representation where lane boundaries appear as prominent edges.

7. Region of Interest (ROI) Masking

A trapezoidal region of interest is applied to restrict computation to the area of the image where lanes are most likely to appear. This reduces false detections from irrelevant regions such as the sky, roadside objects, or buildings. ROI masking significantly improves both accuracy and efficiency.

8. Line Detection using Probabilistic Hough Transform

The Probabilistic Hough Transform is used to detect line segments from the edge image. Unlike the standard Hough Transform, this approach samples edge points randomly, making it faster while still detecting dominant straight lines. Detected line segments are returned as sets of endpoints.

9. Slope-Based Lane Classification

Each detected line segment is characterized by its slope and intercept. These parameters are used to classify segments into left or right lanes. Negative slopes correspond to left lanes, while positive slopes correspond to right lanes. Thresholding on slope magnitude filters out nearly horizontal or irrelevant line segments.

10. Machine Learning Interpretation

Although no complex learning model is used, the slope–intercept averaging step can be viewed as a simple statistical learning process. Each detected line segment acts as a noisy sample, and averaging their parameters estimates the most likely lane boundary. This approach reduces the influence of outliers and stabilizes the final lane prediction, satisfying the machine learning requirement of the assignment in an interpretable way.

11. Final Lane Estimation and Visualization

For each lane group, the average slope and intercept are used to compute a single representative line. These lines are projected back onto the original image and drawn in distinct colors for left and right lanes. The result is a clean and stable visualization of lane boundaries that closely matches human perception.

12. Experimental Results

Across all five test images, the pipeline consistently detects lane lines that align well with visible road markings. The separation of left and right lanes is reliable, and the averaged lane projections remain stable even when individual detected segments vary. Minor changes in perspective and lane width are handled effectively.

13. Mathematical Insight into the Hough Transform

The Hough Transform reformulates line detection as a voting problem in parameter space. Each edge pixel votes for all possible lines that could pass through it. Peaks in the accumulator space correspond to dominant straight lines in the image. The probabilistic variant improves efficiency while preserving accuracy, making it suitable for real-time or resource-limited applications.

14. Performance Analysis

The system performs well on straight road segments under typical lighting conditions. The use of ROI masking and slope-based filtering significantly reduces false positives. The pipeline is fast, interpretable, and easy to debug, which are key advantages over black-box models in safety-critical applications.

15. Observed Limitations

The approach assumes straight lane geometry and therefore struggles with curved roads. Performance may degrade under heavy shadows, worn lane markings, or occlusions caused by vehicles. Since no temporal information is used, the system does not enforce consistency across consecutive frames.

16. Conclusion

This project demonstrates that classical computer vision techniques, when carefully combined with simple statistical learning ideas, can effectively solve structured problems such as straight lane detection. While limited in scope compared to deep learning approaches, the method is computationally efficient, transparent, and well-suited for controlled driving environments. It serves as a strong baseline and a valuable educational exercise in traditional vision pipelines.
