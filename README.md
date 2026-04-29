# CalPersAI
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>PERSy 2.0 — CalPERS Investigations Platform</title>
<style>
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif;background:#f4f4f0;min-height:100vh;display:flex;align-items:center;justify-content:center;padding:24px}
.app{display:flex;height:620px;width:100%;max-width:960px;border-radius:16px;overflow:hidden;border:1px solid #e0ddd5;box-shadow:0 4px 24px rgba(0,0,0,0.08);background:#fff}
.sidebar{width:210px;min-width:210px;background:#042C53;display:flex;flex-direction:column}
.sid-top{padding:20px 16px 16px}
.sid-wordmark{font-size:15px;font-weight:600;color:#fff;letter-spacing:-0.02em}
.sid-wordmark span{color:#85B7EB}
.sid-sub{font-size:11px;color:#378ADD;margin-top:3px;letter-spacing:0.04em;text-transform:uppercase}
.sid-divider{height:1px;background:rgba(255,255,255,0.1);margin:0 16px 10px}
.nav-section{font-size:10px;color:#378ADD;letter-spacing:0.08em;text-transform:uppercase;padding:10px 16px 4px;font-weight:600}
.nav-item{display:flex;align-items:center;gap:10px;padding:9px 16px;font-size:13px;cursor:pointer;color:rgba(255,255,255,0.55);transition:all 0.15s;position:relative}
.nav-item:hover{color:rgba(255,255,255,0.9);background:rgba(255,255,255,0.07)}
.nav-item.active{color:#fff;background:rgba(255,255,255,0.12)}
.nav-item.active::before{content:'';position:absolute;left:0;top:0;bottom:0;width:3px;background:#85B7EB;border-radius:0 2px 2px 0}
.nav-icon{width:16px;height:16px;flex-shrink:0;opacity:0.7}
.nav-item.active .nav-icon{opacity:1}
.sid-footer{margin-top:auto;padding:14px 16px;border-top:1px solid rgba(255,255,255,0.1)}
.avatar-row{display:flex;align-items:center;gap:9px}
.avatar{width:30px;height:30px;border-radius:50%;background:#185FA5;display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:600;color:#B5D4F4;flex-shrink:0}
.avatar-name{font-size:12px;color:rgba(255,255,255,0.8);font-weight:600}
.avatar-role{font-size:11px;color:rgba(255,255,255,0.4)}
.main{flex:1;display:flex;flex-direction:column;overflow:hidden;background:#f4f4f0}
.content{flex:1;overflow-y:auto;padding:18px 22px}
.tab-panel{display:none}
.tab-panel.active{display:block}
.pill{font-size:11px;padding:3px 9px;border-radius:999px;font-weight:500}
.pill-red{background:#FCEBEB;color:#A32D2D}
.pill-amber{background:#FAEEDA;color:#854F0B}
.pill-blue{background:#E6F1FB;color:#0C447C}
.pill-green{background:#EAF3DE;color:#27500A}
.pill-gray{background:#f0efe8;color:#5F5E5A}
.stats-row{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;margin-bottom:18px}
.stat-card{background:#fff;border:1px solid #e8e6df;border-radius:12px;padding:14px 16px;position:relative;overflow:hidden}
.stat-accent{position:absolute;top:0;left:0;right:0;height:3px}
.stat-label{font-size:11px;color:#888780;margin-bottom:6px;text-transform:uppercase;letter-spacing:0.04em}
.stat-value{font-size:26px;font-weight:600;color:#1a1a18;line-height:1}
.stat-delta{font-size:11px;color:#888780;margin-top:5px}
.stat-delta.up{color:#3B6D11}
.stat-delta.warn{color:#854F0B}
.section-hdr{display:flex;align-items:center;justify-content:space-between;margin-bottom:12px}
.section-title{font-size:12px;font-weight:600;color:#888780;text-transform:uppercase;letter-spacing:0.05em}
.card{background:#fff;border:1px solid #e8e6df;border-radius:12px;overflow:hidden}
.case-table{width:100%;border-collapse:collapse;font-size:13px;table-layout:fixed}
.case-table th{text-align:left;padding:10px 14px;font-weight:600;font-size:11px;color:#888780;background:#f8f7f4;border-bottom:1px solid #e8e6df;text-transform:uppercase;letter-spacing:0.04em}
.case-table td{padding:11px 14px;border-bottom:1px solid #f0efe8;color:#1a1a18;vertical-align:middle}
.case-table tr:last-child td{border-bottom:none}
.case-table tr:hover td{background:#f8f7f4;cursor:pointer}
.case-id{font-family:'SF Mono',monospace;font-size:11px;color:#888780}
.case-type{font-size:13px;font-weight:500;color:#1a1a18}
.case-sub{font-size:11px;color:#888780}
.intake-grid{display:grid;grid-template-columns:1fr 1fr;gap:12px}
.form-group{display:flex;flex-direction:column;gap:5px}
.form-label{font-size:11px;font-weight:600;color:#888780;text-transform:uppercase;letter-spacing:0.04em}
input,select,textarea{width:100%;font-size:13px;border-radius:8px;border:1px solid #e0ddd5;padding:8px 10px;font-family:inherit;color:#1a1a18;background:#fff;outline:none}
input:focus,select:focus,textarea:focus{border-color:#185FA5;box-shadow:0 0 0 3px rgba(24,95,165,0.1)}
textarea{resize:vertical;min-height:72px}
.full-width{grid-column:1/-1}
.submit-btn{background:#042C53;color:#B5D4F4;border:none;border-radius:8px;padding:10px 20px;font-size:13px;font-weight:600;cursor:pointer;font-family:inherit}
.submit-btn:hover{background:#0C447C}
.success-flash{font-size:12px;color:#3B6D11;display:none;align-items:center;gap:6px}
.chat-wrap{display:flex;flex-direction:column;gap:10px}
.chat-history{display:flex;flex-direction:column;gap:8px;margin-bottom:8px;max-height:260px;overflow-y:auto}
.msg-wrap{display:flex;flex-direction:column}
.msg-wrap.user{align-items:flex-end}
.msg-sender{font-size:10px;color:#888780;margin-bottom:3px;letter-spacing:0.04em;text-transform:uppercase}
.msg{padding:10px 13px;border-radius:10px;font-size:13px;line-height:1.6;max-width:90%;white-space:pre-wrap}
.msg-ai{background:#fff;border:1px solid #e8e6df;color:#1a1a18}
.msg-user{background:#042C53;color:#B5D4F4}
.qp-row{display:flex;gap:6px;flex-wrap:wrap;margin-bottom:8px}
.qp{font-size:11px;padding:5px 10px;border-radius:999px;border:1px solid #e0ddd5;background:#fff;color:#5F5E5A;cursor:pointer;font-family:inherit}
.qp:hover{background:#f0efe8;color:#1a1a18}
.chat-row{display:flex;gap:8px}
.chat-row input{flex:1}
.send-btn{background:#042C53;color:#B5D4F4;border:none;border-radius:8px;padding:8px 16px;font-size:13px;cursor:pointer;white-space:nowrap;font-family:inherit}
.send-btn:hover{background:#0C447C}
.typing{display:flex;align-items:center;gap:4px;padding:10px 13px}
.typing span{width:6px;height:6px;border-radius:50%;background:#888780;animation:blink 1.2s infinite}
.typing span:nth-child(2){animation-delay:0.2s}
.typing span:nth-child(3){animation-delay:0.4s}
@keyframes blink{0%,80%,100%{opacity:0.2}40%{opacity:1}}
.comp-grid{display:grid;grid-template-columns:1fr 1fr;gap:12px}
.comp-card{background:#fff;border:1px solid #e8e6df;border-radius:12px;overflow:hidden}
.comp-card-hdr{padding:12px 14px;background:#f8f7f4;border-bottom:1px solid #e8e6df;display:flex;align-items:center;justify-content:space-between}
.comp-card-title{font-size:12px;font-weight:600;color:#1a1a18}
.check-list{padding:4px 0}
.check-item{display:flex;align-items:center;gap:9px;padding:8px 14px;font-size:12px;color:#5F5E5A;border-bottom:1px solid #f0efe8}
.check-item:last-child{border-bottom:none}
.ci{width:16px;height:16px;border-radius:50%;flex-shrink:0;display:flex;align-items:center;justify-content:center;font-size:9px;font-weight:700;color:#fff}
.ci-pass{background:#639922}
.ci-warn{background:#BA7517}
.ci-fail{background:#E24B4A}
</style>
</head>
<body>

<div class="app">
  <div class="sidebar">
    <div class="sid-top">
      <div class="sid-wordmark">Persy <span>2.0</span></div>
      <div class="sid-sub">Investigations platform</div>
    </div>
    <div class="sid-divider"></div>
    <div class="nav-section">Workspace</div>
    <div class="nav-item" onclick="showTab('intake',this)">
      <svg class="nav-icon" viewBox="0 0 16 16" fill="none" stroke="currentColor" stroke-width="1.5"><rect x="2" y="2" width="12" height="12" rx="2"/><line x1="5" y1="8" x2="11" y2="8"/><line x1="8" y1="5" x2="8" y2="11"/></svg>
      Case intake
    </div>
    <div class="nav-item active" onclick="showTab('dashboard',this)">
      <svg class="nav-icon" viewBox="0 0 16 16" fill="none" stroke="currentColor" stroke-width="1.5"><rect x="2" y="2" width="5" height="5" rx="1"/><rect x="9" y="2" width="5" height="5" rx="1"/><rect x="2" y="9" width="5" height="5" rx="1"/><rect x="9" y="9" width="5" height="5" rx="1"/></svg>
      Dashboard
    </div>
    <div class="nav-item" onclick="showTab('ai',this)">
      <svg class="nav-icon" viewBox="0 0 16 16" fill="none" stroke="currentColor" stroke-width="1.5"><circle cx="8" cy="8" r="6"/><path d="M6 6.5c0-1.1.9-2 2-2s2 .9 2 2c0 1-1 1.5-2 2v1"/><circle cx="8" cy="12" r="0.5" fill="currentColor"/></svg>
      AI assistant
    </div>
    <div class="nav-item" onclick="showTab('compliance',this)">
      <svg class="nav-icon" viewBox="0 0 16 16" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M8 2L3 4.5v4C3 11.5 5.5 14 8 14s5-2.5 5-5.5v-4L8 2z"/><polyline points="5.5,8 7,9.5 10.5,6"/></svg>
      Compliance
    </div>
    <div class="sid-footer">
      <div class="avatar-row">
        <div class="avatar">HR</div>
        <div>
          <div class="avatar-name">HR Investigator</div>
          <div class="avatar-role">CalPERS — P&amp;I Dept.</div>
        </div>
      </div>
    </div>
  </div>

  <div class="main">
    <div class="content">

      <!-- INTAKE -->
      <div class="tab-panel" id="tab-intake">
        <div class="section-hdr"><span class="section-title">New case submission</span></div>
        <div class="card" style="padding:18px">
          <div class="intake-grid">
            <div class="form-group"><div class="form-label">Complainant</div><input type="text" placeholder="Name or anonymous"/></div>
            <div class="form-group"><div class="form-label">Department</div><select><option>Performance &amp; Investigations</option><option>Health &amp; Benefits</option><option>Talent Acquisition</option><option>Employee Relations</option></select></div>
            <div class="form-group"><div class="form-label">Case type</div><select><option>Workplace misconduct</option><option>FMLA / Leave</option><option>Worker's comp</option><option>Policy violation</option><option>Performance concern</option></select></div>
            <div class="form-group"><div class="form-label">AI-suggested priority</div><select><option>High</option><option selected>Medium</option><option>Low</option></select></div>
            <div class="form-group full-width"><div class="form-label">Case description</div><textarea placeholder="Describe the complaint or concern in detail..."></textarea></div>
            <div class="form-group"><div class="form-label">Assign investigator</div><select><option>E.M. Dominguez-Olea</option><option>E. Garrison</option><option>E. Ralph</option><option>J.E.M. Pagán</option></select></div>
            <div class="form-group" style="justify-content:flex-end"><div class="form-label" style="visibility:hidden">x</div>
              <div style="display:flex;align-items:center;gap:10px">
                <button class="submit-btn" onclick="submitCase()">Submit case</button>
                <div class="success-flash" id="sc">&#10003; Case submitted</div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- DASHBOARD -->
      <div class="tab-panel active" id="tab-dashboard">
        <div class="stats-row">
          <div class="stat-card"><div class="stat-accent" style="background:#185FA5"></div><div class="stat-label">Active cases</div><div class="stat-value">24</div><div class="stat-delta up">+3 this week</div></div>
          <div class="stat-card"><div class="stat-accent" style="background:#1D9E75"></div><div class="stat-label">Avg. resolution</div><div class="stat-value">12d</div><div class="stat-delta up">2 days faster</div></div>
          <div class="stat-card"><div class="stat-accent" style="background:#E24B4A"></div><div class="stat-label">High priority</div><div class="stat-value" style="color:#A32D2D">3</div><div class="stat-delta warn">Needs attention</div></div>
          <div class="stat-card"><div class="stat-accent" style="background:#639922"></div><div class="stat-label">Closed this month</div><div class="stat-value" style="color:#27500A">18</div><div class="stat-delta up">87% resolved</div></div>
        </div>
        <div class="section-hdr"><span class="section-title">Active cases</span><span class="pill pill-gray">5 of 24 shown</span></div>
        <div class="card">
          <table class="case-table">
            <thead><tr><th style="width:110px">Case ID</th><th>Type</th><th>Assigned</th><th style="width:70px">Opened</th><th style="width:80px">Priority</th><th style="width:100px">Status</th></tr></thead>
            <tbody>
              <tr onclick="openCase('INV-2025-041')"><td class="case-id">INV-2025-041</td><td><div class="case-type">Workplace misconduct</div></td><td class="case-sub">E. Garrison</td><td class="case-sub">Apr 22</td><td><span class="pill pill-red">High</span></td><td><span class="pill pill-amber">In review</span></td></tr>
              <tr onclick="openCase('INV-2025-039')"><td class="case-id">INV-2025-039</td><td><div class="case-type">FMLA / Leave</div></td><td class="case-sub">E. Ralph</td><td class="case-sub">Apr 18</td><td><span class="pill pill-red">High</span></td><td><span class="pill pill-amber">Pending docs</span></td></tr>
              <tr onclick="openCase('INV-2025-037')"><td class="case-id">INV-2025-037</td><td><div class="case-type">Policy violation</div></td><td class="case-sub">J.E.M. Pagán</td><td class="case-sub">Apr 15</td><td><span class="pill pill-amber">Medium</span></td><td><span class="pill pill-blue">Investigation</span></td></tr>
              <tr onclick="openCase('INV-2025-035')"><td class="case-id">INV-2025-035</td><td><div class="case-type">Performance concern</div></td><td class="case-sub">E.M. Dominguez-Olea</td><td class="case-sub">Apr 10</td><td><span class="pill pill-amber">Medium</span></td><td><span class="pill pill-blue">Interview stage</span></td></tr>
              <tr onclick="openCase('INV-2025-033')"><td class="case-id">INV-2025-033</td><td><div class="case-type">Worker's comp</div></td><td class="case-sub">E. Garrison</td><td class="case-sub">Apr 8</td><td><span class="pill pill-gray">Low</span></td><td><span class="pill pill-green">Final report</span></td></tr>
            </tbody>
          </table>
        </div>
      </div>

      <!-- AI ASSISTANT -->
      <div class="tab-panel" id="tab-ai">
        <div class="section-hdr"><span class="section-title">AI assistant</span></div>
        <div class="card" style="padding:16px">
          <div class="chat-wrap">
            <div class="chat-history" id="chat-messages">
              <div class="msg-wrap"><div class="msg-sender">PERSy AI</div><div class="msg msg-ai">Hello. I can help you summarize cases, draft letters, check FMLA procedures, or flag compliance issues. What do you need today?</div></div>
            </div>
            <div class="qp-row">
              <button class="qp" onclick="sendQuick('Summarize case INV-2025-041')">Summarize INV-2025-041</button>
              <button class="qp" onclick="sendQuick('Draft a notice of investigation letter')">Draft investigation letter</button>
              <button class="qp" onclick="sendQuick('What are the next steps for an FMLA dispute?')">FMLA next steps</button>
              <button class="qp" onclick="sendQuick('Check policy compliance for workplace misconduct')">Check compliance</button>
            </div>
            <div class="chat-row">
              <input id="chat-input" type="text" placeholder="Ask about a case, policy, or draft a communication..." onkeydown="if(event.key==='Enter')sendMessage()"/>
              <button class="send-btn" onclick="sendMessage()">Send ↗</button>
            </div>
          </div>
        </div>
      </div>

      <!-- COMPLIANCE -->
      <div class="tab-panel" id="tab-compliance">
        <div class="section-hdr"><span class="section-title">Compliance — INV-2025-041</span><span class="pill pill-amber">2 actions needed</span></div>
        <div class="comp-grid">
          <div class="comp-card"><div class="comp-card-hdr"><span class="comp-card-title">Documentation</span><span class="pill pill-amber">1 issue</span></div><div class="check-list"><div class="check-item"><div class="ci ci-pass">&#10003;</div>Initial complaint recorded</div><div class="check-item"><div class="ci ci-pass">&#10003;</div>Case ID assigned</div><div class="check-item"><div class="ci ci-pass">&#10003;</div>Investigator assigned</div><div class="check-item"><div class="ci ci-warn">!</div>Exhibits not yet uploaded</div><div class="check-item"><div class="ci ci-fail">&#10007;</div>Final case report pending</div></div></div>
          <div class="comp-card"><div class="comp-card-hdr"><span class="comp-card-title">Legal &amp; policy</span><span class="pill pill-amber">1 issue</span></div><div class="check-list"><div class="check-item"><div class="ci ci-pass">&#10003;</div>Union contract reviewed</div><div class="check-item"><div class="ci ci-pass">&#10003;</div>Confidentiality maintained</div><div class="check-item"><div class="ci ci-warn">!</div>Legal team notification due</div><div class="check-item"><div class="ci ci-fail">&#10007;</div>Disciplinary notice not sent</div><div class="check-item"><div class="ci ci-pass">&#10003;</div>Data stored securely</div></div></div>
          <div class="comp-card"><div class="comp-card-hdr"><span class="comp-card-title">Timeline</span><span class="pill pill-red">Overdue</span></div><div class="check-list"><div class="check-item"><div class="ci ci-pass">&#10003;</div>Opened within 24 hrs</div><div class="check-item"><div class="ci ci-pass">&#10003;</div>Initial contact made</div><div class="check-item"><div class="ci ci-warn">!</div>Interview overdue by 2 days</div><div class="check-item"><div class="ci ci-fail">&#10007;</div>Resolution deadline: 8 days left</div></div></div>
          <div class="comp-card"><div class="comp-card-hdr"><span class="comp-card-title">Privacy</span><span class="pill pill-green">All clear</span></div><div class="check-list"><div class="check-item"><div class="ci ci-pass">&#10003;</div>Access restricted to assigned staff</div><div class="check-item"><div class="ci ci-pass">&#10003;</div>No public AI tool used</div><div class="check-item"><div class="ci ci-pass">&#10003;</div>PII encrypted at rest</div><div class="check-item"><div class="ci ci-pass">&#10003;</div>Audit log enabled</div></div></div>
        </div>
      </div>

    </div>
  </div>
</div>

<script>
function showTab(id,el){
  ['intake','dashboard','ai','compliance'].forEach(t=>{document.getElementById('tab-'+t).classList.toggle('active',t===id);});
  document.querySelectorAll('.nav-item').forEach(n=>n.classList.remove('active'));
  if(el)el.classList.add('active');
}
function submitCase(){
  const sc=document.getElementById('sc');sc.style.display='flex';
  setTimeout(()=>{sc.style.display='none';},3000);
}
function openCase(id){
  showTab('ai',document.querySelectorAll('.nav-item')[2]);
  setTimeout(()=>{document.getElementById('chat-input').value='Summarize case '+id;sendMessage();},80);
}
const R={
  'summarize case inv-2025-041':'Case INV-2025-041 — workplace misconduct filed Apr 22.\n\nComplainant alleges repeated inappropriate communications from a supervisor over 6 weeks. Evidence: 3 email exhibits, 1 witness statement. Investigator E. Garrison is in active review.\n\nPriority: HIGH — legal notification required within 48 hours.\n\nRecommended next step: schedule formal interview with subject.',
  'draft a notice of investigation letter':'Draft — Notice of Investigation\n\nDear [Employee Name],\n\nThis letter formally notifies you that CalPERS Human Resources has initiated an investigation into a reported workplace concern. Your full cooperation is required throughout this process.\n\nPlease maintain strict confidentiality and contact [Investigator Name] at your earliest convenience to schedule an interview.\n\nThis process will be conducted in accordance with CalPERS policy and applicable union agreements.\n\nSincerely,\nCalPERS Performance & Investigations',
  'what are the next steps for an fmla dispute?':'FMLA dispute — recommended steps:\n\n1. Verify eligibility: 12 months employed + 1,250 hours worked\n2. Request medical certification within 15 calendar days\n3. Notify employee of approval or denial in writing\n4. If disputed, consult legal team and review union contract\n5. Document all communications and decisions\n6. Escalate to CalPERS legal counsel if litigation risk is identified',
  'check policy compliance for workplace misconduct':'Compliance review — workplace misconduct:\n\n✓ Investigation started within 5 business days\n! Interview with subject required within 15 days — INV-2025-041 is approaching deadline\n✓ Confidentiality obligations applied to all parties\n✓ Findings must be documented in structured report\n✗ Disciplinary action requires union notification if subject is represented\n\nStatus: 3 of 5 checkpoints met — action required on interview scheduling and union notification.'
};
function getReply(m){
  const k=m.toLowerCase().replace(/[?]/g,'').trim();
  for(const r in R){const w=r.split(' ');if(w.filter(x=>k.includes(x)&&x.length>3).length>=2)return R[r];}
  return "I've reviewed the available case data. For this specific query, I'd recommend consulting the relevant policy section or escalating to the legal team if compliance risk is identified. Would you like me to draft a communication or check a specific item?";
}
function addMsg(text,isUser){
  const c=document.getElementById('chat-messages');
  const w=document.createElement('div');w.className='msg-wrap'+(isUser?' user':'');
  if(!isUser){const s=document.createElement('div');s.className='msg-sender';s.textContent='PERSy AI';w.appendChild(s);}
  const m=document.createElement('div');m.className='msg '+(isUser?'msg-user':'msg-ai');m.textContent=text;
  w.appendChild(m);c.appendChild(w);c.scrollTop=c.scrollHeight;
}
function addTyping(){
  const c=document.getElementById('chat-messages');
  const w=document.createElement('div');w.id='typ';w.className='msg-wrap';
  const m=document.createElement('div');m.className='msg msg-ai typing';
  m.innerHTML='<span></span><span></span><span></span>';
  w.appendChild(m);c.appendChild(w);c.scrollTop=c.scrollHeight;
}
function removeTyping(){const t=document.getElementById('typ');if(t)t.remove();}
function sendMessage(){
  const inp=document.getElementById('chat-input');const txt=inp.value.trim();if(!txt)return;
  inp.value='';addMsg(txt,true);addTyping();
  setTimeout(()=>{removeTyping();addMsg(getReply(txt),false);},700+Math.random()*400);
}
function sendQuick(t){
  showTab('ai',document.querySelectorAll('.nav-item')[2]);
  setTimeout(()=>{document.getElementById('chat-input').value=t;sendMessage();},60);
}
</script>
</body>
</html>
