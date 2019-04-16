<template>
  <article :class="{ featured: item.featured == 'true' }">
    <a :href="item.link" target="_blank">
      <div class="categories">
        <span v-for="category in splitCategories(item.category)" :key="category">
          {{ category }}
        </span>
      </div>

      <h1>
        {{ item.title }}
      </h1>

      <p v-if="item.featured">
        {{ item.description }}
      </p>

      <footer :class="{ document: item.documentSize }">
        <span v-if="item.documentSize" class="document-size">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 500 500">
            <path d="M327 0H114.7C78.3 0 48.6 29.4 48.6 65.6v368.8c0 36.2 29.6 65.6 66.1 65.6h270.7c36.4 0 66.1-29.4 66.1-65.6V138.1L327 0zm8.7 56.6l64.8 71.9h-64.8V56.6zm49.6 412.2H114.7c-19.1 0-34.6-15.4-34.6-34.4V65.6c0-18.9 15.5-34.4 34.6-34.4h189.5v128.4h115.7v274.7c0 19.1-15.5 34.5-34.6 34.5z" />
            <path d="M154.2 208.3h191.6v31.3H154.2v-31.3zm0 72.2h191.6v31.3H154.2v-31.3zm0 72.1h191.6v31.3H154.2v-31.3z" />
          </svg>
          PDF ({{ item.documentSize }})
        </span>
        <span>
          <svg v-if="item.documentSize" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 500 500">
            <path d="M433.7 352.4c6-5.1 9.5-12.6 9.5-20.5 0-6.2-2.2-12.3-6.1-17.1-9.3-11.3-25.9-12.8-37-3.4l-124 105 .3-389.6C276.4 12 264.7 0 250.2 0s-26.3 11.9-26.3 26.6l-.3 389.5L99.9 311.4c-11.1-9.4-27.7-7.9-37 3.4-3.9 4.8-6.1 10.9-6.1 17.1 0 7.9 3.5 15.4 9.5 20.5l166.9 141.4c4.7 4 10.7 6.2 16.8 6.2s12.1-2.2 16.8-6.2l166.9-141.4z" />
          </svg>
          <svg v-else xmlns="http://www.w3.org/2000/svg" viewBox="0 0 500 500">
            <path d="M352.4 66.3c-5.1-6-12.6-9.5-20.5-9.5-6.2 0-12.3 2.2-17.1 6.1-11.3 9.3-12.8 25.9-3.4 37l105 124-389.6-.3C12 223.6 0 235.3 0 249.8s11.9 26.3 26.6 26.3l389.5.3-104.7 123.7c-9.4 11.1-7.9 27.7 3.4 37 4.8 3.9 10.9 6.1 17.1 6.1 7.9 0 15.4-3.5 20.5-9.5l141.4-166.9c4-4.7 6.2-10.7 6.2-16.8 0-6.1-2.2-12.1-6.2-16.8L352.4 66.3z" />
          </svg>
        </span>
      </footer>
    </a>
  </article>
</template>

<script>
export default {
  name: 'Card',

  props: {
    item: Object
  },

  methods: {
    // Split the categories for each item into an array
    splitCategories: function(string) {
      return string.split(', ');
    }
  }
}
</script>

<style lang="scss">
article {
  border: 1px solid rgba(0,0,0,.2);
  display: flex;
  transition: all .2s;
  position: relative;
  overflow: hidden;

  a {
    display: block;
    width: 100%;
    padding: 3em 2em 4em;
    color: #4A4A4A;
    text-decoration: none;
  }

  h1 {
    font-size: 1.2em;
    margin: 0 0 1rem;
  }

  p {
    line-height: 1.5;
    opacity: .8;
  }

  .categories {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    font-size: .7em;
    padding: 1rem 2rem;
    opacity: 0;
    transition: all .2s;
    transform: translateY(-50%);

    span {
      display: inline-block;
      background: rgba(0,0,0,.25);
      color: #FFF;
      font-weight: bold;
      padding: .2em .5em;
      margin-right: .5em;
    }
  }

  footer {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    display: flex;
    justify-content: flex-end;

    &.document {
      justify-content: space-between;
    }

    svg {
      height: 1em;
      width: 1em;
    }

    span {
      padding: 1rem;

      &.document-size {
        padding-left: 2em;
        display: flex;
        align-items: center;
        opacity: .75;

        svg {
          opacity: .5;
          margin-right: .5em;
        }
      }

      &:last-child {
        font-size: 1.5em;
        line-height: 1;
        transition: all .2s;
      }

      &:last-child path {
        fill: rgb(0, 174, 133);
        transition: all .2s;
      }
    }
  }

  &.featured {
    background-image: linear-gradient(135deg, rgb(0, 164, 201), rgb(0, 174, 133));
    color: #FFF;

    @media screen and (min-width: 625px) {
      grid-column: span 2;
    }

    a {
      color: #FFF;
    }

    h1 {
      font-size: 2em;
      font-weight: 700;
    }

    footer {
      span {
        &:last-child {
          background-color: rgba(0,0,0,.25);

          path {
            fill: rgb(255, 255, 255);
          }
        }
      }
    }
  }

  &:hover {
    border-color: rgba(0,0,0,.5);
    background-color: rgba(0,0,0,.1);
    transform: scale(1.05);
    box-shadow: 0 .25em 1em rgba(0,0,0,.1);
    z-index: 10;

    .categories {
      opacity: 1;
      transform: translateY(0);
    }

    footer {
      span {
        &:last-child {
          background-color: rgba(0,0,0,.5);

          path {
            fill: #FFF;
          }
        }
      }
    }
  }
}
</style>
