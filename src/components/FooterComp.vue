<template>
    <footer class="footer sticky-footer">
      <div class="footer-container">
        <div class="footer-content">
          <p class="copyright">&copy; 2025 Palette Bay. All rights reserved.</p>
          <div class="social-links">
            <a
              href="https://github.com/JeremyShiroya"
              aria-label="GitHub"
              class="social-link"
              target="_blank"
            >
              <i class="uil uil-github"></i>
            </a>
            <a
              href="https://www.linkedin.com/in/jeremy-shiroya"
              aria-label="LinkedIn"
              class="social-link"
              target="_blank"
            >
              <i class="uil uil-linkedin"></i>
            </a>
            <a
              href="https://wa.me/254113562018"
              aria-label="WhatsApp"
              class="social-link"
              target="_blank"
            >
              <i class="uil uil-whatsapp"></i>
            </a>
          </div>
        </div>
        <div class="powered-by">
          Created by
          <a
            href="https://github.com/JeremyShiroya"
            class="obsidian-link"
            target="_blank"
            >Jeremy Shiroya</a
          >
          <!-- with <i class="ri-heart-fill" id="heart"></i> -->
        </div>
      </div>
    </footer>
  </template>
  
  <script setup>
  // No script needed for the footer component
  </script>
  
  <style scoped>
  /* Add the footer styles here */
  .footer {
    background-color: var(--footer-background);
    color: var(--footer-text);
    padding: 3rem 0;
    margin-top: 1rem;
    transition: background-color 0.3s ease, color 0.3s ease;
  }
  
  .footer-container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 2rem;
  }
  
  .footer-content {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 2rem;
  }
  
  .copyright {
    font-size: 0.9rem;
  }
  
  .social-links {
    display: flex;
    gap: 1.5rem;
  }
  
  .social-link {
    color: var(--footer-text);
    font-size: 1.5rem;
    transition: color 0.3s ease, transform 0.3s ease;
  }
  
  .social-link:hover {
    color: #fff;
    transform: translateY(-3px);
  }
  
  .powered-by {
    text-align: center;
    font-size: 0.9rem;
    padding-top: 2rem;
    border-top: 1px solid var(--footer-border);
  }
  
  .obsidian-link {
    color: var(--link-color);
    text-decoration: none;
    font-weight: 600;
    transition: color 0.3s ease;
  }
  
  .obsidian-link:hover {
    color: var(--link-hover-color);
  }

  #heart{
    color: red;
    fill: 1;
  }
  
  /* Add responsive styles here */
  @media (max-width: 768px) {
    .footer-content {
      flex-direction: column;
      gap: 1.5rem;
    }
  
    .copyright {
      text-align: center;
    }
  }
  
  @media (max-width: 600px) {
    .footer-container {
      flex-direction: column;
      gap: 1rem;
      text-align: center;
    }
  
    .footer-content {
      align-items: center;
    }
  
    .footer-nav {
      flex-direction: column;
      align-items: center;
    }
    .powered-by {
      margin-top: 0.5rem;
    }
  }
  
  .sticky-footer {
    position: sticky;
    top: 100vh;
  }
  </style>
  
  