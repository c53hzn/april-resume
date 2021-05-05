<template>
  <div class="resume-wrap main-content">
    <div class="changeBtnOuter">
      <span class="changeBtns">
        <select @change="changeLayout" v-model="selectedLayout">
          <option v-for="(value, name, index) in layout" :key="index">
            {{name}}
          </option>
        </select>
      </span>
      <span class="changeBtns">
        <select @change="toggleLang" v-model="lang">
          <option value='en'>
            English
          </option>
          <option value='zh'>
            中文
          </option>
        </select>
      </span>
      <span class="changeBtns align-right">
        <button id="printBtn" @click="printResume">Print</button>
      </span>
    </div>

  	<layout01 :resume="resume" :isEn="lang=='en'" :ishidden="!layout['Layout 1']" :class="{'resume': layout['Layout 1']}" :key="'Layout 1'+modes.en.status"></layout01>
    <layout02 :resume="resume" :isEn="modes.en.status" :ishidden="!layout['Layout 2']" :class="{'resume': layout['Layout 2']}" :key="'Layout 2'+modes.en.status"></layout02>
    <layout03 :resume="resume" :isEn="modes.en.status" :ishidden="!layout['Layout 3']" :class="{'resume': layout['Layout 3']}" :key="'Layout 3'+modes.en.status"></layout03>
    <layout04 :resume="resume" :isEn="modes.en.status" :ishidden="!layout['Layout 4']" :class="{'resume': layout['Layout 4']}" :key="'Layout 4'+modes.en.status"></layout04>
  </div>
</template>

<script>
import getResume from './getresume';
import config from './resume.config';
import yaml from "yaml";
import layout01 from "./components/resume/Resume-top-down-simple.vue";
import layout02 from "./components/resume/Resume-sidebar-left-pink.vue";
import layout03 from "./components/resume/Resume-top-down-full.vue";
import layout04 from "./components/resume/Resume-sidebar-left-black.vue";

export default {
	name: "April-Resume",
	data() {
		return {
			lang: 'en',
			resumeObj: {
	        en: {}, 
	        zh: {}
		    },
		    modes_en: {
	        en: {status: true},
	        zh: {status: false}
		     },
		    modes_zh: {
	        en: {status: false},
	        zh: {status: true}
		    },
			layout: {
				'Layout 1': true,
				'Layout 2': false,
				'Layout 3': false,
        'Layout 4': false
			},
		   	selectedLayout: 'Layout 1',
		};
  },
	mounted() {
		this.loadResume();
	},
	components: {
    layout01,
    layout02,
    layout03,
    layout04,
	},
	computed: {
    modes(){
    	return this.lang=="zh"?this.modes_zh:this.modes_en;
    },
    resume() {
    	return this.lang=="zh"?this.resumeObj.zh:this.resumeObj.en;
    }
	},
  methods: {
  	loadResume() {
  		var that = this;
  		var en = getResume(config.en);
		  var zh = getResume(config.zh);
		  Promise.all([en,zh]).then(arr=>{
        that.resumeObj.en = yaml.parse(arr[0]);
	      that.resumeObj.zh = yaml.parse(arr[1]);
		  });
  	},
    changeLayout: function() {
      var that = this;
      for (let k in that.layout) {
        if (k == that.selectedLayout) {
          that.layout[k] = true;
        } else {
          that.layout[k] = false;
        }
      }
    },
    printResume: function() {
    	var that = this;
    	var d = document;
    	var resume = d.querySelector('.resume').cloneNode(true);
    	
    	var newWin = window.open("");
      var newHead = newWin.document.head;
    	var newBody = newWin.document.body;
    	var fa = d.createElement("link");
    	fa.rel = "stylesheet";
    	fa.href = "https://cdn.bootcss.com/font-awesome/4.4.0/css/font-awesome.min.css";
      newHead.appendChild(fa);
      
      var styles = d.querySelectorAll('style');
    	for (let i = 0; i < styles.length; i++) {
    		newHead.appendChild(styles[i].cloneNode(true))
    	}
    	
      newBody.style.width = "768px";
    	newBody.appendChild(resume.cloneNode(true));
    	setTimeout(function(){
    		newWin.print();
    	}, 4000);
    },
  }
};
</script>

<style type="text/css">
* {
	box-sizing: border-box;
}
.main-content {
  margin: 20px auto;
  padding: 20px 40px;
  width: 1080px;
  min-height: calc(100vh - 189px);
  background: white;
  border: 1px solid silver;
  border-radius: 5px;
}
@media (max-width: 1080px) {
	.main-content {
    margin: 0px;
    padding: 10px;
    width: auto;
    min-height: calc(100vh - 112px);
    border: none;
    border-radius: 0px;
	}   
}
.resume-wrap {
  position: relative;
}
.changeBtnOuter {
  margin-bottom: 10px;
  display: flex;
}
.changeBtns {
  flex:1 1 auto;
}
.changeBtns select {
	height: 20px;
}
.changeBtnOuter button {
	border-radius: 0px;
}
.changeBtn {
  margin-right: 5px;
}
.align-right {
  text-align: right;
}
</style>