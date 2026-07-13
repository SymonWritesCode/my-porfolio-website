<script>
  let isMobileMenuOpen = $state(false);

  function toggleMobileMenu() {
    isMobileMenuOpen = !isMobileMenuOpen;
  }
</script>

<nav class="navbar glass-panel" id="main-nav" aria-label="Main Navigation">
  <div class="nav-container">
    <a href="#home" class="nav-logo" aria-label="Symon Writes Code Portfolio Home">
      <span class="text-gradient font-bold">&lt;Symon /&gt;</span>
    </a>

    <!-- Desktop Navigation Links -->
    <div class="nav-links-desktop" role="menubar">
      <a href="#home" class="nav-link" role="menuitem">Home</a>
      <a href="#projects" class="nav-link" role="menuitem">Projects</a>
      <a href="#skills" class="nav-link" role="menuitem">Skills</a>
      <a href="#contact" class="nav-link" role="menuitem">Contact</a>
    </div>

    <!-- Mobile Menu Button -->
    <button 
      class="nav-toggle" 
      aria-expanded={isMobileMenuOpen} 
      aria-controls="mobile-menu" 
      aria-label="Toggle navigation menu"
      onclick={toggleMobileMenu}
    >
      <span class="hamburger" class:active={isMobileMenuOpen}></span>
    </button>
  </div>

  <!-- Mobile Menu -->
  {#if isMobileMenuOpen}
    <div class="mobile-menu glass-panel" id="mobile-menu" role="menu">
      <a href="#home" class="mobile-link" role="menuitem" onclick={toggleMobileMenu}>Home</a>
      <a href="#projects" class="mobile-link" role="menuitem" onclick={toggleMobileMenu}>Projects</a>
      <a href="#skills" class="mobile-link" role="menuitem" onclick={toggleMobileMenu}>Skills</a>
      <a href="#contact" class="mobile-link" role="menuitem" onclick={toggleMobileMenu}>Contact</a>
    </div>
  {/if}
</nav>

<style>
  .navbar {
    position: fixed;
    top: 20px;
    left: 50%;
    transform: translateX(-50%);
    width: 90%;
    max-width: 1200px;
    height: 70px;
    z-index: 1000;
    padding: 0 24px;
    border-radius: 35px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .nav-container {
    width: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .nav-logo {
    text-decoration: none;
    font-size: 1.5rem;
    font-weight: 800;
    letter-spacing: -0.5px;
  }

  .nav-links-desktop {
    display: flex;
    gap: 32px;
  }

  .nav-link {
    color: var(--text-secondary);
    text-decoration: none;
    font-size: 0.95rem;
    font-weight: 500;
    transition: color var(--transition-smooth);
  }

  .nav-link:hover {
    color: var(--text-primary);
  }

  .nav-toggle {
    display: none;
    background: none;
    border: none;
    cursor: pointer;
    padding: 12px;
  }

  .hamburger {
    display: block;
    width: 24px;
    height: 2px;
    background: var(--text-primary);
    position: relative;
    transition: background var(--transition-smooth);
  }

  .hamburger::before, .hamburger::after {
    content: '';
    position: absolute;
    width: 24px;
    height: 2px;
    background: var(--text-primary);
    transition: transform var(--transition-smooth);
  }

  .hamburger::before {
    top: -8px;
  }

  .hamburger::after {
    bottom: -8px;
  }

  .hamburger.active {
    background: transparent;
  }

  .hamburger.active::before {
    transform: translateY(8px) rotate(45deg);
  }

  .hamburger.active::after {
    transform: translateY(-8px) rotate(-45deg);
  }

  /* Mobile Dropdown styles */
  .mobile-menu {
    position: absolute;
    top: 85px;
    left: 0;
    width: 100%;
    display: flex;
    flex-direction: column;
    padding: 16px;
    gap: 16px;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.4);
    border-radius: 20px;
  }

  .mobile-link {
    color: var(--text-secondary);
    text-decoration: none;
    font-size: 1.1rem;
    font-weight: 500;
    padding: 12px;
    border-radius: 10px;
    transition: background var(--transition-smooth), color var(--transition-smooth);
  }

  .mobile-link:hover {
    background: rgba(255, 255, 255, 0.05);
    color: var(--text-primary);
  }

  /* Responsive Design */
  @media (max-width: 768px) {
    .nav-links-desktop {
      display: none;
    }

    .nav-toggle {
      display: block;
    }
  }
</style>
