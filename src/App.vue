<template>
  <Header :header="this.header" />
  <div class="content-container" style="width:100%">
    <section class="section-container" id="missions" style="width:435px; height:714px;">
      <div class="section-header clipped-medium-backward">
        <img src="/icons/mission-icon.svg" />
        <h1>Mission Log</h1>
      </div>
      <div class="section-content-container">
        <h3>Current Assignment</h3>
        <Markdown :source="current_md" class="markdown" />
        <h3>Mission List</h3>
        <div class="mission-list-container">
          <Mission
            v-for="item in this.missions"
            :key="item.slug"
            :mission="item"
            :selected="this.mission_slug"
            @click="selectMission(item)"
          />
        </div>
      </div>
    </section>
    <section class="section-container" id="events" style="width:655px; height:714px;">
      <div class="section-header clipped-medium-backward">
        <img src="/icons/events-icon.svg" />
        <h1>Events Log</h1>
      </div>
      <div class="section-content-container">
        <Markdown :source="events" class="markdown" />
      </div>
    </section>
    <section class="section-container" id="pilots" style="width:694px; height:714px;">
      <div style="height:52px; overflow:hidden;">
        <div class="section-header clipped-medium-backward-pilot">
          <img src="/icons/pilot-icon.svg" />
          <h1>Pilot Roster</h1>
        </div>
        <div class="rhombus-back">&nbsp;</div>
      </div>
      <div class="section-content-container">
        <div class="pilot-list-container">
          <Pilot v-for="item in this.pilots" :key="item.slug" :pilot="item" />
        </div>
      </div>
    </section>
     <section class="section-container" id="guest" style="width:494px; height:714px;">
      <div style="height:52px; overflow:hidden;">
        <div class="section-header clipped-medium-backward-pilot">
          <img src="/icons/pilot-icon.svg" />
          <h1>Guest Roster</h1>
        </div>
        <div class="rhombus-back">&nbsp;</div>
      </div>
      <div class="section-content-container">
        <div class="pilot-list-container">
          <Guest v-for="item in this.guests" :key="item.slug" :guest="item" />
        </div>
      </div>
    </section>
  </div>
  <svg
    style="visibility: hidden; position: absolute;"
    width="0"
    height="0"
    xmlns="http://www.w3.org/2000/svg"
    version="1.1"
  >
    <defs>
      <filter id="round">
        <feGaussianBlur in="SourceGraphic" stdDeviation="5" result="blur" />
        <feColorMatrix
          in="blur"
          mode="matrix"
          values="1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 19 -5"
          result="goo"
        />
        <feComposite in="SourceGraphic" in2="goo" operator="atop" />
      </filter>
    </defs>
  </svg>
  <audio autoplay>
    <source src="/startup.ogg" type="audio/ogg" />
  </audio>
  <Footer/>
</template>

<script>
import Header from './components/layout/Header.vue';
import Footer from './components/layout/Footer.vue';
import Mission from './components/Mission.vue';
import Pilot from './components/Pilot.vue';
import Guest from './components/Guest.vue';
import Markdown from 'vue3-markdown-it';

export default {
  components: {
    Header,
    Footer,
    Mission,
    Pilot,
    Guest,
    Markdown
  },

  data() {
    return {
      "mission_slug": "007a",
      "current_md": "007a",
      "events": "",
      "missions": [
        {
          "slug": "007a",
          "name": "Making friends and influencing corpros",
          "status": "start"

        },

         {
          "slug": "007b",
          "name": "Into the blinkspace breach",
          "status": "start"

        },
      ],
      "pilots": [
        {
          "callsign": "chair",
          "alias": "Chadwick O'Brian",
          "code": "462370be-bd0f-41c2-b667-cc75f3a59a96///Umbra-Station//377308ad-ba23-410b-ae37-68a1fb5f8db4",
          "corpro": "Horus",
          "frame": "Pattern Group Balor",
          "mech": "Nega-Gurren_MK_I"
        },
        {
          "callsign": "crosscut",
          "alias": "Johnathan Doomguy #117",
          "code": "7cd700cc-c990-48ed-892f-e5468de724c4///Umbra-Station//a98c3e28-ad4a-4f89-bcd9-501464e960da",
          "corpro": "IPS-N",
          "frame": "Caliban",
          "mech": "Unmakyr"
        },
        {
          "callsign": "example",
          "alias": "Gideon Gilgerde",
          "code": "4be26ce9-923b-4069-b6c9-76437d4be455///Umbra-Station//056940c6-8d55-4190-8e85-57caa043cb1a",
          "corpro": "HA",
          "frame": "Tokugawa",
          "mech": "SILVER HOWL REBAKE 'RISING PHOENIX'"
        },
        {
          "callsign": "quickdraw",
          "alias": "Sven Arf Saith",
          "code": "98ca9616-044e-4f87-b89b-aae4eb3387ec///Umbra-Station//6f572259-6946-41bf-931a-e0543709e892",
          "corpro": "Horus",
          "frame": "Pattern group Pegasus",
          "mech": "Angel Eyes"
        },
        {
          "callsign": "traitor",
          "alias": "Malintzin the Traitor",
          "code": "d1fdf62e-d81e-4e10-97c8-df3bc4860117///Umbra-Station//5a4254aa-9fa2-42ca-a077-8f5bfd1e1ad3",
          "corpro": "Horus",
          "frame": "Pattern group Minotaur",
          "mech": "BABIECA THE MINOTAUR"
        },
         {
          "callsign": "Mama",
          "alias": "Maritsa Yarova",
          "code": "3829e09c-eaad-455e-8596-835eef8276df///Umbra-Station//5a4254aa-9fa2-42ca-a077-8f5bfd1e1ad3",
          "corpro": "IPS-N",
          "frame": "Drake",
          "mech": "New Best Friend"
        },
      ],
      "guests": [
        {
          "callsign": "Zhukov",
          "alias": "Admiral Gaius Van Zhukov",
          "code": "Umbra-Station//377308ad-ba23-410b-ae37-68a1fb5f8db4",
          "corpro": "IPS-N",
        },
        {
          "callsign": "Kaiba",
          "alias": "Seto Kaiba",
          "code": "Umbra-Station//a98c3e28-ad4a-4f89-bcd9-501464e960da",
          "corpro": "SSC",
        },
        {
          "callsign": "Federal Gunship",
          "alias": "The Pilot Known as MultiCannonn",
          "code": "Umbra-Station//056940c6-8d55-4190-8e85-57caa043cb1a",
          "corpro": "Horus",
        },
        {
          "callsign": "John Harrison IV",
          "alias": "For Legal Reasons not actually John Harrison IV",
          "code": "Umbra-Station//6f572259-6946-41bf-931a-e0543709e892",
          "corpro": "HA",
        },
        {
          "callsign": "Mr Nobody",
          "alias": "Still Mr Nobody",
          "code": "Umbra-Station//5a4254aa-9fa2-42ca-a077-8f5bfd1e1ad3",
          "corpro": "GMS",
        },
      ],
      "header": {
        "planet": "Umbra Station >> ???",
        "year": "5014u",
        "system": "Comet KTX-6F",
        "gate": "Cascade-Shasta",
        "ring": "Cascade-Line",
        "headerTitle": "General Massive Systems",
        "headerSubtitle": "Briefings",
        "subheaderTitle": "Crisis Response",
        "subheaderSubtitle": "Delta-Echo-Echo-Zulu",
      },
      "options":{
        "eventsMarkdownPerMission": true
      }
    }
  },

  created() {
    this.loadMissionMarkdown()
    this.loadEventsMarkdown()
  },

  computed: {

  },

  methods: {
    selectMission(mission) {
      this.mission_slug = mission.slug;
      this.loadMissionMarkdown()
      if(this.options.eventsMarkdownPerMission){
        this.loadEventsMarkdown();
      }
    },
    loadMissionMarkdown() {
      let self = this;
      let md = `/missions/${self.mission_slug}.md`
      var client = new XMLHttpRequest();
      client.open('GET', md);
      client.onreadystatechange = function () {
        self.current_md = client.responseText;
      }
      client.send();
    },
    loadEventsMarkdown() {
      let self = this;
      let md = "";

      if(self.options.eventsMarkdownPerMission){
        md = `/events/${self.mission_slug}.md`
      }
      else {
        md = "/events.md"
      }

      var client = new XMLHttpRequest();
      client.open('GET', md);
      client.onreadystatechange = function () {
        self.events = client.responseText;
      }
      client.send();
    }
  }

}
</script>


<style lang="scss">
#app {
  width: 100%;
  height: 910px;
  overflow: hidden;
}
</style>
