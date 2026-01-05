# PPT AI Gen Project
## 1. Project Overview
PPT AIGEN is an AI-powered automated PPT generation system that converts natural language prompts into well-structured PPTX files. The system adopts a front-end and back-end separation architecture, with the back-end built on FastAPI to provide asynchronous task processing capabilities, and the front-end interacting with the back-end through RESTful APIs to achieve functions such as PPT generation task creation, status query, file download, and generation report viewing.
### Core Features
Asynchronous PPT generation: Avoid front-end request blocking by processing PPT generation tasks asynchronously
Task lifecycle management: Full-process tracking of task status (queued, content generation, rendering, completion, failure)
Persistent task storage: In-memory storage combined with file persistence to ensure task information is not lost after service restart
Multi-parameter customization: Support template selection, language setting, content density adjustment and other customization options
Detailed report generation: Record slide-level generation details (such as text overflow handling) and time-consuming statistics
