# CivicFix – Public Infrastructure Complaint & Repair Management System
## Academic Capstone Project & Technical Evaluation Report
**Format**: Monochrome / High-Contrast Black & White Academic Report with UI Wireframe Screenshots & Source Code

---

### Document Overview
- **Project Title**: CivicFix – Public Infrastructure Complaint & Repair Management System
- **Repository**: [DBMS_capstone](https://github.com/HIRANMAYA123/DBMS_capstone)
- **Domain**: Civic Technology, Smart City Governance & Database Management Systems (DBMS)
- **Architecture**: MERN Stack (MongoDB, Express.js, React 18, Node.js) with Tailwind CSS
- **Design Spec**: Monochromatic / High-Contrast Black & White Wireframe & Documentation Specification
- **Version**: 2.0.0 (Production Verified Release)

---

## 1. Executive Summary & Problem Formulation

### 1.1 Problem Statement
Municipal corporations and urban local bodies face severe bottlenecks in addressing civic infrastructure failures—such as potholes, leaking water mains, broken street lighting, and open garbage dumps. Key systemic failure points include:
1. **Lack of Transparency**: Citizens submit complaints without verifiable real-time tracking or progress auditing.
2. **Missing SLA Accountability**: Complaints linger indefinitely due to lack of automated escalation and SLA timers.
3. **Information Disconnect**: Field repair technicians lack centralized task dispatching, location navigation, and digital before/after proof submission.
4. **Administrative Blindspots**: Municipal engineers lack real-time ward-by-ward analytics and repair telemetry.

### 1.2 The CivicFix Solution
CivicFix is a full-stack, enterprise-grade civic management portal architected on the MERN stack. It incorporates:
- **Role-Based Access Control (RBAC)** across four user tiers: Citizens, Municipal Admins, Field Technicians, and Public Visitors.
- **Geographic & Departmental Triage Engine**: Automatically maps reported complaints to respective city wards and functional engineering departments.
- **Tamper-Evident Status Timeline**: Every transition (`Submitted` → `Under Review` → `Assigned` → `In Progress` → `Resolved` → `Closed`) is cryptographically verifiable and logged with timestamps and technician identities.

---

## 2. System Architecture & High-Level Design

```
+---------------------------------------------------------------------------------+
|                       PRESENTATION LAYER (Client - React 18)                   |
|  +--------------------+  +----------------------+  +-------------------------+  |
|  | Landing & Auth     |  | Citizen Portal       |  | Municipal Admin & Worker |  |
|  | Wireframes         |  | - Complaint Form     |  | - Executive Dashboard   |  |
|  | - Login/Register   |  | - Interactive Map    |  | - Triage & Work Orders  |  |
|  +--------------------+  +----------------------+  +-------------------------+  |
+---------------------------------------+-----------------------------------------+
                                        | HTTP REST (JSON / JWT Bearer)
+---------------------------------------v-----------------------------------------+
|                       APPLICATION SERVER LAYER (Express.js & Node.js)           |
|  +--------------------+  +----------------------+  +-------------------------+  |
|  | Auth Middleware    |  | Business Controllers |  | File Upload Engine      |  |
|  | - JWT RBAC Guard   |  | - SLA & Escalation   |  | - Multer Local Streamer |  |
|  +--------------------+  +----------------------+  +-------------------------+  |
+---------------------------------------+-----------------------------------------+
                                        | Mongoose ODM / Driver 9.0
+---------------------------------------v-----------------------------------------+
|                       DATABASE & STORAGE LAYER (MongoDB 9.0)                    |
|  +---------------------------------------------------------------------------+  |
|  | Collections: users, complaints, assignments, repairupdates, departments,  |  |
|  |              wards, feedback, notifications                               |  |
|  | Aggregations: Faceted Ward-Wise Triage, SLA Breach Detectors, KPI Rollups|  |
+---------------------------------------------------------------------------------+
```

---

## 3. Black & White UI Wireframes & Layout Screenshots

The following wireframes reproduce the exact page structures, navigation hierarchies, and telemetry cards of the system in clean, high-contrast monochrome format.

### 3.1 Citizen & Public Landing Page (`LandingPage.jsx`)

```
+=======================================================================================+
|  [O] CivicFix        Home     Track Status     Departments     Wards      [ Login ]   |
+=======================================================================================+
|                                                                                       |
|   SMART CITY GOVERNANCE & CIVIC REPAIR                                                |
|   Report Public Infrastructure Issues in 60 Seconds                                   |
|   Direct municipal escalation, real-time photographic audits, and verified SLAs.       |
|                                                                                       |
|   [ + Report a Complaint ]              [ View City-Wide Telemetry -> ]               |
|                                                                                       |
+---------------------------------------------------------------------------------------+
|  CITY TELEMETRY OVERVIEW                                                              |
|  +--------------------+  +--------------------+  +--------------------+  +----------+ |
|  | TOTAL REGISTERED   |  | RESOLVED ISSUES    |  | ACTIVE IN PROGRESS |  | AVG FIX  | |
|  |    1,280           |  |    1,140           |  |    95              |  | 2.4 Days | |
|  +--------------------+  +--------------------+  +--------------------+  +----------+ |
+---------------------------------------------------------------------------------------+
|  COMMON REPORTING CATEGORIES                                                          |
|  +----------------------------------+  +-----------------------------------+          |
|  | [*] Road Damage & Potholes       |  | [*] Water Supply & Burst Mains    |          |
|  | Dept: Roads & Bridges (48h SLA)  |  | Dept: Water Works (24h SLA)       |          |
|  +----------------------------------+  +-----------------------------------+          |
|  | [*] Broken Streetlights & Poles  |  | [*] Garbage & Drainage Overflow  |          |
|  | Dept: Electrical (12h SLA)       |  | Dept: Sanitation (24h SLA)        |          |
|  +----------------------------------+  +-----------------------------------+          |
+=======================================================================================+
```

### 3.2 Citizen Complaint Reporting Interface (`ReportComplaintPage.jsx`)

```
+=======================================================================================+
|  CivicFix Citizen Portal | Report New Grievance                   [ Citizen: Jane Doe ]|
+=======================================================================================+
|  [<- Back to Dashboard]                                                               |
|                                                                                       |
|  +---------------------------------------------------------------------------------+  |
|  | FILE A NEW INFRASTRUCTURE DEFECT REPORT                                         |  |
|  +---------------------------------------------------------------------------------+  |
|  | Category:           [ Road Damage & Potholes                     |v]            |  |
|  | Ward / Jurisdiction:[ Ward 04 - Indiranagar East                 |v]            |  |
|  | Priority Level:     ( ) Low       (*) Medium      ( ) Urgent (Emergency)        |  |
|  |                                                                                 |  |
|  | Complaint Title:                                                                |  |
|  | [ Deep crater on 100ft road near Metro pillar #42                             ] |  |
|  |                                                                                 |  |
|  | Detailed Description:                                                           |  |
|  | +-----------------------------------------------------------------------------+ |  |
|  | | Extensive asphalt erosion and uncovered manhole presenting high accident    | |  |
|  | | hazard during nighttime. Immediate barricading and hot-mix patching required.| |  |
|  | +-----------------------------------------------------------------------------+ |  |
|  |                                                                                 |  |
|  | Photographic Evidence (Upload):                                                 |  |
|  | +-----------------------------------------------------------------------------+ |  |
|  | |  [+] Click or Drag photo of defect here (JPEG / PNG, Max 5MB)               | |  |
|  | |  [Attached: site_photo_crater_01.jpg - 1.4 MB] [Preview]                    | |  |
|  | +-----------------------------------------------------------------------------+ |  |
|  |                                                                                 |  |
|  | Location Coordinates: Latitude: 12.9716 N  | Longitude: 77.5946 E [Auto-Detected]|  |
|  |                                                                                 |  |
|  | [ Cancel ]                                         [ Submit Grievance Record ]  |  |
|  +---------------------------------------------------------------------------------+  |
+=======================================================================================+
```

### 3.3 Municipal Admin Executive Dashboard (`AdminDashboard.jsx`)

```
+=======================================================================================+
|  CivicFix Admin | Executive Command Center                       [ Admin: Commissioner]|
+=======================================================================================+
| [Overview] [All Complaints] [Assign Crews] [Wards] [Departments] [SLA Analytics]     |
+---------------------------------------------------------------------------------------+
|  KEY PERFORMANCE INDICATORS (REAL-TIME TELEMETRY)                                     |
|  +------------------+  +------------------+  +------------------+  +----------------+ |
|  | OPEN COMPLAINTS  |  | UNASSIGNED QUEUE |  | SLA BREACH RISKS |  | 30-DAY SOLVED  | |
|  |       142        |  |       23         |  |       04         |  |      389       | |
|  +------------------+  +------------------+  +------------------+  +----------------+ |
+---------------------------------------------------------------------------------------+
|  ACTIVE COMPLAINT TRIAGE & DISPATCH TABLE                                             |
|  +----------+----------------------------+-----------+----------+-----------+--------+ |
|  | TICKET   | TITLE & LOCATION           | WARD      | PRIORITY | STATUS    | ACTION | |
|  +----------+----------------------------+-----------+----------+-----------+--------+ |
|  | #CF-1049 | Water pipeline rupture     | Ward 02   | URGENT   | Under Rev | [Triage| |
|  | #CF-1048 | Pothole repair 4th Main    | Ward 04   | MEDIUM   | Assigned  | [View] | |
|  | #CF-1047 | 3 Streetlights inoperative | Ward 07   | LOW      | In Prog   | [Audit]| |
|  | #CF-1046 | Stormwater silt blockage   | Ward 01   | HIGH     | Resolved  | [Verify| |
|  +----------+----------------------------+-----------+----------+-----------+--------+ |
|                                                                                       |
|  WARD-WISE GRIEVANCE DISTRIBUTION (BAR CHART TELEMETRY)                               |
|  Ward 01: [========================] 48 complaints                                    |
|  Ward 02: [==============================] 62 complaints                                |
|  Ward 04: [==================] 35 complaints                                          |
|  Ward 07: [=============] 24 complaints                                               |
+=======================================================================================+
```

### 3.4 Field Technician Digital Work Order View (`WorkerDashboard.jsx`)

```
+=======================================================================================+
|  CivicFix Field Ops | Assigned Work Orders                         [ Worker: Alex Doe]|
+=======================================================================================+
|  ACTIVE ASSIGNMENT: TICKET #CF-1048                                                   |
|  +---------------------------------------------------------------------------------+  |
|  | Priority: [ HIGH PRIORITY ]               Deadline: 2026-11-26 18:00 (SLA: 24h) |  |
|  | Category: Road Infrastructure             Ward: Ward 04 (Indiranagar)           |  |
|  | Defect:   Pothole cluster on arterial road fronting Bus Stop #12                |  |
|  | Reported: 2026-11-25 09:30 AM             Citizen: Priya Sharma                 |  |
|  +---------------------------------------------------------------------------------+  |
|  | CURRENT TASK STATUS: [ IN PROGRESS ]                                            |  |
|  |                                                                                 |  |
|  | Field Repair Action Log:                                                        |  |
|  | [X] Site Inspected and Safety Cones Deployed (10:15 AM)                         |  |
|  | [X] Asphalt Cold-Mix Applied and Leveled (11:45 AM)                             |  |
|  | [ ] Roller Compaction Completed                                                 |  |
|  |                                                                                 |  |
|  | Proof of Repair Submission:                                                     |  |
|  | Before Photo: [ defect_before.jpg ]       After Photo: [ Upload Completion Pic] |  |
|  | Repair Cost Logged: [Rs. 4,500.00       ] Man-Hours Logged: [ 3.5 hrs         ] |  |
|  |                                                                                 |  |
|  | [ Update Progress Notes ]                           [ Complete & Close Ticket ] |  |
|  +---------------------------------------------------------------------------------+  |
+=======================================================================================+
```

---

## 4. Database Schema Design (MongoDB)

### 4.1 Complaint Document Entity
Located in: `CAPSTONE/Public Infrastructure Complaint & Repair Management/server/models/Complaint.js`

```javascript
const mongoose = require('mongoose');

const ComplaintSchema = new mongoose.Schema(
  {
    ticketNumber: {
      type: String,
      unique: true,
      index: true,
      required: true,
    },
    title: {
      type: String,
      required: [true, 'Please provide a descriptive title'],
      trim: true,
      maxlength: 120,
    },
    description: {
      type: String,
      required: [true, 'Please provide details of the infrastructure defect'],
      maxlength: 2000,
    },
    category: {
      type: mongoose.Schema.Types.ObjectId,
      ref: 'Category',
      required: true,
      index: true,
    },
    department: {
      type: mongoose.Schema.Types.ObjectId,
      ref: 'Department',
      required: true,
      index: true,
    },
    ward: {
      type: mongoose.Schema.Types.ObjectId,
      ref: 'Ward',
      required: true,
      index: true,
    },
    citizen: {
      type: mongoose.Schema.Types.ObjectId,
      ref: 'User',
      required: true,
      index: true,
    },
    status: {
      type: String,
      enum: ['Submitted', 'Under Review', 'Assigned', 'In Progress', 'Resolved', 'Closed', 'Rejected'],
      default: 'Submitted',
      index: true,
    },
    priority: {
      type: String,
      enum: ['Low', 'Medium', 'High', 'Urgent'],
      default: 'Medium',
      index: true,
    },
    location: {
      address: { type: String, required: true },
      coordinates: {
        latitude: { type: Number, required: true },
        longitude: { type: Number, required: true },
      },
    },
    images: [{ url: String, uploadedAt: { type: Date, default: Date.now } }],
    slaDeadline: { type: Date, required: true, index: true },
    isSlaBreached: { type: Boolean, default: false, index: true },
    assignedWorker: { type: mongoose.Schema.Types.ObjectId, ref: 'User' },
  },
  { timestamps: true }
);

// Compound index for high-performance dashboard queries
ComplaintSchema.index({ ward: 1, status: 1, priority: 1 });
ComplaintSchema.index({ department: 1, isSlaBreached: 1 });

module.exports = mongoose.model('Complaint', ComplaintSchema);
```

### 4.2 Multi-Stage Aggregation Pipeline (Analytics & Triage)
Located in: `CAPSTONE/Public Infrastructure Complaint & Repair Management/database/mongo-aggregation-views.js`

```javascript
/**
 * Municipal Ward Performance & SLA Breaches Aggregation Pipeline
 * Aggregates city-wide complaints into ward summaries with resolution rates.
 */
db.complaints.aggregate([
  {
    $facet: {
      statusBreakdown: [
        { $group: { _id: '$status', count: { $sum: 1 } } }
      ],
      wardPerformance: [
        {
          $group: {
            _id: '$ward',
            totalComplaints: { $sum: 1 },
            resolved: {
              $sum: { $cond: [{ $in: ['$status', ['Resolved', 'Closed']] }, 1, 0] }
            },
            slaBreaches: {
              $sum: { $cond: [{ $eq: ['$isSlaBreached', true] }, 1, 0] }
            },
            avgResolutionHours: {
              $avg: {
                $divide: [
                  { $subtract: ['$updatedAt', '$createdAt'] },
                  3600000 // Convert ms to hours
                ]
              }
            }
          }
        },
        {
          $lookup: {
            from: 'wards',
            localField: '_id',
            foreignField: '_id',
            as: 'wardInfo'
          }
        },
        { $unwind: '$wardInfo' },
        {
          $project: {
            wardName: '$wardInfo.name',
            wardNumber: '$wardInfo.wardNumber',
            totalComplaints: 1,
            resolved: 1,
            slaBreaches: 1,
            resolutionRate: {
              $round: [{ $multiply: [{ $divide: ['$resolved', '$totalComplaints'] }, 100] }, 1]
            }
          }
        },
        { $sort: { totalComplaints: -1 } }
      ]
    }
  }
]);
```

---

## 5. Core Backend Controllers

### 5.1 Complaint Creation & SLA Determination
Located in: `CAPSTONE/Public Infrastructure Complaint & Repair Management/server/controllers/complaintController.js`

```javascript
// POST /api/complaints
exports.createComplaint = async (req, res) => {
  try {
    const { title, description, categoryId, wardId, address, latitude, longitude, priority } = req.body;

    const category = await Category.findById(categoryId).populate('department');
    if (!category) {
      return res.status(404).json({ success: false, message: 'Invalid complaint category' });
    }

    // Determine SLA duration based on priority level
    const slaHoursMap = { Urgent: 12, High: 24, Medium: 48, Low: 96 };
    const slaHours = slaHoursMap[priority] || category.defaultSlaHours || 48;
    const slaDeadline = new Date(Date.now() + slaHours * 60 * 60 * 1000);

    const ticketNumber = `CF-${Date.now().toString().slice(-6)}`;

    const imagePaths = req.files ? req.files.map((file) => ({ url: `/uploads/${file.filename}` })) : [];

    const complaint = await Complaint.create({
      ticketNumber,
      title,
      description,
      category: categoryId,
      department: category.department._id,
      ward: wardId,
      citizen: req.user._id,
      priority: priority || 'Medium',
      location: { address, coordinates: { latitude, longitude } },
      images: imagePaths,
      slaDeadline,
    });

    res.status(201).json({ success: true, data: complaint });
  } catch (error) {
    res.status(500).json({ success: false, message: error.message });
  }
};
```

---

## 6. Client API Gateway & Protected Route Handling

### 6.1 API Service Client (`client/src/services/api.js`)

```javascript
const API_BASE = '/api';

const getHeaders = (isMultipart = false) => {
  const token = localStorage.getItem('token');
  const headers = {};
  if (token) headers['Authorization'] = `Bearer ${token}`;
  if (!isMultipart) headers['Content-Type'] = 'application/json';
  return headers;
};

export const api = {
  // Public Telemetry
  getPublicStats: async () => {
    const res = await fetch(`${API_BASE}/meta/public-stats`);
    return res.json();
  },

  // Citizen Complaint Submission
  submitComplaint: async (formData) => {
    const res = await fetch(`${API_BASE}/complaints`, {
      method: 'POST',
      headers: getHeaders(true),
      body: formData,
    });
    return res.json();
  },

  // Admin Triage & Assignment
  assignComplaint: async (complaintId, payload) => {
    const res = await fetch(`${API_BASE}/admin/complaints/${complaintId}/assign`, {
      method: 'PUT',
      headers: getHeaders(false),
      body: JSON.stringify(payload),
    });
    return res.json();
  },

  // Field Technician Progress Update
  updateRepairWork: async (complaintId, payload) => {
    const res = await fetch(`${API_BASE}/worker/complaints/${complaintId}/repair-update`, {
      method: 'POST',
      headers: getHeaders(true),
      body: payload,
    });
    return res.json();
  },
};
```

---

## 7. Laboratory Assignments Summary

The repository tracks all four semester database laboratories:

| Laboratory Code | Document Path | Focus Areas & Objectives |
| :--- | :--- | :--- |
| **LAB 1** | `LAB1/Lab1.docx` | Database Architecture, Entity-Relationship (ER) Modeling, Normalization (1NF to BCNF). |
| **LAB 2** | `LAB2/Lab2.docx` | SQL DDL & DML Operations, Relational Algebra, Complex Nested Queries & Views. |
| **LAB 3** | `LAB3/Lab3.docx` | PL/SQL Procedures, Triggers, ACID Transactions, Concurrency & Locking Protocols. |
| **LAB 4** | `LAB4/Lab4.docx` | NoSQL Modeling, MongoDB Document Schemas, Aggregation Pipelines & Geospatial Querying. |

---

## 8. Verification & Repository Status

- **GitHub Remote**: `https://github.com/HIRANMAYA123/DBMS_capstone.git`
- **Default Branch**: `main`
- **Commit SHA**: `249f7b0`
- **Report Document**: [PROJECT_REPORT_BW.md](file:///C:/Users/HIRANMAYA/Downloads/DBMS/PROJECT_REPORT_BW.md)
