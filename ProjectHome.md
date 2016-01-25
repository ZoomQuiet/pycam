Includes filtering, face tracking, object detection and feature detection examples that all run on a live webcam stream. Parts use OpenCV, SciPy and Pygame.

In **trunk/pycam** is a project exploring the new pygame Camera module with opencv. It includes a wrapper class that allows the opencv backend to be used with pygame - this is no longer required as pygame will automatically detect opencv (on linux)
The project contains a video player class that can work with different backend setups, and can incorporate an optional process function. I have had it running on windows - look under http://code.google.com/p/pycam/source/browse/#svn/branches/windows-branch/pycam and cross ones fingers....


In the **speed** directory is a look at the differences in coding style and performance between C++ and Python.
## A few Screen shots ##
```
def locateFaceAndEyeProcess(surf):
    faces = getFaces(surf)
    
    s = eyeDetector.image_scale 
    
    if faces:
        for face in faces:
            r = pygame.Rect(face.x*s,face.y*s,face.width*s,face.height*s)
            pygame.draw.rect(surf,Color("green"),r,1)
            facialSurf = surf.subsurface(r)
            facialCvMat = surf2CV(facialSurf)
            eyeDetector.detect_and_draw(facialCvMat)
            pygame.surfarray.blit_array(facialSurf,cv2SurfArray(facialCvMat))
    return surf

if __name__ == "__main__":
    eyeDetector = ObjectDetector("eye")
    vcp = VideoCapturePlayer(processFunction=locateFaceAndEyeProcess)
    vcp.main()
    pygame.quit()
```
![http://1.bp.blogspot.com/_lewp47C9PZI/Sfp83AQgkDI/AAAAAAAAAXQ/1Z-iAKx0Kxo/s400/eye-locate.png](http://1.bp.blogspot.com/_lewp47C9PZI/Sfp83AQgkDI/AAAAAAAAAXQ/1Z-iAKx0Kxo/s400/eye-locate.png)


![http://docs.google.com/File?id=dfp426p7_156cwvsqzc7_b&anythin.png](http://docs.google.com/File?id=dfp426p7_156cwvsqzc7_b&anythin.png)


For example edge detection:
![http://docs.google.com/File?id=dfp426p7_152cknrsrd5_b&whatever.png](http://docs.google.com/File?id=dfp426p7_152cknrsrd5_b&whatever.png)
The 0 frames per second was on my ppc laptop after just turning on the program - it is not quite that slow on a desktop PC!

