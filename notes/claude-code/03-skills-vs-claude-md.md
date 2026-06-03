Custom Slash Commands (Skills)
    1 คืออะไร
        1.1 ไฟล์ .md ที่เราสร้างขึ้นเองเพื่อเป็น reusable prompt สำหรับงานที่ทำซ้ำบ่อยๆ
        1.2 เรียกใช้ใน Claude Code ด้วยการพิมพ์ /ชื่อไฟล์ ได้เลย
        1.3 ต่างจาก claude.md ตรงที่ claude.md คือ "กฎ" ที่ใช้ตลอด แต่ Skills คือ "คำสั่งด่วน" ที่เรียกใช้เมื่อต้องการ

    2 วิธีสร้างและ scope
        2.1 Project level: วางไว้ใน .claude/commands/<ชื่อ>.md → ใช้ได้เฉพาะ project นี้
        2.2 User level: วางไว้ใน ~/.claude/commands/<ชื่อ>.md → ใช้ได้ทุก project
        2.3 รับ argument ได้ด้วย $ARGUMENTS เช่น "Review PR #$ARGUMENTS for security issues"

    3 ตัวอย่างการประยุกต์ใช้จริง
        3.1 /pr-description
            - เมื่อจะเปิด PR ใหม่ แทนที่จะพิมพ์ context ยาวๆทุกครั้ง
            - Skill นี้จะอ่าน git diff แล้วสร้าง PR description ให้อัตโนมัติ พร้อม summary, test plan, และ breaking changes

        3.2 /security-review
            - รันก่อน merge ทุกครั้ง
            - Skill นี้จะสแกนโค้ดในรอบนี้หา OWASP top 10, exposed secrets, หรือ SQL injection

        3.3 /onboard
            - สำหรับทีมที่มีสมาชิกใหม่เข้ามา
            - Skill นี้จะอ่าน codebase แล้วสร้าง summary ของ architecture, convention, และ gotchas ที่ต้องรู้

        3.4 /migrate $ARGUMENTS
            - ใช้กับ Database migration เช่น /migrate add_user_table
            - Skill นี้จะสร้าง migration file, rollback script, และ seed data ให้พร้อมกันเลย

    4 เปรียบเทียบ Skills vs CLAUDE.md
        | หัวข้อ          | CLAUDE.md                        | Skill                                  |
        |---------------|----------------------------------|----------------------------------------|
        | ทำงานเมื่อ      | ทุก session อัตโนมัติ             | เรียกใช้ด้วย /ชื่อ เท่านั้น             |
        | หน้าที่         | กำหนดกฎ, context, convention     | prompt สำเร็จรูปสำหรับงานซ้ำ           |
        | เปรียบได้กับ     | Employee handbook ของทีม          | Macro / SOP ที่กดใช้เมื่อต้องการ       |
        | ตัวอย่าง        | "ห้าม push ตรง main"              | /pr-description → สร้าง PR description |

        - CLAUDE.md = "Claude ต้องรู้อะไรตลอดเวลา"
        - Skill     = "Claude ต้องทำอะไรเมื่อฉันสั่ง"
        - ถ้า deploy process มี 10 ขั้นตอน → ใส่ใน Skill ไม่ใช่ CLAUDE.md
          เพราะ CLAUDE.md จะถูกอ่านทุก session แม้แค่แก้ bug ธรรมดา (เปลือง token)