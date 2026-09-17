
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
    --danger:#b3543f;
    --ok:#4a7a5a;
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
  #gateMsg{ margin-top:14px; font-size:.85rem; color:var(--danger); min-height:1.2em; }

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

  /* ================== 관리자 도구 스타일 ================== */
  #adminBox{
    max-width:640px; margin:28px auto 0; padding:18px 22px;
    background:var(--card); border:1px solid var(--line); border-radius:14px;
  }
  #adminBox h2{ font-size:.85rem; color:var(--sub); margin:0 0 12px; font-weight:600; letter-spacing:.04em;}
  .adminRow{ display:flex; gap:8px; flex-wrap:wrap; align-items:center; margin-bottom:10px; }
  .adminRow label{ font-size:.8rem; color:var(--sub); }
  .btn{
    border:none; border-radius:8px; padding:9px 16px; font-size:.85rem; cursor:pointer;
    background:var(--ink); color:#fff;
  }
  .btn:hover{ opacity:.85; }
  .btn.secondary{ background:var(--card); color:var(--ink); border:1px solid var(--line); }
  .btn.danger{ background:var(--danger); color:#fff; }
  .btn.small{ padding:5px 10px; font-size:.75rem; }
  #tokenInput{
    flex:1; min-width:180px; padding:8px 10px; border:1px solid var(--line); border-radius:8px;
    font-size:.85rem; background:#fff;
  }
  #syncStatus{ font-size:.78rem; color:var(--sub); min-height:1.2em; margin-top:4px; }
  #syncStatus.ok{ color:var(--ok); }
  #syncStatus.err{ color:var(--danger); }

  .postCard{
    border:1px solid var(--line); border-radius:10px; padding:12px 14px; margin-bottom:10px;
    display:flex; justify-content:space-between; align-items:center; gap:10px; background:#fffdfa;
  }
  .postCard .pTitle{ font-size:.92rem; }
  .postCard .pSub{ font-size:.75rem; color:var(--sub); margin-top:2px; }
  .postCard .pBtns{ display:flex; gap:6px; flex-shrink:0; }
  #emptyPostsMsg{ text-align:center; color:var(--sub); font-size:.85rem; padding:10px 0; }

  /* ---------- 편집 모달 ---------- */
  #editorOverlay{
    display:none; position:fixed; inset:0; background:rgba(43,38,32,.55);
    align-items:flex-start; justify-content:center; padding:30px 16px; z-index:100; overflow-y:auto;
  }
  #editorPanel{
    background:var(--bg); border-radius:16px; max-width:600px; width:100%;
    padding:26px 24px 30px; margin-bottom:40px;
  }
  #editorPanel h3{ margin:0 0 16px; font-size:1.05rem; }
  .field{ margin-bottom:16px; }
  .field label{ display:block; font-size:.78rem; color:var(--sub); margin-bottom:6px; }
  .field input[type=text], .field textarea{
    width:100%; padding:10px 12px; border:1px solid var(--line); border-radius:8px;
    font-size:.92rem; background:#fff; color:var(--ink); font-family:inherit; resize:vertical;
  }
  .field textarea{ min-height:90px; line-height:1.6; }
  .hint{ font-size:.72rem; color:var(--sub); margin-top:4px; }

  .chapterBlock{
    border:1px solid var(--line); border-radius:10px; padding:14px; margin-bottom:12px; background:#fff;
  }
  .chapterBlock .chapterHead{ display:flex; justify-content:space-between; align-items:center; margin-bottom:8px; }
  .chapterBlock .chapterHead input{
    flex:1; margin-right:8px; padding:7px 10px; border:1px solid var(--line); border-radius:6px; font-size:.88rem;
  }

  #editorFooter{ display:flex; justify-content:flex-end; gap:8px; margin-top:20px; }
  #modalMsg{ font-size:.8rem; color:var(--danger); min-height:1.2em; margin-top:8px; }

  details.setupGuide{ margin-top:6px; font-size:.78rem; color:var(--sub); }
  details.setupGuide summary{ cursor:pointer; color:var(--accent); }
  details.setupGuide ol{ padding-left:18px; }
</style>
</head>
<body>

<!-- ============================================================
  ✏️ 여기 CONFIG만 수정하면 됩니다. (아래 script 태그 밖은 건드릴 필요 없음)

  [1] ownerPassword
      게이트 화면에서 이 값을 입력하면 "관리자 모드"로 들어가
      글 작성/수정/삭제 + 발행을 할 수 있습니다. (기본값: 잡다1230)

  [2] remoteSwitchUrl (선택)
      비워두면 항상 열려있음. GitHub Gist 등에 "OPEN" 또는 "CLOSED"
      한 단어만 적힌 raw 텍스트 파일을 만들고 주소를 넣으면,
      그 값을 "CLOSED"로 바꾸는 것만으로 사이트 전체를 즉시
      비공개로 전환할 수 있습니다. (관리자 본인은 계속 볼 수 있음)

  [3] gistId / gistFilename  ← ★ 실제 "코드 수정 없는 배포"의 핵심
      관리자 모드에서 글을 쓰고 "전체 발행"을 누르면, 이 Gist 파일에
      글 데이터(JSON)가 저장되고 모든 열람자가 즉시 그 내용을 보게 됩니다.

      설정 방법:
        1) https://gist.github.com 에서 새 Gist 생성
           - 파일명: posts.json (아래 gistFilename과 동일하게)
           - 내용: [ ]  (빈 배열 하나만 입력하고 생성)
           - "Create secret gist"로 만들어도 되고 public이어도 됩니다.
             (secret이어도 주소를 아는 사람은 볼 수 있어 완전 비공개는
              아니지만, 검색/목록에는 노출되지 않습니다)
        2) 생성된 Gist 주소 끝의 긴 영숫자 문자열이 gistId 입니다.
           예) https://gist.github.com/아이디/1a2b3c4d5e...  ← 이 부분
        3) GitHub → Settings → Developer settings →
           Personal access tokens → Fine-grained tokens 에서
           "gist" 쓰기 권한만 있는 토큰을 발급하세요.
           ⚠️ 이 토큰은 절대 이 파일(코드)에 붙여넣지 마세요!
           관리자 모드 화면의 "GitHub 토큰" 입력창에 그때그때
           입력하거나, "이 브라우저에 기억하기"를 체크했을 때만
           그 브라우저에 저장됩니다.

      gistId를 비워두면 아래 fallbackPosts만 보여주는
      "오프라인 데모 모드"로 동작하며, 발행 기능은 비활성화됩니다.

  [4] fallbackPosts
      Gist를 아직 설정하지 않았을 때, 또는 Gist를 불러오지 못했을 때
      보여줄 기본 글 목록입니다. (Gist 설정 후에는 참고용 예시일 뿐,
      실제 서비스에는 영향 없음)
============================================================= -->
<script>
const CONFIG = {
  ownerPassword: "잡다1230",
  remoteSwitchUrl: "",

  gistId: "",              // 예: "1a2b3c4d5e6f7g8h9i0j"
  gistFilename: "posts.json",

  fallbackPosts: [
    {
      title: "여기에 글 제목을 정확히 입력하세요",
      subtitle: "구독자분들을 위한 짧은 뒷이야기입니다",
      front: [
        "여기에 이미 올리신 앞이야기(원문) 첫 문단을 붙여넣으세요.",
        "문단이 바뀔 때마다 빈 줄로 구분됩니다."
      ],
      chapters: [
        {
          label: "1화",
          paragraphs: ["여기에 뒷이야기 1화 내용을 붙여넣으세요."]
        },
        {
          label: "2화",
          paragraphs: ["여기에 뒷이야기 2화 내용을 붙여넣으세요."]
        }
      ]
    }
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

  <!-- 관리자 모드에서만 보이는 도구 -->
  <div id="adminBox" style="display:none;">
    <h2>관리자 도구</h2>

    <div class="adminRow">
      <label for="tokenInput">GitHub 토큰</label>
      <input type="password" id="tokenInput" placeholder="발행할 때만 필요 (gist 권한)" autocomplete="off">
      <label style="display:flex;align-items:center;gap:4px;">
        <input type="checkbox" id="rememberToken" style="width:auto;"> 이 브라우저에 기억하기
      </label>
    </div>

    <div class="adminRow">
      <button class="btn" id="newPostBtn" type="button">＋ 새 글 작성</button>
      <button class="btn secondary" id="reloadBtn" type="button">↻ 원격에서 다시 불러오기</button>
      <button class="btn secondary" id="publishBtn" type="button">전체 발행</button>
      <button class="btn secondary" id="exportBtn" type="button">JSON 복사</button>
    </div>
    <div id="syncStatus"></div>

    <details class="setupGuide">
      <summary>Gist 배포가 처음이라면 (설정 방법 보기)</summary>
      <ol>
        <li>gist.github.com에서 posts.json 파일(내용 <code>[]</code>)로 새 Gist를 만들고, 주소 끝 ID를 CONFIG.gistId에 넣으세요.</li>
        <li>GitHub에서 gist 쓰기 권한만 있는 개인 토큰을 발급해, 위 "GitHub 토큰" 칸에 입력하세요. (코드에는 절대 넣지 마세요)</li>
        <li>글을 쓰고 "전체 발행"을 누르면 모든 열람자에게 즉시 반영됩니다.</li>
        <li>Gist를 아직 설정하지 않았다면 "JSON 복사"로 현재 글 데이터를 복사해 직접 Gist에 붙여넣어도 됩니다.</li>
      </ol>
    </details>

    <div id="postManageList" style="margin-top:14px;"></div>
  </div>

  <main id="storyMain"></main>

  <footer class="note">
    소중한 시간 내어 읽어주셔서 감사합니다.<br>
    캡처나 재배포는 삼가주시면 정말 감사하겠습니다 🙏
  </footer>
</div>

<!-- 글쓰기/수정 모달 -->
<div id="editorOverlay">
  <div id="editorPanel">
    <h3 id="editorTitle">새 글 작성</h3>

    <div class="field">
      <label>글 제목 (열람자가 입력할 "비밀번호"와 동일해야 함)</label>
      <input type="text" id="editTitle" placeholder="포스타입 글 제목과 똑같이 입력">
    </div>

    <div class="field">
      <label>부제 / 안내 문구 (선택)</label>
      <input type="text" id="editSubtitle" placeholder="예: 구독자분들을 위한 짧은 뒷이야기입니다">
    </div>

    <div class="field">
      <label>앞이야기 (원문) — 문단 사이는 빈 줄로 구분</label>
      <textarea id="editFront" placeholder="첫 문단

둘째 문단"></textarea>
    </div>

    <div class="field">
      <label>뒷이야기 챕터</label>
      <div id="chapterList"></div>
      <button class="btn secondary small" id="addChapterBtn" type="button">＋ 챕터 추가</button>
    </div>

    <div id="modalMsg"></div>
    <div id="editorFooter">
      <button class="btn secondary" id="cancelEditBtn" type="button">취소</button>
      <button class="btn" id="saveEditBtn" type="button">이 글 저장</button>
    </div>
  </div>
</div>

<script>
(function(){
  var gate = document.getElementById('gate');
  var closed = document.getElementById('closed');
  var content = document.getElementById('content');

  var POSTS = [];          // 현재 메모리 상의 글 목록 (열람/편집 공통 소스)
  var isSiteClosed = false;
  var usingFallback = false;

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
    for(var i=0; i<POSTS.length; i++){
      if(normalize(POSTS[i].title) === target){
        return POSTS[i];
      }
    }
    return null;
  }

  /* ---------------- 원격 데이터 불러오기 ---------------- */
  function loadPosts(){
    if(!CONFIG.gistId || CONFIG.gistId.trim() === ""){
      usingFallback = true;
      POSTS = JSON.parse(JSON.stringify(CONFIG.fallbackPosts || []));
      return Promise.resolve();
    }
    return fetch('https://api.github.com/gists/' + CONFIG.gistId, {cache:'no-store'})
      .then(function(r){ if(!r.ok) throw new Error('HTTP '+r.status); return r.json(); })
      .then(function(data){
        var file = data.files && data.files[CONFIG.gistFilename];
        if(file && typeof file.content === 'string'){
          POSTS = JSON.parse(file.content || '[]');
        } else {
          POSTS = [];
        }
        usingFallback = false;
      })
      .catch(function(){
        usingFallback = true;
        POSTS = JSON.parse(JSON.stringify(CONFIG.fallbackPosts || []));
      });
  }

  function checkRemoteSwitch(){
    if(!CONFIG.remoteSwitchUrl || CONFIG.remoteSwitchUrl.trim() === ""){
      isSiteClosed = false;
      return Promise.resolve();
    }
    return fetch(CONFIG.remoteSwitchUrl, {cache:'no-store'})
      .then(function(r){ return r.text(); })
      .then(function(t){ isSiteClosed = t.trim().toUpperCase() === "CLOSED"; })
      .catch(function(){ isSiteClosed = false; });
  }

  /* ---------------- 렌더링(열람자/공통) ---------------- */
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

  function renderPost(post){
    document.getElementById('adminBox').style.display = 'none';
    document.getElementById('pageTitle').textContent = post.title;
    document.getElementById('pageSubtitle').textContent = post.subtitle || '';

    var tocList = document.getElementById('tocList');
    var main = document.getElementById('storyMain');
    tocList.innerHTML = '';
    main.innerHTML = '';

    var frontLi = document.createElement('li');
    frontLi.innerHTML = '<a href="#story-front"><span class="tag">이전</span>앞이야기 (원문)</a>';
    tocList.appendChild(frontLi);
    main.appendChild(buildFrontSection(post, 'story-front'));

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

  /* ---------------- 렌더링(관리자) ---------------- */
  function renderOwnerView(){
    document.getElementById('pageTitle').textContent = '전체 글 관리';
    var subEl = document.getElementById('pageSubtitle');
    subEl.innerHTML = '<span class="roleBadge">관리자 모드' +
      (usingFallback ? ' · 오프라인(예시 데이터)' : ' · 원격 저장소 연결됨') + '</span>';

    document.getElementById('adminBox').style.display = 'block';
    if(!CONFIG.gistId){
      setSyncStatus('CONFIG.gistId가 비어 있어 "발행"이 비활성화된 데모 모드입니다. 위 안내를 참고해 Gist를 연결하세요.', false);
    }

    renderPostManageList();

    // 아래쪽엔 기존처럼 전체 글 미리보기(읽기전용)도 표시
    var tocList = document.getElementById('tocList');
    var main = document.getElementById('storyMain');
    tocList.innerHTML = '';
    main.innerHTML = '';

    if(!POSTS || POSTS.length === 0){
      var emptyP = document.createElement('p');
      emptyP.style.textAlign = 'center';
      emptyP.style.color = 'var(--sub)';
      emptyP.textContent = '아직 등록된 글이 없습니다. 위 "새 글 작성"을 눌러 시작하세요.';
      main.appendChild(emptyP);
      return;
    }

    POSTS.forEach(function(post, pIdx){
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

  function renderPostManageList(){
    var box = document.getElementById('postManageList');
    box.innerHTML = '';
    if(!POSTS || POSTS.length === 0){
      var msg = document.createElement('div');
      msg.id = 'emptyPostsMsg';
      msg.textContent = '등록된 글이 없습니다.';
      box.appendChild(msg);
      return;
    }
    POSTS.forEach(function(post, idx){
      var card = document.createElement('div');
      card.className = 'postCard';

      var info = document.createElement('div');
      var t = document.createElement('div');
      t.className = 'pTitle';
      t.textContent = (idx+1) + '. ' + post.title;
      var s = document.createElement('div');
      s.className = 'pSub';
      s.textContent = '챕터 ' + ((post.chapters||[]).length) + '개';
      info.appendChild(t); info.appendChild(s);

      var btns = document.createElement('div');
      btns.className = 'pBtns';
      var editBtn = document.createElement('button');
      editBtn.className = 'btn secondary small';
      editBtn.type = 'button';
      editBtn.textContent = '수정';
      editBtn.addEventListener('click', function(){ openEditor(idx); });

      var delBtn = document.createElement('button');
      delBtn.className = 'btn danger small';
      delBtn.type = 'button';
      delBtn.textContent = '삭제';
      delBtn.addEventListener('click', function(){
        if(confirm('"' + post.title + '" 글을 목록에서 삭제할까요?\n(전체 발행을 눌러야 실제로 반영됩니다)')){
          POSTS.splice(idx, 1);
          renderOwnerView();
        }
      });

      btns.appendChild(editBtn);
      btns.appendChild(delBtn);
      card.appendChild(info);
      card.appendChild(btns);
      box.appendChild(card);
    });
  }

  function setSyncStatus(text, ok){
    var el = document.getElementById('syncStatus');
    el.textContent = text;
    el.className = ok === true ? 'ok' : (ok === false ? 'err' : '');
  }

  /* ---------------- 글쓰기 모달 ---------------- */
  var editIndex = null; // null이면 새 글

  function openEditor(idx){
    editIndex = (typeof idx === 'number') ? idx : null;
    var post = editIndex !== null ? POSTS[editIndex] : {title:'', subtitle:'', front:[], chapters:[]};

    document.getElementById('editorTitle').textContent = editIndex !== null ? '글 수정' : '새 글 작성';
    document.getElementById('editTitle').value = post.title || '';
    document.getElementById('editSubtitle').value = post.subtitle || '';
    document.getElementById('editFront').value = (post.front || []).join('\n\n');
    document.getElementById('modalMsg').textContent = '';

    var chapterList = document.getElementById('chapterList');
    chapterList.innerHTML = '';
    (post.chapters || []).forEach(function(ch){
      addChapterRow(ch.label, (ch.paragraphs||[]).join('\n\n'));
    });

    document.getElementById('editorOverlay').style.display = 'flex';
  }

  function closeEditor(){
    document.getElementById('editorOverlay').style.display = 'none';
  }

  function addChapterRow(label, text){
    var wrap = document.createElement('div');
    wrap.className = 'chapterBlock';

    var head = document.createElement('div');
    head.className = 'chapterHead';
    var labelInput = document.createElement('input');
    labelInput.type = 'text';
    labelInput.placeholder = '예: 1화';
    labelInput.value = label || '';
    labelInput.className = 'chLabel';

    var removeBtn = document.createElement('button');
    removeBtn.className = 'btn danger small';
    removeBtn.type = 'button';
    removeBtn.textContent = '챕터 삭제';
    removeBtn.addEventListener('click', function(){ wrap.remove(); });

    head.appendChild(labelInput);
    head.appendChild(removeBtn);

    var ta = document.createElement('textarea');
    ta.className = 'chBody';
    ta.placeholder = '문단 사이는 빈 줄로 구분';
    ta.value = text || '';

    wrap.appendChild(head);
    wrap.appendChild(ta);
    document.getElementById('chapterList').appendChild(wrap);
  }

  function splitParagraphs(raw){
    return (raw || '')
      .split(/\n\s*\n/)
      .map(function(s){ return s.trim(); })
      .filter(function(s){ return s.length > 0; });
  }

  function saveEditor(){
    var title = normalize(document.getElementById('editTitle').value);
    var subtitle = document.getElementById('editSubtitle').value.trim();
    var front = splitParagraphs(document.getElementById('editFront').value);

    if(!title){
      document.getElementById('modalMsg').textContent = '글 제목을 입력해 주세요.';
      return;
    }
    var dup = POSTS.some(function(p, i){
      return normalize(p.title) === title && i !== editIndex;
    });
    if(dup){
      document.getElementById('modalMsg').textContent = '이미 같은 제목의 글이 있습니다. 제목은 서로 달라야 합니다.';
      return;
    }

    var chapters = [];
    document.querySelectorAll('#chapterList .chapterBlock').forEach(function(block){
      var label = block.querySelector('.chLabel').value.trim();
      var paragraphs = splitParagraphs(block.querySelector('.chBody').value);
      if(label || paragraphs.length){
        chapters.push({ label: label || '챕터', paragraphs: paragraphs });
      }
    });

    var newPost = { title: title, subtitle: subtitle, front: front, chapters: chapters };

    if(editIndex !== null){
      POSTS[editIndex] = newPost;
    } else {
      POSTS.push(newPost);
    }

    closeEditor();
    renderOwnerView();
    setSyncStatus('글이 목록에 반영되었습니다. "전체 발행"을 눌러야 열람자에게 실제로 공개됩니다.', null);
  }

  /* ---------------- 발행 (Gist 저장) ---------------- */
  function getToken(){
    var input = document.getElementById('tokenInput').value.trim();
    if(input) return input;
    return sessionStorage.getItem('gh_pat_session') || localStorage.getItem('gh_pat_saved') || '';
  }

  function publishPosts(){
    if(!CONFIG.gistId || CONFIG.gistId.trim() === ""){
      alert('CONFIG.gistId가 설정되어 있지 않아 발행할 수 없습니다.\n관리자 도구의 "Gist 배포가 처음이라면" 안내를 확인해 주세요.');
      return;
    }
    var token = getToken();
    if(!token){
      alert('GitHub 토큰을 입력해 주세요. (gist 쓰기 권한이 있는 토큰)');
      return;
    }
    var remember = document.getElementById('rememberToken').checked;
    if(remember){ localStorage.setItem('gh_pat_saved', token); }
    else { sessionStorage.setItem('gh_pat_session', token); }

    setSyncStatus('발행 중...', null);

    fetch('https://api.github.com/gists/' + CONFIG.gistId, {
      method: 'PATCH',
      headers: {
        'Authorization': 'token ' + token,
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({
        files: {
          [CONFIG.gistFilename]: { content: JSON.stringify(POSTS, null, 2) }
        }
      })
    })
    .then(function(res){
      if(!res.ok){
        return res.json().catch(function(){ return {}; }).then(function(err){
          throw new Error('HTTP ' + res.status + (err && err.message ? ' - ' + err.message : ''));
        });
      }
      usingFallback = false;
      setSyncStatus('발행 완료! 열람자들도 이제 최신 내용을 볼 수 있습니다.', true);
    })
    .catch(function(err){
      setSyncStatus('발행 실패: ' + err.message + ' (토큰 권한/Gist ID를 확인해 주세요)', false);
    });
  }

  function exportJson(){
    var text = JSON.stringify(POSTS, null, 2);
    if(navigator.clipboard && navigator.clipboard.writeText){
      navigator.clipboard.writeText(text).then(function(){
        setSyncStatus('현재 글 데이터(JSON)를 클립보드에 복사했습니다. Gist 파일에 붙여넣으면 됩니다.', true);
      }).catch(function(){
        window.prompt('아래 내용을 복사해 Gist에 붙여넣으세요:', text);
      });
    } else {
      window.prompt('아래 내용을 복사해 Gist에 붙여넣으세요:', text);
    }
  }

  /* ---------------- 게이트 흐름 ---------------- */
  function runGate(){
    var role = sessionStorage.getItem('role');

    if(isSiteClosed && role !== 'owner'){
      showClosed();
      return;
    }

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

    if(isOwnerPassword(raw)){
      sessionStorage.setItem('role', 'owner');
      sessionStorage.removeItem('unlockedTitle');
      renderOwnerView();
      showContent();
      return;
    }

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

  document.getElementById('newPostBtn').addEventListener('click', function(){ openEditor(null); });
  document.getElementById('reloadBtn').addEventListener('click', function(){
    setSyncStatus('불러오는 중...', null);
    loadPosts().then(function(){
      renderOwnerView();
      setSyncStatus(usingFallback ? '원격 데이터를 불러오지 못해 예시 데이터를 표시합니다.' : '원격 데이터를 새로 불러왔습니다.', !usingFallback);
    });
  });
  document.getElementById('publishBtn').addEventListener('click', publishPosts);
  document.getElementById('exportBtn').addEventListener('click', exportJson);
  document.getElementById('addChapterBtn').addEventListener('click', function(){ addChapterRow('', ''); });
  document.getElementById('cancelEditBtn').addEventListener('click', closeEditor);
  document.getElementById('saveEditBtn').addEventListener('click', saveEditor);

  // 저장된 토큰이 있으면 입력창/체크박스에 반영
  var savedToken = localStorage.getItem('gh_pat_saved');
  if(savedToken){
    document.getElementById('tokenInput').value = savedToken;
    document.getElementById('rememberToken').checked = true;
  }

  Promise.all([loadPosts(), checkRemoteSwitch()]).then(runGate);

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

  window.addEventListener('blur', function(){ document.body.classList.add('blurred'); });
  window.addEventListener('focus', function(){ document.body.classList.remove('blurred'); });
})();
</script>

</body>
</html>
