# Live Finger Counter 🖐️

A real-time computer vision application that uses your webcam to detect and count the number of fingers you're holding up. Built with OpenCV and MediaPipe for accurate hand tracking and finger counting.

![Python](https://img.shields.io/badge/python-3.7+-blue.svg)
![OpenCV](https://img.shields.io/badge/opencv-4.0+-green.svg)
![MediaPipe](https://img.shields.io/badge/mediapipe-latest-orange.svg)

## Features

- **Real-time Detection**: Counts fingers in real-time using your webcam
- **Hand Landmark Detection**: Uses MediaPipe's robust hand tracking model
- **Visual Feedback**: Displays hand landmarks and finger count on screen
- **Multi-finger Support**: Accurately counts 0-5 fingers
- **Lightweight**: Minimal dependencies and efficient processing

## Requirements

- Python 3.7 or higher
- Webcam/Camera

### Dependencies

```bash
opencv-python
mediapipe
```

## Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/johaankjis/live-finger-counter.git
   cd live-finger-counter
   ```

2. **Install required packages**
   ```bash
   pip install opencv-python mediapipe
   ```

   Or create a `requirements.txt` file:
   ```txt
   opencv-python>=4.0
   mediapipe>=0.8
   ```
   
   Then install:
   ```bash
   pip install -r requirements.txt
   ```

## Usage

1. **Run the application**
   ```bash
   python live.py
   ```

2. **Position your hand** in front of the webcam

3. **Hold up fingers** - the program will count and display the number on screen

4. **Exit** - Press any key to close the application window

## How It Works

The application uses a combination of computer vision techniques:

1. **Video Capture**: OpenCV captures live video feed from your webcam
2. **Hand Detection**: MediaPipe's Hands solution detects hand landmarks (21 points per hand)
3. **Landmark Processing**: The program analyzes the positions of specific landmarks to determine finger states
4. **Finger Counting Logic**:
   - **For fingers (index, middle, ring, pinky)**: Compares the tip landmark with the joint below it
     - If tip's Y-coordinate is less than the joint's Y-coordinate, finger is up
   - **For thumb**: Compares the tip's X-coordinate with a reference point
     - If tip's X-coordinate is greater than reference, thumb is up
5. **Visual Output**: Draws landmarks on the hand and displays the count

### Landmark Coordinates Used

- **Fingers**: 
  - Index: (8, 6)
  - Middle: (12, 10)
  - Ring: (16, 14)
  - Pinky: (20, 18)
- **Thumb**: (4, 2)

## Project Structure

```
live-finger-counter/
│
├── live.py          # Main application script
└── README.md        # Project documentation
```

## Technical Details

### Main Components

- **cv2.VideoCapture(0)**: Accesses the default webcam
- **mp.solutions.hands**: MediaPipe's hand tracking solution
- **Hand Landmarks**: 21 landmarks per hand detected by MediaPipe
- **Drawing Utilities**: Visualizes hand landmarks and connections

### Algorithm

```python
# Finger detection coordinates (tip, joint)
finger_Coord = [(8, 6), (12, 10), (16, 14), (20, 18)]
thumb_Coord = (4, 2)

# Count fingers where tip is above joint
for coordinate in finger_Coord:
    if handList[coordinate[0]][1] < handList[coordinate[1]][1]:
        upCount += 1

# Check thumb position
if handList[thumb_Coord[0]][0] > handList[thumb_Coord[1]][0]:
    upCount += 1
```

## Known Limitations

- Works best with good lighting conditions
- May require calibration for left-handed users (thumb detection logic)
- Single hand detection optimized for right hand
- Camera must remain relatively stable for accurate detection

## Future Improvements

- [ ] Add support for both hands simultaneously
- [ ] Improve thumb detection for left hands
- [ ] Add gesture recognition
- [ ] Include configuration options for camera selection
- [ ] Add recording/screenshot functionality
- [ ] Implement custom hand gestures
- [ ] Add GUI for settings adjustment
- [ ] Support for different lighting conditions

## Troubleshooting

**Camera not opening?**
- Ensure no other application is using the webcam
- Try changing the camera index in `cv2.VideoCapture(0)` to `1` or `2`

**Poor detection accuracy?**
- Ensure good lighting conditions
- Keep hand within camera frame
- Maintain appropriate distance from camera (30-60 cm recommended)

**Dependencies not installing?**
- Ensure pip is up to date: `pip install --upgrade pip`
- Use Python 3.7 or higher

## Contributing

Contributions are welcome! Feel free to:
- Report bugs
- Suggest new features
- Submit pull requests

## License

This project is open source and available under the MIT License.

## Credits

- **OpenCV**: Computer vision library for video capture and image processing
- **MediaPipe**: Google's framework for hand landmark detection
- **Developer**: johaankjis

## Acknowledgments

Built using:
- [OpenCV](https://opencv.org/) - Open Source Computer Vision Library
- [MediaPipe](https://google.github.io/mediapipe/) - Cross-platform ML solutions

---

**Enjoy counting fingers! 🖐️✌️👆**
