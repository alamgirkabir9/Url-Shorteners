# LinkPro - Professional URL Shortener with QR Codes

A modern, full-featured URL shortening service built with Flask and PostgreSQL, featuring automatic QR code generation, click tracking, and a responsive web interface.

## 🚀 Features

### Core Functionality
- **URL Shortening**: Transform long URLs into clean, shareable short links
- **QR Code Generation**: Automatic QR code creation for every shortened URL
- **Click Tracking**: Real-time analytics with click counting and timestamp logging
- **Custom Short IDs**: Collision-resistant random ID generation
- **URL Validation**: Smart URL formatting and validation

### User Experience
- **Responsive Design**: Mobile-first design that works on all devices
- **Modern UI**: Clean, professional interface with smooth animations
- **One-Click Copy**: Easy clipboard integration for sharing links
- **QR Code Management**: Download, share, and toggle QR code visibility
- **Real-time Feedback**: Loading states and success notifications

### Technical Features
- **PostgreSQL Database**: Robust data persistence with proper indexing
- **RESTful API**: Clean API endpoints for programmatic access
- **Error Handling**: Comprehensive error handling and validation
- **Health Monitoring**: Built-in health check endpoint
- **Production Ready**: Configured for deployment on platforms like Render

## 🛠️ Technology Stack

- **Backend**: Python 3.x, Flask
- **Database**: PostgreSQL with psycopg2
- **Frontend**: HTML5, CSS3, JavaScript (ES6+)
- **QR Codes**: Python qrcode library with PIL
- **Styling**: Custom CSS with modern design patterns
- **Icons**: Font Awesome 6.0

## 📋 Prerequisites

- Python 3.7+
- PostgreSQL database
- pip (Python package manager)

## 🔧 Installation & Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/linkpro.git
   cd linkpro
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Set up environment variables**
   Create a `.env` file in the root directory:
   ```env
   DATABASE_URL=postgresql://username:password@localhost:5432/linkpro
   SECRET_KEY=your-secret-key-here
   PORT=5000
   ```

4. **Initialize the database**
   The application will automatically create the required tables on first run.

5. **Run the application**
   ```bash
   python app.py
   ```

6. **Access the application**
   Open your browser and navigate to `http://localhost:5000`

## 📁 Project Structure

```
linkpro/
├── app.py                 # Main Flask application
├── templates/
│   └── index.html        # Frontend template
├── requirements.txt      # Python dependencies
├── .env.example         # Environment variables template
└── README.md           # Project documentation
```

## 🌐 API Endpoints

### POST `/api/shorten`
Create a new short URL with optional QR code generation.

**Request Body:**
```json
{
  "url": "https://example.com/very-long-url"
}
```

**Response:**
```json
{
  "short_url": "https://yourdomain.com/abc123",
  "original_url": "https://example.com/very-long-url",
  "short_id": "abc123",
  "created_at": "2025-06-21T10:30:00",
  "qr_code": "data:image/png;base64,..."
}
```

### GET `/api/qr/<short_id>`
Retrieve QR code for an existing short URL.

### GET `/<short_id>`
Redirect to original URL and track click.

### GET `/health`
Health check endpoint for monitoring.

## 🗄️ Database Schema

### URLs Table
```sql
CREATE TABLE urls (
    id SERIAL PRIMARY KEY,
    short_id VARCHAR(10) UNIQUE NOT NULL,
    original_url TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    clicks INTEGER DEFAULT 0
);
```

### Clicks Table
```sql
CREATE TABLE clicks (
    id SERIAL PRIMARY KEY,
    short_id VARCHAR(10) NOT NULL,
    clicked_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (short_id) REFERENCES urls(short_id)
);
```

## 🚀 Deployment

### Render Deployment
1. Connect your GitHub repository to Render
2. Set environment variables in Render dashboard
3. Use the following build command: `pip install -r requirements.txt`
4. Start command: `python app.py`

### Environment Variables for Production
```env
DATABASE_URL=your-postgresql-connection-string
SECRET_KEY=your-production-secret-key
PORT=10000
```

## 🔒 Security Features

- **Input Validation**: All URLs are validated before processing
- **SQL Injection Protection**: Parameterized queries throughout
- **CSRF Protection**: Flask secret key configuration
- **Error Handling**: Graceful error handling without information leakage

## 📊 Performance Optimizations

- **Database Indexing**: Optimized indexes for fast lookups
- **Connection Pooling**: Efficient database connection management
- **Caching Headers**: Appropriate HTTP caching for static resources
- **Minified Assets**: Optimized CSS and JavaScript

## 🎨 UI/UX Features

- **Modern Design**: Glass morphism and gradient effects
- **Responsive Layout**: Mobile-first responsive design
- **Accessibility**: Semantic HTML and proper contrast ratios
- **Progressive Enhancement**: Works without JavaScript for core features
- **Loading States**: Visual feedback during operations

## 📈 Analytics & Monitoring

- **Click Tracking**: Individual click logging with timestamps
- **Usage Statistics**: Real-time link creation counters
- **Health Monitoring**: `/health` endpoint for uptime monitoring
- **Error Logging**: Comprehensive error logging for debugging

