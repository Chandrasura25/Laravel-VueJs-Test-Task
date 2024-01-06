<script setup>
import Navbar from "./Navbar.vue";
import Sidebar from "./Sidebar.vue";
</script>

<template>
 <div class="container" :class="{ active: popupActive, blank: popupBlank }">
    <Navbar />
    <Sidebar />
    <section class="contextBx">
      <div class="content">
        <div class="top">
          <p>Snapbyte</p>
          <i class="bx bx-chevron-right"></i>
          <p>My Recordings</p>
        </div>
        <div class="title">
          <div>
            <h1>My Recordings</h1>
            <p>25</p>
          </div>
          <div>
            <button class="btn">
              <i class="bx bx-sort-alt-2"></i> By Date
            </button>
            <button class="btn"><i class="bx bxs-drink"></i> Add Filter</button>
            <button class="btn"><i class="bx bx-video"></i> New Request</button>
            <button class="btn" @click="toggle">
              <i class="bx bx-microphone"></i> Start Recording
            </button>
          </div>
        </div>
        <div class="table">
          <table>
            <thead>
              <tr>
                <th>Recordings</th>
                <th>Title</th>
                <th>Views</th>
                <th>Size</th>
                <th>Last Modified</th>
                <th></th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(image, index) in imageArray" :key="index">
                <td>
                  <div class="img">
                    <img :src="image.img" alt="image">
                  </div>
                </td>
                <td>
                  <div class="text">
                    <h3>{{ image.title }}</h3>
                    <p>{{ image.description }}</p>
                  </div>
                </td>
                <td>{{ image.views }}</td>
                <td>{{ image.size }}</td>
                <td>3 months ago</td>
                <td>
                  <span>...</span>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </section>
  </div>
  <div id="popup" :class="{ active: popupActive }">
    <div class="top">
      <h2>New Recording</h2>
      <i class="bx bx-x" @click="toggle"></i>
    </div>
    <div class="selectBox">
      <div class="instruct">
        <p>Save the recording in</p>
        <select>
          <option value="">Select a project</option>
        </select>
      </div>
      <div class="checks">
        <div>
          <p>Record Screen</p>
          <input type="checkbox" v-model="selectedSources.screen" />
        </div>
        <div>
          <p>Record Camera</p>
          <input type="checkbox" v-model="selectedSources.camera" />
        </div>
        <div>
          <p>Record Mic</p>
          <input type="checkbox" v-model="selectedSources.mic" />
        </div>
      </div>
      <div class="btnBx">
        <button @click="toggleAndrequestPermission">Start Recording</button>
      </div>
    </div>
  </div>
  <div id="blank_screen" :class="{ blank: popupBlank }">
  </div>
</template>

<script>
export default {
  data() {
    return {
      imageArray: [
        {
          img: "/src/assets/img.png",
          title: "Image 1",
          description: "Description for Image 1",
          views: "322",
          size: "200",
        },
        {
          img: "/src/assets/img.png",
          title: "Image 2",
          description: "Description for Image 2",
          views: "323",
          size: "400",
        },
        {
          img: "/src/assets/img.png",
          title: "Image 3",
          description: "Description for Image 3",
          views: "323",
          size: "300",
        },
        {
          img: "/src/assets/img.png",
          title: "Image 4",
          description: "Description for Image 4",
          views: "322",
          size: "250",
        },
        {
          img: "/src/assets/img.png",
          title: "Image 5",
          description: "Description for Image 5",
          views: "323",
          size: "350",
        },
      ],
      popupActive: false,
      popupBlank: false,
      selectedSources: {
        screen: false,
        camera: false,
        mic: false,
      },
    };
  },
  methods: {
    toggle() {
      this.popupActive = !this.popupActive;
    },
    toggleAndrequestPermission() {
      this.toggle();
      this.requestPermission();
    },
    async requestPermission() {
      this.popupBlank = !this.popupBlank;
      const constraints = {};
      if (this.selectedSources.screen) {
        constraints.video = { mediaSource: "screen" };
      } else {
        constraints.video = this.selectedSources.camera;
        constraints.audio = this.selectedSources.mic;
      }
      try {
       await navigator.mediaDevices
          .getUserMedia(constraints)
          .then((stream) => {
            this.popupActive = !this.popupActive;
          })
          .catch((error) => {
            console.error("Permission denied or error:", error);
            this.popupBlank = !this.popupBlank;
          })
          .finally(() => {
            this.popupBlank = !this.popupBlank;
          });
      } catch (error) {
        console.error("Error accessing media devices:", error);
        this.popupBlank = !this.popupBlank;
      }
    },
  },
};
</script>
