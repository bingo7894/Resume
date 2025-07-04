<script>
import ResumeSection from "./components/ResumeSection.vue";
import SectionHeadline from "./components/SectionHeadline.vue";
import Sidebar from "./components/Sidebar.vue";
import ColorInput from "./components/ColorInput.vue";
import EditToggle from "./components/EditToggle.vue";

export default {
  components: {
    ResumeSection,
    SectionHeadline,
    Sidebar,
    ColorInput,
    EditToggle,
  },
  data() {
    return {
      isEditMode: false,
      name: "Pokpong Padjunreed",
      title: "Programmer",
      introText:
        "A passionate programmer with a strong foundation in data analytics, software engineering, and backend development. Seeking opportunities to leverage my skills in innovative projects.",
      imageUrl: "/cat.jpg",
      headlines: [
        "About me",
        "Contact",
        "Skills",
        "Certifications",
        "Experience",
        "Education",
      ],
      contact: {
        phone: "081-512-7057",
        email: "pokpong@gmail.com",
        address: "ซอยจันทน์ 27 แขวงทุ่งวัดดอน เขตสาทร กรุงเทพมหานคร",
      },
      skills: [
        { name: "Python (Data Analysis, Automation)" },
        { name: "Python (Data Analysis, Automation" },
        { name: "Java (Spring Boot)" },
      ],
      experience: [
        {
          title: "Programmer",
          company: "Makro",
          location: "Bangkok",
          date: "2022–Present",
          description: [
            "Developed internal web applications using Vue.js and Node.js",
            "Collaborated with cross-functional teams to improve supply chain software",
            "Integrated RESTful APIs and optimized database queries",
          ],
        },
        {
          title: "Software Developer",
          company: "7-Eleven",
          location: "Bangkok",
          date: "2021–2022",
          description: [
            "Built backend services using Java Spring Boot",
            "Designed and maintained MySQL database schemas",
            "Supported deployment pipeline using GitLab CI/CD",
          ],
        },
        {
          title: "Junior Developer",
          company: "Lotus's",
          location: "Bangkok",
          date: "2020–2021",
          description: [
            "Assisted in front-end development using HTML/CSS and Vue.js",
            "Performed unit testing and bug fixing for retail system modules",
            "Wrote documentation for software components",
          ],
        },
      ],
      certifications: [
        {
          name: "Google Data Analytics",
          issuer: "Coursera",
          year: "2024",
        },
        {
          name: "AWS Certified Cloud Practitioner",
          issuer: "Amazon Web Services",
          year: "2023",
        },
      ],
      education: [
        {
          degree: "Bachelor of Engineering",
          major: "Computer Engineering",
          school: "มหาวิทยาลัยเทคโนโลยีราชมงคลกรุงเทพ",
          year: "2022",
        },
        {
          degree: "High School",
          major: "Science-Math Program",
          school: "โรงเรียนพระแม่มารีสาทร",
          year: "2018",
        },
        {
          degree: "Junior High School",
          major: "Science Program",
          school: "โรงเรียนป่างิ้ววิทยา",
          year: "2015",
        },
      ],
      colors: {
        left: {
          highlight: "#ff9900",
          background: "#f5f5f5",
          text: "#000000",
        },
        right: {
          highlight: "#3366ff",
          background: "#ffffff",
          text: "#000000",
        },
      },
    };
  },
  computed: {
    cssVariables() {
      return {
        "--highlight-color-left": this.colors.left.highlight,
        "--background-color-left": this.colors.left.background,
        "--text-color-left": this.colors.left.text,
        "--highlight-color-right": this.colors.right.highlight,
        "--background-color-right": this.colors.right.background,
        "--text-color-right": this.colors.right.text,
      };
    },
  },
  methods: {
    toggleEditMode(isEdit) {
      this.isEditMode = isEdit;
    },
    updateHeadline(newValue, index) {
      this.headlines[index] = newValue;
    },
    updateProperty(event, key) {
      this[key] = event.target.innerText;
    },
    updateNestedProperty(event, key1, key2) {
      this[key1][key2] = event.target.innerText;
    },
    updateExperience(event, key, index) {
      this.experience[index][key] = event.target.innerText;
    },
    updateExperienceDescription(event, index1, index2) {
      this.experience[index1]["description"][index2] = event.target.innerText;
    },
    updateEducation(event, key, index) {
      this.education[index][key] = event.target.innerText;
    },
    updateSkill(event, index) {
      this.skills[index].name = event.target.innerText;
    },
    updateCertification(event, key, index) {
      this.certifications[index][key] = event.target.innerText;
    },
    // เมธอดเพิ่มข้อมูลใหม่
    addSkill() {
      this.skills.push({ name: "ทักษะใหม่" });
    },
    addCertification() {
      this.certifications.push({
        name: "ใบรับรองใหม่",
        issuer: "ผู้ให้ใบรับรอง",
        year: "ปี",
      });
    },
    addExperience() {
      this.experience.push({
        title: "ตำแหน่งงาน",
        company: "บริษัท",
        location: "สถานที่",
        date: "วันที่",
        description: ["รายละเอียดงาน"],
      });
    },
    addEducation() {
      this.education.push({
        degree: "ระดับการศึกษา",
        major: "สาขาวิชา",
        school: "สถาบันการศึกษา",
        year: "ปี",
      });
    },
    addContactField() {
      console.log("เพิ่มฟิลด์ติดต่อใหม่");
    },
    addExperienceDescription(index) {
      this.experience[index].description.push("รายละเอียดใหม่");
    },
    // เมธอดลบข้อมูล
    deleteSkill(index) {
      if (this.skills.length > 1) {
        this.skills.splice(index, 1);
      } else {
        alert("ต้องมีทักษะอย่างน้อย 1 รายการ");
      }
    },
    deleteCertification(index) {
      this.certifications.splice(index, 1);
    },
    deleteExperience(index) {
      if (this.experience.length > 1) {
        this.experience.splice(index, 1);
      } else {
        alert("ต้องมีประสบการณ์อย่างน้อย 1 รายการ");
      }
    },
    deleteEducation(index) {
      if (this.education.length > 1) {
        this.education.splice(index, 1);
      } else {
        alert("ต้องมีประวัติการศึกษาอย่างน้อย 1 รายการ");
      }
    },
    deleteExperienceDescription(expIndex, descIndex) {
      if (this.experience[expIndex].description.length > 1) {
        this.experience[expIndex].description.splice(descIndex, 1);
      } else {
        alert("ต้องมีรายละเอียดงานอย่างน้อย 1 รายการ");
      }
    },
    // เมธอดสำหรับการเปลี่ยนภาพโปรไฟล์
    triggerImageUpload() {
      this.$refs.imageInput.click();
    },
    handleImageUpload(event) {
      const file = event.target.files[0];
      if (file) {
        const reader = new FileReader();
        reader.onload = (e) => {
          this.imageUrl = e.target.result;
        };
        reader.readAsDataURL(file);
      }
    },
    // เมธอดสำหรับ Export
    exportResume() {
      window.print();
    },
  },
};
</script>

<template>
  <main class="container">
    <div class="half">
      <Sidebar>
        <EditToggle @edit-mode-toggled="toggleEditMode" />
        <ColorInput
          label="Highlight color"
          :default-color="colors.left.highlight"
          @color-changed="colors.left.highlight = $event"
        />
        <ColorInput
          label="Background color"
          :default-color="colors.left.background"
          @color-changed="colors.left.background = $event"
        />
        <ColorInput
          label="Text color"
          :default-color="colors.left.text"
          @color-changed="colors.left.text = $event"
        />

        <ColorInput
          label="Highlight color"
          :default-color="colors.right.highlight"
          @color-changed="colors.right.highlight = $event"
        />
        <ColorInput
          label="Background color"
          :default-color="colors.right.background"
          @color-changed="colors.right.background = $event"
        />
        <ColorInput
          label="Text color"
          :default-color="colors.right.text"
          @color-changed="colors.right.text = $event"
        />

        <!-- ปุ่ม Export แสดงเฉพาะเมื่อไม่อยู่ในโหมดแก้ไข -->
        <button v-if="!isEditMode" class="export-btn" @click="exportResume">
          📄 Export Resume
        </button>
      </Sidebar>

      <div>
        <div id="resume" class="d-flex" :style="cssVariables">
          <div class="left-col">
            <ResumeSection class="resume-section">
              <div class="profile-pic-container">
                <img
                  :src="imageUrl"
                  class="profile-pic"
                  alt="profile picture"
                />
                <button
                  v-if="isEditMode"
                  class="change-image-btn"
                  @click="triggerImageUpload"
                  title="เปลี่ยนภาพโปรไฟล์"
                >
                  📷
                </button>
              </div>
              <input
                ref="imageInput"
                type="file"
                accept="image/*"
                @change="handleImageUpload"
                style="display: none"
              />

              <SectionHeadline
                :headline="headlines[0]"
                @headline-edited="updateHeadline($event, 0)"
              />

              <div
                :contenteditable="isEditMode"
                @input="updateProperty($event, 'introText')"
              >
                {{ introText }}
              </div>
            </ResumeSection>

            <ResumeSection>
              <SectionHeadline
                :headline="headlines[1]"
                @headline-edited="updateHeadline($event, 1)"
              />
              <div class="contact-list">
                <div
                  class="contact-item"
                  :contenteditable="isEditMode"
                  @input="updateNestedProperty($event, 'contact', 'phone')"
                >
                  <span class="icon">📞</span> {{ contact.phone }}
                </div>
                <div
                  class="contact-item"
                  :contenteditable="isEditMode"
                  @input="updateNestedProperty($event, 'contact', 'email')"
                >
                  <span class="icon">📧</span> {{ contact.email }}
                </div>
                <div
                  class="contact-item"
                  :contenteditable="isEditMode"
                  @input="updateNestedProperty($event, 'contact', 'address')"
                >
                  <span class="icon">📍</span> {{ contact.address }}
                </div>
              </div>
            </ResumeSection>

            <ResumeSection>
              <SectionHeadline
                :headline="headlines[2]"
                @headline-edited="updateHeadline($event, 2)"
              />
              <ul>
                <li
                  v-for="(skill, index) in skills"
                  :key="index"
                  class="editable-item"
                >
                  <span
                    :contenteditable="isEditMode"
                    @input="updateSkill($event, index)"
                  >
                    {{ skill.name }}
                  </span>
                  <button
                    v-if="isEditMode"
                    class="delete-btn"
                    @click="deleteSkill(index)"
                    title="ลบทักษะ"
                  >
                    ❌
                  </button>
                </li>
              </ul>
              <button v-if="isEditMode" class="add-btn" @click="addSkill">
                + เพิ่มทักษะ
              </button>
            </ResumeSection>

            <div class="resume-section">
              <SectionHeadline
                :headline="headlines[3]"
                @headline-edited="updateHeadline($event, 3)"
              />
              <ul>
                <li
                  v-for="(cert, index) in certifications"
                  :key="index"
                  class="editable-item"
                >
                  <div>
                    <span
                      :contenteditable="isEditMode"
                      @input="updateCertification($event, 'name', index)"
                    >
                      {{ cert.name }}
                    </span>
                    —
                    <span
                      :contenteditable="isEditMode"
                      @input="updateCertification($event, 'issuer', index)"
                    >
                      {{ cert.issuer }}
                    </span>
                    (
                    <span
                      :contenteditable="isEditMode"
                      @input="updateCertification($event, 'year', index)"
                    >
                      {{ cert.year }}
                    </span>
                    )
                  </div>
                  <button
                    v-if="isEditMode"
                    class="delete-btn"
                    @click="deleteCertification(index)"
                    title="ลบใบรับรอง"
                  >
                    ❌
                  </button>
                </li>
              </ul>
              <button
                v-if="isEditMode"
                class="add-btn"
                @click="addCertification"
              >
                + เพิ่มใบรับรอง
              </button>
            </div>
          </div>

          <div class="right-col">
            <div
              class="personal-name"
              :contenteditable="isEditMode"
              @input="updateProperty($event, 'name')"
            >
              {{ name }}
            </div>
            <div
              class="personal-title"
              :contenteditable="isEditMode"
              @input="updateProperty($event, 'title')"
            >
              {{ title }}
            </div>

            <div class="resume-section">
              <h4 class="section-headline">{{ headlines[4] }}</h4>

              <div
                v-for="(item, index) in experience"
                :key="index"
                class="experience-item"
              >
                <div class="experience-header">
                  <div>
                    <strong
                      :contenteditable="isEditMode"
                      @input="updateExperience($event, 'title', index)"
                      >{{ item.title }}</strong
                    >
                  </div>
                  <button
                    v-if="isEditMode"
                    class="delete-btn"
                    @click="deleteExperience(index)"
                    title="ลบประสบการณ์"
                  >
                    ❌
                  </button>
                </div>
                <div class="experience-meta">
                  <em
                    :contenteditable="isEditMode"
                    @input="updateExperience($event, 'company', index)"
                  >
                    {{ item.company }}</em
                  >
                  <span
                    :contenteditable="isEditMode"
                    @input="updateExperience($event, 'date', index)"
                    >{{ item.date }}</span
                  >
                </div>
                <ul>
                  <li
                    v-for="(desc, i) in item.description"
                    :key="i"
                    class="editable-item"
                  >
                    <span
                      :contenteditable="isEditMode"
                      @input="updateExperienceDescription($event, index, i)"
                    >
                      {{ desc }}
                    </span>
                    <button
                      v-if="isEditMode"
                      class="delete-btn"
                      @click="deleteExperienceDescription(index, i)"
                      title="ลบรายละเอียด"
                    >
                      ❌
                    </button>
                  </li>
                </ul>
                <button
                  v-if="isEditMode"
                  class="add-btn small"
                  @click="addExperienceDescription(index)"
                >
                  + เพิ่มรายละเอียดงาน
                </button>
              </div>
              <button v-if="isEditMode" class="add-btn" @click="addExperience">
                + เพิ่มประสบการณ์ทำงาน
              </button>
            </div>

            <div class="resume-section">
              <h4 class="section-headline">{{ headlines[5] }}</h4>
              <div
                v-for="(edu, index) in education"
                :key="index"
                class="education-item"
              >
                <div class="education-header">
                  <div>
                    <div>
                      <strong
                        :contenteditable="isEditMode"
                        @input="updateEducation($event, 'degree', index)"
                        >{{ edu.degree }}</strong
                      >
                      —
                      <span
                        :contenteditable="isEditMode"
                        @input="updateEducation($event, 'major', index)"
                        >{{ edu.major }}</span
                      >
                    </div>
                    <div
                      :contenteditable="isEditMode"
                      @input="updateEducation($event, 'school', index)"
                    >
                      {{ edu.school }}
                    </div>
                    <div
                      :contenteditable="isEditMode"
                      @input="updateEducation($event, 'year', index)"
                    >
                      ({{ edu.year }})
                    </div>
                  </div>
                  <button
                    v-if="isEditMode"
                    class="delete-btn"
                    @click="deleteEducation(index)"
                    title="ลบประวัติการศึกษา"
                  >
                    ❌
                  </button>
                </div>
              </div>
              <button v-if="isEditMode" class="add-btn" @click="addEducation">
                + เพิ่มประวัติการศึกษา
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
#resume {
  display: flex;
  box-shadow: rgba(50, 50, 93, 0.25) 0px 13px 27px -5px,
    rgba(0, 0, 0, 0.3) 0px 8px 16px -8px;
  height: 297mm;
  width: 210mm;
}

.left-col {
  background-color: var(--background-color-left);
  color: var(--text-color-left);
  border-right: 1px solid var(--highlight-color-left);
  width: 30%;
  padding: 30px;
}
.right-col {
  background-color: var(--background-color-right);
  color: var(--text-color-right);
  border-right: 1px solid var(--highlight-color-right);
  width: 70%;
  padding: 30px;
}

.resume-section {
  margin-bottom: 30px;
}
.personal-name {
  font-weight: 300;
  color: var(--highlight-color-right);
  font-size: 28px;
  border-bottom: 1px solid var(--highlight-color-right);
  margin: 0;
  margin-left: -30px;
  padding: 30px;
  padding-bottom: 15px;
}
.personal-title {
  border-bottom: 1px solid var(--highlight-color-right);
  margin: 0 0 20px -30px;
  padding: 15px 0 15px 30px;
  font-weight: 300;
  font-size: 20px;
}
#resume ul {
  padding-inline-start: 16px;
  margin-block-end: 0px;
  margin-block-start: 5px;
}
/* สไตล์ภาพโปรไฟล์ */
.profile-pic-container {
  position: relative;
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

.profile-pic {
  display: block;
  width: 160px;
  height: 160px;
  border: 5px solid var(--highlight-color-left);
  object-fit: cover;
  border-radius: 50%;
}

.change-image-btn {
  position: absolute;
  bottom: 10px;
  right: 10px;
  background-color: var(--highlight-color-left);
  color: white;
  border: none;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  cursor: pointer;
  font-size: 1.2rem;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
}

.change-image-btn:hover {
  background-color: var(--highlight-color-right);
  transform: scale(1.1);
}
.experience-item {
  margin-bottom: 1rem;
}

.experience-meta {
  display: flex;
  justify-content: space-between;
  font-size: 0.9rem;
  color: #555;
}
.half {
  display: flex;
  justify-content: space-between;
}

/* สไตล์ปุ่มเพิ่ม */
.add-btn {
  background-color: var(--highlight-color-left);
  color: white;
  border: none;
  padding: 5px 10px;
  border-radius: 4px;
  cursor: pointer;
  margin-top: 10px;
  font-size: 0.9rem;
  transition: background-color 0.3s;
}

.add-btn:hover {
  background-color: var(--highlight-color-right);
}

.add-btn.small {
  font-size: 0.8rem;
  padding: 3px 8px;
}

.right-col .add-btn {
  background-color: var(--highlight-color-right);
}

.right-col .add-btn:hover {
  background-color: var(--highlight-color-left);
}

/* สไตล์ปุ่มลบ */
.delete-btn {
  background: none;
  border: none;
  cursor: pointer;
  font-size: 0.8rem;
  padding: 2px 4px;
  margin-left: 8px;
  border-radius: 3px;
  transition: background-color 0.3s;
}

.delete-btn:hover {
  background-color: rgba(255, 0, 0, 0.1);
}

/* สไตล์ไอเท็มที่แก้ไขได้ */
.editable-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  position: relative;
}

.experience-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
}

.education-item {
  margin-bottom: 10px;
}

.education-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
}

/* สไตล์ปุ่ม Export */
.export-btn {
  background-color: #28a745;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 6px;
  cursor: pointer;
  font-size: 1rem;
  width: 100%;
  margin-top: 20px;
  transition: background-color 0.3s;
}

.export-btn:hover {
  background-color: #218838;
}

.contact-item {
  margin-bottom: 8px;
}

.contact-item .icon {
  margin-right: 8px;
}

/* ป้องกันการแก้ไขเมื่อไม่อยู่ในโหมดแก้ไข */
[contenteditable="false"] {
  pointer-events: none;
}
</style>
