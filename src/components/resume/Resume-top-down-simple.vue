<template>
	<section class="layout01" :class="{'hidden': ishidden}">
    <article>
      <table class="psnl-info">
        <tbody>
          <tr>
            <td rowspan="2" class="font-24 font-bold">{{resume.fullName}}</td>
            <td class="text-right font-14 text-blue">{{resume.tel}}</td>
            <td class="text-center text-blue"><i class="fa fa-mobile-phone font-24"></i></td>
          </tr>
          <tr>
            <td class="text-right font-14 text-blue">{{resume.email}}</td>
            <td class="text-center text-blue"><i class="fa fa-envelope"></i></td>
          </tr>
          <tr>
            <td class="font-18 text-blue">{{resume.desired_position}}</td>
            <td class="text-right font-14 text-blue">{{resume.location}}</td>
            <td class="text-center text-blue"><i class="fa fa-home font-20"></i></td>
          </tr>
        </tbody>
      </table>
      <p class="padd-10">{{resume.summary}}</p>
      <div class="rsm-header text-blue">
        <h2><i class="fa fa-paint-brush">&nbsp;</i>{{isEn?"Professional Skills":"专业技能"}}</h2>
        <hr>
      </div>
      <div class="rsm-cmpnt margin-top-0">
        <div class="rsm-cmpnt-btm">
          <p class="line-h-30">
            <span v-for="(skill, skill_i) in resume.pro_skills" 
            :key="'skill'+skill_i"><!--
           --><span class="skill-item"
              v-for="(skillName, skillName_i) in skill.names"
              :key="skillName+skillName_i"><!--
            -->{{skillName}}<!--
           --></span><!--
         --></span>
          </p>
        </div>
      </div>
      <div class="rsm-header text-blue">
        <h2><i class="fa fa-language">&nbsp;</i>{{isEn?"Languages":"语言能力"}}</h2>
        <hr>
      </div>
      <div class="rsm-cmpnt margin-top-0">
        <p class="line-h-30">
          <span class="skill-item"
          v-for="(language, language_i) in resume.languages" 
          :key="'language'+language_i"><!--
         -->{{language.name}}<!--
       --></span>
        </p>
      </div>
      <div class="rsm-header text-blue">
        <h2><i class="fa fa-briefcase">&nbsp;</i>{{isEn?"Work Experience":"工作经验"}}</h2>
        <hr>
      </div>
      <div 
      class="rsm-cmpnt" :class="{'margin-top-0': !work.company||work_i == 0}"
      v-for="(work, work_i) in resume.work_exp" 
      :key="'work'+work_i">
        <div class="rsm-cmpnt-top">
          <div class="text-left">
            <div v-if="work.company">{{work.company}}</div>
            <div>{{work.title}}</div>
          </div>
          <div class="text-right font-10 text-blue">
            <div v-if="work.city">
              {{work.city}}
              <i class="fa fa-map-marker font-16"></i>
            </div>
            <div>
              {{work.start_m_y}} - {{work.end_m_y}}
              <i class="fa fa-calendar"></i>
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
              <span class="text-black">{{item}}</span>
            </li>
          </ul>
        </div>
      </div>
      <div class="rsm-header text-blue">
        <h2><i class="fa fa-graduation-cap">&nbsp;</i>{{isEn?"Education":"教育背景"}}</h2>
        <hr>
      </div>
      <div 
      class="rsm-cmpnt" 
      :class="{'margin-top-0': school_i == 0}"
      v-for="(school, school_i) in resume.education" 
      :key="'school'+school_i">
        <div class="rsm-cmpnt-top">
          <div class="text-left">
            <div>{{school.institute}}</div>
            <div>{{school.field}}</div>
          </div>
          <div class="text-right font-10  text-blue">
            <div>
              {{school.start_m_y}} - {{school.end_m_y}}
              <i class="fa fa-calendar"></i>
            </div>
            <div>
              {{school.city}}
              <i class="fa fa-map-marker font-16"></i>
            </div>
          </div>
        </div>
        <div class="rsm-cmpnt-btm" v-for="(highlight, highlight_i) in school.highlights" :key="'work'+highlight_i">
          <p>{{highlight.name}}</p>
          <ul v-if="highlight.details">
            <li v-for="(detail, detail_i) in highlight.details" :key="'detail'+detail_i">
              <span class="text-black">
                {{detail}}
              </span>
            </li>
          </ul>
        </div>
      </div>
      <div class="rsm-header text-blue">
        <h2>{{isEn?"Additional Information":"其他信息"}}</h2>
        <hr>
      </div>
      <div 
      class="rsm-cmpnt margin-top-0" 
      v-for="(addtnl_item, addtnl_i) in resume.additional_info" 
      :key="'addtnl'+addtnl_i">
        <div class="rsm-cmpnt-top">
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
  }
}
</script>

<style>
section.layout01 {
  position: relative;
  margin: 0px auto;
  width: auto;
  min-height: 1080px;
}
.layout01 article {
  margin: 0px auto 10px auto;
  padding: 26px;
  background: white;
}
.layout01 .psnl-info {
  margin: 0px auto 10px auto;
  padding: 10px;
  width: 100%;
  word-break: break-all;
}
.layout01 .psnl-info td:last-child {
  width: 24px;
}
.layout01 .rsm-header {
  margin: 20px 10px 0px 10px;
}
.layout01 .rsm-header h2 {
  margin: 0px;
}
.layout01 .rsm-header hr {
  margin: 0px 0px 10px 0px;
  border: 1px solid #164677;
}
.layout01 .rsm-cmpnt {
  margin: 20px 10px 0px 10px;
}
.layout01 .rsm-cmpnt p {
  margin: 0px;
}
.layout01 .rsm-cmpnt-top {
  margin: 0px auto 6px auto;
  display: flex;
}
.layout01 .rsm-cmpnt-top div {
  flex: 1;
  font-weight: bold;
}
.layout01 .padd-10 {
  padding: 10px;
}
.layout01 .text-blue {
  color: #164677;
}
.layout01 .text-left {
  text-align: left;
}
.layout01 .text-center {
  text-align: center;
}
.layout01 .text-right {
  text-align: right;
}
.layout01 .text-black {
  color: black;
}
.layout01 .margin-top-0 {
  margin-top: 0px;
}
.font-10 {
  font-size: 10px;
}
.font-20 {
  font-size: 20px;
}
.font-24 {
  font-size: 24px;
}
.font-bold {
  font-weight: bold;
}
.layout01 .rsm-cmpnt-mid {
  margin: 0px auto 6px auto;
  font-size: 14px;
  font-style: italic;
}
.layout01 .rsm-cmpnt-btm ul {
  margin: 0px auto 6px auto;
  padding-left: 25px;
  list-style: disc;
}
.layout01 .rsm-cmpnt-btm li {
  font-size: 14px;
  color: #164677;
}
.layout01 .skill-item {
  margin: 0px 10px 10px 0px;
  padding: 0px 4px;
  color: white;
  background: #164677;
  border-radius: 4px;
  display:inline-block;
}
.layout01 .line-h-30 {
  line-height: 30px;
}
.layout01.hidden {
  display: none;
  height: 0px;
}

@media all and (max-width: 450px) {
  .layout01 article {
    padding: 0px;
  }
}
</style>