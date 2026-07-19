<script>
  import Navbar from '../components/Navbar.svelte';
  import Hero from '../components/Hero.svelte';
  import ProjectCard from '../components/ProjectCard.svelte';
  import SkillTag from '../components/SkillTag.svelte';
  import Footer from '../components/Footer.svelte';

  const projects = [
    {
      title: "SkyFlow Weather",
      description: "A premium glassmorphic weather platform showcasing real-time meteorological tracking, dynamic weather-based particle systems, and multi-city forecasting.",
      tags: ["SvelteKit", "API Integration", "CSS Animations"],
      link: "/weather"
    },
    {
      title: "Atmosphere Engine",
      description: "An interactive, web-based physics simulation engine displaying particles under micro-gravity conditions with custom animation systems.",
      tags: ["HTML5 Canvas", "WebAssembly", "Svelte"],
      link: "#"
    },
    {
      title: "Glow UI Ecosystem",
      description: "A collection of highly accessible and lightweight glassmorphic dashboard widgets built to satisfy Core Web Vitals targets.",
      tags: ["CSS Custom Properties", "Vanilla JS", "a11y"],
      link: "#"
    }
  ];

  const skills = [
    { name: "Svelte & SvelteKit", rating: 5 },
    { name: "Vanilla CSS & Flex/Grid", rating: 5 },
    { name: "JavaScript / JSDoc", rating: 5 },
    { name: "Performance Optimization", rating: 4 },
    { name: "Web Accessibility (a11y)", rating: 4 }
  ];

  let email = $state("");
  let message = $state("");
  let successMessage = $state("");

  function handleSubmit(event) {
    event.preventDefault();
    successMessage = "Thank you! Your message was sent successfully.";
    email = "";
    message = "";
    setTimeout(() => {
      successMessage = "";
    }, 5000);
  }
</script>

<svelte:head>
  <title>Symon | Web Developer Portfolio</title>
  <meta name="description" content="Portfolio of Symon, a creative web developer specializing in Svelte, Vanilla CSS, and modern user experiences." />
</svelte:head>

<Navbar />

<main class="page-wrapper">
  <Hero />

  <!-- Projects Section -->
  <section id="projects" class="section projects-section" aria-labelledby="projects-heading">
    <div class="section-container">
      <h2 id="projects-heading" class="section-title">Selected <span class="text-gradient">Projects</span></h2>
      <div class="projects-grid">
        {#each projects as project}
          <ProjectCard {...project} />
        {/each}
      </div>
    </div>
  </section>

  <!-- Skills Section -->
  <section id="skills" class="section skills-section" aria-labelledby="skills-heading">
    <div class="section-container">
      <h2 id="skills-heading" class="section-title">Technical <span class="text-gradient">Proficiency</span></h2>
      <div class="skills-grid">
        {#each skills as skill}
          <SkillTag {...skill} />
        {/each}
      </div>
    </div>
  </section>

  <!-- Contact Section -->
  <section id="contact" class="section contact-section" aria-labelledby="contact-heading">
    <div class="section-container">
      <h2 id="contact-heading" class="section-title">Let's <span class="text-gradient">Collaborate</span></h2>
      <div class="contact-card glass-panel">
        <form class="contact-form" onsubmit={handleSubmit}>
          <div class="form-group">
            <label for="contact-email">Email Address</label>
            <input 
              type="email" 
              id="contact-email" 
              bind:value={email} 
              required 
              placeholder="you@example.com"
              class="form-input" 
            />
          </div>
          <div class="form-group">
            <label for="contact-message">Message</label>
            <textarea 
              id="contact-message" 
              bind:value={message} 
              required 
              placeholder="Tell me about your project..."
              rows="5"
              class="form-input"
            ></textarea>
          </div>
          <button type="submit" class="btn btn-primary form-submit">Send Message</button>
          
          {#if successMessage}
            <div class="success-alert" role="alert">
              {successMessage}
            </div>
          {/if}
        </form>
      </div>
    </div>
  </section>
</main>

<Footer />

<style>
  .page-wrapper {
    width: 100%;
    margin: 0 auto;
  }

  .section {
    padding: 100px 24px;
  }

  .section-container {
    width: 100%;
    max-width: 1200px;
    margin: 0 auto;
  }

  .section-title {
    font-size: clamp(2rem, 4vw, 3rem);
    font-weight: 800;
    margin-bottom: 50px;
    letter-spacing: -1.5px;
    text-align: center;
  }

  /* Projects Grid */
  .projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
    gap: 30px;
  }

  /* Skills Grid */
  .skills-grid {
    display: flex;
    flex-wrap: wrap;
    gap: 16px;
    justify-content: center;
    max-width: 800px;
    margin: 0 auto;
  }

  /* Contact Section */
  .contact-card {
    max-width: 600px;
    margin: 0 auto;
    padding: 40px;
    border-radius: 24px;
  }

  .contact-form {
    display: flex;
    flex-direction: column;
    gap: 24px;
  }

  .form-group {
    display: flex;
    flex-direction: column;
    gap: 8px;
  }

  .form-group label {
    font-size: 0.9rem;
    font-weight: 600;
    color: var(--text-secondary);
  }

  .form-input {
    background: rgba(255, 255, 255, 0.03);
    border: 1px solid var(--glass-border);
    border-radius: 8px;
    padding: 12px 16px;
    color: var(--text-primary);
    font-family: inherit;
    font-size: 1rem;
    transition: border-color var(--transition-smooth), box-shadow var(--transition-smooth);
  }

  .form-input:focus {
    outline: none;
    border-color: var(--color-accent-secondary);
    box-shadow: 0 0 10px rgba(0, 255, 255, 0.15);
  }

  .form-submit {
    align-self: flex-start;
    border: none;
  }

  .success-alert {
    padding: 12px 16px;
    border-radius: 8px;
    background: rgba(0, 255, 0, 0.1);
    border: 1px solid rgba(0, 255, 0, 0.2);
    color: hsl(120, 100%, 75%);
    font-size: 0.95rem;
    text-align: center;
  }
</style>
