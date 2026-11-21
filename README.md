# Rotten Potatoes (310-2205 วิศวกรรมซอฟต์แวร์ 2/2569)

Template repository for Lab L2 (310-2205 Software Engineering, semester 2/2569).

![ci](https://github.com/6810301021-sittipat/-rottenpotatoes-pair-6810301021-6810301014/actions/workflows/ci.yml/badge.svg)

## เริ่มที่นี่ (Start here)

1. เข้าสู่ระบบ GitHub แล้วกด **Use this template** เลือก **Create a new repository**
2. Owner = บัญชีของ A, Repository name = `rottenpotatoes-pair-<รหัส A>-<รหัส B>`, Public แล้วกด **Create repository from template**
3. เปิด Settings → Collaborators แล้วเพิ่มบัญชี GitHub ของ B เป็น collaborator
4. B กด Accept invitation จาก GitHub
5. ทั้งสองคนเปิด IntelliJ IDEA กด **Clone Repository** เลือก GitHub เลือก repository ของคู่ แล้วกด Clone และ Trust Project
6. เปิด Terminal ใน IntelliJ IDEA แล้วรันคำสั่ง

```bash
# macOS / Linux
./mvnw -B verify

# Windows
.\mvnw.cmd -B verify
```

ต้องจบด้วย `BUILD SUCCESS`

7. ทำ Lab L2 ตามสไลด์ และกรอก `docs/L2.md` และ `docs/AI_LOG.md`

## วิธี build

How to build. Requires JDK 25 (check with `java -version`).

```bash
./mvnw -B verify      # macOS / Linux
.\mvnw.cmd -B verify  # Windows
```

## โครงสร้าง

Project structure.

```text
.devcontainer/devcontainer.json   ตั้งค่า Dev Container / Codespaces (JDK 25)
.github/workflows/ci.yml          CI: build + test + coverage ทุกครั้งที่ push
.mvn/wrapper/, mvnw, mvnw.cmd     Maven Wrapper (ไม่ต้องติดตั้ง Maven เอง)
docs/L2.md                        Lab passport ของ L2 ที่ต้องกรอก
docs/AI_LOG.md                    บันทึกการใช้ AI
pom.xml                           ไฟล์ build: Java 25, Spring Boot, JaCoCo, Checkstyle
src/main/java/.../Greeting.java   class ตัวอย่างจาก template
src/test/java/.../GreetingTest.java test ตัวอย่าง (JUnit 6 + AssertJ)
src/main/java/.../domain/         domain classes ของ L2
src/test/java/.../domain/         domain tests ของ L2
```

## L2 checklist

Lab L2 checklist.

- [x] สร้าง repository ของคู่ชื่อ `rottenpotatoes-pair-<รหัส A>-<รหัส B>` และเพิ่ม collaborator ทั้งสองคน
- [x] ทั้งสองคน Clone repository และรัน `./mvnw -B verify` ผ่าน
- [x] สร้าง Issue สำหรับ Movie domain และสร้าง branch ตามเลข Issue
- [x] สร้าง `RatingTest` และ `Rating` แบบ test-first และ commit
- [x] แก้ไข CI badge ใน README ให้ชี้ไปยัง repository ของคู่
- [x] สร้าง `MovieTest` ก่อน `Movie` และ commit ขณะ test ยังไม่ผ่าน (red commit)
- [x] เขียน `Movie` record ให้ test ผ่าน แล้ว commit (green commit)
- [x] สร้าง `MovieCatalogTest` ก่อน `MovieCatalog` และ commit ขณะ test ยังไม่ผ่าน (red commit)
- [x] เขียน `MovieCatalog` โดยใช้ Stream API ให้ test ผ่าน แล้ว commit (green commit)
- [x] Push branch และสร้าง Pull Request สำหรับ Movie domain โดยมี `Closes #<เลข Issue>`
- [x] อีกคน Review และ Approve Pull Request ก่อน Merge
- [x] Pull `main` กลับมาทั้งสองเครื่อง และตรวจสอบ CI ว่าเขียว
- [x] สร้าง Issue สำหรับ Moviegoer และทำงานนอกคาบแบบ test-first
- [x] สร้าง `MoviegoerTest` ก่อน `Moviegoer` และ commit red/green แยกกัน
- [x] Push และสร้าง Pull Request สำหรับ Moviegoer โดยมี `Closes #<เลข Issue>`
- [x] อีกคน Review และ Approve ก่อน Merge
- [x] ตรวจสอบว่า `./mvnw -B verify` ผ่านบน main ทั้งสองเครื่อง
- [x] มี test ผ่านอย่างน้อย 15 ข้อ และ CI เขียวบน GitHub
- [x] กรอก `docs/L2.md` และ `docs/AI_LOG.md` ให้ครบ

## สิ่งที่ต้องสร้างใน Lab L2

| Class | ชนิด | หน้าที่ | จำนวน Test |
|---|---|---|---:|
| Rating | enum | G, PG, PG13, R, NC17 พร้อม label เช่น PG-13 | 3 |
| Movie | record | title, rating, description, releaseDate ตรวจสอบชื่อและปีที่ฉาย | 4 |
| MovieCatalog | class | กรองตาม rating, เรียงชื่อ, เรียงหนังใหม่สุดก่อน และค้นหาตามชื่อ | 5 |
| Moviegoer | record | name และ email ต้องมี @ (งานนอกคาบ) | 2 |
| Greeting | class | ตัวอย่างจาก template | 1 |

รวมทั้งหมด 15 Tests เมื่อทำครบ

ทุก class อยู่ใน package:

`th.ac.cdti.rottenpotatoes.domain`

และ test ทุกไฟล์อยู่ใน package เดียวกันภายใต้ `src/test/java`

## ขั้นตอนการทำงาน (Workflow)

การทำงานเป็นคู่ใช้รูปแบบ Driver และ Navigator โดยสลับหน้าที่ตามที่กำหนดใน Lab L2

| ขั้นตอน | กิจกรรม | Driver |
|---|---|---|
| ขั้นที่ 0 | สร้าง repository, เพิ่ม collaborator, clone และ build | A |
| ขั้นที่ 1 | สร้าง branch, RatingTest, Rating และ CI badge | A |
| ขั้นที่ 2 | MovieTest และ Movie แบบ test-first | B |
| ขั้นที่ 3 | MovieCatalogTest และ MovieCatalog แบบ test-first | A |
| ขั้นที่ 4 | Push, Pull Request, Review และ Merge | ทั้งคู่ |
| นอกคาบ | Moviegoer แบบ test-first | B แล้ว A |

รูปแบบชื่อ branch:

`story/<เลข Issue>-<ชื่อสั้น>`

ตัวอย่าง:

`story/1-movie-domain`

รูปแบบ Commit message:

```text
test: Movie record rules (red)
feat: Movie record with title and release-year checks
test: MovieCatalog queries (red)
feat: MovieCatalog queries with streams
```

## สิ่งที่ต้องส่ง (Lab Passport)

1. Rating, Movie, MovieCatalog และ Moviegoer พร้อม test อย่างน้อย 15 ข้อผ่าน และ CI เขียวบน main
2. Pull Request อย่างน้อย 2 รายการ โดยอีกคนเป็นผู้ Review และ Approve ก่อน Merge
3. Commit red และ green แยกกันตามขั้นตอน test-first
4. กรอก `docs/L2.md` และบันทึกการใช้ AI ใน `docs/AI_LOG.md`

## นโยบาย AI ขั้น R0

AI policy, level R0.

- สามารถถาม AI เพื่อให้อธิบาย error หรือ API ได้
- ห้ามนำ code หรือ test ที่ AI เขียนให้ไปวางในงาน
- ต้องเขียนบันทึกการใช้ AI ใน `docs/L2.md` และ `docs/AI_LOG.md`
- ระบุ `AI used for: ...` หรือ `none` ตามการใช้งานจริง

## ที่มาของเครื่องมือ

Where the tools come from. ดาวน์โหลดจากผู้พัฒนาโดยตรงผ่าน HTTPS

| เครื่องมือ (Tool) | ผู้ดูแล (Maintainer) | แหล่ง (Source) |
|---|---|---|
| JDK 25 Eclipse Temurin | Eclipse Adoptium | adoptium.net |
| Git | Git project, Git for Windows | git-scm.com |
| IntelliJ IDEA | JetBrains | jetbrains.com/idea |
| Apache Maven | Apache Software Foundation | repo.maven.apache.org |
| Spring Boot, JUnit 6, AssertJ, Mockito | ผู้พัฒนาแต่ละโครงการ | Maven Central |
| JaCoCo | EclEmma | Maven Central |
| Checkstyle | Checkstyle | Maven Central |
| GitHub Actions | GitHub | github.com/actions |
| Dev Container | Microsoft | mcr.microsoft.com |

ถ้าเพิ่ม dependency ใหม่ ให้ตรวจสอบผู้ดูแลและแหล่งดาวน์โหลดก่อนนำมาใช้ และบันทึกไว้ใน `docs/L2.md`

## References

- Lab L2 Movie Domain ด้วย Java (310-2205 Software Engineering, 2/2569)
- GitHub Docs: Creating a repository from a template
- GitHub Docs: Creating an issue and pull request
- GitHub Docs: Reviewing proposed changes in a pull request
- Oracle Java SE 25 API
- JUnit 6 and AssertJ Documentation