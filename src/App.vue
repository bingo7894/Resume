<script>
import ResumeSection from "./components/ResumeSection.vue";
import SectionHeadline from "./components/SectionHeadline.vue";
import Sidebar from "./components/Sidebar.vue";
import ColorInput from "./components/ColorInput.vue";
import EditToggle from "./components/EditToggle.vue";

import resumeData from "./data/resumeData.js";

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
      ...resumeData,
      isEditMode: false,
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
    updateSoftSkill(event, index) {
      this.softSkills[index].name = event.target.innerText;
    },
    addSoftSkill() {
      this.softSkills.push({ name: "ทักษะใหม่" });
    },
    deleteSoftSkill(index) {
      if (this.softSkills.length > 1) {
        this.softSkills.splice(index, 1);
      } else {
        alert("ต้องมีทักษะอย่างน้อย 1 รายการ");
      }
    },
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
    // แก้ไขฟังก์ชัน exportResume() ใน methods
    // แทนที่ฟังก์ชัน exportResume() ในส่วน methods
    exportResume() {
      // ลบ style เก่าก่อน (ถ้ามี)
      const oldStyle = document.getElementById("dynamic-print-style");
      if (oldStyle) {
        document.head.removeChild(oldStyle);
      }

      // สร้าง style ใหม่พร้อมกับสีที่กำหนด
      const style = document.createElement("style");
      style.setAttribute("id", "dynamic-print-style");
      style.innerHTML = `
    @media print {
      /* Override CSS Variables with actual color values */
      :root {
        --highlight-color-left: ${this.colors.left.highlight} !important;
        --background-color-left: ${this.colors.left.background} !important;
        --text-color-left: ${this.colors.left.text} !important;
        --highlight-color-right: ${this.colors.right.highlight} !important;
        --background-color-right: ${this.colors.right.background} !important;
        --text-color-right: ${this.colors.right.text} !important;
      }

      /* Apply colors directly to elements */
      .left-col {
        background-color: ${this.colors.left.background} !important;
        color: ${this.colors.left.text} !important;
        border-right: 1px solid ${this.colors.left.highlight} !important;
      }

      .right-col {
        background-color: ${this.colors.right.background} !important;
        color: ${this.colors.right.text} !important;
      }

      .personal-name {
        color: ${this.colors.right.highlight} !important;
        border-bottom: 1px solid ${this.colors.right.highlight} !important;
      }

      .personal-title {
        border-bottom: 1px solid ${this.colors.right.highlight} !important;
      }

      .profile-pic {
        border: 3px solid ${this.colors.left.highlight} !important;
      }

      .add-btn {
        background-color: ${this.colors.left.highlight} !important;
      }

      .right-col .add-btn {
        background-color: ${this.colors.right.highlight} !important;
      }

      .change-image-btn {
        background-color: ${this.colors.left.highlight} !important;
      }

      /* Section headlines color */
      .section-headline {
        color: ${this.colors.left.text} !important;
      }

      .right-col .section-headline {
        color: ${this.colors.right.text} !important;
      }

      /* Contact items */
      .contact-item {
        color: ${this.colors.left.text} !important;
      }

      /* Experience meta */
      .experience-meta {
        color: ${this.colors.right.text} !important;
        opacity: 0.8;
      }

      /* Lists */
      .left-col ul li {
        color: ${this.colors.left.text} !important;
      }

      .right-col ul li {
        color: ${this.colors.right.text} !important;
      }

      /* Force color rendering */
      * {
        -webkit-print-color-adjust: exact !important;
        color-adjust: exact !important;
      }
    }
  `;

      document.head.appendChild(style);

      // แสดง print dialog
      setTimeout(() => {
        // เพิ่ม class สำหรับ print mode
        document.body.classList.add("printing");

        window.print();

        // ลบ class หลังจาก print
        setTimeout(() => {
          document.body.classList.remove("printing");

          // ลบ style หลังจาก print เสร็จ
          const printStyle = document.getElementById("dynamic-print-style");
          if (printStyle) {
            document.head.removeChild(printStyle);
          }
        }, 1000);
      }, 200);
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

            <ResumeSection>
              <SectionHeadline
                :headline="headlines[6]"
                @headline-edited="updateHeadline($event, 6)"
              />
              <ul>
                <li
                  v-for="(softSkill, index) in softSkills"
                  :key="index"
                  class="editable-item"
                >
                  <span
                    :contenteditable="isEditMode"
                    @input="updateSoftSkill($event, index)"
                  >
                    {{ softSkill.name }}
                  </span>
                  <button
                    v-if="isEditMode"
                    class="delete-btn"
                    @click="deleteSoftSkill(index)"
                    title="ลบทักษะ"
                  >
                    ❌
                  </button>
                </li>
              </ul>
              <button v-if="isEditMode" class="add-btn" @click="addSoftSkill">
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

<style src="./style/resume.css"></style>
