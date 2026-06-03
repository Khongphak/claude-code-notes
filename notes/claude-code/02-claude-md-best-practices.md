2. How to use claude.md
    2.1 หากไม่มี claude.md ใน project เท่ากับเราวางดาบกับโล่ไว้ในห้องทำครัวก่อนไปออกรบ เพราะมันคือสิ่งที่ช่วยบอก Project Architecture, Code standard, หรือ สิ่งที่เคยทำผิดพลาดไป
        2.1.1 ถือได้ว่าเป็น memory system ของ Claude code เลย
        2.1.2 Claude code มี Memory hierachy ซึ่งเป็นตัวกำหนด priority อยู่(ตัวไหน priority สูงกว่าตัวนั้นชนะ) ได้แก่
            a. Managed Policy (All users in organization)
                - Organization-wide instructions managed by IT/DevOps
                - macOS: /Library/Application Support/ClaudeCode/CLAUDE.md หรือ Windows: C:\Program Files\ClaudeCode\CLAUDE.md
            b. User instructions (Just you (all projects))
                - Personal preferences for all projects
                - ~/.claude/CLAUDE.md
            c. Project instructions (Team members via source control)
                - Team-shared instructions for the project
                - ./CLAUDE.md or ./.claude/CLAUDE.md
            d. Local instructions (Just you (current project))
                - Personal project-specific preferences; add to .gitignore
                - ./CLAUDE.local.md
        2.1.3 Claude สามารถ import ไฟล์อื่นๆหรือ external URL ได้เพื่อให้ .md ตัวหลักดู clean เมื่อเราใช้การแยก detail ไปอยู่ที่ไฟล์อื่น จึง import เข้ามาในตัวหลัก เช่น @testing.md
    2.2 หลักการเขียน claude.md
        2.2.1 ไม่ควรเกิน 300 บรรทัด ยิ่งสั้นยิ่งดีเพราะยิ่งเยอะความแม่นยำของคำตอบก็จะยิ่งลดลง
        2.2.2 อย่าใช้ /claude init โดยไม่ทำการปรับปรุงในภายหลัง
        2.2.3 อย่าใส่พวก code style ที่เกี่ยวกับ code formatter อย่าง lint ลงไปเพราะเปลือง token โดยใช่เหตุ หันไปใช้ extension จริงๆจาก vscode อย่าง prettier ตรงๆไปเลยดีกว่า
        2.2.4 โครงสร้างหลักที่ควรมี 3 ส่วน
            a. คำอธิบายของโปรเจค 1 บรรทัด
            b. คำสั่งที่ใช้บ่อย เช่น npm run build เป็นต้น
            c. ข้อควรระวังที่ไม่ได้บอกไว้ในโค้ด
        2.2.5 Conditional rules 
            a. แยกไฟล์ไว้ใน folder rules และเขียนเงื่อนไขเพื่อเป็นการป้องกันไม่ให้ claude มาอ่านส่วนที่เป็น rare case ซึ่งเปลือง token โดยใช่เหตุ
            b. ระบุ paths field ที่เป็น YAML frontmatter เพื่อต้องการระบุแบบเฉพาะเจาะจงว่าเคสนี้อ่านไฟล์ประเภทนี้เท่านั้นนะ เช่น
                rules/testing.md
                paths:
                    - "**/*.spec.ts"
                #Testing guidlines 
                ...
        2.2.6 จัดลำดับความสำคัญ
            a. เรื่องสำคัญสุดไว้บนสุด
            b. ใช้ captial case เมื่อต้องการให้ AI สนใจ เช่น IMPORTANT หรือ YOU MUST KNOW ...