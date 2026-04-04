---
title: "5.5 Frontend with S3 & CloudFront"
weight: 5
---

## Frontend Hosting with S3 & CloudFront

This section covers how to build and deploy the React frontend from the `frontend/` folder
using Amazon S3 and Amazon CloudFront.

### Frontend architecture diagrams

![S3 bucket for hosting IMS frontend static website](/images/5-Workshop/5.5-frontend-s3-cloudfront/s3.png)

![CloudFront distribution in front of S3 origin](/images/5-Workshop/5.5-frontend-s3-cloudfront/CloudFront.png)
![CloudFront behavior and cache settings](/images/5-Workshop/5.5-frontend-s3-cloudfront/CloudFront1.png)
![CloudFront distribution details and domain name](/images/5-Workshop/5.5-frontend-s3-cloudfront/CloudFront2.png)

These diagrams illustrate how users access the React app via CloudFront, which serves content from the S3 bucket.

### Frontend Capabilities

The React app provides UI flows for:
- User login and role-based navigation (Admin / Manager / Line Leader).
- Managing production orders and viewing order details.
- Viewing production plans, line schedules, and basic dashboards.
- Accessing AI insights pages (via `aiService`) for production summaries and analysis.

### Building the Frontend

1. Install dependencies locally:
   - `npm install`
2. Configure API base URL (e.g., using environment variables like `VITE_API_BASE_URL`).
3. Build the production bundle:
   - `npm run build`
4. Verify that a `dist/` directory (or similar) is produced with static files.

### Hosting on Amazon S3

1. Create an S3 bucket dedicated to hosting the frontend (e.g., `ims-frontend-prod`).
2. Enable static website hosting (or use CloudFront origin access control for private buckets).
3. Upload the contents of the `dist/` folder to the S3 bucket.
4. Configure the index document (e.g., `index.html`) and error document for SPA routing.

### Distributing via CloudFront

1. Create a **CloudFront distribution** with the S3 bucket as origin.
2. Set the default root object to `index.html`.
3. Configure caching and optional custom error responses for SPA (serving `index.html` on 404).
4. Associate an **ACM certificate** and custom domain (via Route 53) if using HTTPS.

### API Integration & CORS

- Ensure the frontend calls the backend API via the correct base URL (ALB DNS or custom domain).
- Configure CORS on the backend (and/or ALB) so that the CloudFront domain is allowed.
- For production, avoid hard-coding URLs; use environment variables during build.

By the end of this section, the React frontend will be accessible via a CloudFront URL or your custom domain,
serving as the main entrypoint to the IMS system.
