<template>
  <footer>
    <div class="power" v-show="!store.playerState" style="display: flex; justify-content: space-between;">
    
    <div style="width: 50%;  margin: auto; text-align: center; flex: 1;">
      <!-- 以下信息请不要修改哦 -->
      <span class="hidden" style="color: grey;"
        >&nbsp;&nbsp;Made&nbsp;by&nbsp <a
          :href="config.github"
          target="_blank">imsyy
        </a></span
      >&nbsp;
 
       <span style="color: grey;">本站总访问量 <span id="busuanzi_value_site_pv" ></span>                次
       </span>    
    </div>   
  <span class="timetu" 
      v-if="store.siteStartShow" style="margin-right: 10px;"
>
  <span class="text hidden-text" v-html="startDateText" /></span>

                
                
        
      
    </div>
    <div class="lrc" v-show="store.playerState">
      <music-one theme="filled" size="18" fill="#efefef" />
      <span class="lrc-text">
        {{ store.getPlayerLrc ? store.getPlayerLrc : "这句没有歌词" }}
      </span>
      <music-one theme="filled" size="18" fill="#efefef" />
    </div>
  </footer>
</template>
<!--不蒜子计数器-->

<script setup>
import { MusicOne } from "@icon-park/vue-next";
import { mainStore } from "@/store";
import config from "@/../package.json";


import { getTimeCapsule, siteDateStatistics } from "@/utils/getTime.js";
import { onMounted, onBeforeUnmount, ref } from "vue";
const store = mainStore();
let isVisible = false;
let timeData = ref(getTimeCapsule());
let startDate = ref(import.meta.env.VITE_SITE_START);
let startDateText = ref(null);
let timeInterval = null;

onMounted(() => {
  timeInterval = setInterval(() => {
    timeData.value = getTimeCapsule();
    if (startDate.value)
      startDateText.value = siteDateStatistics(new Date(startDate.value));
  }, 1000);
});

let fullYear = new Date().getFullYear();
var bszCaller,bszTag;!function(){var c,d,e,a=!1,b=[];ready=function(c){return a||"interactive"===document.readyState||"complete"===document.readyState?c.call(document):b.push(function(){return c.call(this)}),this},d=function(){for(var a=0,c=b.length;c>a;a++)b[a].apply(document);b=[]},e=function(){a||(a=!0,d.call(window),document.removeEventListener?document.removeEventListener("DOMContentLoaded",e,!1):document.attachEvent&&(document.detachEvent("onreadystatechange",e),window==window.top&&(clearInterval(c),c=null)))},document.addEventListener?document.addEventListener("DOMContentLoaded",e,!1):document.attachEvent&&(document.attachEvent("onreadystatechange",function(){/loaded|complete/.test(document.readyState)&&e()}),window==window.top&&(c=setInterval(function(){try{a||document.documentElement.doScroll("left")}catch(b){return}e()},5)))}(),bszCaller={fetch:function(a,b){var c="BusuanziCallback_"+Math.floor(1099511627776*Math.random());window[c]=this.evalCall(b),a=a.replace("=BusuanziCallback","="+c),scriptTag=document.createElement("SCRIPT"),scriptTag.type="text/javascript",scriptTag.defer=!0,scriptTag.src=a,scriptTag.referrerPolicy="no-referrer-when-downgrade",document.getElementsByTagName("HEAD")[0].appendChild(scriptTag)},evalCall:function(a){return function(b){ready(function(){try{a(b),scriptTag.parentElement.removeChild(scriptTag)}catch(c){bszTag.hides()}})}}},bszCaller.fetch("//busuanzi.ibruce.info/busuanzi?jsonpCallback=BusuanziCallback",function(a){bszTag.texts(a),bszTag.shows()}),bszTag={bszs:["site_pv","page_pv","site_uv"],texts:function(a){this.bszs.map(function(b){var c=document.getElementById("busuanzi_value_"+b);c&&(c.innerHTML=a[b])})},hides:function(){this.bszs.map(function(a){var b=document.getElementById("busuanzi_container_"+a);b&&(b.style.display="none")})},shows:function(){this.bszs.map(function(a){var b=document.getElementById("busuanzi_container_"+a);b&&(b.style.display="inline")})}};
</script>

<style lang="scss" scoped>

.hidden-text {
    visibility: hidden;
    transition: visibility 0.5s ease;
}

.timetu:hover .hidden-text {
    visibility: visible;
}
footer {
  width: 100%;
  position: absolute;
  bottom: 0;
  left: 0;
  height: 36px;
  font-size: 13px;
  line-height: 36px;
  text-align: center;
  backdrop-filter: blur(10px);
  background: rgb(0 0 0 / 25%);
  z-index: 0;
  animation: fade;
  -webkit-animation: fade 0.5s;
  @media (max-width: 720px) {
    font-size: 0.85rem;
  }
  @media (max-width: 480px) {
    .hidden {
      display: none;
    }
  }
  .power {
    animation: fade;
    -webkit-animation: fade 0.3s;
  }
  .lrc {
    padding: 0 20px;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    animation: fade;
    -webkit-animation: fade 0.3s;
    .lrc-text {
      margin: 0 8px;
      display: -webkit-box;
      -webkit-box-orient: vertical;
      -webkit-line-clamp: 1;
      overflow: hidden;
      word-break: break-all;
    }
    .i-icon {
      width: 18px;
      height: 18px;
      display: inherit;
    }
  }
}
</style>
