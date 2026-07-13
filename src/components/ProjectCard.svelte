<script>
  let { title, description, tags, link } = $props();
</script>

<article class="project-card glass-panel glass-interactive" aria-labelledby={title.toLowerCase().replace(/\s+/g, '-')}>
  <div class="card-glow"></div>
  <div class="card-content">
    <header class="card-header">
      <h3 id={title.toLowerCase().replace(/\s+/g, '-')} class="project-title">{title}</h3>
    </header>
    <p class="project-description">{description}</p>
    <footer class="card-footer">
      <div class="tags-list">
        {#each tags as tag}
          <span class="tag-item">{tag}</span>
        {/each}
      </div>
      <a href={link} class="project-link" aria-label={`View code or live demo for ${title}`}>
        <span>Explore</span>
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
          <path stroke-linecap="round" stroke-linejoin="round" d="M14 5l7 7m0 0l-7 7m7-7H3" />
        </svg>
      </a>
    </footer>
  </div>
</article>

<style>
  .project-card {
    position: relative;
    padding: 32px;
    height: 100%;
    display: flex;
    flex-direction: column;
    overflow: hidden;
  }

  .card-glow {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: radial-gradient(circle at 0% 0%, rgba(138, 43, 226, 0.15) 0%, transparent 60%);
    pointer-events: none;
    transition: opacity var(--transition-smooth);
  }

  .project-card:hover .card-glow {
    background: radial-gradient(circle at 100% 100%, rgba(0, 255, 255, 0.15) 0%, transparent 60%);
  }

  .card-content {
    display: flex;
    flex-direction: column;
    height: 100%;
    z-index: 1;
  }

  .project-title {
    font-size: 1.4rem;
    font-weight: 700;
    margin-bottom: 12px;
    letter-spacing: -0.5px;
  }

  .project-description {
    color: var(--text-secondary);
    font-size: 0.95rem;
    line-height: 1.6;
    margin-bottom: 24px;
    flex-grow: 1;
  }

  .card-footer {
    display: flex;
    flex-direction: column;
    gap: 20px;
    margin-top: auto;
  }

  .tags-list {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
  }

  .tag-item {
    font-size: 0.75rem;
    font-weight: 600;
    background: rgba(255, 255, 255, 0.04);
    color: var(--text-secondary);
    padding: 4px 10px;
    border-radius: 6px;
    border: 1px solid rgba(255, 255, 255, 0.05);
  }

  .project-link {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    color: var(--color-accent-secondary);
    text-decoration: none;
    font-weight: 600;
    font-size: 0.9rem;
    transition: color var(--transition-smooth), transform var(--transition-smooth);
    align-self: flex-start;
  }

  .project-link:hover {
    color: var(--text-primary);
    transform: translateX(4px);
  }

  .project-link svg {
    transition: transform var(--transition-smooth);
  }

  .project-link:hover svg {
    transform: translateX(2px);
  }
</style>
