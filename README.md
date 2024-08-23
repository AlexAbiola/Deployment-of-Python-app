

# Python App Deployment in AWS EC2

This guide covers the steps to deploy a Python application on an AWS EC2 instance.

## Prerequisites

- An AWS account with permissions to launch EC2 instances.
- A key pair for SSH access to the instance.
- A GitHub repository containing the Python app code.
- Basic knowledge of Linux commands.

## Step 1: Launch an EC2 Instance

1. **Login to AWS** and navigate to the EC2 dashboard.
2. Click **Launch Instance** and name the instance (e.g., `Python_Server`).
3. **Choose an Amazon Machine Image (AMI)**: Select the Ubuntu AMI.
4. **Select Instance Type**: Choose `t2.micro` (eligible for the free tier).
5. **Configure Security Group**: Use an existing security group or create a new one that allows SSH (port 22) and the required application port (e.g., port 8501 for Streamlit).
6. **Launch the instance** using your existing key pair.

## Step 2: Connect to the EC2 Instance

1. After the instance is running, connect to it using SSH:
   ```bash
   ssh -i "your-key.pem" ubuntu@your-ec2-public-ip
   ```
   Replace `your-key.pem` with your key pair file and `your-ec2-public-ip` with the instance's public IP address.

## Step 3: Update the Instance

1. Run the following commands to update the instance and install required packages:
   ```bash
   sudo apt update
   sudo apt install python3 python3-pip git
   ```

## Step 4: Clone the Python App

1. Create a directory for the app:
   ```bash
   mkdir python_app_demo
   cd python_app_demo
   ```
2. Clone the GitHub repository containing the Python app:
   ```bash
   git clone https://github.com/Spidy20/InNews.git
   cd InNews
   ```

## Step 5: Install Python Dependencies

1. Install the Python dependencies listed in `requirements.txt`:
   ```bash
   pip install -r requirements.txt
   ```

## Step 6: Configure Security Group

1. Open the **AWS EC2 Security Group** settings and allow inbound traffic on the port your app will use (e.g., port 8501 for Streamlit).

## Step 7: Deploy the Python App

1. Run the following command to start the app:
   ```bash
   nohup streamlit run App.py &
   ```
2. Copy the public IP address of your EC2 instance and access the app in your browser by navigating to `http://your-ec2-public-ip:8501`.

## Conclusion

Your Python app should now be deployed and accessible via the public IP address of your EC2 instance. If you encounter any issues, ensure that your security group settings are correct and that all necessary dependencies are installed.

