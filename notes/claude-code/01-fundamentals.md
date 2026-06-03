1. 7 levels pyramids to become claude code expert
    1.1 Foundation(Installing & Running Claude code)
        - ลงผ่าน CMD ด้วย NPM ก็ได้สำหรับ Windows
        - Install application desktop โดยโหลดจาก official website ก็ได้ 
    1.2 Pick your AI teammate 
        - สิ่งสำคัญที่สุดคือเลือก AI ให้เหมาะกับงาน
        - Opus 4.8 → "Senior Engineer": เหมาะกับงานวางแผนหรือ ambiguous task (ใช้ token เยอะ)
        - Sonnet 4.6 → "Engineer": สมดุลระหว่างความสามารถกับความเร็ว เหมาะงานทั่วไป
        - Haiku 4.5 → "Junior": เร็วและถูก เหมาะงานเล็กที่ไม่ซับซ้อน
    1.3 Setup AI team rule 
        - สร้างไฟล์ที่ชื่อ claude.md ที่ root ของโปรเจคเพื่อเป็น Instruction ให้ AI
        - More detail include, the better result you'll get.
        - เพิ่มประสิทธิภาพด้วยการสร้าง strategy ต่างๆ เช่น Branching, Commit style, Coding guidline, หรือ testing rule เป็นต้น
        - สร้าง .md แยกไว้สำหรับ prompt ที่ใช้บ่อย แล้ว import เข้า claude.md หลักด้วย @filename
            - ตัวอย่าง: มี testing.md ที่กำหนด rule ว่าทุก UI Component ต้องมี unit test + web driver test
            - เวลา prompt แค่เพิ่ม @testing.md ต่อท้าย แทนที่จะพิมพ์ rule ซ้ำทุกครั้ง
    1.4 AI debugging(UI&CSS)
        - แคปรูปให้ AI แก้ไข CSS บางอย่างได้เลยเช่นสีของปุ่มเป็นต้น
    1.5 AI Enhanced Multitasking
        - Messaging Queue features ของ Claude Code ช่วยให้เราพิมพ์ prompt ต่อๆกันได้เลยโดยที่เราไม่ต้องรอให้ process ของ prompt ก่อนหน้าทำงานจนเสร็จก่อน
    1.6 Ultra planning
        - Feature ที่ทรงพลังที่สุดของ Claude คือ Plan mode ทุกครั้งที่เรา prompt อะไรไปมันจะไม่ได้ code เลยทันทีแต่จะวิเคราะห์ก่อนลงมือทำ
        - มี 3 levels — ใส่ keyword เหล่านี้ลงใน prompt ได้เลย (ยิ่งสูง ยิ่งกิน token มาก):
            - `think` → วิเคราะห์ทั่วไป
            - `think harder` → วิเคราะห์ลึกขึ้น
            - `ultrathink` → วิเคราะห์เต็มที่ที่สุด
        - สามารถ prompt ให้สร้าง sub-agents ได้ เพราะงาน 1 task จริงๆ ใช้ dev หลายคน (FE, BE, DBA)
            - แค่ระบุใน prompt ว่าต้องการ agent กี่ตัว แต่ละตัวทำอะไร Claude จะแบ่งงานให้เอง
    1.7 AI Enhanced Collaborations
        - ตัวอย่างที่เห็นได้ชัดเจนที่สุดตัวอย่างนึงคือ Github หากเรา implement Claude ด้วย Github actions เราสามารถให้ Claude ช่วยรีวิวโค้ดหรือ scan security issues ได้เลยโดยแค่แท็ก @claude ใน comment ของ PR นั้นๆ
    1.8 หลักการเขียน claude.md ที่ดีจะกล่าวถึงในภายหลังในข้อ 2.2