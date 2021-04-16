<template>
	<section class="layout02" :class="{'hidden': ishidden}">
    <article>
      <h2>{{resume.fullName}}</h2>
      <p class="font-18">{{resume.desired_position}}</p>
      <p class="font-12">
        &nbsp;<i class="fa fa-mobile-phone font-18"></i>
        {{resume.tel}}
      </p>
      <p class="font-12">
        <i class="fa fa-envelope"></i>
        {{resume.email}}
      </p>
      <p class="font-12">
        <i class="fa fa-home font-16"></i>
        {{resume.location}}
      </p>
      <div class="rsm-header">
        <div class="font-18 bold">{{isEn?"Professional Skills":"专业技能"}}</div>
        <hr>
      </div>
      <div class="rsm-cmpnt" 
      v-for="(skill, skill_i) in resume.pro_skills" 
      :key="'skill'+skill_i">
        <div class="rsm-cmpnt-top">
          <div>
            <div class="font-14 bold">{{skill.nature}}</div>
          </div>
        </div>
        <div class="rsm-cmpnt-btm">
          <p class="font-12">
            <span v-for="(skillName, skillName_i) in skill.names" :key="skillName+skillName_i">
              {{skillName}}<span v-if="skillName_i+1<skill.names.length">, </span>
            </span>
          </p>
        </div>
      </div>
      <div class="rsm-header">
        <div class="font-18 bold">{{isEn?"Education":"教育背景"}}</div>
        <hr>
      </div>
      <div 
      class="rsm-cmpnt" 
      v-for="(school, school_i) in resume.education" 
      :key="'school'+school_i">
        <div class="rsm-cmpnt-top">
          <div>
            <div class="font-14 bold">{{school.field}}</div>
            <div class="font-12">{{school.institute}}</div>
            <div class="font-12">
              <i class="fa fa-calendar"></i>
              {{school.start_m_y}} - {{school.end_m_y}}
            </div>
          </div>
        </div>
      </div>
      <div class="rsm-header" v-if="resume.languages">
        <div class="font-18 bold">{{isEn?"Languages":"语言能力"}}</div>
        <hr>
      </div>
      <div class="rsm-cmpnt" v-if="resume.languages">
        <span
        v-for="(language, language_i) in resume.languages" 
        :key="'language'+language_i" class="font-14">
          {{language.name}}
          <span v-if="language_i < resume.languages.length - 1">, </span>
        </span>
      </div>
      <div class="rsm-header" v-if="resume.additional_info">
        <div class="font-18 bold">{{isEn?"Other Information":"其他信息"}}</div>
        <hr>
      </div>
      <div class="rsm-cmpnt" v-if="resume.additional_info">
        <div v-for="(addtnl_item, addtnl_i) in resume.additional_info" 
        :key="'addtnl'+addtnl_i" 
        class="font-14">
          <span v-for="(val, name) in addtnl_item" :key="'name'+name">
            {{name}}: {{val}}
          </span>
        </div>
      </div>
    </article>
    <article>
      <div class="rsm-header">
        <h2>{{isEn?"Summary":"个人简介"}}</h2>
        <hr>
      </div>
      <div class="rsm-cmpnt margin-top-0">{{resume.summary}}</div>
      <div class="rsm-header">
        <h2>{{isEn?"Work Experience":"工作经历"}}</h2>
        <hr>
      </div>
      <div 
      class="rsm-cmpnt" :class="{'margin-top-0': !work.company||work_i==0}"
      v-for="(work, work_i) in resume.work_exp" 
      :key="'work'+work_i">
        <div class="rsm-cmpnt-top bold">
          <div class="text-left flex-2">
            <div v-if="work.company">{{work.company}}</div>
            <div>{{work.title}}</div>
          </div>
          <div class="text-right font-10 flex-1">
            <div>
              {{work.start_m_y}} - {{work.end_m_y}}
              <i class="fa fa-calendar"></i>
            </div>
            <div v-if="work.city">
              {{work.city}}
              <i class="fa fa-map-marker font-16"></i>
            </div>
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
section.layout02 {
  position: relative;
  margin: 0px auto;
  width: auto;
  min-height: 1080px;
  display: flex;
}
.layout02 article {
  margin: 0px auto;
  padding: 24px;
  width: 100%;
  background: white;
}
.layout02 article:first-child {
  width: 300px;
  background: antiquewhite;
}
.layout02 article:first-child h2 {
  margin: 0px;
}
.layout02 .rsm-header {
  margin: 20px auto 0px auto;
}
.layout02 .rsm-header:first-child {
  margin-top: 0px;
}
.layout02 .rsm-header h2 {
  margin: 0px;
}
.layout02 hr {
  margin: 0px 0px 10px 0px;
  border: 1px solid black;
}
.layout02 .rsm-cmpnt {
  margin: 20px 0px 0px 0px;
}
.layout02 article:first-child .rsm-cmpnt {
  margin: 10px auto;
}
.layout02 .rsm-cmpnt p {
  margin: 0px;
}
.layout02 .rsm-cmpnt-top {
  margin: 0px auto 6px auto;
  display: flex;
}
.layout02 .rsm-cmpnt-top div {
  flex: 1;
}
.layout02 .margin-top-0 {
  margin-top: 0px;
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
.font-12 {
  font-size: 12px;
}
.font-14 {
  font-size: 14px;
}
.font-16 {
  font-size: 16px;
}
.font-18 {
  font-size: 18px;
}
.font-20 {
  font-size: 20px;
}
.bold {
  font-weight: bold;
}
.layout02 .rsm-cmpnt-mid {
  margin: 0px auto 6px auto;
  font-size: 14px;
  font-style: italic;
}
.layout02 .rsm-cmpnt-btm ul {
  margin: 0px auto 6px auto;
  padding-left: 25px;
  list-style: disc;
}
.layout02 .rsm-cmpnt-btm li {
  font-size: 14px;
}
.layout02 article:first-child .rsm-cmpnt {
  margin-bottom: 10px;
}
.layout02 article:first-child hr {
  margin-bottom: 0px;
}
.layout02.hidden {
  display: none;
  height: 0px;
}

@media all and (max-width: 450px) {
  section.layout02 {
    display: block;
  }
  .layout02 article:first-child {
    margin: 0px 24px;
    padding: 0px;
    width: auto;
    text-align: center;
  }
  .layout02 article {
    padding: 0px;
  }
  .layout02 article:first-child {
    margin: 0px;
  }
}
</style>