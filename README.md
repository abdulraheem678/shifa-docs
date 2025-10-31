# Telehealth API - Complete Endpoints Documentation

## Base URL
\`\`\`
http://localhost:3000/api
\`\`\`

## Authentication
All endpoints (except registration and login) require an `Authorization` header with a Bearer token:
\`\`\`
Authorization: Bearer {token}
\`\`\`

---

## 1. AUTHENTICATION ENDPOINTS

### 1.1 Register Doctor
- **Method**: POST
- **Endpoint**: `/auth/register/doctor`
- **Authentication**: None
- **Description**: Register a new doctor account

**Request Body**:
\`\`\`json
{
  "email": "doctor@example.com",
  "phone": "+12345678901",
  "password": "SecurePass123",
  "fullName": "Dr. John Doe",
  "specialty": "Cardiology",
  "yearsExperience": 10,
  "about": "Experienced cardiologist",
  "country": "USA",
  "state": "California",
  "city": "Los Angeles",
  "zip": "90001",
  "language": "en",
  "timezone": "America/Los_Angeles",
  "aliasName": "Dr. Doe",
  "profilePic": "https://example.com/pic.jpg",
  "otpPreferredChannel": "EMAIL",
  "sessionDurationMinutes": 30
}
\`\`\`

**Response** (201):
\`\`\`json
{
  "success": true,
  "data": {
    "userId": "507f1f77bcf86cd799439011",
    "email": "doctor@example.com",
    "role": "DOCTOR",
    "status": "PENDING_VERIFICATION",
    "message": "OTP sent to email"
  }
}
\`\`\`

---

### 1.2 Register Assistant
- **Method**: POST
- **Endpoint**: `/auth/register/assistant`
- **Authentication**: None
- **Description**: Register a new medical assistant account

**Request Body**:
\`\`\`json
{
  "email": "assistant@example.com",
  "phone": "+12345678901",
  "password": "SecurePass123",
  "fullName": "Jane Smith",
  "specialty": "General Practice",
  "yearsExperience": 5,
  "about": "Certified medical assistant",
  "country": "USA",
  "state": "California",
  "city": "Los Angeles",
  "zip": "90001",
  "language": "en",
  "timezone": "America/Los_Angeles",
  "aliasName": "Assistant Jane",
  "profilePic": "https://example.com/pic.jpg",
  "otpPreferredChannel": "SMS"
}
\`\`\`

**Response** (201):
\`\`\`json
{
  "success": true,
  "data": {
    "userId": "507f1f77bcf86cd799439012",
    "email": "assistant@example.com",
    "role": "ASSISTANT",
    "status": "PENDING_VERIFICATION"
  }
}
\`\`\`

---

### 1.3 Register Clinic
- **Method**: POST
- **Endpoint**: `/auth/register/clinic`
- **Authentication**: None
- **Description**: Register a new clinic account

**Request Body**:
\`\`\`json
{
  "email": "clinic@example.com",
  "phone": "+12345678901",
  "password": "SecurePass123",
  "clinicName": "Advanced Medical Center",
  "specialty": "Multi-specialty",
  "yearsExperience": 15,
  "about": "Full-service medical center",
  "street": "123 Medical St",
  "country": "USA",
  "state": "California",
  "city": "Los Angeles",
  "zip": "90001",
  "adminContactName": "Admin User",
  "adminContactEmail": "admin@clinic.com",
  "timezone": "America/Los_Angeles",
  "otpPreferredChannel": "EMAIL"
}
\`\`\`

**Response** (201):
\`\`\`json
{
  "success": true,
  "data": {
    "userId": "507f1f77bcf86cd799439013",
    "clinicId": "507f1f77bcf86cd799439014",
    "email": "clinic@example.com",
    "role": "CLINIC",
    "status": "PENDING_VERIFICATION"
  }
}
\`\`\`

---

### 1.4 Register Patient
- **Method**: POST
- **Endpoint**: `/auth/register/patient`
- **Authentication**: None
- **Description**: Register a new patient account

**Request Body**:
\`\`\`json
{
  "email": "patient@example.com",
  "phone": "+12345678901",
  "password": "SecurePass123",
  "fullName": "John Patient",
  "dateOfBirth": "1990-05-15",
  "gender": "MALE",
  "country": "USA",
  "state": "California",
  "city": "Los Angeles",
  "zip": "90001",
  "language": "en",
  "timezone": "America/Los_Angeles",
  "otpPreferredChannel": "EMAIL"
}
\`\`\`

**Response** (201):
\`\`\`json
{
  "success": true,
  "data": {
    "userId": "507f1f77bcf86cd799439015",
    "email": "patient@example.com",
    "role": "PATIENT",
    "status": "PENDING_VERIFICATION"
  }
}
\`\`\`

---

### 1.5 Verify OTP (Registration)
- **Method**: POST
- **Endpoint**: `/auth/verify-otp`
- **Authentication**: None
- **Description**: Verify OTP code sent during registration

**Request Body**:
\`\`\`json
{
  "userId": "507f1f77bcf86cd799439011",
  "code": "123456"
}
\`\`\`

**Response** (200):
\`\`\`json
{
  "success": true,
  "data": {
    "userId": "507f1f77bcf86cd799439011",
    "email": "doctor@example.com",
    "status": "ACTIVE",
    "message": "Account verified successfully"
  }
}
\`\`\`

---

### 1.6 Login
- **Method**: POST
- **Endpoint**: `/auth/login`
- **Authentication**: None
- **Description**: Initiate login with email and password

**Request Body**:
\`\`\`json
{
  "email": "doctor@example.com",
  "password": "SecurePass123",
  "otpChannel": "EMAIL"
}
\`\`\`

**Response** (200):
\`\`\`json
{
  "success": true,
  "data": {
    "userId": "507f1f77bcf86cd799439011",
    "email": "doctor@example.com",
    "requiresOTP": true,
    "message": "OTP sent to registered email"
  }
}
\`\`\`

---

### 1.7 Verify Login OTP
- **Method**: POST
- **Endpoint**: `/auth/verify-login-otp`
- **Authentication**: None
- **Description**: Verify OTP code sent during login

**Request Body**:
\`\`\`json
{
  "userId": "507f1f77bcf86cd799439011",
  "code": "123456"
}
\`\`\`

**Response** (200):
\`\`\`json
{
  "success": true,
  "data": {
    "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "user": {
      "id": "507f1f77bcf86cd799439011",
      "email": "doctor@example.com",
      "role": "DOCTOR",
      "fullName": "Dr. John Doe"
    }
  }
}
\`\`\`

---

### 1.8 Forgot Password
- **Method**: POST
- **Endpoint**: `/auth/forgot-password`
- **Authentication**: None
- **Description**: Initiate password reset process

**Request Body**:
\`\`\`json
{
  "email": "doctor@example.com",
  "channel": "EMAIL"
}
\`\`\`

**Response** (200):
\`\`\`json
{
  "success": true,
  "data": {
    "userId": "507f1f77bcf86cd799439011",
    "message": "Reset code sent to email"
  }
}
\`\`\`

---

### 1.9 Reset Password
- **Method**: POST
- **Endpoint**: `/auth/reset-password`
- **Authentication**: None
- **Description**: Reset password with OTP code

**Request Body**:
\`\`\`json
{
  "userId": "507f1f77bcf86cd799439011",
  "code": "123456",
  "newPassword": "NewSecurePass456"
}
\`\`\`

**Response** (200):
\`\`\`json
{
  "success": true,
  "data": {
    "message": "Password reset successfully"
  }
}
\`\`\`

---

### 1.10 Change Password
- **Method**: POST
- **Endpoint**: `/auth/change-password`
- **Authentication**: Required
- **Description**: Change password for authenticated user

**Request Body**:
\`\`\`json
{
  "oldPassword": "SecurePass123",
  "newPassword": "NewSecurePass456"
}
\`\`\`

**Response** (200):
\`\`\`json
{
  "success": true,
  "data": {
    "message": "Password changed successfully"
  }
}
\`\`\`

---

### 1.11 Logout
- **Method**: POST
- **Endpoint**: `/auth/logout`
- **Authentication**: Required
- **Description**: Logout current user

**Request Body**: Empty

**Response** (200):
\`\`\`json
{
  "success": true,
  "message": "Logged out"
}
\`\`\`

---

## 2. USER ENDPOINTS

### 2.1 Get User Profile
- **Method**: GET
- **Endpoint**: `/users/profile`
- **Authentication**: Required
- **Description**: Get authenticated user profile

**Request Body**: Empty

**Response** (200):
\`\`\`json
{
  "success": true,
  "data": {
    "id": "507f1f77bcf86cd799439011",
    "email": "doctor@example.com",
    "fullName": "Dr. John Doe",
    "phone": "+12345678901",
    "role": "DOCTOR",
    "status": "ACTIVE",
    "country": "USA",
    "state": "California",
    "city": "Los Angeles",
    "timezone": "America/Los_Angeles",
    "language": "en",
    "createdAt": "2024-01-15T10:30:00Z",
    "updatedAt": "2024-01-20T15:45:00Z"
  }
}
\`\`\`

---

### 2.2 Update User Profile
- **Method**: PUT
- **Endpoint**: `/users/profile`
- **Authentication**: Required
- **Description**: Update authenticated user profile

**Request Body**:
\`\`\`json
{
  "fullName": "Dr. John Doe Jr",
  "phone": "+19876543210",
  "country": "USA",
  "state": "California",
  "city": "San Francisco",
  "language": "en",
  "timezone": "America/Los_Angeles"
}
\`\`\`

**Response** (200):
\`\`\`json
{
  "success": true,
  "data": {
    "id": "507f1f77bcf86cd799439011",
    "email": "doctor@example.com",
    "fullName": "Dr. John Doe Jr",
    "phone": "+19876543210",
    "updatedAt": "2024-01-20T16:00:00Z"
  }
}
\`\`\`

---

## 3. DOCTOR ENDPOINTS

### 3.1 Create Doctor Profile
- **Method**: POST
- **Endpoint**: `/doctors/profile`
- **Authentication**: Required (Doctor role)
- **Description**: Create or update doctor profile

**Request Body**:
\`\`\`json
{
  "specialty": ["Cardiology", "Internal Medicine"],
  "yearsExperience": 12,
  "about": "Board-certified cardiologist with 12 years of experience",
  "aliasName": "Dr. John",
  "language": ["English", "Spanish"],
  "country": "USA",
  "state": "California",
  "city": "Los Angeles",
  "zip": "90001"
}
\`\`\`

**Response** (201):
\`\`\`json
{
  "success": true,
  "data": {
    "doctorId": "507f1f77bcf86cd799439020",
    "userId": "507f1f77bcf86cd799439011",
    "specialty": ["Cardiology", "Internal Medicine"],
    "yearsExperience": 12,
    "about": "Board-certified cardiologist with 12 years of experience",
    "approvalStatus": "PENDING",
    "createdAt": "2024-01-15T10:30:00Z"
  }
}
\`\`\`

---

### 3.2 List All Doctors
- **Method**: GET
- **Endpoint**: `/doctors/`
- **Authentication**: None
- **Description**: List all approved doctors with filtering and pagination

**Query Parameters**:
\`\`\`
?specialty=Cardiology&city=Los%20Angeles&page=1&limit=20&sort=rating&order=desc
\`\`\`

**Response** (200):
\`\`\`json
{
  "success": true,
  "data": [
    {
      "doctorId": "507f1f77bcf86cd799439020",
      "fullName": "Dr. John Doe",
      "specialty": ["Cardiology", "Internal Medicine"],
      "yearsExperience": 12,
      "rating": 4.8,
      "reviewCount": 150,
      "city": "Los Angeles",
      "state": "California",
      "language": ["English", "Spanish"],
      "isAvailable": true
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 20,
    "total": 150,
    "pages": 8
  }
}
\`\`\`

---

## 4. ASSISTANT ENDPOINTS

### 4.1 Create Assistant Profile
- **Method**: POST
- **Endpoint**: `/assistants/profile`
- **Authentication**: Required (Assistant role)
- **Description**: Create or update assistant profile

**Request Body**:
\`\`\`json
{
  "specialty": "General Practice",
  "yearsExperience": 5,
  "about": "Certified medical assistant with 5 years experience",
  "language": ["English"],
  "country": "USA",
  "state": "California",
  "city": "Los Angeles",
  "zip": "90001"
}
\`\`\`

**Response** (201):
\`\`\`json
{
  "success": true,
  "data": {
    "assistantId": "507f1f77bcf86cd799439025",
    "userId": "507f1f77bcf86cd799439012",
    "specialty": "General Practice",
    "yearsExperience": 5,
    "about": "Certified medical assistant with 5 years experience",
    "createdAt": "2024-01-15T10:30:00Z"
  }
}
\`\`\`

---

### 4.2 Get Assistant Profile
- **Method**: GET
- **Endpoint**: `/assistants/profile`
- **Authentication**: Required (Assistant role)
- **Description**: Get current assistant profile

**Response** (200):
\`\`\`json
{
  "success": true,
  "data": {
    "assistantId": "507f1f77bcf86cd799439025",
    "userId": "507f1f77bcf86cd799439012",
    "fullName": "Jane Smith",
    "email": "assistant@example.com",
    "specialty": "General Practice",
    "yearsExperience": 5,
    "language": ["English"],
    "approvalStatus": "ACTIVE",
    "createdAt": "2024-01-15T10:30:00Z"
  }
}
\`\`\`

---

### 4.3 Update Assistant Profile
- **Method**: PUT
- **Endpoint**: `/assistants/profile`
- **Authentication**: Required (Assistant role)
- **Description**: Update assistant profile

**Request Body**:
\`\`\`json
{
  "specialty": "General Practice & Nursing",
  "yearsExperience": 6,
  "about": "Certified medical assistant and nurse",
  "language": ["English", "Spanish"]
}
\`\`\`

**Response** (200):
\`\`\`json
{
  "success": true,
  "data": {
    "assistantId": "507f1f77bcf86cd799439025",
    "specialty": "General Practice & Nursing",
    "yearsExperience": 6,
    "updatedAt": "2024-01-20T16:00:00Z"
  }
}
\`\`\`

---

### 4.4 List All Assistants
- **Method**: GET
- **Endpoint**: `/assistants/`
- **Authentication**: None
- **Description**: List all active assistants

**Response** (200):
\`\`\`json
{
  "success": true,
  "data": [
    {
      "assistantId": "507f1f77bcf86cd799439025",
      "fullName": "Jane Smith",
      "specialty": "General Practice",
      "yearsExperience": 5,
      "city": "Los Angeles",
      "language": ["English", "Spanish"]
    }
  ]
}
\`\`\`

---

## 5. PATIENT ENDPOINTS

### 5.1 Create Patient Profile
- **Method**: POST
- **Endpoint**: `/patients/profile`
- **Authentication**: Required (Patient role)
- **Description**: Create or update patient profile

**Request Body**:
\`\`\`json
{
  "fullName": "John Patient",
  "dateOfBirth": "1990-05-15",
  "gender": "MALE",
  "bloodType": "O+",
  "allergies": ["Penicillin", "Sulfa"],
  "medicalHistory": "Diabetes, Hypertension",
  "emergencyContactName": "Jane Patient",
  "emergencyContactPhone": "+12345678901",
  "insuranceProvider": "Blue Cross",
  "insurancePolicyNumber": "BC123456789",
  "country": "USA",
  "state": "California",
  "city": "Los Angeles",
  "zip": "90001"
}
\`\`\`

**Response** (201):
\`\`\`json
{
  "success": true,
  "data": {
    "patientId": "507f1f77bcf86cd799439030",
    "userId": "507f1f77bcf86cd799439015",
    "fullName": "John Patient",
    "dateOfBirth": "1990-05-15",
    "gender": "MALE",
    "bloodType": "O+",
    "medicalHistory": "Diabetes, Hypertension",
    "createdAt": "2024-01-15T10:30:00Z"
  }
}
\`\`\`

---

## 6. CLINIC ENDPOINTS

### 6.1 Create Clinic Profile
- **Method**: POST
- **Endpoint**: `/clinics/`
- **Authentication**: Required
- **Description**: Create or update clinic profile

**Request Body**:
\`\`\`json
{
  "clinicName": "Advanced Medical Center",
  "specialty": ["Multi-specialty", "Emergency"],
  "yearsExperience": 20,
  "about": "Full-service medical center",
  "street": "123 Medical St",
  "country": "USA",
  "state": "California",
  "city": "Los Angeles",
  "zip": "90001",
  "adminContactName": "Admin User",
  "adminContactEmail": "admin@clinic.com",
  "phone": "+12345678901",
  "website": "https://clinic.example.com"
}
\`\`\`

**Response** (201):
\`\`\`json
{
  "success": true,
  "data": {
    "clinicId": "507f1f77bcf86cd799439035",
    "clinicName": "Advanced Medical Center",
    "approvalStatus": "PENDING",
    "createdAt": "2024-01-15T10:30:00Z"
  }
}
\`\`\`

---

## 7. APPOINTMENT ENDPOINTS

### 7.1 Create Appointment
- **Method**: POST
- **Endpoint**: `/appointments/`
- **Authentication**: Required
- **Description**: Create a new appointment

**Request Body**:
\`\`\`json
{
  "patientId": "507f1f77bcf86cd799439015",
  "doctorId": "507f1f77bcf86cd799439020",
  "clinicId": "507f1f77bcf86cd799439035",
  "appointmentType": "VIDEO_CONSULTATION",
  "startTime": "2024-02-01T10:00:00Z",
  "endTime": "2024-02-01T10:30:00Z",
  "symptoms": "Chest pain, shortness of breath",
  "notes": "First time patient",
  "desiredSpecialist": "Cardiology"
}
\`\`\`

**Response** (201):
\`\`\`json
{
  "success": true,
  "data": {
    "appointmentId": "507f1f77bcf86cd799439040",
    "patientId": "507f1f77bcf86cd799439015",
    "doctorId": "507f1f77bcf86cd799439020",
    "appointmentType": "VIDEO_CONSULTATION",
    "startTime": "2024-02-01T10:00:00Z",
    "endTime": "2024-02-01T10:30:00Z",
    "status": "SCHEDULED",
    "createdAt": "2024-01-20T10:00:00Z"
  }
}
\`\`\`

---

### 7.2 Get Appointment Details
- **Method**: GET
- **Endpoint**: `/appointments/:id`
- **Authentication**: Required
- **Description**: Get specific appointment details

**Response** (200):
\`\`\`json
{
  "success": true,
  "data": {
    "appointmentId": "507f1f77bcf86cd799439040",
    "patientName": "John Patient",
    "doctorName": "Dr. John Doe",
    "appointmentType": "VIDEO_CONSULTATION",
    "startTime": "2024-02-01T10:00:00Z",
    "endTime": "2024-02-01T10:30:00Z",
    "status": "SCHEDULED",
    "meetingLink": "https://meet.example.com/room123",
    "symptoms": "Chest pain, shortness of breath",
    "notes": "First time patient"
  }
}
\`\`\`

---

## 8. AVAILABILITY ENDPOINTS

### 8.1 Set Doctor Availability
- **Method**: POST
- **Endpoint**: `/availability/`
- **Authentication**: Required (Doctor role)
- **Description**: Set doctor availability schedule

**Request Body**:
\`\`\`json
{
  "rules": [
    {
      "dayOfWeek": 1,
      "segments": [
        {
          "start": "09:00",
          "end": "12:00"
        },
        {
          "start": "14:00",
          "end": "18:00"
        }
      ]
    },
    {
      "dayOfWeek": 2,
      "segments": [
        {
          "start": "09:00",
          "end": "12:00"
        }
      ]
    }
  ],
  "blackout": [
    {
      "startUTC": "2024-02-14T00:00:00Z",
      "endUTC": "2024-02-14T23:59:59Z"
    }
  ]
}
\`\`\`

**Response** (201):
\`\`\`json
{
  "success": true,
  "data": {
    "availabilityId": "507f1f77bcf86cd799439045",
    "doctorId": "507f1f77bcf86cd799439020",
    "message": "Availability set successfully",
    "createdAt": "2024-01-20T10:00:00Z"
  }
}
\`\`\`

---

## 9. MESSAGE ENDPOINTS

### 9.1 Send Message
- **Method**: POST
- **Endpoint**: `/messages/`
- **Authentication**: Required
- **Description**: Send a message between users

**Request Body**:
\`\`\`json
{
  "recipientId": "507f1f77bcf86cd799439020",
  "appointmentId": "507f1f77bcf86cd799439040",
  "content": "Hi Doctor, I have some follow-up questions about my appointment",
  "attachments": []
}
\`\`\`

**Response** (201):
\`\`\`json
{
  "success": true,
  "data": {
    "messageId": "507f1f77bcf86cd799439050",
    "senderId": "507f1f77bcf86cd799439015",
    "recipientId": "507f1f77bcf86cd799439020",
    "content": "Hi Doctor, I have some follow-up questions about my appointment",
    "status": "SENT",
    "createdAt": "2024-01-20T14:30:00Z"
  }
}
\`\`\`

---

## 10. MEETING ENDPOINTS

### 10.1 Create Meeting
- **Method**: POST
- **Endpoint**: `/meetings/`
- **Authentication**: Required
- **Description**: Create a video meeting for appointment

**Request Body**:
\`\`\`json
{
  "appointmentId": "507f1f77bcf86cd799439040",
  "meetingType": "VIDEO_CONSULTATION",
  "duration": 30,
  "timezone": "America/Los_Angeles"
}
\`\`\`

**Response** (201):
\`\`\`json
{
  "success": true,
  "data": {
    "meetingId": "507f1f77bcf86cd799439055",
    "appointmentId": "507f1f77bcf86cd799439040",
    "meetingLink": "https://meet.example.com/room123",
    "roomId": "room123",
    "status": "CREATED",
    "createdAt": "2024-01-20T15:00:00Z"
  }
}
\`\`\`

---

## 11. REVIEW ENDPOINTS

### 11.1 Create Review
- **Method**: POST
- **Endpoint**: `/reviews/`
- **Authentication**: Required
- **Description**: Create a review for doctor or clinic

**Request Body**:
\`\`\`json
{
  "doctorId": "507f1f77bcf86cd799439020",
  "rating": 5,
  "comment": "Excellent doctor, very knowledgeable and compassionate",
  "appointmentId": "507f1f77bcf86cd799439040",
  "tags": ["Professional", "Friendly", "Effective"]
}
\`\`\`

**Response** (201):
\`\`\`json
{
  "success": true,
  "data": {
    "reviewId": "507f1f77bcf86cd799439060",
    "doctorId": "507f1f77bcf86cd799439020",
    "patientId": "507f1f77bcf86cd799439015",
    "rating": 5,
    "comment": "Excellent doctor, very knowledgeable and compassionate",
    "createdAt": "2024-01-20T16:00:00Z"
  }
}
\`\`\`

---

## 12. FILE ENDPOINTS

### 12.1 Upload File
- **Method**: POST
- **Endpoint**: `/files/`
- **Authentication**: Required
- **Description**: Upload medical files or documents

**Request Body**: Form Data
\`\`\`
file: [binary file]
appointmentId: 507f1f77bcf86cd799439040
documentType: MEDICAL_REPORT
\`\`\`

**Response** (201):
\`\`\`json
{
  "success": true,
  "data": {
    "fileId": "507f1f77bcf86cd799439065",
    "fileName": "medical_report.pdf",
    "fileUrl": "https://storage.example.com/medical_report.pdf",
    "documentType": "MEDICAL_REPORT",
    "fileSize": 524288,
    "uploadedAt": "2024-01-20T17:00:00Z"
  }
}
\`\`\`

---

## 13. BLOCKLIST ENDPOINTS

### 13.1 Block User
- **Method**: POST
- **Endpoint**: `/blocklist/block`
- **Authentication**: Required
- **Description**: Block a user

**Request Body**:
\`\`\`json
{
  "blockUserId": "507f1f77bcf86cd799439020",
  "reason": "Inappropriate behavior"
}
\`\`\`

**Response** (201):
\`\`\`json
{
  "success": true,
  "data": {
    "blocklistId": "507f1f77bcf86cd799439070",
    "blockedUserId": "507f1f77bcf86cd799439020",
    "blockReason": "Inappropriate behavior",
    "createdAt": "2024-01-20T18:00:00Z"
  }
}
\`\`\`

---

## 14. ADMIN ENDPOINTS

### 14.1 Approve Doctor
- **Method**: PUT
- **Endpoint**: `/admin/approve-doctor/:doctorId`
- **Authentication**: Required (Admin role)
- **Description**: Approve pending doctor registration

**Request Body**:
\`\`\`json
{
  "status": "APPROVED",
  "notes": "All documents verified",
  "credentials": {
    "licenseNumber": "MD123456",
    "licenseState": "CA",
    "licenseExpiry": "2026-12-31"
  }
}
\`\`\`

**Response** (200):
\`\`\`json
{
  "success": true,
  "data": {
    "doctorId": "507f1f77bcf86cd799439020",
    "status": "APPROVED",
    "approvedAt": "2024-01-20T19:00:00Z",
    "approvedBy": "admin@example.com"
  }
}
\`\`\`

---

## Error Responses

### 400 Bad Request
\`\`\`json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Validation failed",
    "details": [
      {
        "field": "email",
        "message": "Invalid email format"
      }
    ]
  }
}
\`\`\`

### 401 Unauthorized
\`\`\`json
{
  "success": false,
  "error": {
    "code": "UNAUTHORIZED",
    "message": "Authentication required"
  }
}
\`\`\`

### 403 Forbidden
\`\`\`json
{
  "success": false,
  "error": {
    "code": "FORBIDDEN",
    "message": "Insufficient permissions"
  }
}
\`\`\`

### 404 Not Found
\`\`\`json
{
  "success": false,
  "error": {
    "code": "NOT_FOUND",
    "message": "Resource not found"
  }
}
\`\`\`

### 500 Internal Server Error
\`\`\`json
{
  "success": false,
  "error": {
    "code": "INTERNAL_SERVER_ERROR",
    "message": "An unexpected error occurred"
  }
}
\`\`\`

---

## Rate Limiting
- Requests are rate-limited to 1000 requests per hour per IP address
- Rate limit headers are included in all responses:
  - `X-RateLimit-Limit`: 1000
  - `X-RateLimit-Remaining`: 999
  - `X-RateLimit-Reset`: 1642703400

---

## Pagination
All list endpoints support pagination:
- `page`: Page number (default: 1)
- `limit`: Items per page (default: 20, max: 100)
- Response includes `pagination` object with `total`, `pages`, `page`, `limit`

---

## Sorting
List endpoints support sorting:
- `sort`: Field to sort by
- `order`: `asc` or `desc`
\`\`\`
/doctors?sort=rating&order=desc
\`\`\`

---

## Date Format
All dates are in ISO 8601 format: `2024-01-20T15:30:00Z`
