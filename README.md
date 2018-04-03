# Camera_Calibration
This repository contains a simple program for camera calibration based on OpenCv-python.(similar with the one in Opencv Tutorial)
3D points are called object points and 2D image points are called image points.
### Dependencies
- OpenCV-python
- Numpy
- glob
(Please make sure you have installed all this packages)

### Get images

```bash
images = glob.glob('PATH\TO\IMAGES\*.jpg')
```
### Get the chessboardorners (Get the obeject points )
```bash
objp = np.zeros((6*7,3), np.float32)
objp[:,:2] = np.mgrid[0:7,0:6].T.reshape(-1,2)
```

### Get the chessboardorners (Get the image points )
We can find the points in chessboard using cv2.drawChessboardCorners() which are the image points.
```bash
ret, corners = cv2.findChessboardCorners(gray, (7,6),None)
```

### Calibrate the camera
So now we have our object points and image points we are ready to go for calibration. For that we use the function, cv2.calibrateCamera(). It returns the camera matrix, distortion coefficients, rotation and translation vectors etc.
```bash
ret, mtx, dist, rvecs, tvecs = cv2.calibrateCamera(objpoints, imgpoints, gray.shape[::-1],None,None)
```
### Undistortion
Now we can take an image and undistort it.
```bash
dst = cv2.undistort(img, mtx, dist, None, newcameramtx)
# crop the image
x,y,w,h = roi
dst = dst[y:y+h, x:x+w]
#output the picture after undistortion.
cv2.imwrite('PATH/TO/OUTPUT',dst)
```
