ตัวอย่างไฟล์จริงที่ใช้ในการทำงานร่วมกัน (Next.js Project)

1. ตัวอย่าง CLAUDE.md สำหรับ Next.js Project จริง
    ไฟล์นี้วางที่ root ของ project เช่น my-app/CLAUDE.md

    ```markdown
    # Project Context
    นี่คือ Next.js 15 app ใช้ App Router, TypeScript, Tailwind CSS
    เชื่อมต่อ PostgreSQL ผ่าน Prisma และใช้ Auth.js สำหรับ authentication

    # Tech Stack
    - Framework: Next.js 15 (App Router)
    - Language: TypeScript (strict mode)
    - Styling: Tailwind CSS v4
    - DB: PostgreSQL ผ่าน Prisma ORM
    - Auth: Auth.js v5
    - Validation: Zod
    - State: Zustand (client), React Query (server state)
    - Test: Jest + React Testing Library, Playwright (E2E)

    # Architecture Rules
    - ใช้ Server Component เป็น default เสมอ เพิ่ม "use client" เมื่อจำเป็นเท่านั้น
    - Data fetching ทำใน Server Component โดยตรง ห้าม fetch ใน Client Component โดยไม่จำเป็น
    - Server Action ใช้สำหรับ mutation (form submit, update, delete) แทน API route
    - API Route (route.ts) ใช้เฉพาะเมื่อต้องการ endpoint สำหรับ 3rd party หรือ webhook

    # Folder Structure
    - app/ → pages และ layouts ตาม App Router convention
    - app/actions/ → Server Actions ทั้งหมด
    - components/ui/ → reusable UI components (ไม่มี business logic)
    - components/features/ → feature-specific components
    - lib/ → utilities, helpers, constants
    - lib/db.ts → Prisma client singleton
    - lib/validations/ → Zod schemas

    # Coding Rules
    - ทุก Server Action ต้อง validate input ด้วย Zod ก่อนเสมอ
    - ห้าม expose Prisma model ตรงๆ ไปยัง client ให้ select เฉพาะ field ที่ต้องการ
    - Image ทุกรูปต้องใช้ next/image ห้ามใช้ <img> tag ตรงๆ
    - Link ทุกตัวต้องใช้ next/link ห้ามใช้ <a> tag ตรงๆ
    - ห้าม console.log ใน production ให้ใช้ logger จาก lib/logger.ts
    - Error boundary ต้องมีใน layout ของทุก route segment

    # Git Convention
    - Branch: feature/xxx, fix/xxx, chore/xxx
    - Commit: "feat: ...", "fix: ...", "chore: ..."
    - ห้าม push ตรง main ต้องผ่าน PR เสมอ
    - PR ต้องผ่าน review อย่างน้อย 1 คนก่อน merge

    # Testing Rules
    @.claude/testing.md

    # Security Rules
    @.claude/security.md
    ```

2. ตัวอย่างไฟล์ย่อยที่ import เข้า CLAUDE.md
    2.1 .claude/testing.md — กฎการเขียน test

    ```markdown
    # Testing Rules

    ## Unit & Integration (Jest + RTL)
    - ทุก Server Action ต้องมี unit test
    - ทุก component ที่มี logic ต้องมี RTL test
    - Test file วางคู่กับ source: components/features/LoginForm.test.tsx
    - Mock next/navigation และ next/headers ใน test เสมอ
    - ห้าม test implementation detail ให้ test พฤติกรรมที่ user เห็น

    ## E2E (Playwright)
    - ทุก critical user flow ต้องมี Playwright test
    - เช่น: login, checkout, create/edit/delete content
    - Test ไว้ใน tests/e2e/ และรันบน CI ก่อน deploy เสมอ
    - Coverage ไม่ต่ำกว่า 70% สำหรับ Server Actions
    ```

    2.2 .claude/security.md — กฎ security

    ```markdown
    # Security Rules
    - ทุก Server Action ต้องเช็ค session ก่อนทำงานเสมอ (ห้าม trust client)
    - ห้าม log ข้อมูล sensitive (password, token, เลขบัตร)
    - ทุก input ต้อง sanitize ผ่าน Zod ก่อน query database
    - ห้ามเขียน raw SQL ให้ใช้ Prisma เสมอ
    - Environment variable ที่ขึ้นต้นด้วย NEXT_PUBLIC_ จะถูก expose ไป client — ห้ามใส่ secret
    - Content Security Policy ต้องเปิดใน next.config.ts
    ```

3. ตัวอย่าง Skills (.claude/commands/)
    3.1 .claude/commands/pr.md — สร้าง PR description อัตโนมัติ

    ```markdown
    คุณคือ senior Next.js developer ในทีม

    อ่าน git diff ของ branch นี้แล้วสร้าง PR description ในรูปแบบ:

    ## What Changed
    (สรุปว่าแก้อะไร ทำไมต้องแก้)

    ## Type of Change
    - [ ] New feature
    - [ ] Bug fix
    - [ ] Refactor
    - [ ] Performance improvement

    ## How to Test
    (ขั้นตอน test ทีละ step รวมถึง URL ที่ต้องเปิด)

    ## Breaking Changes
    (มีไหม ถ้าไม่มีให้ระบุ "None")

    ## Checklist
    - [ ] Tests added/updated
    - [ ] No console.log left
    - [ ] Server/Client component ใช้ถูกต้อง
    - [ ] Prisma migration included (if schema changed)
    - [ ] No secrets in NEXT_PUBLIC_ vars
    ```

    เรียกใช้: พิมพ์ /pr ใน Claude Code ได้เลย

    3.2 .claude/commands/component.md — สร้าง component ใหม่

    ```markdown
    สร้าง Next.js component ชื่อ $ARGUMENTS ตาม convention ของ project นี้

    ถามตัวเองก่อน:
    - ต้องการ interactivity ไหม? → ถ้าไม่ → Server Component
    - ต้องการ useState/useEffect/event handler? → Client Component

    สร้างไฟล์ตามโครงสร้าง:
    - ถ้าเป็น reusable UI → components/ui/$ARGUMENTS.tsx
    - ถ้าเป็น feature-specific → components/features/$ARGUMENTS.tsx

    ทุก component ต้องมี:
    1. TypeScript interface สำหรับ props
    2. Export แบบ named export (ไม่ใช่ default)
    3. Test file คู่กัน (.test.tsx)
    ```

    เรียกใช้: พิมพ์ /component ProductCard

    3.3 .claude/commands/action.md — สร้าง Server Action ใหม่

    ```markdown
    สร้าง Server Action สำหรับ $ARGUMENTS ใน app/actions/ ตาม pattern นี้:

    1. ไฟล์: app/actions/$ARGUMENTS.ts
    2. เริ่มด้วย "use server"
    3. validate input ด้วย Zod ก่อนเสมอ
    4. เช็ค session ก่อน mutation ทุกครั้ง
    5. return { success, data?, error? } เสมอ — ห้าม throw ออกมาถึง client
    6. revalidatePath หรือ revalidateTag หลัง mutation สำเร็จ
    7. สร้าง unit test คู่กันด้วย
    ```

    เรียกใช้: พิมพ์ /action createProduct

    3.4 .claude/commands/review.md — review code ก่อน merge

    ```markdown
    รีวิว diff ของ branch นี้โดยเช็คตามลำดับ:

    1. Next.js-specific: Server/Client component ใช้ถูกไหม, มี "use client" ที่ไม่จำเป็นไหม
    2. Security: Server Action เช็ค auth ไหม, มี exposed secret ไหม, Zod validation ครบไหม
    3. Performance: fetch ซ้ำซ้อนไหม, image ใช้ next/image ไหม, missing Suspense boundary ไหม
    4. Code quality: ปฏิบัติตาม rules ใน CLAUDE.md ไหม

    สรุปเป็น:
    🔴 Critical (ต้องแก้ก่อน merge)
    🟡 Warning (ควรแก้)
    🟢 Suggestion (แก้ได้ถ้าสะดวก)
    ```

    เรียกใช้: พิมพ์ /review ก่อน push PR ทุกครั้ง

4. โครงสร้างไฟล์สุดท้ายที่ควรมี

    ```
    my-app/
    ├── CLAUDE.md                          ← กฎหลักของทีม
    ├── .claude/
    │   ├── testing.md                     ← กฎ test (import ใน CLAUDE.md)
    │   ├── security.md                    ← กฎ security (import ใน CLAUDE.md)
    │   └── commands/
    │       ├── pr.md                      ← /pr
    │       ├── component.md               ← /component
    │       ├── action.md                  ← /action
    │       └── review.md                  ← /review
    ├── app/
    │   ├── actions/                       ← Server Actions ทั้งหมด
    │   └── ...
    ├── components/
    │   ├── ui/                            ← reusable UI
    │   └── features/                      ← feature-specific
    └── lib/
        ├── db.ts                          ← Prisma singleton
        ├── logger.ts
        └── validations/                   ← Zod schemas
    ```

5. Workflow จริงของทีมที่ใช้ทุกวัน
    - เพิ่ม component ใหม่: พิมพ์ /component ProductCard
    - เพิ่ม feature ที่ต้องแก้ DB: พิมพ์ /action createProduct
    - ก่อน push: พิมพ์ /review เพื่อให้ Claude สแกน
    - เปิด PR: พิมพ์ /pr แล้ว copy ผลไป GitHub
