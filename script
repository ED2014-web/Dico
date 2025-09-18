// script.js - fetch definition from Wiktionnaire API (French)
const form = document.getElementById('searchForm');
const input = document.getElementById('wordInput');
const resultBox = document.getElementById('result');

form.addEventListener('submit', async (e) => {
  e.preventDefault();
  const word = input.value.trim();
  if (!word) return;

  resultBox.innerHTML = '<p>Recherche en cours...</p>';

  try {
    const url = `https://fr.wiktionary.org/api/rest_v1/page/definition/${encodeURIComponent(word)}`;
    const response = await fetch(url);
    if (!response.ok) {
      throw new Error('Mot non trouvé.');
    }
    const data = await response.json();
    displayDefinition(word, data);
  } catch (err) {
    resultBox.innerHTML = `<p style="color:red">${err.message}</p>`;
  }
});

function displayDefinition(word, data) {
  let html = `<h2>${word}</h2>`;
  if (data.fr && Array.isArray(data.fr)) {
    data.fr.forEach(block => {
      if (block.partOfSpeech) {
        html += `<h3>${block.partOfSpeech}</h3>`;
      }
      if (block.definitions) {
        html += '<ul>';
        block.definitions.forEach(def => {
          html += `<li>${def.definition}`;
          if (def.examples && def.examples.length > 0) {
            html += `<br><em>Exemple : ${def.examples.join('; ')}</em>`;
          }
          html += `</li>`;
        });
        html += '</ul>';
      }
    });
  } else {
    html += '<p>Aucune définition trouvée en français.</p>';
  }
  resultBox.innerHTML = html;
}
