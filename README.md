# **Project Title**: Innovative Hackathon on Cyber Safety for Women: Unique Image ID for Tracking and Deletion
# 1. Introduction
**1.1 Problem Statement**
Cyber safety is a significant concern, especially for women, who are often the targets of cybercrimes like image-based abuse. When private images are leaked or shared without consent, the repercussions can be devastating. Traditional methods of tracking and deleting such images are inadequate, as images can be quickly disseminated across multiple platforms, making it challenging to identify and remove all copies

**1.2 Proposed Solution**
This project aims to develop an innovative solution that automatically generates a unique ID for every image shared online or on social media, embedding it into the image metadata for easy identification and tracking. By leveraging perceptual image hashing, the system accurately detects and identifies leaks, even if the image is altered or cropped. Each shared image's unique ID is stored in a database, enabling future detection and deletion of leaked images. Acting as an add-on for social platforms, this solution ensures that any leaked image can be efficiently detected and removed, safeguarding user privacy and content integrity.

# 2. Project details:

**1. Importing Libraries**
**hashlib**: Provides hashing functions to create unique identifiers.

**io**: For handling byte streams (e.g., image data).

**requests**: To download images from URLs.

**PIL**: Python Imaging Library for image processing. Includes Image for opening and manipulating images, UnidentifiedImageError for error handling, and PngImagePlugin for PNG metadata.

**imagehash**: To generate perceptual hashes for image comparison.

**piexif**: For handling EXIF metadata in JPEG images.

**cv2**: OpenCV library, though not used in the provided code snippet.

**numpy**: For numerical operations, especially useful for image manipulation.

**cryptography.hazmat.primitives**: Provides cryptographic functions, including HMAC for creating signatures.

# 2. Generating a Unique ID
**Purpose**: Create a unique ID using both the image content and user-specific information.

**Steps:**
Read the image file in binary mode.

Compute a SHA-256 hash of the image data.

Combine the user info with the image hash and compute another SHA-256 hash to generate the final unique ID.

# 3. Embedding the Unique ID in Metadata
**Purpose**: Add the unique ID to the image's metadata.

**Steps**:
Open the image.

For JPEG images, load the EXIF data, add the unique ID to the UserComment field, and save the image with the updated EXIF data.

For PNG images, use PngImagePlugin to add the unique ID as text metadata and save it.

Print a message confirming the save operation.

# 4. Embedding a Hidden Watermark
**Purpose**: Hide a watermark in the image using steganography.

**Steps**:

Open and convert the image to RGB format.

Convert the watermark text into a binary string.

Modify the least significant bit (LSB) of the pixel values to embed the watermark.

Flatten the image array, embed the binary watermark, then reshape and save the image.

# 5. Generating Image Hashes
**Purpose**: Generate perceptual hashes to compare image similarities.

**Steps**:
Compute both pHash (perceptual hash) and dHash (difference hash) of the image.
Handle any errors that occur during hashing.

# 6. Generating a Cryptographic Signature
**Purpose**: Create a secure cryptographic signature for the image using HMAC.

**Steps**:
Read the image data.
Use HMAC with SHA-256 to generate a signature.
Return the generated signature.

# 7. Comparing Image Hashes
**Purpose**: Compare perceptual and difference hashes to determine image similarity.

**Steps**:
Calculate the difference between hashes.
Compute similarity percentages.
Return True if both hash similarities are within the tolerance level.

# 8. Unique ID Comparison
**Purpose**:
Confirm image leakage by comparing unique IDs and hash values.

**Steps**:

Calculate the difference between the unique ID embedded in the original image and the ID in the suspected leaked image.

Use perceptual and difference hashing techniques to compare the images' content, ensuring that the unique ID is accurately detected despite possible alterations.

If both the unique IDs and hash values match, confirm the image as a leak.

Initiate a request for the deletion of the confirmed leaked image from the platforms where it was found.

# 9. Searching and Deleting Leaked Images
**Purpose**: Check images against a known reference image to detect leaks and potentially initiate deletion.

**Steps**:

Search for Metadata ID: Look for the embedded metadata ID within the image on the social platform.

Utilize Image Hash: Apply perceptual and difference hashes to locate similar images.

For Each Image URL:
Download the Image: Retrieve the image from the given URL.

Extract Metadata ID: Access and extract the embedded metadata ID from the image’s metadata.

Generate Hashes: Compute perceptual and difference hashes for the downloaded image.

Compare Metadata ID: Check if the extracted metadata ID matches the original unique ID stored in the database.

Compare Hashes: Calculate and compare hash similarities to determine if they fall within the tolerance level.

Print Messages: Output messages indicating whether a leak was detected, and whether the image was successfully deleted or not.

# Demo Workflow
**Objective**: Demonstrate the process of generating a unique ID for an image, embedding it with security features, and detecting potential leaks through comparison and automated deletion requests.

Steps:

# Upload Original Image:

**Image and User Information**: Begin by uploading the original image along with the user's security key and account information.
Generate Unique ID: Create a unique ID based on the image content and user details. This ID is generated using a combination of hashing and encryption techniques to ensure its uniqueness and security.
Embed Security Features:

**Metadata and Watermarks**: Embed the unique ID into the image’s metadata. Additionally, apply watermarks and a cryptographic signature to the image to further secure it against unauthorized use and modifications.

**Store the Image**: Upload the secured image to a hosting service, such as Postimg, with intentional alterations (e.g., slight changes in size or format) to simulate real-world scenarios.

# Leak Detection:

**Image Download**: Use the provided URL to download the image from the hosting service.

**Extract Metadata ID**: Access and extract the metadata ID from the downloaded image.

**Hash and Signature Verification:** Compute perceptual and difference hashes for the downloaded image and compare them with the original image. Verify the cryptographic signature to ensure it matches the security features embedded in the original image.

**Compare IDs**: Check if the extracted metadata ID from the downloaded image matches the original unique ID.

**Leak Detection and Action**: If the image is found to be leaked (based on metadata ID and hash comparisons), initiate a delete request to remove the image from the hosting service.

# Automated Deletion:

**Send Deletion Request:** Automatically send a request to the hosting platform to delete the leaked image, ensuring that unauthorized copies are promptly removed.
This workflow outlines a practical demonstration of how the unique ID, embedded security features, and automated tools work together to track, detect, and handle leaked images efficiently.


**project demo drive link** : https://drive.google.com/drive/folders/11kXW-XH55_G6rL7Ed18fH5nYCmMshiqR?usp=sharing

