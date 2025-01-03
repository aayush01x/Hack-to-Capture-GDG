# 
scanning the qr code gives message to see closer
Used this python program to extract the messages in the smaller qr codes  
```
import cv2
import numpy as np

 # Constants
SCALE = 300

def scan(img):
    """Scans a single image region for QR codes."""
    # XOR operation to modify the image
    scalar_value = ~int(img[0, 0]) & 0xFF  # Ensure the scalar is in 8-bit range
    img = cv2.bitwise_xor(img, scalar_value)
    # Resize for better QR detection
    img = cv2.resize(img, (SCALE * 5, SCALE * 5), interpolation=cv2.INTER_AREA)
    # Initialize QRCodeDetector
    qr_detector = cv2.QRCodeDetector()
    # Decode QR code
    data, _, _ = qr_detector.detectAndDecode(img)
    return data.encode('utf-8') if data else b''

def main():
    # Read the input image in grayscale
    img = cv2.imread('qrcode.png', cv2.IMREAD_GRAYSCALE)
    if img is None:
        print("Error: Could not load the image 'qrcode.png'.")
        return

    # Get image dimensions
    h, w = img.shape

    # Process the image in blocks and scan for QR codes
    msg = b''.join(
        scan(img[y:y + SCALE, x:x + SCALE])
        for y in range(0, h, SCALE)
        for x in range(0, w, SCALE)
    )

    # Output the decoded message
    print("Decoded message:", msg.decode('utf-8'))

if __name__ == "__main__":
    main()
```   
Got message   
```
Decoded message: CTFlearn is a dream. Is Cobb still dreaming? I hope you scripted the retrieval of this message because "we need to go deeper"... iVBORw0KGgoAAAANSUhEUgAAACUAAAAlAQAAAADt5R2uAAAAsUlEQVR4nGP4DwQ/GDDJD9IGDhUM369x3q9g+BJgdBFIRvQEAsnwKUD290uzgOIfREOBav5/jgSq/3T2sQtQb865mgqGn46fGn4wfLE/eqaC4VN/1jkgmVFdBdR7sripguGPMrfeD4ZvUhO1fjD8+P73JlAl58YDQPEfGxf/YPjuFcQINPOLSRHQDULCQUCRG6olQL0xh9lBLpkXAVQfM6sU6IYrr78B1Yga2mFzP5gEAB2SgeETXS+JAAAAAElFTkSuQmCC
```  
Decoded it in a online base64 to qr reader  
Got the new qr code  
Scanned it   
Flag: CTFlearn{Y0u_4re_in_QR-cOd3_l1mb0}
