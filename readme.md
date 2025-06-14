# 🌐 Static Website Hosting using Amazon S3 and CloudFront

## 📌 Project Overview

This project demonstrates how to host a static website using **Amazon S3** and improve its global performance using **Amazon CloudFront (CDN)**.  
The goal is to deliver website content efficiently, securely, and at scale.

---

## 🎯 Objectives

- Host a static website on **Amazon S3**
- Use **Amazon CloudFront** for fast content delivery
- Secure S3 bucket by allowing access only via CloudFront

---

## 🧰 Technologies Used

- Amazon S3 (Simple Storage Service)
- Amazon CloudFront (Content Delivery Network)
- IAM Policies for security
- AWS Management Console

---

## 📂 Project Folder Structure

/website
├── index.html
├── error.html
├── css/
├── js/
└── images/

pgsql
Copy
Edit

---

## 🚀 Step-by-Step Implementation

### 🔸 Step 1: Create and Configure S3 Bucket
- Go to S3 in AWS Console
- Create a bucket (with unique name) in `us-west-2` region
- Disable "Block all public access"
- Enable **Static Website Hosting**
  - Index document: `index.html`
  - Error document: `error.html`

### 🔸 Step 2: Upload Website Files
- Upload all files inside the `/website` folder
- Ensure `index.html` is at root level (not inside a subfolder)

### 🔸 Step 3: Set Bucket Policy (Temporarily Public)

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AddPerm",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::YOUR_BUCKET_NAME/*"
    }
  ]
}
Replace YOUR_BUCKET_NAME with your actual bucket name

Save the policy

🔸 Step 4: Test Website via S3
Go to Properties → Static website hosting

Copy the endpoint and open in browser

🔸 Step 5: Create CloudFront Distribution
Go to CloudFront → Create Distribution

Origin domain: use S3 website endpoint

Create Origin Access Control (OAC)

Set default root object: index.html

Leave WAF and cache settings as default

Click Create distribution

🔸 Step 6: Secure the Bucket
Replace the bucket policy with the new one provided by CloudFront

Block all public access in S3 permissions

Confirm changes

🔸 Step 7: Test Website via CloudFront
Wait until distribution status is Deployed

Copy the CloudFront domain name

Open in browser — your website will load from CloudFront

✅ Final Output
Website is hosted in S3

Content is delivered globally using CloudFront

S3 bucket is secured (not publicly accessible)

Website is scalable, fast, and reliable