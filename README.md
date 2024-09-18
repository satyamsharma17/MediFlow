# MediFlow - Hospital Management System

MediFlow is a comprehensive hospital management solution designed to streamline patient admissions, manage bed availability, optimize OPD queues, and enhance overall healthcare efficiency. The system integrates seamlessly with existing hospital infrastructure and provides real-time data management through a combination of microservices, REST APIs, and GraphQL. The solution also extends its capabilities to city-wide healthcare management, offering a unified platform for healthcare providers and authorities.

## Project Architecture

### Architecture Overview
MediFlow follows a microservices architecture for scalability and flexibility. Each microservice handles a specific aspect of hospital management, such as patient admission, OPD queue management, bed allocation, and inventory management. Below is an overview of the architectural components:

- **Backend**:
  - **Microservices**: Individual services for managing OPDs, patient admissions, bed availability, inventory, and city-wide integration.
  - **REST API**: Used for core operations like patient management, inventory tracking, city-wide data aggregation, and integration with third-party systems.
  - **GraphQL**: Used for complex data queries and efficient data retrieval for the frontend.
  - **Databases**:
    - **MongoDB**: Manages unstructured data like patient records, medical history, and treatment plans.
    - **PostgreSQL**: Handles relational data such as bed allocations, appointments, and city-level healthcare analytics.
  - **Message Broker**:
    - **Apache Kafka**: Facilitates real-time data streaming for critical events like bed availability, patient status updates, and city-wide notifications.

- **City-Wide Module**:
  - **Integration Service**: Aggregates data from multiple hospitals and clinics within the city for a unified view.
  - **Data Synchronization**: Uses REST APIs and Kafka for real-time data synchronization between hospitals and the city-wide control center.
  - **Centralized Dashboard**: Provides a city-wide overview of healthcare resources, including OPD statuses, bed availability, and critical alerts.
  - **Inter-Hospital Coordination**: Enables the transfer of patients between hospitals based on bed availability and specialization.

- **Frontend**:
  - **Android App**:
    - **Architecture**: Follows the MVVM (Model-View-ViewModel) pattern to ensure a clean separation of concerns.
    - **Components**:
      - **Model**: Represents the data layer, including access to REST APIs and local databases.
      - **View**: UI components built using Jetpack Compose, observing the ViewModel for data changes.
      - **ViewModel**: Acts as a mediator between the View and Model, handling UI-related data and logic.
    - **Data Fetching**: Uses Retrofit for REST API calls and LiveData for reactive UI updates.
    - **City-Wide Features**: Provides patients with city-wide data, such as available beds across different hospitals.
  
  - **Admin Panel**:
    - **Framework**: Built using React.js for a responsive and interactive web-based admin interface.
    - **Components**:
      - **Dashboard**: Displays real-time statistics on OPD queues, bed availability, inventory status, and city-wide healthcare metrics.
      - **Management Modules**: Separate modules for managing patients, beds, OPD schedules, inventory, and city-wide resources.
      - **City Control**: Central dashboard for city authorities to monitor healthcare facilities and coordinate resources.
    - **Data Fetching**: Uses Axios to interact with the REST APIs and GraphQL for complex data queries.
    - **State Management**: Utilizes React Context API and Redux for efficient state management across components.

- **DevOps & Monitoring**:
  - **Jenkins**: Continuous integration and deployment.
  - **GitLab**: Source control and version management.
  - **Prometheus & Grafana**: Real-time monitoring and data visualization.

### Data Flow
1. **Patient Admission**: 
   - Patients register via the Android app, triggering REST API calls to the admission microservice.
   - Data is stored in MongoDB for patient records and PostgreSQL for appointment scheduling.
   - City-wide updates are sent to the central module for real-time data aggregation.
2. **OPD Queue Management**:
   - OPD microservice manages patient queues using REST APIs, with real-time updates via Apache Kafka.
   - The Android app and Admin Panel fetch and display queue status using GraphQL.
3. **Bed Allocation**:
   - Bed management microservice checks availability and updates status in PostgreSQL.
   - Real-time updates are broadcasted using Kafka and displayed on the Admin Panel and city-wide module.
4. **Inventory Management**:
   - Inventory microservice tracks consumables and medicines, storing data in MongoDB.
   - Automated stock alerts and reports are generated through Prometheus and Grafana.
5. **City-Wide Data Aggregation**:
   - The integration service aggregates data from all hospitals, providing city-level insights on bed availability, OPD queues, and resource status.
   - Enables inter-hospital coordination for patient transfers and critical resource allocation.

## Key Features

- **Patient Management**: Streamlined registration, admission, and discharge processes.
- **OPD Queue Management**: Efficiently manage patient flow in OPDs, reducing wait times.
- **Bed Availability**: Real-time tracking and management of bed occupancy across departments and hospitals city-wide.
- **Inventory Management**: Automated tracking of medicines and consumables with stock alerts.
- **City-Wide Coordination**: A centralized system for city authorities to monitor healthcare facilities and coordinate resources.
- **Data Security**: Implements encryption and role-based access controls to ensure patient data privacy.
- **Real-time Monitoring**: Use of Apache Kafka for real-time event streaming and Grafana for data visualization.
- **Scalable Microservices**: Microservices architecture allows for scalable and flexible system enhancements.
- **Interoperability**: Integrates with existing hospital systems and third-party services via REST APIs.

## Technologies Used

- **Programming Languages**: Java, JavaScript, Kotlin
- **Frameworks**: Spring Boot (Backend), React.js (Admin Panel), Jetpack Compose/Kotlin Multiplatform (Android App)
- **Databases**: MongoDB, PostgreSQL
- **APIs**: REST, GraphQL
- **Message Broker**: Apache Kafka
- **DevOps**: Jenkins, GitLab
- **Monitoring**: Prometheus, Grafana

## Getting Started

1. **Clone the Repository**:

    ```bash
    git clone https://github.com/satyamsharma17/MediFlow.git
    ```

2. **Install Dependencies**:

    - Android App:
   
      - Open the Android project in Android Studio and sync the Gradle dependencies.
    
3. **Run Services**:
    - Start backend microservices:
  
      ```bash
      cd backend
      mvn spring-boot:run
      ```

    - Start Admin Panel:

      ```bash
      cd admin-panel
      npm start
      ```

    - Deploy the Android app to an emulator or connected device through Android Studio.

4. **Access the Application**: 
    - Admin Panel: Open your browser and navigate to `http://localhost:3000`.
    - Android App: Run on an emulator or Android device.

## License

This project is licensed under the MIT License.
