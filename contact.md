---
layout: page
title: Contact Mortgage4U
description: "Contact EsmÃ© Le Roux for expert home loan advice. Get pre-approved today for your bond application with personalized mortgage solutions."
background: muted
---

<div id="contact" class="contact-page">
  <div class="row">
    <div class="col-lg-12 text-center">
      <h1 class="section-heading text-uppercase">Contact Mortgage4U</h1>
      <p class="section-subheading text-muted">Reach Esme directly by phone, email, or WhatsApp.</p>
    </div>
  </div>

  <div class="contact-inner">
    <aside class="contact-details-card" aria-label="Contact details">
      <div class="contact-details-header">
        <i class="far fa-address-card contact-details-icon" aria-hidden="true"></i>
        <h2 class="contact-details-title">Speak to Us</h2>
      </div>

      <div class="contact-methods">
        {% for method in site.data.sitetext.contact.methods %}
        <a class="contact-method" href="{{ method.url }}" {% if method.url contains 'http' %}target="_blank" rel="noopener"{% endif %}>
          <span class="contact-method-icon">
            <i class="{{ method.icon }}" aria-hidden="true"></i>
          </span>
          <span>
            <strong>{{ method.title }}</strong>
            <span>{{ method.text }}</span>
          </span>
        </a>
        {% endfor %}
      </div>
      <p class="contact-details-note">Use any of the options above and Esme will help you with pre-qualification, bond applications, and bank feedback.</p>
    </aside>

    <aside class="team-hours-card contact-hours-card" aria-label="Office hours">
      <div class="team-hours-header">
        <i class="far fa-clock team-hours-icon" aria-hidden="true"></i>
        <h2 class="team-hours-title">{{ site.data.sitetext.team.hours.title | default: "Office Hours" }}</h2>
      </div>

      <div class="team-hours-list">
        {% for item in site.data.sitetext.team.hours.list %}
        <p>{{ item }}</p>
        {% endfor %}
      </div>

      {% if site.data.sitetext.team.hours.note %}
      <div class="team-hours-note">
        <i class="fas fa-info-circle" aria-hidden="true"></i>
        <span>{{ site.data.sitetext.team.hours.note }}</span>
      </div>
      {% endif %}
    </aside>
  </div>
</div>
