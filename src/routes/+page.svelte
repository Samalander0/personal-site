<script>
  import './styles.scss'
  import { onMount } from 'svelte';

  import { book, open_book, arrow, emoji, artist, gear, school, brain, oldsites, boring, peek, petrichor, postcards, github, instagram, twitter, discord } from '$lib/images/images';
  
  import Metatags from '$lib/components/Metatags.svelte';
  
  let emojiNum = 2;
  let currentEmoji = emoji[emojiNum];
  function changeEmoji() {
    emojiNum++
    if (emojiNum >= 7) {
      emojiNum = 0
    }
    currentEmoji = emoji[emojiNum]
  }
  let interval = null;
  function rollEmoji() {
    let iteration = 0;
    
    clearInterval(interval);
    interval = setInterval(() => {
      changeEmoji()
    }, 150);
  }

  let projectsSection;
  let project1;
  let project2;
  let project3;
  let project4;

  // GSAP
  // GSAP
  import { gsap } from "gsap/dist/gsap";
  import { ScrollTrigger } from "gsap/dist/ScrollTrigger";
  import { ScrollSmoother } from "$lib/gsap/src/ScrollSmoother";
  gsap.registerPlugin(ScrollTrigger, ScrollSmoother);

  let smoother;
  let aboutTimeline = gsap.timeline();
  onMount(() => {
    smoother = ScrollSmoother.create({
      smooth: 0.5,
      effects: true,  
      smoothTouch: 0.1,
    });

    gsap.to("#header .line-1", {
      y: "10vh",
      scrollTrigger: {
        trigger: "#header",
        start: "top top",
        end: "bottom top",
        scrub: 1.5,
      }
    })
    gsap.to("#header .line-2", {
      y: "10vh",
      scrollTrigger: {
        trigger: "#header",
        start: "top top",
        end: "bottom top",
        scrub: 1,
      }
    })
    gsap.to(".navbar", {
      y: "25vh",
      scrollTrigger: {
        trigger: "#header",
        start: "top top",
        end: "top+=750 top",
        scrub: true,
      }
    })
    gsap.to("#arrow", {
      y: "2vh",
      scrollTrigger: {
        trigger: "#header",
        start: "top top",
        end: "bottom top",
        scrub: true,
      }
    })

    aboutTimeline.from("#about .section-1", {
      height: 0,
      duration: 1
    }, "<")
    .from("#about .line-1", {
      opacity: 0,
      duration: 1
    })
    .from("#about .line-1 .highlight", {
      background: "transparent",
      duration: 1.5
    }, "<")
    .from("#about .line-2", {
      opacity: 0,
      duration: 1
    })
    .from("#about .line-2 .highlight", {
      background: "transparent",
      duration: 1.5
    }, "<")
    .from("#about .line-3", {
      opacity: 0,
      duration: 1
    })
    .from("#about .line-3 .highlight", {
      background: "transparent",
      scale: 0,
      duration: 1.5
    }, "<")
    .from("#about .section-2", {
      height: 0,
      duration: 1
    }, "<")
    .from("#about .line-4", {
      opacity: 0,
      duration: 1
    })
    .from("#about .line-5", {
      opacity: 0,
      duration: 1
    })
    .from("#about .line-5 .highlight", {
      background: "transparent",
      duration: 1.5
    }, "<")
    .to("#about", {
      duration: 1
    })
    .to("#about", {
      clipPath: "polygon(0 50%, 100% 50%, 100% 50%, 0 50%)",
      duration: 2,
    })
    .to("#about", {
      duration: 0.5
    })
    .from("#past-sites .small", {
      opacity: 0,
      duration: 1,
    })
    .from("#past-sites .big", {
      opacity: 0,
      duration: 1,
    })
    .from("#past-sites .images", {
      scale: 0,
      opacity: 0,
      duration: 1,
    })
    .to("#past-sites .images", {
      scale: 1.1,
      duration: 2
    })
    .from(".old-site", {
      marginRight: "-35vmax",
      duration: 2,
    }, "<")
    ScrollTrigger.create({
      trigger: "#about-scroll-section",
      animation: aboutTimeline,
      start: "top top",
      end: "+=4500vh",
      scrub: 0.5,
      pin: true,
    })  
  })
</script>

<Metatags/>

<nav class="navbar">
  <a href="#" id="title">
    <h2><span>S</span><span>a</span><span>m</span> <span>C</span><span>h</span><span>e</span><span>n</span><span>g</span></h2>
  </a>
  <div id="socials">
    <a href="https://github.com/samalander0" target="_blank" rel="noreferrer" aria-label="Go to Sam's Github"><img src={github} alt="github logo"/></a>
    <a href="https://instagram.com/samaland3r_" target="_blank" rel="noreferrer" aria-label="Go to Sam's Instagram"><img src={instagram} alt="instagram logo"/></a>
    <a href="https://twitter.com/samaland3r" target="_blank" rel="noreferrer" aria-label="Go to Sam's Twitter"><img src={twitter} alt="twitter logo"/></a>
    <a href="https://discord.com/users/588480933108121618" target="_blank" rel="noreferrer" aria-label="Go to Sam's Discord"><img src={discord} alt="discord logo"/></a>
  </div>
</nav>

<header id="header">
  <h1>
    <span class="line line-1">
      <span class="wrapper">
        <span class="content">I tell</span>
      </span>
      <span class="wrapper stories-wrapper">
        <span id="stories" class="highlight content">
          <span class="text">stories</span>
          <img src={book} alt="book emoji" class="emoji"/>
          <img src={open_book} alt="open book emoji" class="emoji"/>
          <img src={book} alt="book emoji" class="emoji"/>
        </span> 
      </span>
      <span class="wrapper">
        <span class="content">on the web</span>
      </span>
    </span>
    <span class="line line-2">
      <span class="wrapper">
        <span class="content">And I'd love to tell</span>
      </span>
      <span class="wrapper yours-wrapper">
        <span id="yours" class="highlight content" on:mouseenter={rollEmoji} on:mouseleave={clearInterval(interval)}>
          <span class="text">yours</span>
          <img src={currentEmoji} class="emoji" alt="emoji"/>
        </span>
      </span>
    </span>
  </h1>
  <div id="arrow">
    <img src={arrow} alt="down arrow"/>
    <img src={arrow} alt="down arrow"/>
  </div>
</header>

<main>
  <div id="about-scroll-section">
    <section id="about">
      <div class="inner">
        <h2>So... who am I?</h2>
        <h3 class="section-1">
          <span class="line line-1">
            I'm a 
            <span class="highlight" style="color: #FDD641;">
              <span class="highlight-content">
                <img src={artist} alt="artist emoji"/>
                Digital Designer
              </span>
            </span>
            ,
          </span>
          <span class="line line-2">
            <span class="highlight" style="color: #CDC4D6;">
              <span class="highlight-content">
                <img src={gear} alt="gear emoji"/>
                Web Developer
              </span>
            </span>
            , and
          </span>
          <span class="line line-3">
            <span class="highlight" style="color: #FFCE7C;">
              <span class="highlight-content">
                <img src={school} alt="school emoji"/>
                Student
              </span>
            </span>
          </span>
        </h3>
        <h3 class="section-2">
          <span class="line line-4">
            But mostly, I'm a
          </span>
          <span class="line line-5">
            <span class="highlight" style="color: #FF6DC6;">
              <span class="highlight-content">
                <img src={brain} alt="brain emoji"/>
                Problem Solver
              </span>
            </span>
            ...
          </span>
        </h3>
      </div>
    </section>
    <section id="past-sites">
      <h2>
        <span class="small">...and I'm always</span>
        <span class="big">learning</span>
      </h2>
      <div class="images">
        {#each oldsites as site (site.number)}
          <img src={site.image} id={`site${site.number}`} alt={`old site ${site.number}`} class="old-site"/>
        {/each}
      </div>
    </section>
  </div>
  <section id="projects" bind:this={projectsSection}>
    <h2>Projects</h2>
    <div id="scroller">
      <article class="project" bind:this={project1}>
        <a href="https://boring.samalander.dev/" target="_blank" rel="noreferrer" aria-label="go to featured website">
          <img src={boring} alt="[boring] website screenshot"/>
        </a>
        <a href="https://boring.samalander.dev/" target="_blank" rel="noreferrer" class="project-title">
          <h3>[Boring]</h3>
        </a>
      </article>
      <article class="project" bind:this={project2}>
        <a href="https://postcard.samalander.dev/" target="_blank" rel="noreferrer" aria-label="go to featured website">
          <img src={postcards} alt="digital postcard website screenshot"/>
        </a>
        <a href="https://postcard.samalander.dev/" target="_blank" rel="noreferrer" class="project-title">
          <h3>Digital Postcards</h3>
        </a>
      </article>
      <article class="project" bind:this={project3}>
        <a href="https://peekfriends.com/" target="_blank" rel="noreferrer" aria-label="go to featured website">
          <img src={peek} alt="peek website screenshot"/>
        </a>
        <a href="https://peekfriends.com/" target="_blank" rel="noreferrer" class="project-title">
          <h3>Peek</h3>
        </a>
      </article>
      <article class="project" bind:this={project4}>
        <a href="https://www.petrichorgames.com/" target="_blank" rel="noreferrer" aria-label="go to featured website">
          <img src={petrichor} alt="petrichor website screenshot"/>
        </a>
        <a href="https://www.petrichorgames.com/" target="_blank" rel="noreferrer" class="project-title">
          <h3>Petrichor Games</h3>
        </a>
      </article>
    </div>
  </section>
  <section id="contact">
    <div id="contact-wrapper">
      <h2>I'd love to work with you</h2>
      <div id="contact-content">
        <div id="contact-info">
          <p>Do you have a question, idea, or a project you need help with? <br/> Reach out - I'd love to hear from you.</p>
          <div>
            <div class="contact-info-line">
              <h3>Social Media</h3>
              <div class="contact-social-media">
                <a href="https://github.com/samalander0" target="_blank" rel="noreferrer" aria-label="Go to Sam's Github"><img src={github} alt="github logo"/></a>
                <a href="https://instagram.com/samaland3r_" target="_blank" rel="noreferrer" aria-label="Go to Sam's Instagram"><img src={instagram} alt="instagram logo"/></a>
                <a href="https://twitter.com/samaland3r" target="_blank" rel="noreferrer" aria-label="Go to Sam's Twitter"><img src={twitter} alt="twitter logo"/></a>
                <a href="https://discord.com/users/588480933108121618" target="_blank" rel="noreferrer" aria-label="Go to Sam's Discord"><img src={discord} alt="discord logo"/></a>
              </div>
            </div>
            <div class="contact-info-line">
              <h3>Email</h3>
              <a href="mailto:sam@samalander.dev" target="_blank">sam@samalander.dev</a>
            </div>
            <div class="contact-info-line">
              <h3>Location</h3>
              <a href="https://goo.gl/maps/UXvrrJ4wXHNE7E1PA" target="_blank" rel="noreferrer">Silicon Valley - California</a>
            </div>
          </div>
        </div>
        <form name="contact-form" acceptCharset="utf-8" action="https://getform.io/f/5f6698d1-3659-4132-9fd1-5ed5854b9740" method="post">
          <fieldset>
            <input type="text" name="name" id="your-name" placeholder="Name" required/>
            <input type="email" name="email" id="your-email" placeholder="Email" required/>
          </fieldset>
          <textarea name="message" id="message" placeholder="Message" required/>
          <input type="submit" value="Submit"/>
        </form>
      </div>
    </div>
  </section>
</main>