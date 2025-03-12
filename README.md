# Store Monitoring API

## Overview
This project provides backend APIs to monitor the uptime and downtime of restaurants in the US. Restaurant owners can track their store’s activity and generate reports based on business hours and active/inactive status logs.

## Features
- **Data Processing**: Parses CSV data from three sources (store activity logs, business hours, and time zones).
- **Real-time Report Generation**: Generates uptime/downtime statistics dynamically.
- **Trigger-Poll Architecture**: API design follows a trigger-and-fetch model for efficient data retrieval.
- **Database Integration**: Stores parsed data and generates reports based on live data.
- **Extrapolation Logic**: Fills missing data points within business hours using interpolation techniques.

## APIs
### **1. Trigger Report**
**Endpoint:**
```
POST /trigger_report
```
**Response:**
```json
{
  "report_id": "<random_string>"
}
```

### **2. Get Report**
**Endpoint:**
```
GET /get_report?report_id=<report_id>
```
**Response:**
- If report is still processing:
  ```json
  {
    "status": "Running"
  }
  ```
- If report is complete:
  ```json
  {
    "status": "Complete",
    "csv_file": "<download_link>"
  }
  ```

## Challenges Faced
### **1. Complex Prediction Logic**
- Extrapolating uptime and downtime between periodic observations was challenging, especially for calculating last hour and last day.
- Required careful handling of missing data, edge cases, and interpolation techniques.

### **2. Handling Different Time Zones**
- Business hours were in local time, while store activity logs were in UTC, making direct comparisons difficult.
- Implemented a conversion mechanism to standardize time calculations.

### **3. Optimizing Query Performance**
- Fetching large datasets and computing uptime/downtime efficiently required indexing and caching strategies.

## Future Improvements
- **Real-time Streaming**: Implementing WebSockets or Kafka for real-time monitoring.
- **Better Interpolation Techniques**: Improve uptime/downtime estimation using ML models.
- **Automated Alerts**: Notify restaurant owners when downtime exceeds a threshold.
- **Scalability Enhancements**: Optimize database structure for handling large-scale data.

## Setup and Execution
### **1. Install Dependencies**
```sh
npm install
```

### **2. Start the Server**
```sh
npm run dev
```

### **3. Check Database Tables**
```sql
SELECT * FROM reports;
SELECT * FROM report_statuses;
```

### **4. Trigger Report**
Use Postman or CURL:
```sh
curl -X POST http://localhost:3004/trigger_report
```

### **5. Check Report Status**
```sh
curl -X GET http://localhost:3004/get_report?report_id=<generated_report_id>
```

## Sample Output
This link provides a complete demonstration of the project. : https://www.loom.com/share/e12fdf6cd15c4541adaf889646f4e0b7?sid=f23403f9-8ace-42ad-ab6d-8ff7fe241df2

This project demonstrates the ability to handle real-life data processing, efficient API design, and complex algorithmic challenges. 🚀

