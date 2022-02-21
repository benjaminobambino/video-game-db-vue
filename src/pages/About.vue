<template>
<div class="about">
      <h1>About</h1>
      <p>
        Welcome to my RAWG video games app. In this app, visitors may find a variety of video games either by genre or by a name search. This app was built using Vue.js and multiple API calls. While I built a similar app using React, this version has some definite improvements to navigation, game details, and overall functionality.
      </p>
      <section class="credits">
        <h4>Credits:</h4>
        <ul>
          <li>
            <a
              href="https://www.linkedin.com/in/benjaminlpeck/"
              target="_blank"
              rel="noopener noreferrer"
            >
              Benjamin Peck:
            </a>
            app creator
          </li>
          <li>
            <a
              href="https://www.andrepato.com/"
              target="_blank"
              rel="noopener noreferrer"
            >
              Andre Pato
            </a>
            and
            <a
              href="https://michaellackey.com/"
              target="_blank"
              rel="noopener noreferrer"
            >
              Michael Lackey:
            </a>
            prompt and starter code
          </li>
          <li>
            <a
              href="https://rawg.io/apidocs"
              target="_blank"
              rel="noopener noreferrer"
            >
              RAWG:
            </a>
            Video Games Database API used for game genres, images, titles,
            ratings, and other details
          </li>
          <li>
            <a
              href="https://pluspng.com/png-54686.html"
              target="_blank"
              rel="noopener noreferrer"
            >
              PlusPNG:
            </a>
            App favicon
          </li>
        </ul>
      </section>
    </div>
</template>

<script>
export default {
  name: 'About'
}
</script>
