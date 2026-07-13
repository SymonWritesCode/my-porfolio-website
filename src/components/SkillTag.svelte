<script>
  let { name, rating } = $props();
</script>

<div class="skill-tag glass-panel glass-interactive" role="group" aria-label={`Skill level for ${name}`}>
  <span class="skill-name">{name}</span>
  <div class="rating-dots" aria-hidden="true">
    {#each Array(5) as _, i}
      <span class="dot" class:filled={i < rating}></span>
    {/each}
  </div>
</div>

<style>
  .skill-tag {
    display: inline-flex;
    align-items: center;
    justify-content: space-between;
    padding: 12px 20px;
    gap: 16px;
    border-radius: 12px;
  }

  .skill-name {
    font-size: 0.95rem;
    font-weight: 600;
    color: var(--text-primary);
  }

  .rating-dots {
    display: flex;
    gap: 4px;
  }

  .dot {
    width: 6px;
    height: 6px;
    border-radius: 50%;
    background: rgba(255, 255, 255, 0.1);
    transition: background var(--transition-smooth), transform var(--transition-smooth);
  }

  .dot.filled {
    background: var(--gradient-accent);
  }

  .skill-tag:hover .dot.filled {
    transform: scale(1.3);
  }
</style>
