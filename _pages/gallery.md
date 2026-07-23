---
layout: single
title: "Field & Species Gallery"
permalink: /gallery/
author_profile: true
---

A visual record of field surveys, herpetofauna species, and research sites across South Korea.

---

## 📸 Live iNaturalist Observations

<!-- iNaturalist 연동 구역 -->
<div id="inat-observations" class="photo-grid">
  <p style="color: #666; grid-column: 1 / -1;">iNaturalist에서 최근 관찰 기록을 불러오는 중...</p>
</div>

<script>
  const inatUsername = "kyongman"; 
  const displayLimit = 33; 

  fetch(`https://api.inaturalist.org/v1/observations?user_id=${inatUsername}&per_page=${displayLimit}&order=desc&order_by=created_at`)
    .then(response => response.json())
    .then(data => {
      const container = document.getElementById('inat-observations');
      container.innerHTML = ''; 

      if (!data.results || data.results.length === 0) {
        container.innerHTML = '<p style="grid-column: 1 / -1;">관찰 기록이 없거나 아이디를 찾을 수 없습니다.</p>';
        return;
      }

      data.results.forEach(obs => {
        if (obs.photos && obs.photos.length > 0) {
          const imgUrl = obs.photos[0].url.replace('square', 'medium');
          const fullImgUrl = obs.photos[0].url.replace('square', 'large');
          
          const taxonName = obs.taxon ? obs.taxon.name : 'Unidentified';
          const commonName = (obs.taxon && obs.taxon.preferred_common_name) ? obs.taxon.preferred_common_name : taxonName;
          
          const place = obs.place_guess || 'South Korea';
          const obsDate = obs.observed_on_string || '';

          const card = document.createElement('div');
          card.className = 'photo-card';
          card.innerHTML = `
            <a href="${fullImgUrl}" class="image-popup" title="${commonName} (${taxonName})">
              <img src="${imgUrl}" alt="${commonName}">
            </a>
            <p>
              <b>${commonName}</b> (<i>${taxonName}</i>)<br>
              <small>📍 ${place}</small><br>
              <small style="color: #888;">🗓️ ${obsDate}</small><br>
              <a href="${obs.uri}" target="_blank" style="font-size: 0.75rem; color: #74b816; text-decoration: underline;">iNaturalist에서 보기 ↗</a>
            </p>
          `;
          container.appendChild(card);
        }
      });
    })
    .catch(error => {
      console.error('iNaturalist API Error:', error);
      document.getElementById('inat-observations').innerHTML = '<p style="grid-column: 1 / -1;">관찰 기록을 불러오는 중 오류가 발생했습니다.</p>';
    });
</script>

---

## 🐸 Amphibians (양서류)

<div class="photo-grid">
  <div class="photo-card">
    <a href="/assets/images/gallery/treefrog_1.jpg" class="image-popup" title="Japanese Treefrog (Dryophytes japonicus)">
      <img src="/assets/images/gallery/treefrog_1.jpg" alt="Japanese Treefrog">
    </a>
    <p><b>Japanese Treefrog</b> (<i>Dryophytes japonicus</i>)<br><small>Jeju Island Coastal Pool</small></p>
  </div>
  <div class="photo-card">
    <a href="/assets/images/gallery/salamander_1.jpg" class="image-popup" title="Southern Korean Salamander (Hynobius notialis)">
      <img src="/assets/images/gallery/salamander_1.jpg" alt="Southern Korean Salamander">
    </a>
    <p><b>Southern Korean Salamander</b> (<i>Hynobius notialis</i>)<br><small>Southern Forest Habitat</small></p>
  </div>
</div>

---

## 🦎 Reptiles (파충류)

<div class="photo-grid">
  <div class="photo-card">
    <a href="/assets/images/gallery/snake_1.jpg" class="image-popup" title="Red-banded Snake (Lycodon rufozonatus)">
      <img src="/assets/images/gallery/snake_1.jpg" alt="Red-banded Snake">
    </a>
    <p><b>Red-banded Snake</b> (<i>Lycodon rufozonatus</i>)<br><small>Jeju Island Survey</small></p>
  </div>
</div>

---

## 🌿 In the Field (야외 조사 현장)

<div class="photo-grid">
  <div class="photo-card">
    <a href="/assets/images/gallery/field_1.jpg" class="image-popup" title="Nocturnal Field Survey">
      <img src="/assets/images/gallery/field_1.jpg" alt="Field Survey">
    </a>
    <p><b>Nocturnal Field Survey</b><br><small>Stream habitat investigation</small></p>
  </div>
</div>
