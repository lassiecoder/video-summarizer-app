# 🎥 Video Summarizer AI

A powerful AI-powered video summarization tool that transforms any video into concise, intelligent summaries using Google's Gemini AI. Features both a beautiful web interface and command-line tool.

![Video Summarizer Demo](https://img.shields.io/badge/Status-Live-green) ![Node.js](https://img.shields.io/badge/Node.js-18+-blue) ![TypeScript](https://img.shields.io/badge/TypeScript-5.0+-blue) ![Deployed](https://img.shields.io/badge/Deployed-Cloud%20Run-blue)

## 🌐 **Live Demo**

**Your Video Summarizer AI is now live and ready to use!**

- **🌐 Web Interface**: [https://video-summarizer-282723408863.us-central1.run.app](https://video-summarizer-282723408863.us-central1.run.app)
- **🏥 Health Check**: `https://video-summarizer-282723408863.us-central1.run.app/health`

### 🚀 **Try It Now**

1. Visit the web interface above
2. Enter any video URL
3. Add a custom prompt (optional)
4. Click "Generate Summary"
5. Get your AI-powered summary instantly!

## 📋 Table of Contents

- [Live Demo](#-live-demo)
- [Features](#-features)
- [Project Structure](#-project-structure)
- [File Descriptions](#-file-descriptions)
- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
- [Configuration](#-configuration)
- [Usage](#-usage)
- [Deployment](#-deployment)
- [API Reference](#-api-reference)
- [Development](#-development)
- [Security](#-security)
- [Troubleshooting](#-troubleshooting)
- [Contributing](#-contributing)

## ✨ Features

### 🎨 **Web Interface**

- **Modern UI**: Beautiful, responsive design with animations
- **Real-time Processing**: Live feedback during video analysis
- **Custom Prompts**: Flexible summarization instructions
- **Example Templates**: Pre-built prompt suggestions
- **Progress Tracking**: Visual progress indicators and timeouts
- **Mobile Responsive**: Works perfectly on all devices

### 🛠️ **Technical Features**

- **AI-Powered**: Uses Google Gemini 2.0 Flash model
- **Multiple Formats**: Supports various video formats and URLs
- **Rate Limiting**: Prevents API abuse and controls costs
- **Security**: API key protection and input validation
- **Error Handling**: Comprehensive error management
- **Performance**: Optimized for speed and reliability

### 📱 **Command Line Interface**

- **Quick Processing**: Fast video summarization from terminal
- **Batch Support**: Process multiple videos efficiently
- **Custom Prompts**: Flexible command-line arguments

## 📁 Project Structure

```
video-summarizer-app/
├── src/
│   ├── index.ts          # CLI entry point
│   └── server.ts         # Web server and API
├── public/
│   └── index.html        # Web interface
├── package.json          # Dependencies and scripts
├── README.md            # This file
├── SECURITY.md          # Security guidelines
└── node_modules/        # Dependencies (auto-generated)
```

## 📄 File Descriptions

### 🖥️ **Core Application Files**

#### `src/index.ts` - Command Line Interface

**Purpose**: Entry point for CLI video summarization
**Key Functions**:

- Parses command-line arguments (video URL, custom prompt)
- Initializes Gemini AI with API key
- Processes video and outputs summary to console
- Handles errors and validation

**Usage**:

```bash
npm run cli <video_url> [custom_prompt]
```

#### `src/server.ts` - Web Server & API

**Purpose**: Express.js server providing web interface and API endpoints
**Key Functions**:

- Serves static web files
- Provides `/api/summarize` endpoint for video processing
- Implements rate limiting (10 requests/15min per IP)
- Security headers and input validation
- Timeout handling (5-minute limit)
- API key management and masking

**Endpoints**:

- `GET /` - Serves web interface
- `POST /api/summarize` - Processes video and returns summary

#### `public/index.html` - Web User Interface

**Purpose**: Complete web application with modern UI
**Key Features**:

- Responsive two-column layout
- Form validation and error handling
- Real-time loading states and animations
- Example prompt templates
- Progress tracking and timeout warnings
- Mobile-optimized design

**Sections**:

- **Left Column**: Input form with URL, prompts, and controls
- **Right Column**: Results display with loading states
- **Animations**: Entrance effects, hover states, transitions

### 📦 **Configuration Files**

#### `package.json` - Project Configuration

**Purpose**: Defines project metadata, dependencies, and scripts
**Key Sections**:

- **Dependencies**: Production packages (Express, Genkit, etc.)
- **Dev Dependencies**: Development tools (TypeScript, TSX)
- **Scripts**: npm commands for running the application
- **Type**: ES modules configuration

**Available Scripts**:

```bash
npm start      # Start production server
npm run dev    # Start development server with hot reload
npm run cli    # Run command-line interface
npm run build  # Build TypeScript code
```

#### `SECURITY.md` - Security Guidelines

**Purpose**: Comprehensive security documentation
**Contents**:

- API key usage and protection
- Security best practices
- Rate limiting configuration
- Production deployment checklist
- Key rotation procedures

## 🔧 Prerequisites

### Required Software

- **Node.js** (v18 or higher)
- **npm** (comes with Node.js)
- **Git** (for cloning)

### Required Accounts

- **Google AI Studio Account**: For Gemini API access
- **Google Cloud Project**: For API key management

### System Requirements

- **RAM**: Minimum 512MB, Recommended 1GB+
- **Storage**: 100MB free space
- **Network**: Stable internet connection for API calls

## 🚀 Installation

### Step 1: Clone the Repository

```bash
git clone <repository-url>
cd video-summarizer-app
```

### Step 2: Install Dependencies

```bash
npm install
```

### Step 3: Get API Key

1. Visit [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Sign in with your Google account
3. Click "Create API Key"
4. Copy the generated key

### Step 4: Configure API Key

#### Option A: Environment Variable (Recommended)

```bash
export GEMINI_API_KEY=your_api_key_here
```

#### Option B: .env File

```bash
echo "GEMINI_API_KEY=your_api_key_here" > .env
```

#### Option C: Permanent Setup (macOS/Linux)

```bash
echo 'export GEMINI_API_KEY=your_api_key_here' >> ~/.zshrc
source ~/.zshrc
```

### Step 5: Verify Installation

```bash
npm run cli https://example.com/video.mp4 "Test prompt"
```

## ⚙️ Configuration

### Environment Variables

| Variable         | Description           | Required | Default |
| ---------------- | --------------------- | -------- | ------- |
| `GEMINI_API_KEY` | Google Gemini API key | ✅ Yes   | None    |
| `PORT`           | Server port           | ❌ No    | 3000    |

### Rate Limiting

- **Requests per IP**: 10 per 15 minutes
- **Timeout**: 5 minutes per video
- **Concurrent requests**: Limited by server capacity

### Security Settings

- **API Key Masking**: Only first 10 and last 4 characters shown in logs
- **Security Headers**: XSS protection, content type options
- **Input Validation**: URL validation and sanitization

## 📖 Usage

### 🌐 Web Interface (Recommended)

#### Start the Server

```bash
npm start
```

#### Access the Application

1. Open your browser
2. Navigate to `http://localhost:3000`
3. Enter a video URL
4. Add custom prompt (optional)
5. Click "Generate Summary"

#### Features

- **Example Prompts**: Click to use pre-built templates
- **Progress Tracking**: Real-time processing feedback
- **Error Handling**: Clear error messages and suggestions
- **Reset Function**: Clear form and start over

### 💻 Command Line Interface

#### Basic Usage

```bash
npm run cli <video_url>
```

#### With Custom Prompt

```bash
npm run cli <video_url> "Summarize the key points in bullet points"
```

#### Examples

```bash
# Basic summary
npm run cli https://www.youtube.com/watch?v=example

# Detailed analysis
npm run cli https://example.com/video.mp4 "What are the main takeaways?"

# Bullet points
npm run cli https://example.com/video.mp4 "Summarize in bullet points"
```

### 🎯 Example Prompts

#### Quick Summaries

- "Summarize the key points of this video in bullet points"
- "What are the main takeaways from this video?"
- "Create a brief overview of this content"

#### Detailed Analysis

- "Create a detailed summary with timestamps"
- "Explain the concepts discussed in this video in simple terms"
- "What are the key insights and actionable items?"

## 🔌 API Reference

### Endpoint: `POST /api/summarize`

#### Request Body

```json
{
  "videoURL": "https://example.com/video.mp4",
  "prompt": "Please summarize this video"
}
```

#### Response

```json
{
  "summary": "This video discusses..."
}
```

#### Error Response

```json
{
  "error": "Error message",
  "details": "Additional details"
}
```

#### Status Codes

- `200`: Success
- `400`: Bad request (missing URL)
- `408`: Timeout
- `429`: Rate limit exceeded
- `500`: Server error

## 🛠️ Development

### Development Server

```bash
npm run dev
```

- Hot reload enabled
- Automatic TypeScript compilation
- Real-time error reporting

### Building for Production

```bash
npm run build
```

### Code Structure

- **TypeScript**: Full type safety
- **ES Modules**: Modern JavaScript modules
- **Express.js**: Web server framework
- **Genkit**: Google AI integration

### Adding Features

1. **Frontend**: Modify `public/index.html`
2. **Backend**: Update `src/server.ts`
3. **CLI**: Edit `src/index.ts`
4. **Dependencies**: Update `package.json`

## 🔒 Security

### API Key Protection

- ✅ Environment variable storage
- ✅ Masked logging (first 10, last 4 characters)
- ✅ No client-side exposure
- ✅ Rate limiting protection

### Input Validation

- ✅ URL format validation
- ✅ Content type checking
- ✅ Size limits and timeouts
- ✅ XSS protection

### Best Practices

- ✅ Regular key rotation
- ✅ Usage monitoring
- ✅ Error logging
- ✅ Security headers

## 🤝 Contributing

### Development Setup

1. Fork the repository
2. Create feature branch: `git checkout -b feature-name`
3. Make changes and test
4. Commit: `git commit -m 'Add feature'`
5. Push: `git push origin feature-name`
6. Submit pull request

### Code Standards

- **TypeScript**: Use strict mode
- **ESLint**: Follow linting rules
- **Prettier**: Consistent formatting
- **Tests**: Add tests for new features

### Pull Request Guidelines

- Clear description of changes
- Include screenshots for UI changes
- Test on multiple browsers/devices
- Update documentation if needed

### Useful Links

- [Google AI Studio](https://makersuite.google.com/app/apikey)
- [Genkit Documentation](https://genkit.dev/)
- [Express.js Guide](https://expressjs.com/)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/)

---

**Made with ❤️ using Google Gemini AI & Genkit**
