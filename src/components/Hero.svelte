<script>
  // Simple state for an interactive animation indicator
  let hovered = $state(false);
</script>

<section id="home" class="hero-section" aria-label="Introduction & Welcome">
  <div class="hero-container">
    <div class="hero-content">
      <div class="badge glass-panel">Available for Work</div>
      <h1 class="hero-title">
        Building the <br />
        <span class="text-gradient">Next-Gen Web</span> <br />
        with Clean Code.
      </h1>
      <p class="hero-description">
        Hi, I'm a developer focusing on crafting highly interactive, visually aesthetic, and performant web applications using Svelte, modern APIs, and clean engineering practices.
      </p>
      <div class="hero-actions">
        <a href="#projects" class="btn btn-primary">View Projects</a>
        <a href="#contact" class="btn btn-secondary">Get in Touch</a>
      </div>
    </div>
    
    <div 
      class="hero-visual"
      onmouseenter={() => hovered = true}
      onmouseleave={() => hovered = false}
      role="img"
      aria-label="Interactive abstract coding art visualization"
    >
      <div class="visual-wrapper glass-panel" class:hovered>
        <!-- Dynamic abstract coding elements -->
        <svg class="visual-svg" viewBox="0 0 400 400" width="400" height="400" xmlns="http://www.w3.org/2000/svg" fetchpriority="high">
          <!-- Central glowing sphere -->
          <defs>
            <radialGradient id="sphereGlow" cx="50%" cy="50%" r="50%">
              <stop offset="0%" stop-color="var(--color-accent-secondary)" stop-opacity="0.3"/>
              <stop offset="100%" stop-color="var(--color-accent)" stop-opacity="0"/>
            </radialGradient>
          </defs>
          <circle cx="200" cy="200" r="160" fill="url(#sphereGlow)" />
          
          <!-- Outer orbital lines -->
          <circle cx="200" cy="200" r="120" fill="none" stroke="rgba(255, 255, 255, 0.15)" stroke-width="2" stroke-dasharray="10 15" class="spin-clockwise" />
          <circle cx="200" cy="200" r="90" fill="none" stroke="rgba(255, 255, 255, 0.08)" stroke-width="1.5" class="spin-counter-clockwise" />
          
          <!-- Inner creative wireframe -->
          <polygon points="200,80 304,260 96,260" fill="none" stroke="var(--color-accent)" stroke-width="2" stroke-linejoin="round" class="pulse" />
          <polygon points="200,320 96,140 304,140" fill="none" stroke="var(--color-accent-secondary)" stroke-width="2" stroke-linejoin="round" class="pulse-delayed" />
        </svg>
        <div class="stats-card glass-panel">
          <p class="stats-title">Performance Score</p>
          <p class="stats-value text-gradient">100%</p>
        </div>
      </div>
    </div>
  </div>
</section>

<style>
  .hero-section {
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 120px 24px 80px;
  }

  .hero-container {
    width: 100%;
    max-width: 1200px;
    display: grid;
    grid-template-columns: 1.2fr 0.8fr;
    gap: 60px;
    align-items: center;
  }

  .hero-content {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
  }

  .badge {
    padding: 6px 16px;
    font-size: 0.85rem;
    font-weight: 600;
    color: var(--color-accent-secondary);
    border-radius: 20px;
    margin-bottom: 24px;
    border-color: rgba(0, 255, 255, 0.2);
  }

  .hero-title {
    font-size: clamp(2.5rem, 5vw, 4.5rem);
    font-weight: 800;
    line-height: 1.1;
    margin-bottom: 24px;
    letter-spacing: -2px;
  }

  .hero-description {
    font-size: clamp(1rem, 2vw, 1.25rem);
    color: var(--text-secondary);
    max-width: 580px;
    margin-bottom: 40px;
  }

  .hero-actions {
    display: flex;
    gap: 16px;
  }

  .btn {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    padding: 14px 28px;
    font-size: 1rem;
    font-weight: 600;
    border-radius: 30px;
    text-decoration: none;
    transition: transform var(--transition-smooth), box-shadow var(--transition-smooth), opacity var(--transition-smooth);
    cursor: pointer;
  }

  .btn-primary {
    background: var(--gradient-accent);
    color: var(--bg-primary);
    box-shadow: 0 4px 20px rgba(138, 43, 226, 0.3);
  }

  .btn-primary:hover {
    transform: translateY(-2px);
    box-shadow: 0 6px 24px rgba(138, 43, 226, 0.45);
  }

  .btn-secondary {
    background: var(--glass-bg);
    border: 1px solid var(--glass-border);
    color: var(--text-primary);
  }

  .btn-secondary:hover {
    transform: translateY(-2px);
    border-color: rgba(255, 255, 255, 0.2);
    background: rgba(255, 255, 255, 0.05);
  }

  .hero-visual {
    display: flex;
    justify-content: center;
    align-items: center;
    perspective: 1000px;
  }

  .visual-wrapper {
    position: relative;
    padding: 30px;
    border-radius: 24px;
    display: flex;
    justify-content: center;
    align-items: center;
    transition: transform 0.5s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  }

  .visual-wrapper.hovered {
    transform: rotateY(10deg) rotateX(10deg) scale(1.03);
  }

  .visual-svg {
    max-width: 100%;
    height: auto;
  }

  .stats-card {
    position: absolute;
    bottom: -10px;
    left: -20px;
    padding: 16px 24px;
    border-radius: 16px;
    border-color: rgba(138, 43, 226, 0.2);
    animation: float 4s ease-in-out infinite;
  }

  .stats-title {
    font-size: 0.75rem;
    color: var(--text-muted);
    text-transform: uppercase;
    letter-spacing: 1px;
  }

  .stats-value {
    font-size: 1.75rem;
    font-weight: 800;
  }

  /* SVG Animations */
  @keyframes spin-cw {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
  }

  @keyframes spin-ccw {
    from { transform: rotate(360deg); }
    to { transform: rotate(0deg); }
  }

  :global(.spin-clockwise) {
    transform-origin: center;
    animation: spin-cw 30s linear infinite;
  }

  :global(.spin-counter-clockwise) {
    transform-origin: center;
    animation: spin-ccw 20s linear infinite;
  }

  @keyframes pulse-anim {
    0%, 100% { opacity: 0.5; transform: scale(1) rotate(0deg); }
    50% { opacity: 0.9; transform: scale(1.05) rotate(5deg); }
  }

  :global(.pulse) {
    transform-origin: center;
    animation: pulse-anim 6s ease-in-out infinite;
  }

  :global(.pulse-delayed) {
    transform-origin: center;
    animation: pulse-anim 6s ease-in-out infinite;
    animation-delay: -3s;
  }

  @keyframes float {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-10px); }
  }

  /* Responsive styling */
  @media (max-width: 992px) {
    .hero-container {
      grid-template-columns: 1fr;
      gap: 40px;
      text-align: center;
    }

    .hero-content {
      align-items: center;
    }

    .hero-visual {
      order: -1;
    }

    .stats-card {
      left: 10px;
      bottom: 10px;
    }
  }
</style>
