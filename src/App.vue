<template>
  <div id="app">
    <Header />
    <Page />
    <Footer />
  </div>
</template>

<script>


import Header from "./components/Header";
import Page from "./components/Page";
import Footer from "./components/Footer";
export default {
  name: 'App',
  components: {
    Footer,
    Page,
    Header,
  }
}
</script>

<style lang="scss">
  html, body, div, span, applet, object, iframe,
  h1, h2, h3, h4, h5, h6, p, blockquote, pre,
  a, abbr, acronym, address, big, cite, code,
  del, dfn, em, img, ins, kbd, q, s, samp,
  small, strike, strong, sub, sup, tt, var,
  b, u, i, center,
  dl, dt, dd, ol, ul, li,
  fieldset, form, label, legend,
  table, caption, tbody, tfoot, thead, tr, th, td,
  article, aside, canvas, details, embed,
  figure, figcaption, footer, header, hgroup,
  menu, nav, output, ruby, section, summary,
  time, mark, audio, video {
    margin: 0;
    padding: 0;
    border: 0;
    font-size: 100%;
    font: inherit;
    vertical-align: baseline;
  }

  article, aside, details, figcaption, figure,
  footer, header, hgroup, menu, nav, section {
    display: block;
  }
  body {
    line-height: 1;
  }
  ol, ul {
    list-style: none;
  }
  blockquote, q {
    quotes: none;
  }
  blockquote:before, blockquote:after,
  q:before, q:after {
    content: '';
    content: none;
  }
  table {
    border-collapse: collapse;
    border-spacing: 0;
  }

  @font-face {
    font-family: "Helvetica Regular";
    src: url("/assets/fonts/HelveticaRegular/HelveticaRegular.eot") format("eot"),
    url("/assets/fonts/HelveticaRegular/HelveticaRegular.ttf") format("ttf"),
    url("/assets/fonts/HelveticaRegular/HelveticaRegular.woff") format("woff");
  }
  @font-face {
    font-family: "Helvetica Thin";
    src: url("/assets/fonts/HelveticaThin/HelveticaThin.eot") format("eot"),
    url("/assets/fonts/HelveticaThin/HelveticaThin.ttf") format("ttf"),
    url("/assets/fonts/HelveticaThin/HelveticaThin.woff") format("woff");
  }

body {
  height: 100%;
  font-family: "Helvetica Regular",sans-serif;
  margin: 0;
}
#app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;

  .container {
    max-width: 1232px;
    margin: 0 auto;
  }
  footer, header {
    background: #F2EEEE;
    .menu {
      display: flex;
      align-items: center;
    }
  }
  .btn {
    background-color: #FF634A;
    border-radius: 6px;
    border: none;
      cursor: pointer;
  }
}

  @media (max-width: 1252px) {
      #app {
          .container {
              margin: 0 20px;
          }
      }
  }
</style>
