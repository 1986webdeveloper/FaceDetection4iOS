# FaceDetection4iOS

FaceDetection

it is easy to implement face detection in your app. In iOS11, Apple introduces the Vision Framework, it's much easier to detect human faces in real time.
Apple added detection of all landmarks within the face.
Features 

	⁃	Detect all parts of Face
	⁃	like  nose, Lips, Eye, Eyebrow, faceContour

Requirements

Swift 4.0
IOS 10.0+
Xcode 9.x


Usage

1)	import this two framework in your viewcontroller
	
	  import AVFoundation
	import Vision

2)	Make sure that your view controller conforms to the AVCaptureVideoDataOutputSampleBufferDelegate  protocol

class YourViewController: UIViewController, AVCaptureVideoDataOutputSampleBufferDelegate {
}

3)	Implement of delegate function

// this delegate function use for detect face
func captureOutput(_ output: AVCaptureOutput, didOutput sampleBuffer: CMSampleBuffer, from connection: AVCaptureConnection) {
let pixelBuffer = CMSampleBufferGetImageBuffer(sampleBuffer)
        
        let attachments = CMCopyDictionaryOfAttachments(kCFAllocatorDefault, sampleBuffer, kCMAttachmentMode_ShouldPropagate)
        let ciImage = CIImage(cvImageBuffer: pixelBuffer!, options: attachments as! [String : Any]?)
        
        //leftMirrored for front camera
        let ciImageWithOrientation = ciImage.oriented(forExifOrientation: Int32(UIImageOrientation.leftMirrored.rawValue))
        
        detectFace(on: ciImageWithOrientation)
}
