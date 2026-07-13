<footer class="footer" aria-label="Page Footer">
  <div class="footer-container">
    <div class="footer-left">
      <p>&copy; {new Date().getFullYear()} Symon. All rights reserved.</p>
    </div>
    <div class="footer-right">
      <a href="https://github.com" class="footer-link" target="_blank" rel="noopener noreferrer" aria-label="GitHub Profile">GitHub</a>
      <a href="https://linkedin.com" class="footer-link" target="_blank" rel="noopener noreferrer" aria-label="LinkedIn Profile">LinkedIn</a>
    </div>
  </div>
</footer>

<style>
  .footer {
    border-top: 1px solid var(--glass-border);
    padding: 40px 24px;
    margin-top: 100px;
    background: rgba(0, 0, 0, 0.2);
  }

  .footer-container {
    width: 100%;
    max-width: 1200px;
    margin: 0 auto;
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: var(--text-muted);
    font-size: 0.9rem;
  }

  .footer-right {
    display: flex;
    gap: 24px;
  }

  .footer-link {
    color: var(--text-muted);
    text-decoration: none;
    transition: color var(--transition-smooth);
  }

  .footer-link:hover {
    color: var(--text-primary);
  }

  @media (max-width: 768px) {
    .footer-container {
      flex-direction: column;
      gap: 16px;
      text-align: center;
    }
  }
</style>
