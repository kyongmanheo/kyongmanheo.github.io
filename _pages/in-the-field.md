---
title: "In the Field"
layout: single
permalink: /in-the-field/
author_profile: true
---

Fieldwork is at the heart of my research. Whether it's wading through muddy rice paddies at midnight or scaling coastal volcanic rocks in Jeju Island, collecting reliable ecological data in situ is where the science begins.

---

### Recent Field Expeditions

#### 🌊 Jeju Island Coastal Monitoring
Conducting salinity and water temperature profiles in coastal tide pools. Tracking the development and survival of *Dryophytes japonicus* tadpoles under tidal influences.

#### 🌾 Suweon Tree Frog Surveys
Acoustic monitoring of calling males during the spring breeding season to map remaining populations of *Dryophytes suweonensis* in Gyeonggi-do.

---

### Citizen Science & Public Engagement
I strongly believe in translating scientific findings into public awareness. 
* **Collaborative Monitoring:** Working alongside citizen scientists and local conservation groups (e.g., '숲과나눔' Foundation) to track amphibian breeding habitats in urbanized zones.
* **Ecological Education:** Conducting workshops for local communities on the importance of temporary wetlands and biosecurity measures.

---

<!-- iNaturalist 연동 구역 -->
<div id="inat-observations" class="photo-grid">
  <p style="color: #666; grid-column: 1 / -1;">iNaturalist에서 최근 관찰 기록을 불러오는 중...</p>
</div>

<script>
  // 박사님의 iNaturalist 사용자 ID를 입력하세요 (예: 'kyongman')
  const inatUsername = "kyongman"; 
  
  // 불러올 관찰 기록 개수 (기본 6개)
  const displayLimit = 33; 

  fetch(`https://api.inaturalist.org/v1/observations?user_id=${inatUsername}&per_page=${displayLimit}&order=desc&order_by=created_at`)
    .then(response => response.json())
    .then(data => {
      const container = document.getElementById('inat-observations');
      container.innerHTML = ''; // 로딩 텍스트 제거

      if (!data.results || data.results.length === 0) {
        container.innerHTML = '<p style="grid-column: 1 / -1;">관찰 기록이 없거나 아이디를 찾을 수 없습니다.</p>';
        return;
      }

      data.results.forEach(obs => {
        if (obs.photos && obs.photos.length > 0) {
          // 사진 URL (medium 크기로 변환)
          const imgUrl = obs.photos[0].url.replace('square', 'medium');
          const fullImgUrl = obs.photos[0].url.replace('square', 'large');
          
          // 학명 및 국명/통상명
          const taxonName = obs.taxon ? obs.taxon.name : 'Unidentified';
          const commonName = (obs.taxon && obs.taxon.preferred_common_name) ? obs.taxon.preferred_common_name : taxonName;
          
          // 위치 및 날짜 정보
          const place = obs.place_guess || 'South Korea';
          const obsDate = obs.observed_on_string || '';

          // HTML 카드 생성 (기존 photo-card 구조 및 라이트박스 클래스 활용)
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
