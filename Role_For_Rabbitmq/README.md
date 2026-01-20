# Hello App – GitLab CI/CD Demo

This repository demonstrates a clean GitLab CI/CD pipeline using:
- Python application
- Docker containerization
- Helm chart
- Secure CI/CD practices

---

## Author Information


| Created by | Created on | Version | Last updated ON | Reviewer |
|------------|------------|---------|-----------------|-----|
| Nitin Sharma    | 13-01-2025 | V 1.0   | 13-01-2026      | Sweta Tyagi| 

---


## Table of Contents

- [Introduction](#1-introduction)
- [Prerequisite](#2-prerequisite)
- [Procedure](#3-procedure)
- [Contact Information](#5-contact-information)
- [References](#6-references)

---

## Introduction


Hello App is a simple Python application designed to demonstrate a complete GitLab CI/CD workflow.  
The project highlights:
- Automated code validation
- Containerization using Docker
- Helm chart deployment for Kubernetes
- Best practices for CI/CD pipelines

---

## Pre-Requisite


Before running this pipeline, ensure you have:

- GitLab account with access to a project repository
- GitLab Runner installed
- Docker installed on the runner machine
- Helm installed (for Kubernetes deployments)
- Basic knowledge of Python and Docker


---

## Procedure


**1. Clone this repository:**

```bash
git clone <repository-url>
cd hello-app
```

**2. Build the application locally to verify:**

```bash
python app.py
```

**3. Run the CI/CD pipeline by pushing changes to GitLab. The pipeline will automatically:**

- Validate code syntax

- Install dependencies

- Run tests

- Build and push Docker image 


---



## Pipeline Stages
1. Validate – syntax & sanity checks
2. Build – dependency installation
3. Test – application test
4. Docker – image build & push

## Requirements
- GitLab Runner with Dock
- GitLab Container Registry enabled








---

## Build Docker image

```bash
docker build -t hello-app .
docker run hello-app
```


---

## Contact Information

| Name           | Email address                                                         |
| -------------- | --------------------------------------------------------------------- |
| Nitin Sharma | [nitin.sharma.snaatak@mygurukulam.co](mailto:nitin.sharma.snaatak@mygurukulam.co) |


---
