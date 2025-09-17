# Docker Google Cloud Run Gradio Demo

This repository demonstrates how to deploy a simple Gradio application using Docker containers on Google Cloud Run. The implementation follows the official Google Cloud documentation for deploying Python Gradio services.

## 📚 Reference

This project is based on the tutorial from:
https://cloud.google.com/run/docs/quickstarts/build-and-deploy/deploy-python-gradio-service#gcloud

## 🎯 Purpose

The main goal of this repository is to demonstrate:

- Container deployment using Google Cloud Run
- Gradio application development and deployment
- Integration between Docker, Google Cloud Platform, and Gradio

## 📁 Project Structure

```
.
├── app.py              # Main Gradio application
├── requirements.txt    # Python dependencies
└── README.md          # Project documentation
```

## 🚀 Application Overview

The application is a simple Gradio interface that:

- Echo user input like streaming chatbots

## 🛠️ Local Development

### Prerequisites

- Python 3.11+
- pip

### Installation & Setup

1. **Clone the repository**:

   ```bash
   git clone <repository-url>
   cd Docker_Gcloud_Gradio
   ```

2. **Install dependencies**:

   ```bash
   pip install -r requirements.txt
   ```

3. **Run the application locally**:

   ```bash
   python app.py
   ```

4. **Access the application**:
   Open your browser and navigate to the URL displayed in the terminal (typically `http://127.0.0.1:7860`)

## 🐳 Docker Deployment

### Local Docker Testing

1. **Build the Docker image**:

   ```bash
   docker build -t gradio-app .
   ```

2. **Run the container**:
   ```bash
   docker run -p 8080:8080 gradio-app
   ```

## ☁️ Google Cloud Run Deployment

### Prerequisites

- Google Cloud account
- Google Cloud CLI installed and configured
- Docker installed

### Deployment Steps

1. **Set up Google Cloud project**:

   ```bash
   gcloud config set project YOUR_PROJECT_ID
   ```

2. **Enable Cloud Run API**:

   ```bash
   gcloud services enable run.googleapis.com
   ```

3. **Enable Cloud Build API**:

   ```bash
   gcloud services enable cloudbuild.googleapis.com
   ```

4. **Deploy to Cloud Run**:

   ```bash
   gcloud run deploy gradio-service --allow-unauthenticated --region=us-east1 --platform=managed --source .
   ```

5. **Access your deployed application**:
   After deployment, Google Cloud will provide a URL where your application is accessible.

### Configuration Options

- **Region**: You can change the deployment region based on your needs
- **Authentication**: Remove `--allow-unauthenticated` if you want to require authentication
- **Memory/CPU**: Configure resources based on your application requirements

## 🛠️ Managing Deployments

Assuming your service name is `gradio-service` and region is `us-east1`:

### Services

1. **Check active services**:

   ```bash
   gcloud run services list
   ```

2. **Get service details**:

   ```bash
   gcloud run services describe gradio-service --region=us-east1
   ```

3. **Delete the Cloud Run service**:

   ```bash
   gcloud run services delete gradio-service --region=us-east1
   ```

### Artifacts

1. **List all repositories in Artifact Registry**:

   ```bash
   gcloud artifacts repositories list
   ```

2. **List images in the cloud-run-source-deploy repository**:

   ```bash
   gcloud artifacts docker images list us-east1-docker.pkg.dev/YOUR_PROJECT_ID/cloud-run-source-deploy
   ```

3. **Get detailed information about a specific image**:

   ```bash
   gcloud artifacts docker images describe us-east1-docker.pkg.dev/YOUR_PROJECT_ID/cloud-run-source-deploy/gradio-service
   ```

4. **Delete specific image from Artifact Registry**:

   ```bash
   gcloud artifacts docker images delete us-east1-docker.pkg.dev/YOUR_PROJECT_ID/cloud-run-source-deploy/gradio-service --delete-tags
   ```

5. **Delete all images for the service**:

   ```bash
   gcloud artifacts docker images delete us-east1-docker.pkg.dev/YOUR_PROJECT_ID/cloud-run-source-deploy/gradio-service
   ```

6. **Delete entire Artifact Registry repository (use with extreme caution!)**:

   ```bash
   gcloud artifacts repositories delete cloud-run-source-deploy --location=us-east1
   ```

### Notes:

- Replace `YOUR_PROJECT_ID` with your actual Google Cloud project ID
- The repository name `cloud-run-source-deploy` is the default for Cloud Run source deployments
- **⚠️ WARNING**: Deleting an entire repository cannot be undone and will remove all images permanently
- Be careful with deletion commands as they cannot be undone
- The cleanup command removes images older than 30 days to save storage costs

## �📦 Dependencies

- **gradio==5.39.0**: Web UI framework for machine learning applications

## 🔧 Customization

To modify the application:

1. **Update the greeting function** in `app.py`
2. **Modify the Gradio interface** parameters (inputs, outputs, theme, etc.)
3. **Add new dependencies** to `requirements.txt`
4. **Redeploy** using the same Cloud Run command

## 📝 Notes

- The application uses Gradio's `flagging_mode="never"` to disable user feedback collection
- The soft theme provides a clean, professional appearance
- The slider allows intensity values that control the number of exclamation marks

## 🤝 Contributing

Feel free to fork this repository and submit pull requests for improvements or additional features.

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

**Happy Deploying! 🚀**
