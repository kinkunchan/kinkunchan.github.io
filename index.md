---
layout: default
title: Welcome
permalink: /
---

<div class="hero-section hero-minimal">
  <div class="hero-content">
    <h1 class="hero-name">Mark Jin</h1>
    <p class="hero-title">ML Engineer at Woven by Toyota</p>
    <div class="hero-social">
      <a href="https://linkedin.com/in/markjin" class="hero-social-link" title="LinkedIn">
        <i class="fab fa-linkedin"></i>
      </a>
      <a href="https://scholar.google.com/citations?user=y8YVvSAAAAAJ&hl=en" class="hero-social-link" title="Google Scholar">
        <i class="fa-brands fa-google-scholar"></i>
      </a>
    </div>

    <div class="experience-terminal">
      <div class="terminal-header">
        <span class="terminal-label">experience.log</span>
        <span class="terminal-status">live</span>
      </div>
      <div class="terminal-body">
        <div class="terminal-line">
          <span class="prompt">$</span>
          <span class="typed-text" data-lines="Woven by Toyota — Senior ML Solutions Engineer (current)|ex-PayPal — Staff Machine Learning Engineer (Recommendation)|Education — MSiA @ Northwestern|Education — B.S Computer Science @ UMich|Education - B.S Electrical and Computer Eng., UM-SJTU JI"></span>
          <span class="typed-cursor" aria-hidden="true"></span>
        </div>
      </div>
    </div>

  </div>
</div>

<section class="news-section">
  <div class="news-header">
    <p class="news-kicker">signal feed</p>
    <h2>Personal News</h2>
  </div>
  <div class="news-grid">
    <article class="news-card">
      <div class="news-meta">
        <span class="news-location"><i class="fa-solid fa-location-dot"></i> Tokyo, JP</span>
        <span class="news-date">Nov 2025</span>
      </div>
      <h3>Woven by Toyota</h3>
      <p>Join Woven by Toyota in Tokyo, Japan. Focus on building AI/ML solutions in Computer Vision, NLP, and LLM.</p>
    </article>
    <article class="news-card">
      <div class="news-meta">
        <span class="news-location"><i class="fa-solid fa-location-dot"></i> San Jose, US</span>
        <span class="news-date">Feb 2023</span>
      </div>
      <h3>PayPal</h3>
      <p>Join PayPal in San Jose, US. Focus on personalization, recommendation, and LLM applications.</p>
    </article>
    <article class="news-card">
      <div class="news-meta">
        <span class="news-location"><i class="fa-solid fa-location-dot"></i> Evanston, US</span>
        <span class="news-date">Sep 2021</span>
      </div>
      <h3>Northwestern University</h3>
      <p>Start Master of Science in Analytics Program at Northwestern University.</p>
    </article>
    <article class="news-card">
      <div class="news-meta">
        <span class="news-location"><i class="fa-solid fa-location-dot"></i> Tokyo, Japan</span>
        <span class="news-date">Nov 2020</span>
      </div>
      <h3>早稲田言語学院</h3>
      <p>Start Japanese language program at Waseda Language School.</p>
    </article>
  </div>
</section>

<section class="pubs-section">
  <div class="pubs-header">
    <p class="pubs-kicker">papers</p>
    <div class="pubs-title-row">
      <h2>Publications</h2>
    </div>
  </div>
  <div class="pubs-grid">
    <article class="pub-card">
      <div class="pub-meta">
        <span class="pub-venue">KDD ’22</span>
        <span class="pub-year">2022</span>
      </div>
      <h3 class="pub-title">How does Heterophily Impact the Robustness of Graph Neural Networks? Theoretical Connections and Practical Implications</h3>
      <p class="pub-authors">Jiong Zhu, <span class="author-me">Junchen Jin</span>, Donald Loveland, Michael T. Schaub, Danai Koutra</p>
    </article>
    <article class="pub-card">
      <div class="pub-meta">
        <span class="pub-venue">ACM TKDD</span>
        <span class="pub-year">2021</span>
      </div>
      <h3 class="pub-title">Toward Understanding and Evaluating Structural Node Embeddings</h3>
      <p class="pub-authors"><span class="author-me">Junchen Jin</span>, Mark Heimann, Di Jin, Danai Koutra</p>
    </article>
    <article class="pub-card">
      <div class="pub-meta">
        <span class="pub-venue">KDD MLG Workshop</span>
        <span class="pub-year">2020</span>
      </div>
      <h3 class="pub-title">Understanding and evaluating structural node embedding’s</h3>
      <p class="pub-authors"><span class="author-me">Junchen Jin</span>, Mark Heimann, Di Jin, Danai Koutra</p>
    </article>
  </div>
</section>

<script>
  document.addEventListener('DOMContentLoaded', () => {
    const typed = document.querySelector('.typed-text');
    const cursor = document.querySelector('.typed-cursor');

    if (!typed || !cursor) return;

    const lines = typed.dataset.lines ? typed.dataset.lines.split('|') : [];
    let lineIndex = 0;
    let charIndex = 0;
    let deleting = false;

    const typingSpeed = () => (deleting ? 40 : 80);

    const loop = () => {
      const line = lines[lineIndex] || '';

      if (!deleting) {
        typed.textContent = line.slice(0, charIndex + 1);
        charIndex += 1;

        if (charIndex === line.length) {
          deleting = true;
          return setTimeout(loop, 1100);
        }
      } else {
        typed.textContent = line.slice(0, Math.max(0, charIndex - 1));
        charIndex -= 1;

        if (charIndex === 0) {
          deleting = false;
          lineIndex = (lineIndex + 1) % lines.length;
          return setTimeout(loop, 260);
        }
      }

      setTimeout(loop, typingSpeed());
    };

    loop();

    const hero = document.querySelector('.hero-section');
    if (hero) {
      let rafId;

      const setParallax = (x, y) => {
        hero.style.setProperty('--parallax-x', x);
        hero.style.setProperty('--parallax-y', y);
      };

      const handleMove = (event) => {
        const rect = hero.getBoundingClientRect();
        const x = ((event.clientX - rect.left) / rect.width - 0.5) * 1.1;
        const y = ((event.clientY - rect.top) / rect.height - 0.5) * 1.1;

        cancelAnimationFrame(rafId);
        rafId = requestAnimationFrame(() => setParallax(x.toFixed(3), y.toFixed(3)));
      };

      hero.addEventListener('pointermove', handleMove);
      hero.addEventListener('pointerleave', () => setParallax(0, 0));
    }

    const revealCards = document.querySelectorAll('.news-card, .pub-card');
    if (revealCards.length) {
      const observer = new IntersectionObserver((entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            entry.target.classList.add('is-visible');
          } else {
            entry.target.classList.remove('is-visible');
          }
        });
      }, { threshold: 0.25 });

      revealCards.forEach((card, index) => {
        card.style.setProperty('--card-index', index);
        observer.observe(card);
      });
    }
  });
</script>

<footer class="site-footer">
  <p>© {{ site.time | date: "%Y" }} Mark Jin. All rights reserved.</p>
</footer>
