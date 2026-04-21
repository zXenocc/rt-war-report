ระบบแจ้งเตือนและสรุปสถานการณ์ความขัดแย้งทั่วโลกแบบเรียลไทม์ ผ่าน LINE Messaging API โดยใช้ n8n และเทคโนโลยี AI ในการวิเคราะห์ข้อมูล
Overview (Information Overload) และข่าวปลอมแพร่กระจายอย่างรวดเร็ว RT War Report ถูกสร้างขึ้นเพื่อเป็นตัวกรองข้อมูลที่เชื่อถือได้ ช่วยให้ประชาชน นักเดินทาง หรือนักธุรกิจที่ได้รับผลกระทบจากความตึงเครียดทางภูมิรัฐศาสตร์ สามารถรับรู้เหตุการณ์สำคัญได้ทันท่วงที พร้อมบทสรุปที่เข้าใจง่ายและระบบถาม-ตอบอัจฉริยะ

✨ Key Features
• Real-time Alerts: แจ้งเตือนด่วน (Push Notification) เมื่อมีเหตุการณ์สำคัญเกิดขึ้น
• AI Summarization: สรุปเนื้อหาข่าวที่ยาวและซับซ้อนให้เหลือเพียงประเด็นสำคัญที่ต้องรู้
• Sentiment & Credibility Analysis: วิเคราะห์ระดับความรุนแรงและกรองข่าวซ้ำ/ข่าวปลอมเบื้องต้น
• Interactive AI Agent: ผู้ใช้สามารถพิมพ์ถามรายละเอียดเพิ่มเติมเกี่ยวกับสถานการณ์ผ่าน LINE ได้โดยตรง
• Verified Sources: ดึงข้อมูลจากแหล่งข่าวที่ผ่านการจัดกลุ่มและยืนยันแล้วผ่าน Event Registry API
⚙️ Tech Stack & Workflow
โปรเจคนี้ขับเคลื่อนด้วยการ Automate ข้อมูลผ่าน n8n โดยมีโครงสร้างดังนี้:
1. Trigger:
• Schedule: ดึงข้อมูลข่าวสารใหม่ทุก 1-3 ชั่วโมง
• Webhook: รับข้อความจากผู้ใช้งานผ่าน LINE Messaging API
2. Processing (n8n Nodes):
• Event Registry API: ดึงข้อมูลเหตุการณ์ (Events) ตาม Keyword ที่เกี่ยวข้องกับความขัดแย้ง
• AI Agent (Gemini/OpenAI): * สรุปเนื้อหาข่าว (Summarization)
• วิเคราะห์ความรู้สึกและระดับภัยคุกคาม (Sentiment Analysis)
• เป็นสมองหลักในการตอบคำถามผู้ใช้ (RAG Processing)
• Code Node: จัดการโครงสร้าง JSON และกรองข้อมูลดิบให้พร้อมใช้งาน
3. Output:
• LINE Official Account: ส่งข้อความแจ้งเตือนและโต้ตอบกับผู้ใช้
🎯 Target Audience
• Risk Area Residents: ผู้ที่อาศัยอยู่ในพื้นที่เสี่ยงภัย
• Business & Supply Chain: นักธุรกิจที่ต้องประเมินความเสี่ยงในการขนส่งและทรัพยากร
• News Enthusiasts: ผู้ที่ต้องการติดตามสถานการณ์โลกอย่างใกล้ชิดและถูกต้อง
• Travelers: นักเดินทางที่ต้องการตรวจสอบความปลอดภัยของจุดหมายปลายทาง
Installation & Setup (For Developers)
Clone Repository: 
git clone https://github.com/"ชื่อโปรเจ็ค"
Prerequisites:
ติดตั้ง n8n (Self-hosted หรือ Cloud)
สมัคร API Key สำหรับ Event Registry (NewsAPI.ai)
สร้างบัญชี LINE Developers และตั้งค่า Messaging API
เตรียม API Key สำหรับ AI Model (Google AI Studio หรือ OpenAI)
Import Workflow
นำไฟล์ workflow.json เข้าไปใน n8n
ตั้งค่า Environment Variables สำหรับ API Keys ต่างๆ
```mermaid
graph TD
    %% Start Node
    Start([Start]) --> TriggerSystem[Trigger System]

    %% Input Section
    TriggerSystem --> Schedule["<b>Schedule Trigger</b><br/>(ดึงข่าวทุก 1-3 ชม.)"]
    TriggerSystem --> Webhook["<b>Webhook Trigger (LINE)</b><br/>(ผู้ใช้ส่งข้อความมา)"]

    %% Processing Section
    Schedule --> API[Call API: Event Registry]
    Webhook --> API

    API --> RawData[/Raw News Data/]
    
    RawData --> CodeNode{{"<b>Code Node (Data Processing)</b><br/>- Clean Data<br/>- Remove Duplicate<br/>- Filter Conflict/War Only"}}
    
    CodeNode --> AIAgent[<b>AI Agent Processing</b><br/>- Summarize ข่าว<br/>- วิเคราะห์ Sentiment<br/>- ตรวจความน่าเชื่อถือ<br/>- ตอบคำถาม]

    %% Decision Logic
    AIAgent --> Decision{Decision Node}

    Decision -- ข่าวสำคัญ --> AutoAlert[<b>Auto Alert Mode</b>]
    Decision -- ตอบคำถามผู้ใช้ --> UserQuery[<b>User Query Mode</b>]

    %% Output Section
    AutoAlert --> Format[<b>Format Message</b><br/>สรุปสั้น + ระดับความรุนแรง + พื้นที่]
    UserQuery --> Format

    Format --> LineAPI[Send via LINE Messaging API]
    LineAPI --> UserReceive([User Receive Notification])
    
    UserReceive --> EndLoop([End / Loop])

    %% Styling (ทำให้ดูสวยขึ้น)
    style Start fill:#f9f,stroke:#333,stroke-width:2px
    style EndLoop fill:#f9f,stroke:#333,stroke-width:2px
    style Decision fill:#fff4dd,stroke:#d4a017,stroke-width:2px
    style AIAgent fill:#e1f5fe,stroke:#01579b,stroke-width:2px
    style CodeNode fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px
```
