<template>
	<section class="layout03" :class="{'hidden': ishidden}">
    <article>
      <table class="psnl-info">
        <tbody>
          <tr>
            <td rowspan="2" class="text-left">{{isEn?"Tel":"手机"}}: <br>{{resume.tel}}</td>
            <td class="text-center font-20">{{resume.fullName}}</td>
            <td rowspan="2" class="text-right">email: <br>{{resume.email}}</td>
          </tr>
          <tr>
            <td class="text-center font-16">{{resume.desired_position}}</td>
          </tr>
        </tbody>
      </table>
      <div class="rsm-header">
        <h2>{{isEn?"Work Experience":"工作经验"}}</h2>
        <hr>
      </div>
      <div class="rsm-cmpnt"  :class="{'margin-top-0': !work.company|| work_i == 0}"
      v-for="(work, work_i) in resume.work_exp" 
      :key="'work'+work_i">
        <div class="rsm-cmpnt-top">
          <div class="text-left">
            <div v-if="work.company">{{work.company}}</div>
            <div>{{work.title}}</div>
          </div>
          <div class="text-right font-10">
            <div>{{work.start_m_y}} - {{work.end_m_y}}</div>
            <div v-if="work.city">{{work.city}}</div>
          </div>
        </div>
        <div class="rsm-cmpnt-mid" v-if="work.company_desc">
          {{work.company_desc}}
        </div>
        <div class="rsm-cmpnt-btm" v-for="(duty, duty_i) in work.duties" :key="'duty'+duty_i">
          <p>{{duty.name}}</p>
          <ul v-if="duty.details">
            <li v-for="(item, item_i) in duty.details" :key="'item'+item_i">
              {{item}}
            </li>
          </ul>
        </div>
      </div>
      <div class="rsm-header">
        <h2>{{isEn?"Professional Skills":"专业技能"}}</h2>
        <hr>
      </div>
      <div class="rsm-cmpnt" 
      :class="{'margin-top-0': skill_i==0}"
      v-for="(skill, skill_i) in resume.pro_skills" 
      :key="'skill'+skill_i">
        <div class="rsm-cmpnt-top">
          <div class="text-left">
            <div>{{skill.nature}}</div>
          </div>
        </div>
        <div class="rsm-cmpnt-btm">
          <p>
            <span v-for="(skillName, skillName_i) in skill.names" :key="skillName+skillName_i">
              {{skillName}}<span v-if="skillName_i+1<skill.names.length">, </span>
            </span>
          </p>
          <ul v-if="skill.details">
            <li v-for="(skillItemdetail, skillItemdetail_i) in skill.details" :key="'skillItemdetail'+skillItemdetail_i">{{skillItemdetail}}</li>
          </ul>
        </div>
      </div>
      <div class="rsm-header">
        <h2>{{isEn?"Education":"教育背景"}}</h2>
        <hr>
      </div>
      <div 
      class="rsm-cmpnt" 
      :class="{'margin-top-0': school_i==0}"
      v-for="(school, school_i) in resume.education" 
      :key="'school'+school_i">
        <div class="rsm-cmpnt-top">
          <div class="text-left">
            <div>{{school.institute}}</div>
            <div>{{school.field}}</div>
          </div>
          <div class="text-right font-10">
            <div>{{school.start_m_y}} - {{school.end_m_y}}</div>
            <div>{{school.city}}</div>
          </div>
        </div>
        <div class="rsm-cmpnt-btm" v-for="(highlight, highlight_i) in school.highlights" :key="'work'+highlight_i">
          <p>{{highlight.name}}</p>
          <ul v-if="highlight.details">
            <li v-for="(detail, detail_i) in highlight.details" :key="'detail'+detail_i">{{detail}}</li>
          </ul>
        </div>
      </div>
      <div class="rsm-header" v-if="resume.languages">
        <h2>{{isEn?"Natural Languages":"语言能力"}}</h2>
        <hr>
      </div>
      <div class="rsm-cmpnt margin-top-0" v-if="resume.languages">
        <span
        v-for="(language, language_i) in resume.languages" 
        :key="'language'+language_i">
          {{language.name}}: {{language.proficiency}}&nbsp;|&nbsp;
        </span>
      </div>
      <div class="rsm-header" v-if="resume.additional_info">
        <h2>{{isEn?"Additional Information":"其他信息"}}</h2>
        <hr>
      </div>
      <div 
      class="rsm-cmpnt margin-top-0" 
      v-for="(addtnl_item, addtnl_i) in resume.additional_info" 
      :key="'addtnl'+addtnl_i"
      v-if="resume.additional_info">
        <div>
          <div v-for="(val, name) in addtnl_item" :key="'name'+name">
            {{name}}: {{val}}
          </div>
        </div>
      </div>
    </article>
  </section>
</template>

<script>
export default {
  props: {
    resume: {
        type: Object,
        required: true
    },
    ishidden: {
      type: Boolean,
      required: true
    },
    isEn: {
      type: Boolean,
      required: true
    }
  },
}
</script>

<style>
section.layout03 {
  position: relative;
  margin: 0px auto;
  width: auto;
  min-height: 1080px;
}
.layout03 article {
  margin: 0px auto 10px auto;
  padding: 26px;
  width: 100%;
  background: white;
}
.layout03 table.psnl-info {
  padding: 10px;
  width: 100%;
}
.layout03 table.psnl-info td:first-child {
  width: 20%;
  word-break: break-all;
}
.layout03 table.psnl-info td:last-child {
  width: 23%;
  word-break: break-all;
}
.layout03 .rsm-header {
  margin: 20px 10px 0px 10px;
}
.layout03 .rsm-header h2 {
  margin: 0px;
}
.layout03 .rsm-header hr {
  margin: 0px 0px 10px 0px;
  border: 1px solid black;
}
.layout03 .rsm-cmpnt {
  margin: 20px 10px 0px 10px;
}
.layout03 .margin-top-0 {
  margin-top: 0px;
}
.layout03 .rsm-cmpnt p {
  margin: 0px;
}
.layout03 .rsm-cmpnt-top {
  margin: 0px auto 6px auto;
  display: flex;
}
.layout03 .rsm-cmpnt-top div {
  flex: 1;
  font-weight: bold;
}
.text-left {
  text-align: left;
}
.text-center {
  text-align: center;
}
.text-right {
  text-align: right;
}
.font-10 {
  font-size: 10px;
}
.font-20 {
  font-size: 20px;
}
.layout03 .rsm-cmpnt-mid {
  margin: 0px auto 6px auto;
  font-size: 14px;
  font-style: italic;
}
.layout03 .rsm-cmpnt-btm ul {
  margin: 0px auto 6px auto;
  padding-left: 25px;
  list-style: disc;
}
.layout03 .rsm-cmpnt-btm li {
  font-size: 14px;
}
.layout03 .cmpnt-btn {
  background: #d8d8d8;
}
.layout03 .cmpnt-p-btn {
  background: #eaeaea;
}
.layout03 .cmpnt-li-btn {
  background: white;
}
.layout03.hidden {
  display: none;
}

@media all and (max-width: 450px) {
  .layout03 article {
    padding: 0px;
  }
}
</style>