
<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="robots" content="noindex, nofollow">
<title>뒷이야기</title>
<style>
  :root{
    --bg:#faf7f2;
    --ink:#2b2620;
    --sub:#8a8075;
    --line:#e5ddd0;
    --accent:#7a6a53;
    --card:#ffffff;
  }
  *{box-sizing:border-box;}
  html,body{margin:0;padding:0;}
  body{
    background:var(--bg);
    color:var(--ink);
    font-family:"Pretendard","Apple SD Gothic Neo","Malgun Gothic",sans-serif;
    line-height:1.85;
    -webkit-user-select:none;
    -moz-user-select:none;
    user-select:none;
    min-height:100vh;
  }
  /* 입력창만 선택/복사 허용 */
  input, textarea { -webkit-user-select:text; user-select:text; }

  img{ -webkit-user-drag:none; user-drag:none; pointer-events:none; }

  /* ---------- 인쇄 시 전부 숨김 ---------- */
  @media print{
    body::before{
      content:"인쇄 및 캡처는 지원하지 않습니다.";
      display:block; padding:40px; font-size:20px; text-align:center;
    }
    body *{ display:none !important; }
  }

  /* ---------- 게이트 화면 ---------- */
  #gate{
    min-height:100vh;
    display:flex; align-items:center; justify-content:center;
    flex-direction:column;
    padding:24px; text-align:center;
  }
  #gate h1{ font-size:1.05rem; font-weight:600; color:var(--sub); margin-bottom:6px; letter-spacing:.02em;}
  #gate p.desc{ color:var(--sub); font-size:.92rem; max-width:360px; margin:0 0 28px; }
  #gate input{
    width:280px; max-width:80vw;
    padding:12px 14px; border:1px solid var(--line); border-radius:10px;
    font-size:1rem; text-align:center; background:var(--card); color:var(--ink);
    outline:none;
  }
  #gate input:focus{ border-color:var(--accent); }
  #gate button{
    margin-top:14px; padding:11px 28px; border:none; border-radius:10px;
    background:var(--ink); color:#fff; font-size:.95rem; cursor:pointer;
  }
  #gate button:hover{ opacity:.85; }
  #gateMsg{ margin-top:14px; font-size:.85rem; color:#b3543f; min-height:1.2em; }

  /* ---------- 비공개 전환 화면 ---------- */
  #closed{
    display:none;
    min-height:100vh; align-items:center; justify-content:center;
    flex-direction:column; text-align:center; padding:24px;
  }
  #closed p{ color:var(--sub); }

  /* ---------- 본문 ---------- */
  #content{ display:none; }
  header.top{
    position:relative;
    max-width:640px; margin:0 auto; padding:56px 24px 20px; text-align:center;
    border-bottom:1px solid var(--line);
  }
  header.top h1{ font-size:1.4rem; margin:0 0 8px; }
  header.top p{ color:var(--sub); font-size:.88rem; margin:0; }
  header.top p.roleBadge,
  header.top span.roleBadge{
    display:inline-block; margin-top:10px; padding:3px 10px;
    border:1px solid var(--line); border-radius:99px;
    font-size:.72rem; color:var(--accent); letter-spacing:.02em;
  }

  #lockBtn{
    position:absolute; top:18px; right:20px;
    border:1px solid var(--line); background:var(--card); color:var(--sub);
    font-size:.75rem; padding:6px 12px; border-radius:99px; cursor:pointer;
  }
  #lockBtn:hover{ color:var(--accent); border-color:var(--accent); }

  nav#toc{
    max-width:640px; margin:28px auto; padding:20px 24px;
    background:var(--card); border:1px solid var(--line); border-radius:14px;
  }
  nav#toc h2{ font-size:.85rem; color:var(--sub); margin:0 0 10px; font-weight:600; letter-spacing:.04em;}
  nav#toc ul{ list-style:none; margin:0; padding:0; }
  nav#toc li{ border-top:1px solid var(--line); }
  nav#toc li:first-child{ border-top:none; }
  nav#toc a{
    display:block; padding:11px 4px; color:var(--ink); text-decoration:none; font-size:.96rem;
  }
  nav#toc a:hover{ color:var(--accent); }
  nav#toc a span.tag{
    display:inline-block; font-size:.72rem; color:var(--sub); margin-right:8px;
  }
  nav#toc li.groupHead a{
    font-weight:600; padding-top:16px;
  }
  nav#toc li.groupHead:not(:first-child){
    margin-top:4px;
  }

  main{ max-width:640px; margin:0 auto; padding:10px 24px 100px; }
  section.story{ margin-top:56px; scroll-margin-top:24px; }
  section.story h2{
    font-size:1.05rem; color:var(--accent); border-bottom:1px solid var(--line);
    padding-bottom:10px; margin-bottom:22px;
  }
  section.story .body p{ margin:0 0 1.1em; font-size:1rem; white-space:pre-wrap; }

  .backTop{
    display:block; text-align:center; margin:40px 0 0; font-size:.85rem; color:var(--sub); text-decoration:none;
  }

  footer.note{
    max-width:640px; margin:60px auto 0; padding:20px 24px; text-align:center;
    color:var(--sub); font-size:.8rem; border-top:1px solid var(--line);
  }

  /* 포커스를 잃으면(다른 창 전환 등) 흐리게 - 완전한 방지는 아니지만 약한 억제 효과 */
  body.blurred #content, body.blurred #gate{
    filter: blur(14px);
    transition: filter .15s ease;
  }
</style>
</head>
<body>

<!-- ============================================================
  ✏️ 여기 CONFIG만 수정하면 됩니다. (코드의 다른 부분은 건드리지 않아도 됩니다)

  - ownerPassword: 본인(게시자) 확인용 비밀번호.
      게이트 화면 입력창에 이 값을 그대로 입력하면
      "글 제목"이 아니어도 모든 글 목록을 볼 수 있는
      게시자 모드로 들어갑니다. (기본값: 잡다1230)

  - remoteSwitchUrl: (선택) 비워두면 항상 열려있음.
      깃허브 Gist 등에 "OPEN" 또는 "CLOSED" 한 단어만 적힌
      raw 텍스트 파일을 만들고 그 주소를 넣으면,
      그 파일 내용을 "CLOSED"로 바꾸는 것만으로
      이 페이지 전체를 즉시 비공개 화면으로 전환할 수 있습니다.
      (단, 게시자 모드로 이미 들어와 있는 경우에는 CLOSED 상태여도
       본인은 계속 볼 수 있습니다.)

  - posts: 게시글 목록. 새 글을 올릴 때마다 이 배열에
      객체 하나를 추가하면 됩니다.
      title           → 열람자가 입력해야 하는 "비밀번호"이자
                        포스타입에 올리신 실제 글 제목 (똑같이 적어주세요)
      subtitle        → 안내 문구 (선택)
      front           → 앞이야기(원문) 문단들, 배열 안에 문단별로 문자열 하나씩
      chapters        → 뒷이야기들. label은 목차에 뜨는 이름 (예: "1화")
                        paragraphs는 그 화의 문단들

  아래 posts 배열의 첫 번째 항목은 예시입니다.
  그대로 복사해서 새 글을 추가하고, 예시는 지우거나 내용을 바꿔서 쓰세요.
============================================================= -->
<script>
const CONFIG = {
  ownerPassword: "잡다1230",
  remoteSwitchUrl: "",
  posts: [
    {
      title: "여기에 글 제목을 정확히 입력하세요",
      subtitle: "구독자분들을 위한 짧은 뒷이야기입니다",
      front: [
        "여기에 이미 올리신 앞이야기(원문) 첫 문단을 붙여넣으세요.",
        "문단이 바뀔 때마다 배열에 문자열을 하나씩 추가하면 됩니다."
      ],
      chapters: [
        {
          label: "1화",
          paragraphs: [
            "여기에 뒷이야기 1화 내용을 붙여넣으세요."
          ]
        },
        {
          label: "2화",
          paragraphs: [
            "여기에 뒷이야기 2화 내용을 붙여넣으세요."
          ]
        }
        // 화가 늘어나면 위 형식으로 { label:"3화", paragraphs:[...] } 추가
      ]
    }
    // 새 글을 올릴 때마다 여기 콤마(,) 뒤에 { ... } 객체를 통째로 추가하세요
  ]
};
</script>

<div id="gate">
  <h1>비공개 페이지</h1>
  <p class="desc">보고 싶은 글의 제목을 그대로 입력해 주세요.</p>
  <input type="text" id="passInput" placeholder="글 제목 입력" autocomplete="off">
  <br>
  <button id="passBtn">들어가기</button>
  <div id="gateMsg"></div>
</div>

<div id="closed">
  <p>이 글은 현재 비공개로 전환되었습니다.</p>
</div>

<div id="content">
  <header class="top">
    <button id="lockBtn" type="button">🔒 잠금</button>
    <h1 id="pageTitle"></h1>
    <p id="pageSubtitle"></p>
  </header>

  <nav id="toc">
    <h2>목차</h2>
    <ul id="tocList"></ul>
  </nav>

  <main id="storyMain"></main>

  <footer class="note">
    소중한 시간 내어 읽어주셔서 감사합니다.<br>
    캡처나 재배포는 삼가주시면 정말 감사하겠습니다 🙏
  </footer>
</div>

<script>
(function(){
  var gate = document.getElementById('gate');
  var closed = document.getElementById('closed');
  var content = document.getElementById('content');

  function showClosed(){
    gate.style.display='none';
    content.style.display='none';
    closed.style.display='flex';
  }
  function showGate(){
    closed.style.display='none';
    content.style.display='none';
    gate.style.display='flex';
  }
  function showContent(){
    gate.style.display='none';
    closed.style.display='none';
    content.style.display='block';
  }

  // 문자열 비교: 앞뒤 공백 제거 + 중간 공백 여러 칸을 한 칸으로 정리해서 비교
  function normalize(s){
    return (s || '').trim().replace(/\s+/g, ' ');
  }

  function isOwnerPassword(val){
    var pw = normalize(CONFIG.ownerPassword || '');
    if(!pw) return false;
    return normalize(val) === pw;
  }

  function findPost(inputTitle){
    var target = normalize(inputTitle);
    for(var i=0; i<CONFIG.posts.length; i++){
      if(normalize(CONFIG.posts[i].title) === target){
        return CONFIG.posts[i];
      }
    }
    return null;
  }

  function buildFrontSection(post, id){
    var frontSection = document.createElement('section');
    frontSection.className = 'story';
    frontSection.id = id;
    var frontH2 = document.createElement('h2');
    frontH2.textContent = '앞이야기 (원문)';
    var frontBody = document.createElement('div');
    frontBody.className = 'body';
    (post.front || []).forEach(function(para){
      var p = document.createElement('p');
      p.textContent = para;
      frontBody.appendChild(p);
    });
    frontSection.appendChild(frontH2);
    frontSection.appendChild(frontBody);
    return frontSection;
  }

  function buildChapterSection(ch, id, headingPrefix){
    var section = document.createElement('section');
    section.className = 'story';
    section.id = id;
    var h2 = document.createElement('h2');
    h2.textContent = (headingPrefix ? headingPrefix + ' · ' : '') + '뒷이야기 · ' + ch.label;
    var body = document.createElement('div');
    body.className = 'body';
    (ch.paragraphs || []).forEach(function(para){
      var p = document.createElement('p');
      p.textContent = para;
      body.appendChild(p);
    });
    section.appendChild(h2);
    section.appendChild(body);
    return section;
  }

  function appendBackLink(main){
    var backLink = document.createElement('a');
    backLink.className = 'backTop';
    backLink.href = '#toc';
    backLink.textContent = '↑ 목차로 돌아가기';
    main.appendChild(backLink);
  }

  // ---------- 열람자 모드: 글 하나만 표시 ----------
  function renderPost(post){
    document.getElementById('pageTitle').textContent = post.title;
    document.getElementById('pageSubtitle').textContent = post.subtitle || '';

    var tocList = document.getElementById('tocList');
    var main = document.getElementById('storyMain');
    tocList.innerHTML = '';
    main.innerHTML = '';

    // 앞이야기
    var frontLi = document.createElement('li');
    frontLi.innerHTML = '<a href="#story-front"><span class="tag">이전</span>앞이야기 (원문)</a>';
    tocList.appendChild(frontLi);
    main.appendChild(buildFrontSection(post, 'story-front'));

    // 뒷이야기 챕터들
    (post.chapters || []).forEach(function(ch, idx){
      var id = 'story-' + (idx+1);

      var li = document.createElement('li');
      var a = document.createElement('a');
      a.href = '#' + id;
      a.innerHTML = '<span class="tag">뒷이야기</span>' + ch.label;
      li.appendChild(a);
      tocList.appendChild(li);

      main.appendChild(buildChapterSection(ch, id, ''));
    });

    appendBackLink(main);
  }

  // ---------- 게시자 모드: 전체 글 목록을 한 페이지에 표시 ----------
  function renderOwnerView(){
    document.getElementById('pageTitle').textContent = '전체 글 관리';
    document.getElementById('pageSubtitle').innerHTML =
      '<span class="roleBadge">게시자 모드 · 모든 글이 보입니다</span>';

    var tocList = document.getElementById('tocList');
    var main = document.getElementById('storyMain');
    tocList.innerHTML = '';
    main.innerHTML = '';

    if(!CONFIG.posts || CONFIG.posts.length === 0){
      var emptyP = document.createElement('p');
      emptyP.style.textAlign = 'center';
      emptyP.style.color = 'var(--sub)';
      emptyP.textContent = '아직 등록된 글이 없습니다.';
      main.appendChild(emptyP);
      return;
    }

    CONFIG.posts.forEach(function(post, pIdx){
      var frontId = 'post-' + pIdx + '-front';

      var groupLi = document.createElement('li');
      groupLi.className = 'groupHead';
      var groupA = document.createElement('a');
      groupA.href = '#' + frontId;
      groupA.innerHTML = '<span class="tag">글 ' + (pIdx+1) + '</span>';
      groupA.appendChild(document.createTextNode(post.title));
      groupLi.appendChild(groupA);
      tocList.appendChild(groupLi);

      main.appendChild(buildFrontSection(post, frontId));

      (post.chapters || []).forEach(function(ch, cIdx){
        var chId = 'post-' + pIdx + '-ch-' + cIdx;

        var li = document.createElement('li');
        var a = document.createElement('a');
        a.href = '#' + chId;
        a.innerHTML = '<span class="tag">　뒷이야기</span>' + ch.label;
        li.appendChild(a);
        tocList.appendChild(li);

        main.appendChild(buildChapterSection(ch, chId, post.title));
      });
    });

    appendBackLink(main);
  }

  function initGateFlow(){
    // 원격 스위치가 설정된 경우, 먼저 상태를 확인
    if(CONFIG.remoteSwitchUrl && CONFIG.remoteSwitchUrl.trim() !== ""){
      fetch(CONFIG.remoteSwitchUrl, {cache:"no-store"})
        .then(function(r){ return r.text(); })
        .then(function(t){
          var isClosed = t.trim().toUpperCase() === "CLOSED";
          // 게시자 본인은 비공개 상태여도 계속 볼 수 있음
          if(isClosed && sessionStorage.getItem('role') !== 'owner'){
            showClosed();
          } else {
            runGate();
          }
        })
        .catch(function(){
          // 원격 파일을 못 불러오면 안전하게 게이트만 보여줌
          runGate();
        });
    } else {
      runGate();
    }
  }

  function runGate(){
    var role = sessionStorage.getItem('role');

    if(role === 'owner'){
      renderOwnerView();
      showContent();
      return;
    }

    if(role === 'viewer'){
      var savedTitle = sessionStorage.getItem('unlockedTitle');
      var post = savedTitle ? findPost(savedTitle) : null;
      if(post){
        renderPost(post);
        showContent();
        return;
      }
    }

    showGate();
  }

  function tryUnlock(){
    var raw = document.getElementById('passInput').value;
    var msg = document.getElementById('gateMsg');

    // 1) 게시자 본인 확인용 비밀번호
    if(isOwnerPassword(raw)){
      sessionStorage.setItem('role', 'owner');
      sessionStorage.removeItem('unlockedTitle');
      renderOwnerView();
      showContent();
      return;
    }

    // 2) 글 제목으로 열람
    var post = findPost(raw);
    if(post){
      sessionStorage.setItem('role', 'viewer');
      sessionStorage.setItem('unlockedTitle', post.title);
      renderPost(post);
      showContent();
      return;
    }

    msg.textContent = "일치하는 글을 찾을 수 없습니다.";
  }

  function lockAndReturn(){
    sessionStorage.removeItem('role');
    sessionStorage.removeItem('unlockedTitle');
    document.getElementById('passInput').value = '';
    document.getElementById('gateMsg').textContent = '';
    showGate();
  }

  document.getElementById('passBtn').addEventListener('click', tryUnlock);
  document.getElementById('passInput').addEventListener('keydown', function(e){
    if(e.key === 'Enter') tryUnlock();
  });
  document.getElementById('lockBtn').addEventListener('click', lockAndReturn);

  initGateFlow();

  // ---------- 복사/캡처 억제 (완전 차단은 아님) ----------
  document.addEventListener('contextmenu', function(e){ e.preventDefault(); });
  document.addEventListener('copy', function(e){ e.preventDefault(); });
  document.addEventListener('cut', function(e){ e.preventDefault(); });
  document.addEventListener('dragstart', function(e){ e.preventDefault(); });

  document.addEventListener('keydown', function(e){
    var k = e.key.toLowerCase();
    var blockedCombo =
      (e.ctrlKey || e.metaKey) && ['c','x','u','s','p'].indexOf(k) !== -1;
    var devtoolsKey = (e.key === 'F12') ||
      ((e.ctrlKey||e.metaKey) && e.shiftKey && ['i','j','c'].indexOf(k) !== -1);
    if(blockedCombo || devtoolsKey){ e.preventDefault(); }
  });

  // 다른 창/탭으로 포커스를 옮기면 살짝 블러 처리 (약한 억제 장치)
  window.addEventListener('blur', function(){ document.body.classList.add('blurred'); });
  window.addEventListener('focus', function(){ document.body.classList.remove('blurred'); });
})();
</script>

</body>
</html>
