# 🔒 Security Guide - Video Summarizer AI

## 🔑 API Key Usage

### How the API Key is Used

The Gemini API key is used in the following way:

1. **Environment Variable**: Stored as `GEMINI_API_KEY` environment variable
2. **Server Startup**: Validated when the server starts
3. **Genkit Integration**: Automatically used by the Google AI plugin
4. **Video Processing**: Used for each video summarization request

### Current Implementation

```typescript
// 1. Environment variable check
if (!process.env.GEMINI_API_KEY) {
  console.error("❌ GEMINI_API_KEY environment variable is not set!");
  process.exit(1);
}

// 2. Masked logging for security
const maskedKey = `${apiKey.substring(0, 10)}...${apiKey.substring(
  apiKey.length - 4
)}`;
console.log(`🔑 API Key configured: ${maskedKey}`);

// 3. Genkit initialization
const ai = genkit({
  plugins: [googleAI()], // Automatically uses GEMINI_API_KEY
  model: googleAI.model("gemini-2.0-flash")
});
```

## 🛡️ Security Features

### ✅ Implemented Security Measures

1. **API Key Masking**: Only first 10 and last 4 characters shown in logs
2. **Rate Limiting**: 10 requests per 15 minutes per IP
3. **Security Headers**: XSS protection, content type options, frame options
4. **Input Validation**: URL validation and sanitization
5. **Timeout Protection**: 5-minute timeout for video processing
6. **Error Handling**: Secure error messages without exposing internals

### 🔒 Rate Limiting Configuration

```typescript
const limiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 10, // 10 requests per IP per window
  message: {
    error: "Too many requests from this IP, please try again later.",
    details: "Rate limit exceeded. Please wait 15 minutes before trying again."
  }
});
```

## ⚠️ Security Best Practices

### Do's ✅

- ✅ Use environment variables for API keys
- ✅ Set up rate limiting to prevent abuse
- ✅ Mask sensitive data in logs
- ✅ Validate all user inputs
- ✅ Use HTTPS in production
- ✅ Regularly rotate API keys
- ✅ Monitor API usage and costs

### Don'ts ❌

- ❌ Never commit API keys to version control
- ❌ Don't expose API keys in client-side code
- ❌ Don't log full API keys
- ❌ Don't share API keys publicly
- ❌ Don't use the same key for multiple applications

## 🚀 Production Deployment

### Environment Setup

```bash
# Set API key securely
export GEMINI_API_KEY=your_api_key_here

# Or use a .env file (add to .gitignore)
echo "GEMINI_API_KEY=your_api_key_here" > .env
```

### Security Checklist

- [ ] API key stored in environment variables
- [ ] Rate limiting enabled
- [ ] Security headers configured
- [ ] HTTPS enabled (for production)
- [ ] API key monitoring set up
- [ ] Regular security audits scheduled

## 📊 API Usage Monitoring

### Current Monitoring

- Server logs show masked API key status
- Rate limiting logs show abuse attempts
- Processing time tracking
- Error logging for debugging

### Recommended Monitoring

- Set up Google Cloud Console monitoring
- Track API usage and costs
- Monitor for unusual activity
- Set up alerts for high usage

## 🔄 Key Rotation

### When to Rotate

- Every 90 days (recommended)
- If key is compromised
- When changing applications
- After security incidents

### How to Rotate

1. Generate new API key in Google AI Studio
2. Update environment variable
3. Restart application
4. Monitor for any issues
5. Delete old key after confirmation

---

**Remember**: API keys are sensitive credentials. Always treat them with the same security as passwords!
