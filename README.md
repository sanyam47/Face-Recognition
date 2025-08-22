cam = webcam;
faceDetector = vision.CascadeObjectDetector();
videoPlayer = vision.VideoPlayer('Position', [100, 100, 640, 480]);

while true
    frame = snapshot(cam);
    bbox = step(faceDetector, frame);
    annotatedFrame = insertObjectAnnotation(frame, 'rectangle', bbox, 'Face');
    step(videoPlayer, annotatedFrame);
    
    if ~isOpen(videoPlayer)
        break;
    end
end

clear cam;
release(videoPlayer);
