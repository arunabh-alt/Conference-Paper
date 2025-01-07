# Cattle Management System

This repository contains the frontend and backend code for the Cattle Management System.

<p align="center">
  <img src="https://angular.io/assets/images/logos/angular/angular.svg" alt="Angular Logo" width="100">
  <img src="https://www.oracle.com/a/ocom/img/cb71-java-logo.png" alt="Java Logo" width="100">
  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/93/Amazon_Web_Services_Logo.svg/2560px-Amazon_Web_Services_Logo.svg.png" alt="AWS Logo" width="100">
</p>

## Table of Contents
- [Frontend Setup](#frontend-setup)
  - [Building the Frontend](#building-the-frontend)
  - [Deploying to EC2](#deploying-to-ec2)
- [Backend Setup](#backend-setup)
  - [Running the Java Application](#running-the-java-application)
  - [Stopping the Java Application](#stopping-the-java-application)
- [Node Package Management](#node-package-management)
- [Development](#development)
- [Testing](#testing)
  - [Unit Tests](#unit-tests)
  - [End-to-End Tests](#end-to-end-tests)
- [Further Help](#further-help)

---

## Frontend Setup

### Building the Frontend
1. Ensure Angular CLI is installed. If not, install it with the following command:
   ```bash
   npm install --save-dev @angular-devkit/build-angular
   ```
2. Build the Angular project in production mode:
   ```bash
   ng build --configuration production
   ```
3. After the build is complete, copy the `cattle-app` folder from the `dist` directory to your EC2 home directory:
   ```bash
   scp -r dist/cattle-app/ ec2-user@<your-ec2-ip>:/home/ec2-user/
   ```

### Deploying to EC2
1. SSH into the EC2 instance and navigate to the NGINX directory:
   ```bash
   ssh ec2-user@<your-ec2-ip>
   cd /data/nginx
   ```
2. Remove the existing files:
   ```bash
   sudo rm -rf *
   ```
3. Copy the built Angular app from your home directory to the NGINX directory:
   ```bash
   sudo cp -R /home/ec2-user/cattle-app/* /data/nginx/
   ```
4. Restart the NGINX server:
   ```bash
   sudo systemctl restart nginx
   ```

---

## Backend Setup

### Running the Java Application
1. Navigate to the Java application directory:
   ```bash
   cd cattle-management/utapCattle/utapCattle-main/
   ```
2. Build the project using Maven:
   ```bash
   mvn clean install
   ```
3. Go to the target directory:
   ```bash
   cd target/
   ```
4. Run the application:
   ```bash
   java -jar utapCattle-0.0.1-SNAPSHOT.jar
   ```
   To run the application in the background (no logs displayed on the console):
   ```bash
   nohup java -jar utapCattle-0.0.1-SNAPSHOT.jar > /dev/null 2>&1 &
   ```

### Stopping the Java Application
1. Find the running Java process:
   ```bash
   ps -ef | grep utapCattle-0.0.1-SNAPSHOT.jar
   ```
2. Kill the process by its PID (Process ID):
   ```bash
   kill <PID>
   ```

---

## Node Package Management

To install all dependencies, navigate to the root folder and run:
```bash
npm install
```

---

## Development

1. Start the development server:
   ```bash
   ng serve
   ```
2. Open your browser and navigate to:
   ```
   http://localhost:4200/
   ```
   The application will automatically reload if you make changes to the source files.

3. To scaffold new code, use Angular CLI commands such as:
   ```bash
   ng generate component component-name
   ng generate directive|pipe|service|class|guard|interface|enum|module
   ```

---

## Testing

### Unit Tests
Run the unit tests using Karma:
```bash
ng test
```

### End-to-End Tests
To execute end-to-end tests, first add a package that supports E2E testing (e.g., Protractor or Cypress). Run:
```bash
ng e2e
```

---

## Further Help

For more help with the Angular CLI, use:
```bash
ng help
```
Or visit the [Angular CLI Overview and Command Reference](https://angular.io/cli).
