<template>
   <div class="header">
     <div class="top">
       <a class="logo" href="/about" title="234">
         <img width="32" height="32" src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNzcuNjcgMjc3LjY3Ij48ZGVmcz48c3R5bGU+LmNscy0xe2ZpbGw6IzBjNjRjZDt9PC9zdHlsZT48L2RlZnM+PGcgaWQ9IkxheWVyXzIiIGRhdGEtbmFtZT0iTGF5ZXIgMiI+PGcgaWQ9IkxheWVyXzEtMiIgZGF0YS1uYW1lPSJMYXllciAxIj48Y2lyY2xlIGNsYXNzPSJjbHMtMSIgY3g9IjEzOC44IiBjeT0iNjYuNTEiIHI9IjExLjQ3Ii8+PGNpcmNsZSBjbGFzcz0iY2xzLTEiIGN4PSIyMDAuOCIgY3k9IjE0MS4yNiIgcj0iMTEuNDciLz48Y2lyY2xlIGNsYXNzPSJjbHMtMSIgY3g9IjgwLjMiIGN5PSIxMTUuMzgiIHI9IjExLjQ3Ii8+PHBhdGggY2xhc3M9ImNscy0xIiBkPSJNMjc3LjY3LDE2Ny41MVYxMTAuMThoLTM5YTEwMi43NCwxMDIuNzQsMCwwLDAtOS0yMS42NGwyNy42LTI3LjZMMjE2LjczLDIwLjQsMTg5LjEzLDQ4YTEwMi44MywxMDIuODMsMCwwLDAtMjEuNjUtOVYwSDExMC4xNVYzOWExMDMuMjcsMTAzLjI3LDAsMCwwLTIxLjYyLDlMNjAuOTIsMjAuMzgsMjAuMzgsNjAuOTIsNDgsODguNTNhMTAzLDEwMywwLDAsMC05LDIxLjY1SDB2NTcuMzNIMzlhMTAzLDEwMywwLDAsMCw5LDIxLjY0bC0yNy42LDI3LjU5TDM1LjI1LDIzMS42bDM2Ljg0LTM3LjEzVjEzOC4zNWEyNC40MSwyNC40MSwwLDEsMSwxNi40OSwwdjYyLjg3bC00MS42OSw0MiwxNCwxNCwyNy42LTI3LjZhMTAyLjc3LDEwMi43NywwLDAsMCwyMS42Miw5djM5aDIwLjQ0Vjg5LjQ4YTI0LjQxLDI0LjQxLDAsMSwxLDE2LjQ5LDBWMjc3LjY3aDIwLjR2LTM5YTEwMi45MSwxMDIuOTEsMCwwLDAsMjEuNjYtOWwyNy41OCwyNy41OCwxNC4zOS0xNC4zOS0zOC41Mi0zOS4wNVYxNjQuMjNhMjQuNDEsMjQuNDEsMCwxLDEsMTYuNDksMFYxOTdsMzMuNywzNC4xOCwxNC40OC0xNC40OC0yNy41OS0yNy41OGExMDIuODUsMTAyLjg1LDAsMCwwLDktMjEuNjNaIi8+PC9nPjwvZz48L3N2Zz4=">
         <h3 class="name"> {{$t('LogoName')}}</h3>
       </a>
       <div style="flex-grow: 1"></div>
       <div class="language">
         <el-link type="primary" @click="changeLanguage">{{languageTxt}}</el-link>
       </div>
       <div >
         <div class="right" v-popover="popoverRef" v-click-outside="onClickOutside">
                      <span class="userName">test</span> <el-avatar :size="30"> L </el-avatar>
           <el-popover
             ref="popoverRef"
             trigger="hover"
             width="10px"
             virtual-triggering
             persistent
           >
             <div style="text-align: center"><el-link type="primary" @click="logout">退出</el-link></div>
           </el-popover>

         </div>
       </div>

     </div>
  </div>
</template>

<script setup>
import { onMounted, ref,unref } from "vue";
import { Language } from "@/model/enum";
import { ClickOutside as vClickOutside } from 'element-plus'
import router from "@/router";

const languageTxt=ref('')
const changeLanguage=()=>{
  languageTxt.value=languageTxt.value===Language.zh?Language.en:Language.zh
  localStorage.setItem('lang',languageTxt.value)
  window.location.reload();
}
onMounted(()=>{
  languageTxt.value=localStorage.getItem('lang')
})

const buttonRef = ref()
const popoverRef = ref()
const onClickOutside = () => {
  unref(popoverRef).popperRef?.delayHide?.()
}
const logout=()=>{
  localStorage.removeItem("token")
  router.replace("/login")
}

</script>

<style scoped lang="scss">
 .header{
   z-index: 1200;
   display: flex;
   position: fixed;

   width: 100%;
   box-shadow: 0px 8px 24px rgba(0, 53, 133, 0.1);
   background-color: #fff;
   padding: 0px 16px 0px 16px;

   .top{
     width: 100%;
     display: flex;
     align-items: center;
     min-height: 60px;
     height: 60px;
     .logo{
       display: flex;
       flex-wrap: nowrap;
       align-items: center;
       margin-right: 10px;
       border-radius: 50px;
       padding: 8px;
       .name{
         margin: 0;
         color: #0C64CD;
         margin-left: 12px;
         white-space: nowrap;
         font-size: 16px;
         font-family: Montserrat, sans-serif;
         font-weight: 600;
         line-height: 1.167;
         letter-spacing: 0em;
       }
     }
     .logo:hover{
       background: rgba(0,0,0,0.04)
     }
     .right{
       margin-right: 50px;
       color: #051221;
       border: 1px solid #E6E7E9;
       padding: 6px 8px;
       border-radius: 10px;
       align-items: center;
       .userName{
         cursor: pointer;
         padding-left: 6px;
         padding-right: 10px;
         margin-right: 2px   ;
         font-size: 14px;
         font-family: Nunito Sans, sans-serif;
         font-weight: 600;
         line-height: 1.5;
         letter-spacing: 0.00938em;
       }

     }
     .right:hover{
       cursor: pointer;
     }
     .language{
       margin-right: 20px;
     }
     .language:hover{
       cursor: pointer;
     }
   }

}

</style>