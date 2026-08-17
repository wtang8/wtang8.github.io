---
layout: page
title: "STEM Tutoring"
permalink: /tutoring/
description: "STEM & Physics tutoring from a PhD physicist and ML researcher for GCSE, A-Level, and University."
nav: true
nav_order: 7

_styles: >
  /* ============================================================
     TUTORING PAGE - SCOPED STYLES
     All colours use --global-* tokens for dark/light mode compat.
     ============================================================ */

  /* Suppress default post-header; hero handles the heading */
  .post > .post-header { display: none; }

  /* ---- Reset & base ---------------------------------------- */
  .tp {
    font-family: "Inter", "Helvetica Neue", Helvetica, Arial, sans-serif;
    color: var(--global-text-color);
    line-height: 1.65;
  }
  .tp *, .tp *::before, .tp *::after { box-sizing: border-box; }

  /* ---- Layout helpers -------------------------------------- */
  .tp-section {
    padding: 4rem 0;
    border-bottom: 1px solid var(--global-divider-color);
  }
  .tp-section:last-child { border-bottom: none; }
  .tp-container {
    max-width: 900px;
    margin: 0 auto;
    padding: 0 1.25rem;
  }
  .tp-grid-3 {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1.25rem;
  }
  .tp-grid-2 {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1.5rem;
  }
  @media (max-width: 720px) {
    .tp-grid-3, .tp-grid-2 { grid-template-columns: 1fr; }
    .tp-section { padding: 2.5rem 0; }
  }

  /* ---- Section labels -------------------------------------- */
  .tp-eyebrow {
    font-size: 0.72rem;
    font-weight: 600;
    letter-spacing: 0.14em;
    text-transform: uppercase;
    color: var(--global-theme-color);
    margin-bottom: 0.6rem;
  }
  .tp-section-title {
    font-family: "Inter", "Helvetica Neue", Helvetica, Arial, sans-serif;
    font-size: 1.55rem;
    font-weight: 600;
    letter-spacing: -0.025em;
    color: var(--global-text-color);
    margin: 0 0 0.4rem;
  }
  .tp-section-sub {
    font-size: 0.97rem;
    color: var(--global-text-color-light);
    margin: 0 0 2.25rem;
    max-width: 600px;
  }

  /* ============================================================
     HERO
     ============================================================ */
  .tp-hero {
    position: relative;
    padding: 4.5rem 1.25rem 4rem;
    overflow: hidden;
    border-bottom: 1px solid var(--global-divider-color);
  }
  /* Animated dot-grid background - CSS only */
  .tp-hero::before {
    content: "";
    position: absolute;
    inset: 0;
    background-image:
      radial-gradient(circle, var(--global-theme-color) 1px, transparent 1px);
    background-size: 28px 28px;
    opacity: 0.06;
    pointer-events: none;
    animation: tp-drift 28s linear infinite;
  }
  @keyframes tp-drift {
    from { background-position: 0 0; }
    to   { background-position: 56px 56px; }
  }
  .tp-hero::after {
    content: "";
    position: absolute;
    bottom: 0; left: 0; right: 0;
    height: 3px;
    background: linear-gradient(90deg,
      transparent,
      var(--global-theme-color) 30%,
      var(--global-theme-color) 70%,
      transparent);
    opacity: 0.5;
  }
  .tp-hero-inner {
    position: relative;
    max-width: 900px;
    margin: 0 auto;
  }
  .tp-hero-kicker {
    font-size: 0.72rem;
    font-weight: 600;
    letter-spacing: 0.16em;
    text-transform: uppercase;
    color: var(--global-theme-color);
    margin-bottom: 1rem;
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }
  .tp-hero-kicker::before {
    content: "";
    display: inline-block;
    width: 24px; height: 1.5px;
    background: var(--global-theme-color);
  }
  .tp-hero h1 {
    font-family: "Inter", "Helvetica Neue", Helvetica, Arial, sans-serif;
    font-size: clamp(1.8rem, 4vw, 2.6rem);
    font-weight: 700;
    letter-spacing: -0.035em;
    line-height: 1.15;
    color: var(--global-text-color);
    margin: 0 0 1rem;
    max-width: 720px;
  }
  .tp-hero-sub {
    font-size: 1.05rem;
    color: var(--global-text-color-light);
    line-height: 1.6;
    max-width: 620px;
    margin: 0 0 1.75rem;
    font-family: "Charter", "Georgia", serif;
  }

  /* Trust badges */
  .tp-badges {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
    margin-bottom: 2rem;
  }
  .tp-badge {
    display: inline-flex;
    align-items: center;
    gap: 0.35rem;
    padding: 0.3rem 0.75rem;
    font-size: 0.75rem;
    font-weight: 600;
    letter-spacing: 0.02em;
    border: 1px solid var(--global-divider-color);
    color: var(--global-text-color-light);
    background: var(--global-card-bg-color);
    transition: border-color 0.15s, color 0.15s;
    white-space: nowrap;
  }
  .tp-badge i { color: var(--global-theme-color); font-size: 0.7rem; }
  .tp-badge:hover {
    border-color: var(--global-theme-color);
    color: var(--global-text-color);
  }

  /* CTA buttons */
  .tp-cta-row {
    display: flex;
    flex-wrap: wrap;
    gap: 0.75rem;
    align-items: center;
  }
  .tp-btn {
    display: inline-flex;
    align-items: center;
    gap: 0.4rem;
    padding: 0.65rem 1.4rem;
    font-family: "Inter", "Helvetica Neue", Helvetica, Arial, sans-serif;
    font-size: 0.9rem;
    font-weight: 600;
    letter-spacing: 0.01em;
    text-decoration: none;
    border: 1.5px solid var(--global-theme-color);
    transition: background 0.18s, color 0.18s, transform 0.12s;
    cursor: pointer;
  }
  .tp-btn:hover { transform: translateY(-1px); text-decoration: none; }
  .tp-btn-primary {
    background: var(--global-theme-color);
    color: var(--global-hover-text-color);
  }
  .tp-btn-primary:hover {
    background: transparent;
    color: var(--global-theme-color);
  }
  .tp-btn-secondary {
    background: transparent;
    color: var(--global-theme-color);
  }
  .tp-btn-secondary:hover {
    background: var(--global-theme-color);
    color: var(--global-hover-text-color);
  }

  /* ============================================================
     PHILOSOPHY CARDS
     ============================================================ */
  .tp-phil-card {
    border: 1px solid var(--global-divider-color);
    background: var(--global-card-bg-color);
    padding: 1.5rem;
    transition: border-color 0.2s, transform 0.2s;
    position: relative;
  }
  .tp-phil-card::before {
    content: "";
    position: absolute;
    left: 0; top: 0; bottom: 0;
    width: 3px;
    background: var(--global-theme-color);
    opacity: 0;
    transition: opacity 0.2s;
  }
  .tp-phil-card:hover { transform: translateY(-2px); border-color: var(--global-theme-color); }
  .tp-phil-card:hover::before { opacity: 1; }
  .tp-phil-icon {
    font-size: 1.3rem;
    color: var(--global-theme-color);
    margin-bottom: 0.75rem;
  }
  .tp-phil-card h3 {
    font-family: "Inter", "Helvetica Neue", Helvetica, Arial, sans-serif;
    font-size: 0.97rem;
    font-weight: 700;
    letter-spacing: -0.01em;
    margin: 0 0 0.5rem;
    color: var(--global-text-color);
  }
  .tp-phil-card p {
    font-size: 0.875rem;
    color: var(--global-text-color-light);
    margin: 0;
    line-height: 1.6;
  }

  /* ============================================================
     SUBJECT TIERS
     ============================================================ */
  .tp-tier-card {
    border: 1px solid var(--global-divider-color);
    background: var(--global-card-bg-color);
    padding: 0;
    overflow: hidden;
    transition: border-color 0.2s, transform 0.2s;
  }
  .tp-tier-card:hover { transform: translateY(-2px); }
  .tp-tier-header {
    padding: 1rem 1.25rem 0.85rem;
    border-bottom: 1px solid var(--global-divider-color);
  }
  .tp-tier-accent {
    height: 3px;
    margin-bottom: 0.9rem;
  }
  .tp-tier-gcse   .tp-tier-accent { background: #16a34a; }
  .tp-tier-alevel .tp-tier-accent { background: #2563eb; }
  .tp-tier-uni    .tp-tier-accent { background: #7c3aed; }
  .tp-tier-card:hover.tp-tier-gcse   { border-color: #16a34a; }
  .tp-tier-card:hover.tp-tier-alevel { border-color: #2563eb; }
  .tp-tier-card:hover.tp-tier-uni    { border-color: #7c3aed; }
  .tp-tier-label {
    font-size: 0.68rem;
    font-weight: 700;
    letter-spacing: 0.14em;
    text-transform: uppercase;
    margin-bottom: 0.25rem;
  }
  .tp-tier-gcse   .tp-tier-label { color: #16a34a; }
  .tp-tier-alevel .tp-tier-label { color: #2563eb; }
  .tp-tier-uni    .tp-tier-label { color: #7c3aed; }
  .tp-tier-card h3 {
    font-family: "Inter", "Helvetica Neue", Helvetica, Arial, sans-serif;
    font-size: 1rem;
    font-weight: 700;
    margin: 0;
    color: var(--global-text-color);
    letter-spacing: -0.01em;
  }
  .tp-tier-body { padding: 1rem 1.25rem 1.25rem; }
  .tp-chips { display: flex; flex-wrap: wrap; gap: 0.4rem; margin-bottom: 0.85rem; }
  .tp-chip {
    font-size: 0.72rem;
    font-weight: 500;
    padding: 0.2rem 0.6rem;
    border: 1px solid var(--global-divider-color);
    color: var(--global-text-color-light);
    background: transparent;
  }
  .tp-tier-note {
    font-size: 0.8rem;
    color: var(--global-text-color-light);
    font-family: "Charter", "Georgia", serif;
    font-style: italic;
    margin: 0;
  }

  /* ============================================================
     PRICING
     ============================================================ */
  .tp-pricing-card {
    border: 1px solid var(--global-divider-color);
    background: var(--global-card-bg-color);
    padding: 1.75rem 1.5rem;
    position: relative;
    transition: border-color 0.2s, transform 0.2s;
    display: flex;
    flex-direction: column;
  }
  .tp-pricing-card:hover { transform: translateY(-2px); }
  .tp-pricing-card.featured {
    border-color: var(--global-theme-color);
  }
  .tp-pricing-card.featured::after {
    content: "Most Popular";
    position: absolute;
    top: -1px; right: 1.25rem;
    font-size: 0.65rem;
    font-weight: 700;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    padding: 0.2rem 0.65rem;
    background: var(--global-theme-color);
    color: var(--global-hover-text-color);
  }
  .tp-pricing-level {
    font-size: 0.7rem;
    font-weight: 700;
    letter-spacing: 0.14em;
    text-transform: uppercase;
    color: var(--global-theme-color);
    margin-bottom: 0.4rem;
  }
  .tp-pricing-card h3 {
    font-family: "Inter", "Helvetica Neue", Helvetica, Arial, sans-serif;
    font-size: 1.05rem;
    font-weight: 700;
    margin: 0 0 1rem;
    color: var(--global-text-color);
  }
  .tp-price {
    display: flex;
    align-items: baseline;
    gap: 0.2rem;
    margin-bottom: 1rem;
    padding-bottom: 1rem;
    border-bottom: 1px solid var(--global-divider-color);
  }
  .tp-price-amount {
    font-size: 2rem;
    font-weight: 700;
    color: var(--global-text-color);
    letter-spacing: -0.04em;
    font-family: "Inter", "Helvetica Neue", Helvetica, Arial, sans-serif;
  }
  .tp-price-currency {
    font-size: 1.2rem;
    font-weight: 600;
    color: var(--global-text-color-light);
    align-self: flex-start;
    margin-top: 0.3rem;
  }
  .tp-price-unit {
    font-size: 0.8rem;
    color: var(--global-text-color-light);
  }
  .tp-price-note {
    font-size: 0.75rem;
    color: var(--global-text-color-light);
    margin: -0.5rem 0 1rem;
  }
  .tp-feature-list {
    list-style: none;
    margin: 0;
    padding: 0;
    flex: 1;
  }
  .tp-feature-list li {
    font-size: 0.83rem;
    color: var(--global-text-color-light);
    display: flex;
    align-items: flex-start;
    gap: 0.5rem;
    margin-bottom: 0.55rem;
    line-height: 1.4;
  }
  .tp-feature-list li i {
    color: var(--global-theme-color);
    font-size: 0.75rem;
    margin-top: 0.15rem;
    flex-shrink: 0;
  }
  .tp-pricing-cta {
    display: block;
    text-align: center;
    padding: 0.6rem 1rem;
    margin-top: 1.25rem;
    font-size: 0.85rem;
    font-weight: 600;
    font-family: "Inter", "Helvetica Neue", Helvetica, Arial, sans-serif;
    border: 1.5px solid var(--global-theme-color);
    color: var(--global-theme-color);
    text-decoration: none;
    transition: background 0.15s, color 0.15s;
  }
  .tp-pricing-cta:hover {
    background: var(--global-theme-color);
    color: var(--global-hover-text-color);
    text-decoration: none;
  }
  .tp-pricing-card.featured .tp-pricing-cta {
    background: var(--global-theme-color);
    color: var(--global-hover-text-color);
  }
  .tp-pricing-card.featured .tp-pricing-cta:hover {
    background: transparent;
    color: var(--global-theme-color);
  }

  /* Block booking callout */
  .tp-block-callout {
    margin-top: 1.75rem;
    padding: 1.1rem 1.4rem;
    border: 1px solid var(--global-divider-color);
    border-left: 3px solid var(--global-theme-color);
    background: var(--global-card-bg-color);
    font-size: 0.875rem;
    color: var(--global-text-color-light);
    display: flex;
    gap: 0.75rem;
    align-items: flex-start;
  }
  .tp-block-callout i {
    color: var(--global-theme-color);
    margin-top: 0.15rem;
    flex-shrink: 0;
  }
  .tp-block-callout strong { color: var(--global-text-color); }

  /* ============================================================
     BOOKING & CONTACT
     ============================================================ */
  .tp-booking-placeholder {
    border: 1px dashed var(--global-divider-color);
    padding: 2.5rem 1.5rem;
    text-align: center;
    margin-bottom: 2rem;
  }
  .tp-booking-placeholder i {
    font-size: 2rem;
    color: var(--global-theme-color);
    margin-bottom: 0.75rem;
    display: block;
  }
  .tp-booking-placeholder p {
    font-size: 0.875rem;
    color: var(--global-text-color-light);
    margin: 0 0 1rem;
  }

  .tp-form { margin-top: 0; }
  .tp-form-row {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1rem;
    margin-bottom: 1rem;
  }
  @media (max-width: 560px) { .tp-form-row { grid-template-columns: 1fr; } }
  .tp-form-group { display: flex; flex-direction: column; margin-bottom: 1rem; }
  .tp-form-group label {
    font-size: 0.78rem;
    font-weight: 600;
    letter-spacing: 0.03em;
    color: var(--global-text-color-light);
    margin-bottom: 0.35rem;
    text-transform: uppercase;
  }
  .tp-form-group input,
  .tp-form-group select,
  .tp-form-group textarea {
    font-family: "Inter", "Helvetica Neue", Helvetica, Arial, sans-serif;
    font-size: 0.9rem;
    padding: 0.6rem 0.85rem;
    border: 1px solid var(--global-divider-color);
    background: var(--global-card-bg-color);
    color: var(--global-text-color);
    outline: none;
    transition: border-color 0.15s;
    appearance: none;
    border-radius: 0;
    width: 100%;
  }
  .tp-form-group input:focus,
  .tp-form-group select:focus,
  .tp-form-group textarea:focus {
    border-color: var(--global-theme-color);
    box-shadow: 0 0 0 2px color-mix(in srgb, var(--global-theme-color) 12%, transparent);
  }
  .tp-form-group textarea { resize: vertical; min-height: 100px; }
  .tp-form-submit {
    background: var(--global-theme-color);
    color: var(--global-hover-text-color);
    border: 1.5px solid var(--global-theme-color);
    padding: 0.7rem 1.75rem;
    font-family: "Inter", "Helvetica Neue", Helvetica, Arial, sans-serif;
    font-size: 0.9rem;
    font-weight: 600;
    cursor: pointer;
    transition: background 0.15s, color 0.15s, transform 0.12s;
    display: inline-flex;
    align-items: center;
    gap: 0.4rem;
    border-radius: 0;
  }
  .tp-form-submit:hover {
    background: transparent;
    color: var(--global-theme-color);
    transform: translateY(-1px);
  }

  .tp-contact-info {
    padding: 1.5rem;
    border: 1px solid var(--global-divider-color);
    background: var(--global-card-bg-color);
    margin-top: 1.5rem;
  }
  .tp-contact-info h3 {
    font-family: "Inter", "Helvetica Neue", Helvetica, Arial, sans-serif;
    font-size: 0.9rem;
    font-weight: 700;
    margin: 0 0 1rem;
    color: var(--global-text-color);
  }
  .tp-contact-row {
    display: flex;
    align-items: center;
    gap: 0.6rem;
    font-size: 0.875rem;
    margin-bottom: 0.65rem;
    color: var(--global-text-color-light);
  }
  .tp-contact-row i { color: var(--global-theme-color); width: 1rem; text-align: center; }
  .tp-contact-row a { color: var(--global-theme-color); text-decoration: none; }
  .tp-contact-row a:hover { text-decoration: underline; }

  /* ============================================================
     FAQ ACCORDION
     ============================================================ */
  .tp-faq { margin-top: 0; }
  .tp-faq details {
    border-bottom: 1px solid var(--global-divider-color);
  }
  .tp-faq details:first-child {
    border-top: 1px solid var(--global-divider-color);
  }
  .tp-faq summary {
    font-family: "Inter", "Helvetica Neue", Helvetica, Arial, sans-serif;
    font-size: 0.93rem;
    font-weight: 600;
    color: var(--global-text-color);
    padding: 1.1rem 2rem 1.1rem 0;
    cursor: pointer;
    list-style: none;
    position: relative;
    transition: color 0.15s;
    letter-spacing: -0.01em;
  }
  .tp-faq summary::-webkit-details-marker { display: none; }
  .tp-faq summary::after {
    content: "+";
    position: absolute;
    right: 0; top: 50%;
    transform: translateY(-50%);
    font-size: 1.2rem;
    font-weight: 300;
    color: var(--global-theme-color);
    transition: transform 0.2s;
  }
  .tp-faq details[open] summary::after {
    content: "-";
  }
  .tp-faq summary:hover { color: var(--global-theme-color); }
  .tp-faq-body {
    font-size: 0.88rem;
    color: var(--global-text-color-light);
    padding: 0 0 1.1rem;
    line-height: 1.65;
    font-family: "Charter", "Georgia", serif;
  }
  .tp-faq-body a { color: var(--global-theme-color); }

  /* ============================================================
     COMBINED TIER+PRICING CARDS
     ============================================================ */
  .tp-combo-card {
    border: 1px solid var(--global-divider-color);
    background: var(--global-card-bg-color);
    overflow: hidden;
    transition: border-color 0.2s, transform 0.2s;
    display: flex;
    flex-direction: column;
  }
  .tp-combo-card:hover { transform: translateY(-3px); }
  .tp-combo-card.featured { border-color: var(--global-theme-color); }
  .tp-combo-card.featured .tp-tier-header { position: relative; }
  .tp-combo-card.featured .tp-tier-header::after {
    content: "Most Popular";
    position: absolute;
    top: 0.75rem; right: 1rem;
    font-size: 0.62rem;
    font-weight: 700;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    padding: 0.18rem 0.55rem;
    background: var(--global-theme-color);
    color: var(--global-hover-text-color);
  }
  .tp-combo-body {
    padding: 1rem 1.25rem;
    flex: 1;
    display: flex;
    flex-direction: column;
  }
  .tp-combo-divider {
    height: 1px;
    background: var(--global-divider-color);
    margin: 0.9rem 0;
  }
  .tp-combo-price-row {
    display: flex;
    align-items: baseline;
    justify-content: space-between;
    margin-bottom: 0.2rem;
  }
  .tp-combo-price {
    display: flex;
    align-items: baseline;
    gap: 0.15rem;
  }
  .tp-combo-price .tp-price-currency {
    font-size: 1rem;
    font-weight: 600;
    color: var(--global-text-color-light);
    align-self: flex-start;
    margin-top: 0.2rem;
  }
  .tp-combo-price .tp-price-amount {
    font-size: 1.65rem;
    font-weight: 700;
    letter-spacing: -0.04em;
    color: var(--global-text-color);
    font-family: "Inter", "Helvetica Neue", Helvetica, Arial, sans-serif;
  }
  .tp-combo-price .tp-price-unit {
    font-size: 0.77rem;
    color: var(--global-text-color-light);
  }
  .tp-combo-block-note {
    font-size: 0.72rem;
    color: var(--global-text-color-light);
    margin: 0 0 0.85rem;
  }
  .tp-combo-cta {
    display: block;
    text-align: center;
    padding: 0.55rem 1rem;
    margin-top: auto;
    font-size: 0.83rem;
    font-weight: 600;
    font-family: "Inter", "Helvetica Neue", Helvetica, Arial, sans-serif;
    border: 1.5px solid var(--global-theme-color);
    color: var(--global-theme-color);
    text-decoration: none;
    transition: background 0.15s, color 0.15s;
  }
  .tp-combo-cta:hover {
    background: var(--global-theme-color);
    color: var(--global-hover-text-color);
    text-decoration: none;
  }
  .tp-combo-card.featured .tp-combo-cta {
    background: var(--global-theme-color);
    color: var(--global-hover-text-color);
  }
  .tp-combo-card.featured .tp-combo-cta:hover {
    background: transparent;
    color: var(--global-theme-color);
  }
---

{% comment %} ============================================================
Schema.org JSON-LD for Educational Service
============================================================ {% endcomment %}

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "EducationalOccupationalProgram",
  "name": "STEM & Tutoring",
  "description": "One-to-one online tutoring in Physics, Mathematics, and Computing across GCSE, A-Level, and University level. Direct instruction from a PhD physicist and machine learning researcher.",
  "provider": {
    "@type": "Person",
    "name": "Wai Shing Tang",
    "jobTitle": "PhD Physicist & Machine Learning Researcher",
    "email": "wstangtutor@gmail.com",
    "url": "https://wtang8.github.io"
  },
  "educationalProgramMode": "online",
  "url": "https://wtang8.github.io/tutoring/",
  "offers": [
    {
      "@type": "Offer",
      "name": "GCSE / IGCSE Tutoring",
      "priceCurrency": "GBP",
      "price": "45",
      "description": "Foundation & Higher Tier Physics, Mathematics, Chemistry"
    },
    {
      "@type": "Offer",
      "name": "A-Level Tutoring",
      "priceCurrency": "GBP",
      "price": "55",
      "description": "A-Level Physics, Mathematics, Further Mathematics"
    },
    {
      "@type": "Offer",
      "name": "University & Advanced Tutoring",
      "priceCurrency": "GBP",
      "price": "70",
      "description": "Classical Mechanics, Electromagnetism, Computational Physics, Python & Data Science"
    }
  ]
}
</script>

<div class="tp">

  <!-- ============================================================
       HERO
       ============================================================ -->
  <section class="tp-hero" aria-labelledby="tutor-hero-heading">
    <div class="tp-hero-inner">
      <p class="tp-hero-kicker">1-on-1 sessions &middot; Online &middot; Available worldwide</p>
      <h1 id="tutor-hero-heading">
        STEM Tutoring by an Active AI Research Scientist
      </h1>
      <p class="tp-hero-sub">
        From GCSE to university level &middot; Clear, exam-focused teaching in Physics, Maths, and Computing, from a practising PhD physicist and machine learning researcher.
      </p>

      <div class="tp-badges" role="list" aria-label="Tutor credentials">
        <span class="tp-badge" role="listitem">
          <i class="fa-solid fa-graduation-cap" aria-hidden="true"></i> PhD in Physics, Brown University
        </span>
        <span class="tp-badge" role="listitem">
          <i class="fa-solid fa-chart-line" aria-hidden="true"></i> 10+ yrs Scientific &amp; Software Development
        </span>
        <span class="tp-badge" role="listitem">
          <i class="fa-solid fa-hourglass" aria-hidden="true"></i> 200+ hours taught in 2026
        </span>
        <span class="tp-badge" role="listitem">
          <i class="fa-solid fa-certificate" aria-hidden="true"></i> Enhanced DBS Checked
        </span>

      </div>

      <div class="tp-cta-row">
        <a href="#booking" class="tp-btn tp-btn-primary" id="hero-cta-book">
          <i class="fa-regular fa-calendar" aria-hidden="true"></i>
          Book a Free Consultation
        </a>
        <a href="#pricing" class="tp-btn tp-btn-secondary" id="hero-cta-rates">
          View Subject Tiers &amp; Rates
          <i class="fa-solid fa-arrow-down" aria-hidden="true"></i>
        </a>
      </div>
    </div>

  </section>

  <!-- ============================================================
       TEACHING PHILOSOPHY
       ============================================================ -->
  <section class="tp-section" id="philosophy" aria-labelledby="philosophy-heading">
    <div class="tp-container">
      <p class="tp-eyebrow">Approach</p>
      <h2 class="tp-section-title" id="philosophy-heading">How I Teach</h2>
      <p class="tp-section-sub">
        Every session builds the critical thinking skills that separate top-scoring students from average ones.
      </p>

      <div class="tp-grid-3" role="list">

        <article class="tp-phil-card" role="listitem">
          <div class="tp-phil-icon" aria-hidden="true">
            <i class="fa-solid fa-layer-group"></i>
          </div>
          <h3>First-Principles Understanding</h3>
          <p>
            No formula-bashing. You'll learn why each equation works and how it connects to the big picture, so you can adapt it to any question you encounter.
          </p>
        </article>

        <article class="tp-phil-card" role="listitem">
          <div class="tp-phil-icon" aria-hidden="true">
            <i class="fa-solid fa-pencil-ruler"></i>
          </div>
          <h3>Exam Technique</h3>
          <p>
            We work through past papers and mark schemes so you learn exactly how to present your answers to earn top grades.
          </p>
        </article>

        <article class="tp-phil-card" role="listitem">
          <div class="tp-phil-icon" aria-hidden="true">
            <i class="fa-solid fa-chalkboard-user"></i>
          </div>
          <h3>Interactive Problem Solving</h3>
          <p>
            Sessions are highly interactive, with real-time problem solving and discussions to train your scientific thinking and problem-solving skills.
          </p>
        </article>

      </div>
    </div>

  </section>

  <!-- ============================================================
       SUBJECT TIERS & PRICING (COMBINED)
       ============================================================ -->
  <section class="tp-section" id="pricing" aria-labelledby="pricing-heading">
    <div class="tp-container">
      <p class="tp-eyebrow">Curriculum &amp; Rates</p>
      <h2 class="tp-section-title" id="pricing-heading">Subject Tiers &amp; Session Rates</h2>
      <p class="tp-section-sub">
        Every session is 1-on-1, matched to your exact exam board, year, and weaknesses. Async Q&amp;A between lessons, no extra charges for that.
      </p>

      <div class="tp-grid-3" role="list">

        <!-- GCSE -->
        <article class="tp-combo-card tp-tier-gcse" role="listitem" aria-labelledby="combo-gcse-title">
          <div class="tp-tier-accent" aria-hidden="true"></div>
          <div class="tp-tier-header">
            <p class="tp-tier-label">Year 10/11</p>
            <h3 id="combo-gcse-title" style="margin:0;font-size:1rem;font-weight:700;color:var(--global-text-color);">GCSE &amp; IGCSE</h3>
          </div>
          <div class="tp-combo-body">
            <div class="tp-chips" aria-label="Subjects covered">
              <span class="tp-chip">Physics</span>
              <span class="tp-chip">Mathematics</span>
              <span class="tp-chip">Chemistry</span>
              <span class="tp-chip">Further Maths</span>
              <span class="tp-chip">AQA</span>
              <span class="tp-chip">Edexcel</span>
              <span class="tp-chip">OCR</span>
            </div>
            <div class="tp-combo-divider"></div>
            <div class="tp-combo-price-row">
              <div class="tp-combo-price" aria-label="45 pounds per hour">
                <span class="tp-price-currency" aria-hidden="true">&pound;</span>
                <span class="tp-price-amount">45</span>
                <span class="tp-price-unit">&thinsp;/ hr</span>
              </div>
            </div>
            <a href="#booking" class="tp-combo-cta" id="pricing-gcse-cta">Book a Session</a>
          </div>
        </article>

        <article class="tp-combo-card tp-tier-alevel" role="listitem" aria-labelledby="combo-alevel-title">
          <div class="tp-tier-accent" aria-hidden="true"></div>
          <div class="tp-tier-header">
            <p class="tp-tier-label">Year 12/13</p>
            <h3 id="combo-alevel-title" style="margin:0;font-size:1rem;font-weight:700;color:var(--global-text-color);">A-Level</h3>
          </div>
          <div class="tp-combo-body">
            <div class="tp-chips" aria-label="Subjects covered">
              <span class="tp-chip">Physics</span>
              <span class="tp-chip">Mathematics</span>
              <span class="tp-chip">Further Mathematics</span>
              <span class="tp-chip">Statistics</span>
              <span class="tp-chip">AQA</span>
              <span class="tp-chip">Edexcel</span>
              <span class="tp-chip">OCR</span>
            </div>
            <!-- <p class="tp-tier-note" style="margin-bottom:0;">
              Mechanics, waves, fields, calculus, complex numbers, and more.
            </p> -->
            <div class="tp-combo-divider"></div>
            <div class="tp-combo-price-row">
              <div class="tp-combo-price" aria-label="55 pounds per hour">
                <span class="tp-price-currency" aria-hidden="true">&pound;</span>
                <span class="tp-price-amount">55</span>
                <span class="tp-price-unit">&thinsp;/ hr</span>
              </div>
            </div>
            <!-- <ul class="tp-feature-list" aria-label="What's included">
              <li><i class="fa-solid fa-check" aria-hidden="true"></i> 1-on-1 live session (60 min)</li>
              <li><i class="fa-solid fa-check" aria-hidden="true"></i> Tailored homework + mark scheme</li>
              <li><i class="fa-solid fa-check" aria-hidden="true"></i> Async Q&amp;A between lessons</li>
              <li><i class="fa-solid fa-check" aria-hidden="true"></i> UCAS personal statement &amp; university admissions guidance</li>
              <li><i class="fa-solid fa-check" aria-hidden="true"></i> Mock exam &amp; feedback (block students)</li>
            </ul> -->
            <a href="#booking" class="tp-combo-cta" id="pricing-alevel-cta">Book a Session</a>
          </div>
        </article>

        <!-- University -->
        <article class="tp-combo-card tp-tier-uni" role="listitem" aria-labelledby="combo-uni-title">
          <div class="tp-tier-accent" aria-hidden="true"></div>
          <div class="tp-tier-header">
            <p class="tp-tier-label">University</p>
            <h3 id="combo-uni-title" style="margin:0;font-size:1rem;font-weight:700;color:var(--global-text-color);">Undergraduate / Postgrad</h3>
          </div>
          <div class="tp-combo-body">
            <div class="tp-chips" aria-label="Subjects covered">
              <span class="tp-chip">Classical Mechanics</span>
              <span class="tp-chip">Electromagnetism</span>
              <span class="tp-chip">Thermodynamics</span>
              <span class="tp-chip">Statistical Mechanics</span>
              <span class="tp-chip">Quantum Mechanics</span>
              <span class="tp-chip">Computational Physics</span>
              <span class="tp-chip">Algorithms</span>
              <span class="tp-chip">Discrete Mathematics</span>
              <span class="tp-chip">Machine Learning</span>
              <span class="tp-chip">Data Science</span>
              <span class="tp-chip">Bayesian Methods</span>
              <span class="tp-chip">Programming</span>
            </div>
            <div class="tp-combo-divider"></div>
            <div class="tp-combo-price-row">
              <div class="tp-combo-price" aria-label="70 pounds per hour">
                <span class="tp-price-currency" aria-hidden="true">&pound;</span>
                <span class="tp-price-amount">70</span>
                <span class="tp-price-unit">&thinsp;/ hr</span>
              </div>
            </div>
            <a href="#booking" class="tp-combo-cta" id="pricing-uni-cta">Book a Session</a>
          </div>
        </article>

      </div>
    </div>

  </section>

  <!-- ============================================================
       BOOKING & CONTACT
       ============================================================ -->
  <section class="tp-section" id="booking" aria-labelledby="booking-heading">
    <div class="tp-container">
      <p class="tp-eyebrow">Get Started</p>
      <h2 class="tp-section-title" id="booking-heading">Book a Session</h2>
      <p class="tp-section-sub">
        Your first 30-minute consultation is free — no commitment, no payment.
        We'll discuss your goals, find your gaps, and agree a study plan.
      </p>

      <a href="mailto:wstangtutor@gmail.com?subject=Tutoring%20Enquiry%20%E2%80%93%20Free%20Consultation&body=Hi%20Wai%20Shing%2C%0A%0AI%27m%20interested%20in%20booking%20a%20free%20consultation.%0A%0ALevel%3A%20%5BGCSE%20%2F%20A-Level%20%2F%20University%5D%0AExam%20board%20%2F%20institution%3A%20%0AGoals%20%26%20challenges%3A%20%0APreferred%20times%20%28GMT%29%3A%20%0A%0AThanks"
         class="tp-btn tp-btn-primary"
         id="booking-email-cta"
         style="display:inline-flex;margin-bottom:2rem;">
        <i class="fa-regular fa-envelope" aria-hidden="true"></i>
        Send an Enquiry Email
      </a>

      <div class="tp-contact-info" aria-label="Contact information">
        <h3>Contact</h3>
        <p class="tp-contact-row">
          <i class="fa-regular fa-envelope" aria-hidden="true"></i>
          <a href="mailto:wstangtutor@gmail.com" id="contact-email-link">wstangtutor@gmail.com</a>
        </p>
        <p class="tp-contact-row">
          <i class="fa-regular fa-clock" aria-hidden="true"></i>
          Replies within 24 hours (typically same day)
        </p>
        <p class="tp-contact-row">
          <i class="fa-solid fa-globe" aria-hidden="true"></i>
          Sessions via Google Meet - worldwide
        </p>
        <p class="tp-contact-row">
          <i class="fa-solid fa-sterling-sign" aria-hidden="true"></i>
          Payment by bank transfer
        </p>
      </div>

    </div>

  </section>

  <!-- ============================================================
       FAQ
       ============================================================ -->
  <section class="tp-section" id="faq" aria-labelledby="faq-heading">
    <div class="tp-container">
      <p class="tp-eyebrow">FAQ</p>
      <h2 class="tp-section-title" id="faq-heading">Frequently Asked Questions</h2>
      <p class="tp-section-sub">Everything you need to know before your first session.</p>

      <div class="tp-faq">

        <details id="faq-platform">
          <summary>How are online lessons conducted?</summary>
          <div class="tp-faq-body">
            Sessions take place over <strong>Google Meet</strong>.
            A live whiteboard is used throughout for visual explanations
            and worked examples.
          </div>
        </details>

        <details id="faq-trial">
          <summary>Do you offer an introductory consultation?</summary>
          <div class="tp-faq-body">
            Yes. The <strong>first 30-minute consultation is free</strong> — no payment, no obligation.
            We'll talk through your goals and build a study plan. Just send an email to get started.
          </div>
        </details>

        <details id="faq-payment">
          <summary>How do payments work?</summary>
          <div class="tp-faq-body">
            Individual sessions are invoiced after each lesson. Block bookings are invoiced upfront.
            Accepted payment methods: <strong>UK bank transfer (BACS)</strong>.
            Invoices are due within 48 hours of issue.
          </div>
        </details>

        <details id="faq-cancel">
          <summary>What is the cancellation and rescheduling policy?</summary>
          <div class="tp-faq-body">
            Sessions cancelled or rescheduled with <strong>more than 24 hours notice</strong> are
            moved at no charge. Cancellations within 24 hours of the session start are charged
            at 50% of the session rate. No-shows are charged in full. Block-booking sessions are
            transferable indefinitely - they never expire.
          </div>
        </details>

        <details id="faq-materials">
          <summary>Do I need to provide any materials or textbooks?</summary>
          <div class="tp-faq-body">
            For <strong>GCSE and A-Level</strong>: no materials needed. All necessary materials are provided.
            Bring your school textbook if you have one and I will tailor sessions to follow your exact course.
            For <strong>University level</strong>: please share your module syllabus and the textbook your course uses so sessions can be tailored precisely to your assessments.
            Notes will be provided after each lesson.
          </div>
        </details>

        <details id="faq-frequency">
          <summary>How often should I have sessions, and when should I start?</summary>
          <div class="tp-faq-body">
            For exam students: <strong>one session per week</strong> throughout the year,
            with the option to intensify to 2–3 sessions/week in the 4-8 weeks before exams.
            Start early - understanding physics and maths takes months to build, not days to cram.
          </div>
        </details>

      </div>
    </div>

  </section>

</div><!-- end .tp -->
