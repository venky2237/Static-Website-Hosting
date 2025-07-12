# 🌍 Static Website Hosting with Amazon S3 and CloudFront

Hello! 👋  
In this project, I have successfully hosted a static website using *Amazon S3* and *CloudFront*. This setup helps in loading the website faster and makes it available worldwide. Below are the steps I followed to complete this project.

---

## 🧾 Project Overview

- Hosted a static website on *S3 bucket*
- Connected it with *CloudFront* for global delivery
- Enabled *OAC (Origin Access Control)* for security
- Configured *HTTPS, **index.html, and **style.css*

---

## 🛠 Step-by-Step Process

### ✅ 1. Created an S3 Bucket

- *Bucket Name*: confg-static-website-15-06
- Region: ap-south-1 (Mumbai)
- Disabled "Block all public access" (for initial testing, later secured using OAC)
- Enabled *Static Website Hosting*
  - *Index document*: index.html
  - *style document*: style.css
- Uploaded:
  - index.html 
  - style.css

---

### ✅ 2. Created CloudFront Distribution

- Opened *CloudFront* > Created *Web Distribution*
- *Origin domain*: Selected confg-static-website-14-06.s3.ap-south-1.amazonaws.com (REST endpoint)
- *Created new Origin Access Control (OAC)*:
  - Name: S3-OAC-Static-Site
  - Signing Behavior: *Sign requests (recommended)*
  - Origin Type: S3
- Set *Default root object*: index.html
- Viewer protocol policy: *Redirect HTTP to HTTPS*
- Cache policy: CachingOptimized

---

### ✅ 3. Updated Bucket Policy for OAC Access

After the CloudFront distribution was created, I updated my S3 bucket policy to allow CloudFront to access it securely.

#### 🔐 S3 Bucket Policy Used:

json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowCloudFrontServicePrincipalReadOnly",
      "Effect": "Allow",
      "Principal": {
        "Service": "cloudfront.amazonaws.com"
      },
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::confg-static-website-15-06/*",
      "Condition": {
        "StringEquals": {
          "AWS:SourceArn": "arn:aws:cloudfront::<YOUR-AWS-ACCOUNT-ID>:distribution/<YOUR-DISTRIBUTION-ID>"
        }
      }
    }
  ]
}


📝 Replace <YOUR-AWS-ACCOUNT-ID> and <YOUR-DISTRIBUTION-ID> with your actual values.

---

### ✅ 4. Accessing My Website

- Once the status was *Deployed, I copied the **CloudFront Domain Name*:
  
  https://dxxxxxxxxxxx.cloudfront.net
  
- Pasted it in the browser, and my index.html page loaded perfectly!

---

## 📄 My WEBSITE Files

### 🔹 index.html,style.css
## 🧰 Tools & Services Used

- *Amazon S3*
- *CloudFront*
- *Origin Access Control (OAC)*
- *IAM Policy*
- *HTML/CSS*
- *AWS Console UI* (no CLI used)

---

## ✍ Created By

This project is created and configured by *me – venky chukkala*, as part of my AWS learning journey.  
