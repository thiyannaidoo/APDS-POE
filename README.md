# Customer Portal

## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Technologies Used](#technologies-used)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Environment Variables](#environment-variables)
- [Usage Guide](#usage-guide)
  - [Customer Workflow](#customer-workflow)
  - [Admin Workflow](#admin-workflow)
- [CI/CD Pipeline and Quality Assurance](#cicd-pipeline-and-quality-assurance)
  - [CircleCI Workflow](#circleci-workflow)
  - [SonarQube Code Quality Checks](#sonarqube-code-quality-checks)
- [Folder Structure](#folder-structure)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

---

YouTube Link: https://www.youtube.com/watch?v=OihC0Cxd_Wk

## Overview

The Customer Portal is a secure web application where customers can register, log in, and transfer funds to other users. Additionally, the platform includes an admin portal where administrators can review, approve, or reject payments, manage user accounts, and add new administrators. The application has been developed with a focus on security, functionality, and scalability, and includes automated CI/CD processes to maintain high standards of code quality and application stability.

## Features

### Customer Features
- *User Registration and Login*: Customers can create an account and log in securely.
- *Fund Transfer*: Customers can make payments to other users by entering recipient details, amount, and currency.
- *Currency Conversion*: Supports conversion of various currencies to South African Rand (ZAR) using predefined rates.
- *Transaction History*: View detailed records of past transactions.

### Admin Features
- *Admin Dashboard*: Provides an overview of pending payments and options to approve or reject them.
- *User Management*: Ability to add new admin accounts with unique permissions.
- *Payment Approval System*: Admins can validate and approve customer-initiated payments.

### DevOps & Quality Assurance
- *CircleCI Integration*: Automates the CI/CD pipeline to ensure reliable deployments.
- *SonarQube Integration*: Scans the codebase for vulnerabilities, code smells, and technical debt.

## Technologies Used

- *Frontend*: React, Tailwind CSS
- *Backend*: Node.js, Express.js
- *Database*: MongoDB
- *Authentication*: JSON Web Tokens (JWT)
- *CI/CD*: CircleCI
- *Code Quality*: SonarQube

## Getting Started

### Prerequisites

- *Node.js* and *npm*: Make sure you have Node.js and npm installed on your system. Install from [Node.js Official Site](https://nodejs.org/).
- *MongoDB*: MongoDB can be installed locally or used through a cloud service like MongoDB Atlas.
- *CircleCI Account*: Required for CI/CD pipeline setup.
- *SonarQube Account*: Required for code quality checks.

### Installation

1. *Clone the repository*:
   bash
   git clone https://github.com/yourusername/customer-portal.git
   cd customer-portal
   

2. *Install dependencies*:
   bash
   npm install
   

3. *Set up environment variables*:
   Create a .env file in the root directory with the following configuration:

   env
   # Server configuration
   PORT=5000

   # MongoDB URI
   MONGO_URI=mongodb+srv://<username>:<password>@cluster.mongodb.net/customer-portal?retryWrites=true&w=majority

   # JWT secret
   JWT_SECRET=your_jwt_secret

   # SonarQube configuration (for CircleCI integration)
   SONAR_TOKEN=your_sonarqube_token
   SONAR_ORG=your_sonarqube_organization
   SONAR_PROJECT_KEY=your_sonarqube_project_key
   

### Environment Variables

In addition to the basic configuration, ensure that your .env file contains the correct credentials for MongoDB, JWT, and SonarQube. These are essential for running the application and ensuring smooth integration with the CI/CD pipeline.

---

## Usage Guide

### Customer Workflow

#### 1. *Register a New Account*
   - Go to the registration page.
   - Fill out the registration form with your details (name, email, password, etc.).
   - Submit the form to create an account.

#### 2. *Log In*
   - Go to the login page.
   - Enter your email and password to log in.
   - Upon successful login, you will be directed to your dashboard.

#### 3. *Make a Payment*
   - In the dashboard, select the *Make Payment* option.
   - Enter the recipient's email, SWIFT code, amount, and select the currency.
   - Confirm the transaction; a confirmation dialog will appear to review the payment details.
   - Upon confirmation, the payment request is submitted and will await admin approval.

#### 4. *View Payment History*
   - Navigate to the *Transaction History* section.
   - Here you can see all past transactions, including the status (Pending, Approved, or Rejected).

### Admin Workflow

#### 1. *Admin Login*
   - Log in with your admin credentials.
   - Only admin accounts have access to the admin dashboard.

#### 2. *Approve or Reject Payments*
   - On the *Admin Dashboard*, view the list of pending payments.
   - Each payment displays details of the sender, recipient, amount, and currency.
   - Use the *Approve* or *Reject* buttons to take action on each payment. 
   - Approved payments are processed immediately, while rejected ones are marked as such.

#### 3. *Add New Admin*
   - Admins can add new administrators from the *Add New Admin* section on the dashboard.
   - Enter the details of the new admin and submit the form.
   - The new admin can log in and perform administrative tasks after creation.

---

## CI/CD Pipeline and Quality Assurance

### CircleCI Workflow

CircleCI automates the build, test, and deployment process. Our CircleCI pipeline is defined in the .circleci/config.yml file and is structured as follows:

1. *Build Step*: Installs dependencies and compiles the application.
2. *Test Step*: Runs automated tests to ensure functionality.
3. *SonarQube Analysis*: Scans the code for vulnerabilities, code smells, and other quality issues.
4. *Deployment*: Deploys the application to the specified environment if all checks pass.

#### Setting Up CircleCI

1. Link your GitHub repository to CircleCI.
2. Add the following environment variables in CircleCI:
   - SONAR_TOKEN: Your SonarQube token.
   - SONAR_ORG: Your SonarQube organization key.
   - SONAR_PROJECT_KEY: Your SonarQube project key.

3. Push changes to GitHub to trigger the pipeline and view progress on the CircleCI dashboard.

### SonarQube Code Quality Checks

SonarQube integration ensures the codebase adheres to high standards by identifying issues such as:

- *Bugs and Vulnerabilities*: Potential points of failure and security risks.
- *Code Smells*: Non-critical issues that may lead to complex, hard-to-maintain code.
- *Hotspots*: Areas of the codebase that need further attention due to potential security issues.

After every push, CircleCI triggers a SonarQube scan. You can view the detailed report on the SonarQube dashboard to address any issues found.

---

## Folder Structure

The project has a structured folder layout to maintain separation of concerns:


customer-portal/
├── .circleci/           # CircleCI configuration
├── config/              # Configuration files for MongoDB and JWT
├── controllers/         # Application logic for routes
├── middleware/          # Authentication and authorization middleware
├── models/              # MongoDB models (User, Payment, etc.)
├── routes/              # API routes (auth, payment, admin)
├── public/              # Static files
├── views/               # React components and views
├── .env                 # Environment variables
├── .gitignore           # Git ignore file
├── README.md            # Project documentation
├── package.json         # Node.js dependencies and scripts
└── server.js            # Main application entry point


---

## Troubleshooting

- *Error 500 on Payment Creation*: Ensure the recipient email exists in the database. Double-check MongoDB credentials and connectivity.
- *CircleCI Pipeline Fails*: Verify that all environment variables are correctly set in CircleCI.
- *SonarQube Scan Fails*: Check the SonarQube project key and organization key in the .env and CircleCI settings. Review SonarQube’s error logs for specific issues.

---

## Contributing

We welcome contributions to improve the Customer Portal. Here’s how you can help:

1. Fork the repository.
2. Create a new branch for your feature/bug fix (git checkout -b feature-name).
3. Commit and push your changes.
4. Submit a pull request with a detailed description of your changes.

Please ensure all changes pass the CircleCI checks and meet SonarQube quality standards.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
