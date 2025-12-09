# AI Anomaly Detector for X-ray Scans

This project is a full-stack web application designed to assist customs officers in identifying anomalies in vehicle X-ray images. It leverages an AI model to automatically compare X-ray scans and highlight potential irregularities, modifications, or hidden objects that may indicate smuggling.

The system was developed to support the National Revenue Administration (KAS) by automating the analysis of large quantities of X-ray images from border crossings, thereby making the inspection process faster and more efficient.

## Introduction - Organization, Situation, and Current Status

The National Revenue Administration (KAS) utilizes large-scale X-ray devices at the external EU border for customs and fiscal control. These devices are used for non-invasive inspection of containers, heavy goods vehicles, passenger cars, coaches, and railway wagons. The suppliers of these devices include Nuctech and Multicontrol. X-ray operators (Customs and Fiscal Service officers) assess the factual status based on X-ray images and decide on further proceedings, which may include ordering a physical inspection to verify whether undeclared goods are present in the vehicle structure or the transported cargo. All X-ray images are sent to a central repository for storage. Previous experience of the Customs and Fiscal Service indicates that smugglers hide undeclared goods both within the structural elements of vehicles and within the goods formally declared. X-ray operators analyzing these images require analytical support, in the form of an AI-based analytical tool, that compares analyzed X-ray images from large-scale X-ray devices with reference images and indicates differences that may suggest the transport of undeclared goods (smuggling).

Currently, KAS employs an AI-based non-invasive control tool for the automatic detection of cigarettes in vehicles and goods based on analyzed X-ray images. However, for the smuggling of small quantities of cigarettes hidden in structural elements of vehicles, the effectiveness of this tool is unsatisfactory. In such cases, details, structural changes, and modifications to create hiding places for smuggling purposes may indicate illicit activities.

## Problem Statement

Customs operators manually inspect thousands of X-ray images daily in search of smuggled goods hidden within vehicle structures or cargo. This process is time-consuming and highly susceptible to human error, especially when dealing with subtle modifications. This project aims to provide an intelligent tool that supports operators by automatically flagging suspicious areas.

## Solution

The application provides a web interface where users can view and manage X-ray scans. A powerful backend, driven by a PyTorch-based machine learning model, performs anomaly detection.

### Key Features

-   **AI-powered Anomaly Detection**: A deep learning model analyzes X-ray images in `.bmp` format to find deviations from normal patterns.
-   **Image Comparison**: The system can compare a vehicle X-ray scan with a "clean" reference image or identify anomalies based on learned patterns.
-   **Visual Feedback**: Suspicious areas and detected anomalies are highlighted directly on the image in the user interface.
-   **Automated Workflow**: A folder-watching mechanism automatically processes new X-ray images as they appear.
-   **Scalable Architecture**: Designed to handle large image files (~50MB each) and large datasets.

## Getting Started

The entire application can be built and run using Docker Compose.

### Prerequisites

-   Docker and Docker Compose
-   A local folder containing the X-ray images you wish to analyze.

### Installation and Running

1.  **Environment Setup**:
    Create a `.env` file in the project's root directory. Add the following line, replacing the placeholder with the absolute path to your image folder:
    ```
    SEARCH_FOLDER=<path_to_your_images_folder>
    ```
    This variable mounts the image folder into the backend container for processing.

2.  **Build and Run with Docker Compose**:
    Open a terminal in the project's root directory and execute:
    ```bash
    docker-compose up -d --build
    ```

3.  **Access the Application**:
    -   The frontend will be accessible at **`http://localhost:3000`**.
    -   The backend API will be accessible at **`http://localhost:8000`**.

## Technology Stack

-   **Frontend**: Next.js, React, TypeScript, Tailwind CSS
-   **Backend**: Python, FastAPI, PyTorch, OpenCV
-   **Orchestration**: Docker

## System Architecture

The project employs a modern client-server architecture:
-   **Frontend** is a Next.js application providing a responsive and interactive user interface for viewing scan results.
-   **Backend** is a FastAPI service that offers a REST API and WebSocket for image processing. It hosts the AI model for anomaly detection and manages image data.
-   **Docker Compose** orchestrates both services, simplifying setup and deployment.