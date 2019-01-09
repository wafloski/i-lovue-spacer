<template>
  <div class="modal-wrapper">
    <div class="outer-wrapper">
      <div class="inner-wrapper">
        <div class="photo">
          <img :src="photo" :alt="title">
        </div>
        <div class="description">
          <h2 class="title">{{ title }}</h2>
          <p class="content">
            {{ description }}
          </p>
        </div>
      </div>
      <div class="close" @click="$emit('closeModal')"/>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DetailsModal',
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      photo: null,
      title: null,
      description: null,
    };
  },
  mounted() {
    this.photo = this.item.links[0].href;
    this.title = this.item.data[0].title;
    this.description = this.item.data[0].description.substring(0, 200);
  },
};
</script>

<style lang="scss" scoped>
  .modal-wrapper {
    width: 100%;
    height: 100vh;
    background-color: rgba(0,0,0,0.5);
    position: fixed;
    top: 0;
    .outer-wrapper {
      max-width: 100%;
      height: 100%;
      position: fixed;
      top: 0;
      left: 0;
      background-color: #fafafa;
      @media (min-width:1024px) {
        max-width: 70%;
        height: 60%;
        left: 0;
        top: 0;
        right: 0;
        bottom: 0;
        margin: auto;
        box-shadow: 0px 30px 90px 0px rgba(0, 0, 0, 0.8);
      }
      .inner-wrapper {
        display: flex;
        height: 100%;
        padding: 50px;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        @media (min-width: 1024px) {
          flex-direction: row;
          .photo {
            min-width: 50%;
            margin-right: 20px;
          }
        }
        .photo {
          width: 100%;
          max-height: 100%;
          background: #000;
          overflow: hidden;
          display: flex;
          align-items: center;
          justify-content: center;
          img {
            width: 100%;
            height: 100%;
          }
        }
        .description {
          color: #444;
        }
      }
      .close {
        position: absolute;
        width: 30px;
        height: 30px;
        right: 0;
        top: 0;
        padding: 30px;
        cursor: pointer;
        &::before,
        &::after{
          position: absolute;
          content: '';
          width: 20px;
          height: 2px;
          background-color: #000;
          display: block;
          top: 30px;
          right: 20px;
        }
        &::before {
          transform: rotate(45deg);
        }
        &::after {
          transform: rotate(-45deg);
        }
      }
    }
  }
</style>
