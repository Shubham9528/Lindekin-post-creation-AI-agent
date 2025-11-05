# LinkedIn Automation Workflow

An intelligent automation system that transforms post ideas into polished LinkedIn content with AI-generated visuals, powered by Make.com (formerly Integromat).

## 🎯 Overview

This workflow automates the entire LinkedIn content creation process:
- Reads post ideas from Google Sheets
- Generates professional LinkedIn posts using Google Gemini AI
- Creates custom image prompts for visual content
- Generates images using Ideogram AI
- Uploads images to Google Drive
- Updates the spreadsheet with generated content and status


<img width="1647" height="657" alt="image" src="https://github.com/user-attachments/assets/61ec4ffa-bc6c-4e7e-8280-31618bc889b2" />


##Certificate by outskill
<img width="747" height="465" alt="image" src="https://github.com/user-attachments/assets/18c4af16-8270-4199-b8e5-0064aa64963b" />


## 🏗️ Architecture

### Workflow Components

```
Google Sheets → Router → [Route 1] LinkedIn Post Generation
                      → [Route 2] Content Retrieval & Update
```

#### Route 1: AI Content Generation
1. **Google Sheets Filter** - Reads post ideas from spreadsheet
2. **Router** - Directs flow to appropriate processing route
3. **Gemini AI (Post Generator)** - Creates LinkedIn post from idea
4. **Gemini AI (Image Prompt)** - Generates image generation prompt
5. **Ideogram AI** - Creates visual content based on prompt
6. **Google Drive Upload** - Stores generated image
7. **Google Sheets Update** - Updates row with post, image link, and status

#### Route 2: Alternative Flow
1. **Google Drive Get File** - Retrieves existing content
2. **Google Sheets Update** - Updates spreadsheet with retrieved data

## 📋 Prerequisites

### Required Accounts & Connections
- **Google Account** - For Sheets and Drive integration
- **Google Gemini API** - For AI content generation
- **Ideogram AI Account** - For image generation
- **Make.com Account** - To run the automation

### Google Sheets Structure

Your spreadsheet should have the following columns:

| Column | Name | Description |
|--------|------|-------------|
| A | Post Idea | Original content idea/topic |
| B | LinkedIn Post Draft | AI-generated LinkedIn post |
| C | Facebook Post Draft | (Optional) Facebook version |
| D | Channel | Target platform |
| E | Image Link | Google Drive link to generated image |
| F | Control | Status field ("Ready to review", etc.) |

## 🚀 Setup Instructions

### 1. Import Blueprint to Make.com

1. Log in to your Make.com account
2. Create a new scenario
3. Click on the three dots menu → "Import Blueprint"
4. Upload `Linkedin Automation.blueprint.json`

### 2. Configure Connections

#### Google Sheets Connection
- **Connection Type**: `google`
- **Spreadsheet ID**: Update to your spreadsheet ID
- **Sheet Name**: Default is "Sheet1" (modify if needed)

#### Google Drive Connection
- **Connection Type**: `google-restricted`
- **Folder ID**: Set your target folder for image uploads

#### Gemini AI Connection
- **Connection Name**: "Social media Automation"
- **Model**: `gemini-2.5-flash`
- **API Key**: Add your Gemini API key in Make.com

#### Ideogram AI Connection
- **API Key**: Configure in Make.com connections

### 3. Customize AI Prompts

#### LinkedIn Post Generator Prompt
The system uses a sophisticated copywriting framework:
- **Voice**: Conversational-authority tone
- **Structure**: Hook → Context → Insight → Takeaway → CTA
- **Length**: 200-350 words
- **Format**: Mobile-optimized with emojis and bold text

#### Image Prompt Generator
Creates scroll-stopping visuals optimized for:
- **Aspect Ratio**: 4:5 or 16:9 for LinkedIn
- **Style**: Professional but eye-catching
- **Quality**: High contrast for mobile viewing

### 4. Set Trigger Schedule

Configure when the automation runs:
- Manual trigger (on-demand)
- Scheduled (e.g., daily at specific time)
- Webhook trigger (when sheet is updated)

## 🎨 AI Copywriting Framework

### LinkedIn Post Structure

```
🔥 Hook (1-2 lines)
- Provocative question, contrarian claim, or surprise stat
- Max 120 characters

📖 Context Story (2-3 lines)
- Include metric, year, or brand reference
- Set up the insight

💡 Insight/Framework (4-7 bullets)
- **Bold Keyword** – 12-word descriptor
- Actionable takeaways

✅ Application (1-2 lines)
- Turn insight into immediate action

❓ CTA (1 line)
- Question, poll, or challenge
```

### Voice Guidelines
- **Tone**: Coach-like, direct, zero fluff
- **Syntax**: Sentences ≤ 30 words
- **Evidence**: Hard numbers and concrete examples
- **Formatting**: 1 emoji per section, blank lines between blocks

## 🖼️ Image Generation Strategy

### Visual Best Practices
- **Format**: 1200x627px or 1080x1350px (4:5)
- **Style**: Clean minimalism with bold focal points
- **Composition**: High contrast for mobile screens
- **Avoid**: Generic stock photos, cluttered layouts

### Prompt Structure
- Main subject embodying core insight
- Style & mood (photography style, emotional tone)
- Composition (layout, perspective)
- Color palette (2-4 dominant colors)
- Lighting specifications
- Technical specs (camera angle, depth of field)

## 📊 Workflow Execution

### Process Flow

1. **Trigger**: Automation starts (manual/scheduled)
2. **Read**: Fetches rows from Google Sheets
3. **Route Decision**: Determines processing path
4. **Generate Post**: AI creates LinkedIn content
5. **Generate Prompt**: AI creates image description
6. **Create Image**: Ideogram generates visual
7. **Upload**: Saves image to Google Drive
8. **Update**: Writes back to spreadsheet with:
   - Generated LinkedIn post (Column B)
   - Image Drive link (Column E)
   - Status: "Ready to review" (Column F)

### Error Handling
- **Max Errors**: 3 per execution
- **Auto Commit**: Enabled
- **Sequential Processing**: Disabled (parallel execution)

## 🔧 Customization Options

### Modify AI Behavior

**Post Tone**: Edit system instructions in module #2
```json
"system_instruction": {
  "parts": [{
    "text": "Your custom instructions here..."
  }]
}
```

**Image Style**: Edit system instructions in module #3
```json
"system_instruction": {
  "parts": [{
    "text": "Your visual strategy here..."
  }]
}
```

### Adjust Filters
Add conditions to process only specific rows:
- Filter by status column
- Filter by channel type
- Filter by date range

### Change Output Columns
Modify the `values` mapping in module #7:
```json
"values": {
  "1": "{{2.result}}",        // Column B: LinkedIn Post
  "4": "{{6.id}}",            // Column E: Image Link
  "5": "Ready to review"      // Column F: Status
}
```

## 🔐 Security & Best Practices

### API Key Management
- Store API keys securely in Make.com connections
- Never commit API keys to version control
- Rotate keys periodically

### Data Privacy
- Ensure Google Sheets permissions are properly configured
- Review Make.com data retention policies
- Consider GDPR compliance for user data

### Rate Limits
- **Gemini API**: Monitor usage quotas
- **Ideogram API**: Check generation limits
- **Google APIs**: Respect rate limits

## 📈 Monitoring & Optimization

### Track Performance
- Monitor execution history in Make.com
- Check error logs for failed runs
- Review generated content quality

### Optimization Tips
1. **Batch Processing**: Process multiple rows per run
2. **Conditional Logic**: Skip already-processed rows
3. **Error Notifications**: Set up email alerts for failures
4. **Content Review**: Implement approval workflow before posting

## 🐛 Troubleshooting

### Common Issues

**Connection Errors**
- Verify all API keys are valid
- Check Google account permissions
- Ensure spreadsheet is accessible

**AI Generation Issues**
- Check Gemini API quota
- Verify prompt formatting
- Review model availability

**Image Upload Failures**
- Confirm Drive folder permissions
- Check file size limits
- Verify connection scope

**Sheet Update Problems**
- Validate spreadsheet ID
- Check column range settings
- Ensure row numbers are correct

## 📝 Example Usage

### Input (Column A - Post Idea)
```
The importance of async communication in remote teams
```

### Output (Column B - Generated Post)
```
🔥 Your team's biggest productivity killer isn't meetings.

It's the expectation of instant responses.

I analyzed 50+ remote teams over 18 months.
The pattern was clear: async-first cultures shipped 40% faster.

Here's the framework that works:

**Default to Writing** – Document decisions in shared spaces
**Respect Focus Time** – No "quick questions" during deep work
**Set Response SLAs** – 4-hour windows, not 4 minutes
**Record Everything** – Meetings become searchable artifacts

The shift isn't easy. But it's worth it.

What's one async practice your team swears by? 👇
```

### Output (Column E - Image Link)
```
https://drive.google.com/file/d/[generated-file-id]
```

## 🤝 Contributing

To improve this automation:
1. Test modifications in a separate Make.com scenario
2. Document changes in this README
3. Export updated blueprint
4. Share improvements with the team

## 📄 License

This automation blueprint is provided as-is for internal use.

## 🔗 Resources

- [Make.com Documentation](https://www.make.com/en/help/home)
- [Google Gemini API](https://ai.google.dev/)
- [Ideogram AI](https://ideogram.ai/)
- [Google Sheets API](https://developers.google.com/sheets/api)
- [LinkedIn Best Practices](https://business.linkedin.com/marketing-solutions/best-practices)

## 📞 Support

For issues or questions:
- Check Make.com execution logs
- Review API documentation
- Contact automation team lead

---

**Version**: 1.0  
**Last Updated**: 2024  
**Platform**: Make.com (eu2.make.com)


