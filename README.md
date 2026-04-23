1. Project Title & Description
ชื่อโปรเจค: RT War Report (Real-Time War Report)
(Tagline): ระบบแจ้งเตือนและสรุปสถานการณ์ความขัดแย้งทั่วโลกแบบเรียลไทม์ด้วย AI ผ่าน LINE
ภาพรวม:โปรเจคนี้ทำหน้าที่ (ดึงข่าว -> สรุปด้วย AI -> แจ้งเตือน -> ตอบคำถาม)
2. Key Features (ฟีเจอร์หลัก)
Real-time Alerts: แจ้งเตือนเหตุการณ์สำคัญทันทีผ่าน LINE Messaging API
AI Summarization: สรุปเนื้อหาข่าวที่ซับซ้อนให้เข้าใจง่ายใน 3-5 บรรทัด
Sentiment & Credibility Filter: กรองข่าวปลอมและวิเคราะห์โทนของข่าว
Interactive Chatbot: ผู้ใช้สามารถสอบถามรายละเอียดเพิ่มเติมเกี่ยวกับเหตุการณ์เฉพาะเจาะจงได้
Multi-source Aggregation: ดึงข้อมูลจากแหล่งข่าวที่เชื่อถือได้ทั่วโลกผ่าน Event Registry
วิธีการติดตั้ง แอดไลน์ 
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
