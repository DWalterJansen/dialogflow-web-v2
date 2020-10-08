<template>
  <div class="welcome-view">
    <!-- Agent Icon -->
    <!-- <img class="agent-icon" src="../assets/img/DrPresente_v2.png" :alt="drpresente" /> -->

    <!-- Agent Title -->
    <!-- <div class="agent-title">Dr. Presente</div> -->
    <!-- <img class="agent-title-img" src="../assets/img/logo_outubrorosa.png" :alt="drpresente-logo" /> -->
    <img class="agent-head-icon" src="https://i.imgur.com/0DORkTh.png" alt="drpresente-logo">

    <!-- Agent Description -->
    <!-- <img class="agent-banner" src="https://i.imgur.com/vSWISzi.png" alt="Banner Teste Anemia"> -->
    <div class="agent-title">
      Suspeita de <span class="agent-destaque">anemia</span>?
    </div>
    <div class="agent-description">
      Realize o seu teste rápido de anemia e ainda encontre médicos especializados que vão te ajudar a entender mais sobre o assunto. Para começar digite "Oi".
    </div>
    <div class="agent-term">
      * Ao participar do Teste, você concorda com a <a href="https://hhelp.io/#/politica-privacidade" target="_blank" >Política de Privacidade</a> da hhelp. 
    </div>
    <!-- Language picker, if your Agent supports more than one language -->
    <!-- <div v-if="agent.supportedLanguageCodes && agent.supportedLanguageCodes.length > 0" class="language-picker">
            <select v-model="sel_lang" :aria-label="(translations[lang()] && translations[lang()].selectLanguageTitle) || translations[config.fallback_lang].selectLanguageTitle">
                <option :value="agent.defaultLanguageCode">{{agent.defaultLanguageCode | toLang}}</option>
                <option v-for="language in agent.supportedLanguageCodes" :key="language" :value="language">{{language | toLang}}</option>
            </select>
            <i aria-hidden="true" class="material-icons">arrow_drop_down</i>
    </div>-->
  </div>
</template>

<style lang="sass" scoped>
@import '@/style/mixins'


.welcome-view
  text-align: center
  display: flex
  flex-direction: column
  align-items: center

.agent-icon
  width: 180px
  height: 220px
  object-fit: cover

.agent-head-icon
  padding-top: 5px
  width: 160px
  height: 60px

.agent-title-img
  width: 250px
  height: 50px

.agent-title
  font-size: 36px
  margin-top: 30px
  color: var(--accent)
  line-height: 36px
  font-weight: bold

.agent-destaque
  color: var(--destaque)

.agent-description
  font-size: 18px
  color: var(--accent)
  padding-top: 30px
  padding-bottom: 20px
  
.agent-term a
  font-weight: bold
  color: var(--accent)

.agent-term
  font-size: 14px
  color: var(--text-term)
  padding-top: 10px
  padding-bottom: 20px

.agent-banner
  @media screen and (max-width: 600px)
    width: 320px
    height: 100px

  @media (min-width: 600px) and (max-width: 1000px)
    width: 560px
    height: 200px

  @media (min-width: 800px) and (max-width: 1000px)
    width: 800px
    height: 260px

.language-picker
  display: inline-flex
  border: var(--border)
  border-radius: 40px
  cursor: pointer
  margin-right: 2px
  color: var(--text-primary)
  align-items: center

  select
    width: 100%
    padding: 8px 12px
    margin-right: -24px
    padding-right: 24px

    i
      pointer-events: none
</style>

<script>
import * as langs from "langs";

export default {
  name: "WelcomeView",
  filters: {
    /* This filter turns language code to the local language name using the langs dependency (example "en" -> "English") */
    toLang(code) {
      return langs.where("1", code.substring(0, 2)).local;
    }
  },
  props: {
    agent: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      sel_lang: ""
    };
  },
  watch: {
    /* Save selected language */
    sel_lang(lang) {
      if (this.history()) sessionStorage.setItem("lang", lang);
      else {
        this.config.fallback_lang = lang;
      }
    }
  },
  /* Set default language on load (or fallback) */
  created() {
    if (this.agent && this.agent.defaultLanguageCode) {
      this.sel_lang = this.agent.defaultLanguageCode;
    } else {
      this.sel_lang = this.config.fallback_lang;
    }
  }
};
</script>
