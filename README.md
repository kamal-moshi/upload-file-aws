# AWS S3 File Upload API Documentation

## Overview

The AWS S3 File Upload API allows you to effortlessly upload files to an AWS S3 bucket with the added feature of optional WebP conversion for images. This API is designed to handle file submissions through a POST request, facilitating seamless uploads to a specified S3 bucket.

## Endpoint
###  base url POST : https://uploadfile.moshimoshi.cloud/api/v1/upload/:bucket/:key
```plaintext
Request
URL Parameters
:key (string): The key or path within the bucket for storing the file.
Headers
No specific headers are required for this request.

Body
The request body should adhere to the standard multipart/form-data format for sending files.

Response
Success Response (200 OK)
json
Copy code
{
  "urls": [
    "https://s3.amazonaws.com/bucket/key/filename1.webp",
    "https://s3.amazonaws.com/bucket/key/filename2.webp",
    ...
  ]
}
urls (array of strings): A list of URLs representing the locations of the uploaded file(s) on S3.
Error Response (500 Internal Server Error)
json

{
  "message": "Error message details..."
}
message (string): A detailed error message for better troubleshooting.
Example Usage (Frontend)
Using Fetch API

const uploadFile = async (file, bucket, key) => {
  const formData = new FormData();
  formData.append('file', file);

  try {
    const response = await fetch(`/api/v1/upload/${bucket}/${key}`, {
      method: 'POST',
      body: formData,
    });

    const data = await response.json();
    console.log('File uploaded successfully:', data.urls);
  } catch (error) {
    console.error('Error uploading file:', error.message);
  }
};

// Example usage
const fileInput = document.getElementById('fileInput'); // Assuming you have an input element with type="file"
fileInput.addEventListener('change', (event) => {
  const file = event.target.files[0];
  const bucket = 'your-s3-bucket-name';
  const key = 'your-s3-key-path';
  uploadFile(file, bucket, key);
});
Replace 'your-s3-bucket-name' and 'your-s3-key-path' with your actual S3 bucket name and key path.

This documentation assumes the presence of a form or UI element for users to select files. Adjust the frontend code according to your application's requirements.
