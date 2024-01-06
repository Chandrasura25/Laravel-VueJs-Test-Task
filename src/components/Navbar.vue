<template>
  <header class="navhead">
    <a href="#" class="logo">
      <div>
        <img src="/src/assets/swarm.svg" />
      </div>
      <p>Adilo</p>
    </a>
    <div id="menuToggle" @click="toggleMenu" :class="{ active: toggleActive }"></div>
    <div class="notification" :class="{ active: toggleActive }">
      <ul class="firstNav">
      <li><a href="#">Projects</a></li>
      <li>
        <a href="#">Tools & Apps <i class="bx bx-chevron-down"></i></a>
        <ul>
          <li><a href="#">Snapbyte Recorder</a></li>
          <li><a href="#">AudioBounce</a></li>
          <li><a href="#">Suger Voice</a></li>
        </ul>
      </li>
      <li><a href="#">Channels</a></li>
      <li><a href="#">Contacts</a></li>
      <li><a href="#">Analytics</a></li>
      <li><a href="#">Settings</a></li>
    </ul>
    <ul class="secNav">
      <li><a href="#">Help</a></li>
      <li>
        <a href="#">
          <div>
            <span>
              <img src="/src/assets/swarm.svg" />
            </span>
            <div>
              <p>Cody Fisher</p>
              <p>Cody Fisher@gmail.com</p>
            </div>
          </div>
        </a>
      </li>
    </ul>
    </div>
  </header>
</template>
<script>
export default {
  data() {
    return {
      toggleActive: false,
    };
  },
  methods: {
    toggleMenu() {
      this.toggleActive = !this.toggleActive;
    },
  },
};
</script>
