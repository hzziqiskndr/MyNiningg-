

<!DOCTYPE html>
<html lang="ms">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Sayang Mama</title>
<style>
  body { font-family: Arial, sans-serif; background: #fff0f5; color: #333; text-align: center; padding: 20px;}
  h1 { color: #c71585; }
  button { margin: 10px; padding: 10px 20px; font-size: 16px; border-radius: 8px; cursor: pointer;}
  .no-btn { position: relative; }
  .no-btn:hover { background: #f08080; color: white; }
  #memories { margin-top: 20px; font-size: 18px; color: #8b008b;}
  .hidden { display: none; }
</style>
</head>
<body>
<h1>Sayang Mama</h1>
<div id="questionnaire">
  <p>Awak sayang saya tak?</p>
  <button id="yesBtn">Yes</button>
  <button id="noBtn" class="no-btn">No</button>
</div>

<div id="followUp" class="hidden">
  <p>Awak rindukan saya?</p>
  <button class="followYes">Yes</button>
  <button class="followNo no-btn">No</button>
</div>

<div id="secondFollowUp" class="hidden">
  <p>Awak cintakan saya?</p>
  <button class="followYes">Yes</button>
  <button class="followNo no-btn">No</button>
</div>

<div id="thirdFollowUp" class="hidden">
  <p>Awak risaukan saya?</p>
  <button class="followYes">Yes</button>
  <button class="followNo no-btn">No</button>
</div>

<div id="fourthFollowUp" class="hidden">
  <p>Awak fikirkan saya tak time kerja tadi?</p>
  <button class="followYes">Yes</button>
  <button class="followNo no-btn">No</button>
</div>

<div id="challenge" class="hidden">
  <p>Betul ke ni?</p>
  <button class="challengeBtn">Yes</button>
</div>

<div id="challenge2" class="hidden">
  <p>Srs lah yes?</p>
  <button class="challengeBtn">Yes</button>
</div>

<div id="challenge3" class="hidden">
  <p>Dah fikir elok ii?</p>
  <button class="challengeBtn">Yes</button>
</div>

<div id="challenge4" class="hidden">
  <p>Betulll ke ni?</p>
  <button class="challengeBtn">Yes</button>
</div>

<div id="memories" class="hidden">
  <h2>Kenangan Kita</h2>
  <ul>
    <li>Mandi water park dekat Flastmania</li>
    <li>Lepak makan buat TikTok sama ii</li>
    <li>Pergi beli barang sama ii</li>
    <li>Teman mak dia beli barang</li>
    <li>Selalu cakap dia sorang je ada dalam diri saya</li>
    <li>Lagi ii bila time kami tengok bunga apa sama ii</li>
    <li>Hari-hari dia tak pernah jemu untuk tengok saya</li>
  </ul>
</div>

<script>
  const noBtn = document.getElementById('noBtn');
  const yesBtn = document.getElementById('yesBtn');
  const questionnaire = document.getElementById('questionnaire');

  let noClicks = 0;
  noBtn.addEventListener('mouseenter', () => {
    // Move button no randomly on screen to make it hard to click
    noClicks++;
    if (noClicks > 20) {
      noBtn.style.position = 'static';
      noBtn.style.marginLeft = '20px';
      noBtn.style.marginTop = '0';
      noBtn.textContent = 'Please say Yes';
      noBtn.disabled = true;
      return;
    }
    const x = Math.random() * (window.innerWidth - noBtn.offsetWidth);
    const y = Math.random() * (window.innerHeight - noBtn.offsetHeight - 200);
    noBtn.style.position = 'absolute';
    noBtn.style.left = x + 'px';
    noBtn.style.top = y + 'px';
  });

  yesBtn.onclick = () => {
    questionnaire.style.display = 'none';
    document.getElementById('followUp').classList.remove('hidden');
  };

  // Follow up questions with yes/no
  const followUps = ['followUp', 'secondFollowUp', 'thirdFollowUp', 'fourthFollowUp'];
  let currentFollow = 0;
  let allYes = true;

  function setupFollowUpButtons(divId) {
    const div = document.getElementById(divId);
    div.querySelector('.followYes').onclick = () => {
      div.style.display = 'none';
      currentFollow++;
      if (currentFollow < followUps.length) {
        document.getElementById(followUps[currentFollow]).classList.remove('hidden');
      } else {
        showChallenge(0);
      }
    };
    div.querySelector('.followNo').onclick = () => {
      allYes = false;
      // Show no button evasion trick again?
      alert('Awak kena jawab jujur ya! Cuba tekan yes dulu.');
    };
  }

  followUps.forEach(setupFollowUpButtons);

  // Challenge questions
  const challenges = ['challenge', 'challenge2', 'challenge3', 'challenge4'];
  let currentChallenge = 0;

  function showChallenge(index) {
    if (index >= challenges.length) {
      showMemories();
      return;
    }
    challenges.forEach(c => document.getElementById(c).classList.add('hidden'));
    const current = document.getElementById(challenges[index]);
    current.classList.remove('hidden');
    current.querySelector('.challengeBtn').onclick = () => {
      showChallenge(index + 1);
    };
  }

  function showMemories() {
    challenges.forEach(c => document.getElementById(c).classList.add('hidden'));
    document.getElementById('memories').classList.remove('hidden');
  }
</script>
</body>
</html>
