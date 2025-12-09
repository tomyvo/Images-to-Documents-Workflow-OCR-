# 🖼️➡️📄 Images to Documents Workflow (OCR)

Welcome to the **Images to Docs** workflow built in **n8n**! This workflow automatically converts images uploaded to a Google Drive folder into structured text documents using **OCR (Optical Character Recognition)**. Currently, tables are not supported, but it efficiently extracts plain text from images and outputs clean, formatted files.

---

## 🌈 Workflow Overview

This workflow is designed to **detect new images**, **extract text**, **format it intelligently**, and **save it back to Google Drive** as a document file.  

### High-Level Steps:
1. **Trigger**: Detects when new files are added to a specific Google Drive folder.
2. **Download**: Fetches the file content for processing.
3. **OCR Processing**: Uses [OCR.Space API](https://ocr.space/) to convert images to text.
4. **Text Cleanup**: Cleans and formats the OCR output for readability.
5. **Convert to File**: Transforms the cleaned text into a downloadable file.
6. **Upload**: Saves the processed file back to Google Drive.

---

## 🚀 Node Details

| Node Name | Purpose | Key Features |
|-----------|---------|-------------|
| **Triggers when something was created** | Watches Google Drive folder | Fires on new file creation |
| **Download file** | Downloads new file | Supports any binary file type |
| **Space OCR** | Sends image to OCR.Space API | Extracts text from images; supports multiple languages (currently German) |
| **Extracts only Text** | Filters parsed OCR text | Keeps only the text, removing extra JSON or metadata |
| **Code in JavaScript** | Cleans and formats text | Fixes line breaks, removes extra spaces, adds logical breaks based on keywords or symbols |
| **Convert to File** | Converts cleaned text to a downloadable file | Outputs text as a proper file object |
| **Upload file** | Saves the final document to Google Drive | Can specify folder and file name |

---

## 🎨 Features

- **Automated Image Detection**: Monitors a Google Drive folder continuously.
- **OCR Text Extraction**: Extracts text accurately from images.
- **Intelligent Text Cleanup**: Handles line breaks, removes excess spaces, and formats content for readability.
- **Output as Document**: Creates a clean, downloadable text file from images.
- **Google Drive Integration**: Automatically uploads processed documents back to Drive.

---

## 💡 Text Cleanup Logic

The JavaScript node ensures the text is readable by:

1. Converting all escape sequences (`\r\n`, `\n`, `\r`) into proper line breaks.  
2. Reducing multiple spaces and tabs to a single space.  
3. Adding line breaks after key patterns like:  
   - Currency symbols (€, $)  
   - Invoice-related keywords (`Invoice`, `Customer`, `Total`, `Date`, etc.)  
   - New sentences starting with capital letters.  
4. Removing excessive consecutive line breaks.  
5. Trimming leading and trailing whitespace.

This ensures your OCR output is **structured and professional**.

---

## ⚡ Setup Instructions

1. **Google Drive OAuth2**:  
   - Add your credentials in n8n.
   - Specify the folder to monitor for new image files.

2. **OCR.Space API**:  
   - Sign up at [OCR.Space](https://ocr.space/ocrapi) and get an API key.
   - Insert the API key in the HTTP Request node.

3. **Workflow Activation**:  
   - Enable the workflow in n8n.
   - New images will automatically be processed and saved back to Google Drive.

---

## 📌 Notes

- Supports **multiple image formats** (PNG, JPG, JPEG, etc.).
- Currently, **tables and structured data are not extracted**.
- Language is configurable; currently set to **German** (`ger`) in the OCR API.
- Ideal for digitizing invoices, receipts, scanned documents, and notes.

---

## 🌟 References

- [n8n Documentation](https://docs.n8n.io/)  
- [OCR.Space API](https://ocr.space/ocrapi)  
- [Google Drive API](https://developers.google.com/drive/api)  

---

## 🎉 License

MIT License – free to use, adapt, and share for personal or business workflows.
