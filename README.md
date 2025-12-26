# Face Recognition Based Attendance System

A comprehensive attendance management system using face recognition, QR codes, and blink detection for secure and automated attendance tracking.

## 🎯 Features

- **Face Recognition**: Train and recognize student faces using OpenCV
- **QR Code Generation**: Unique QR codes for each student
- **Blink Detection**: Liveness detection to prevent photo spoofing
- **Multi-Step Verification**: QR scan → Blink → Face recognition
- **Student Management**: Add, edit, delete students with face training
- **Attendance Reports**: View, filter, export, and delete attendance records
- **Dashboard**: Real-time statistics and branch-wise attendance
- **Role-Based Access**: Separate interfaces for faculty and students

## 📋 Requirements

- **Python**: 3.10 or higher
- **Operating System**: Windows
- **Hardware**: Webcam (built-in or external)
- **Browser**: Chrome, Edge, or Firefox (Chrome recommended)

## 🚀 Step-by-Step Installation & Setup

### Step 1: Download/Clone the Project

1. Download the project or clone it to your desired location
2. Extract to a folder (e.g., `D:\faceProject`)

### Step 2: Open in VS Code or Command Prompt

**Option A: Using VS Code**
1. Open VS Code
2. Click `File` → `Open Folder`
3. Select the `faceProject` folder
4. Open the integrated terminal: `View` → `Terminal` or press `` Ctrl+` ``

**Option B: Using Command Prompt**
1. Press `Win + R`, type `cmd`, press Enter
2. Navigate to project folder:
   ```cmd
   cd D:\faceProject
   ```

### Step 3: Create Virtual Environment (Recommended)

**In VS Code Terminal or Command Prompt:**

```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# For Command Prompt:
venv\Scripts\activate

# For PowerShell (VS Code default):
venv\Scripts\Activate.ps1

# You should see (venv) at the beginning of your command line
```

> **Note**: If you get an error about execution policies in PowerShell, run:
> ```powershell
> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
> ```

### Step 4: Install Dependencies

**Make sure your virtual environment is activated** (you should see `(venv)` in the terminal)

```bash
# Install all required packages
pip install flask opencv-python numpy pandas pillow qrcode pyzbar

# Verify installation
python -c "import cv2, flask, pandas; print('All packages installed successfully!')"
```

**Expected output**: `All packages installed successfully!`

### Step 5: Verify Project Structure

Make sure you have these folders (they will be created automatically if missing):
```
D:\faceProject\
├── data\
├── static\
├── templates\
└── venv\
```

## 🏃 Running the Application

### Method 1: Using VS Code

1. **Open Terminal** in VS Code (`` Ctrl+` ``)
2. **Activate virtual environment** (if not already active):
   ```bash
   venv\Scripts\Activate.ps1
   ```
3. **Run the application**:
   ```bash
   python app.py
   ```
   Or if you have multiple Python versions:
   ```bash
   py -3.10 app.py
   ```

4. **Wait for the server to start**. You should see:
   ```
   * Running on http://127.0.0.1:5000
   * Running on http://10.x.x.x:5000
   ```

5. **Open your browser** and go to: **http://127.0.0.1:5000**

### Method 2: Using Command Prompt

1. **Open Command Prompt**
2. **Navigate to project folder**:
   ```cmd
   cd D:\faceProject
   ```
3. **Activate virtual environment**:
   ```cmd
   venv\Scripts\activate
   ```
4. **Run the application**:
   ```cmd
   python app.py
   ```
5. **Open browser**: **http://127.0.0.1:5000**

### Stopping the Server

- Press `Ctrl + C` in the terminal where the server is running
- Wait for the server to shut down gracefully

## 🔐 Default Credentials

**Faculty Login:**
- **Username**: `Faculty`
- **Password**: `Faculty123`

> **Important**: Change these credentials in `config.py` for production use!

## 📖 Usage Guide

### For Faculty

#### 1. Login
- Navigate to Faculty Login
- Enter credentials
- Access faculty dashboard

#### 2. Add Students
- Go to "Manage Students"
- Fill in student details:
  - Roll Number
  - Name
  - Gender
  - Email
  - Phone
  - Branch
- Click "Save Student Data"

#### 3. Train Face Recognition
- Click "Train Face" button for a student
- Modal opens with webcam
- Capture 3 clear images of the student's face
- Click "Train & Complete LM"
- System trains the face recognition model
- Success message appears

#### 4. Generate QR Codes
- Click "Generate QR" for a student
- QR code is created and saved
- Students can download/print it

#### 5. Mark Attendance
- Go to "Mark Attendance"
- Click "Start Camera"
- **Step 1**: Student shows QR code to camera
- **Step 2**: Student details appear
- **Step 3**: Student blinks when prompted
- **Step 4**: Face recognition verifies identity
- **Step 5**: Click "Mark Attendance"

#### 6. View Reports
- Go to "Reports"
- Filter by date, branch, or search
- Export to CSV
- Delete attendance records (🗑️ button)

### For Students

#### 1. Access System
- Navigate to main page
- Click "Student Access"

#### 2. View Attendance
- See your attendance records
- Filter by date

## 📁 Project Structure

```
d:/faceProject/
├── app.py                          # Main Flask application
├── config.py                       # Configuration settings
├── data_manager.py                 # CSV data management
├── face_recognition_module.py      # Face recognition logic
├── qr_module.py                    # QR code generation/scanning
├── data/
│   ├── students.csv                # Student records
│   ├── attendance.csv              # Attendance records
│   ├── face_encodings.pkl          # Face recognition data
│   └── training_images/            # Training images by roll number
├── static/
│   ├── css/style.css               # Styling
│   ├── js/main.js                  # JavaScript utilities
│   └── qr_codes/                   # Generated QR codes
└── templates/
    ├── role_selection.html         # Landing page
    ├── faculty_login.html          # Faculty login
    ├── dashboard.html              # Faculty dashboard
    ├── student_management.html     # Student CRUD + training
    ├── webcam_attendance.html      # Attendance marking
    ├── attendance_report.html      # Reports
    └── student_dashboard.html      # Student view
```

## ⚙️ Configuration

Edit `config.py` to customize:

```python
# Flask settings
SECRET_KEY = 'your-secret-key-here'
DEBUG = True

# Faculty credentials
FACULTY_CREDENTIALS = {
    'username': 'Faculty',
    'password': 'Faculty123'
}

# Face recognition
IMAGES_PER_STUDENT = 3              # Number of training images
FACE_RECOGNITION_TOLERANCE = 0.6    # Recognition threshold

# Blink detection
EYE_AR_THRESHOLD = 0.25
EYE_AR_CONSEC_FRAMES = 2

# Branches
BRANCHES = ['CSE', 'ECE', 'EEE', 'MECH', 'CIVIL', 'IT', 'AI', 'DS', 'CS', 'CAI']
```

## 🔧 Troubleshooting

### Issue: "No module named 'cv2.face'"
**Solution**: Install opencv-contrib-python
```bash
pip uninstall opencv-python
pip install opencv-contrib-python
```

### Issue: Webcam not working
**Solution**: 
- Check if webcam is connected
- Allow browser to access webcam
- Try a different browser (Chrome recommended)

### Issue: Face recognition accuracy is low
**Solution**:
- Retrain the face with better lighting
- Capture images from different angles
- Ensure face is clearly visible without glasses/mask
- The system uses LBPH which provides good accuracy

### Issue: QR code not scanning
**Solution**:
- Ensure good lighting
- Hold QR code steady
- Try adjusting distance from camera

## 🎨 Features in Detail

### Face Recognition
- Uses OpenCV LBPH (Local Binary Patterns Histograms) Face Recognizer
- Trains on 3 images per student
- Real-time face detection with Haar Cascades
- Visual feedback with face boxes and eye markers

### Blink Detection
- Detects eye blinks for liveness verification
- Prevents photo spoofing
- Uses Haar Cascade eye detection

### QR Code System
- Unique QR codes for each student
- Contains encrypted student information
- Fast scanning with pyzbar

### Security
- Faculty authentication required
- Session management
- Role-based access control
- Secure attendance marking workflow

## 📊 Database Schema

### students.csv
```
roll_number, name, gender, email, phone, branch, qr_code_path, face_trained
```

### attendance.csv
```
roll_number, name, branch, date, time, timestamp
```

## 🚦 API Endpoints

### Faculty Endpoints
- `POST /api/save-student` - Save student data
- `POST /api/delete-student` - Delete student
- `POST /api/train-face` - Initialize face training
- `POST /api/capture-training-image` - Capture training image
- `POST /api/complete-training` - Complete face training
- `POST /api/generate-qr` - Generate QR code
- `POST /api/mark-attendance` - Mark attendance
- `POST /api/delete-attendance` - Delete attendance record
- `GET /api/export-attendance` - Export to CSV

### Public Endpoints
- `POST /api/process-frame` - Process webcam frame (QR/blink/face)
- `GET /api/get-attendance-report` - Get attendance data
- `GET /api/get-dashboard-stats` - Get statistics

## 🎯 Workflow

### Attendance Marking Process

```
1. Start Camera
   ↓
2. Scan QR Code
   ├─ Decode student information
   └─ Display student details
   ↓
3. Blink Detection
   ├─ Detect face
   ├─ Detect eyes
   └─ Verify blink
   ↓
4. Face Recognition
   ├─ Detect face
   ├─ Extract features
   ├─ Compare with trained model
   └─ Verify match with QR student
   ↓
5. Mark Attendance
   ├─ Check if already marked today
   ├─ Save to CSV
   └─ Show success message
```

## 🛠️ Development

### Adding New Branches
Edit `config.py`:
```python
BRANCHES = ['CSE', 'ECE', 'YOUR_BRANCH']
```

### Changing Faculty Credentials
Edit `config.py`:
```python
FACULTY_CREDENTIALS = {
    'username': 'your_username',
    'password': 'your_password'
}
```

### Customizing Face Recognition
Adjust threshold in `face_recognition_module.py`:
```python
threshold = 25000  # Lower = stricter matching
```

## 📝 Notes

- Face training requires good lighting and clear face visibility
- Each student needs 3 training images for optimal accuracy
- Attendance can only be marked once per day per student
- QR codes are stored in `static/qr_codes/`
- Training images are stored in `data/training_images/{roll_number}/`
- All data is stored in CSV files for easy management

## 🤝 Support

For issues or questions:
1. Check the troubleshooting section
2. Verify all dependencies are installed
3. Ensure webcam permissions are granted
4. Check terminal for error messages

## 📄 License

This project is for educational purposes.

---

**Made with ❤️ using Flask, OpenCV, and Python**
