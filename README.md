<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="default">
<meta name="theme-color" content="#1a73e8">
<title>Family Insurance</title>
<style>
:root {
  --primary:#1a73e8;--primary-dark:#1557b0;--primary-light:#e8f0fe;
  --success:#34a853;--success-light:#e6f4ea;
  --warning:#fbbc04;--warning-light:#fef9e7;
  --danger:#ea4335;--danger-light:#fce8e6;
  --purple:#9c27b0;--purple-light:#f3e5f5;
  --orange:#ff6d00;--orange-light:#fff3e0;
  --g50:#f8f9fa;--g100:#f1f3f4;--g200:#e8eaed;--g300:#dadce0;
  --g400:#bdc1c6;--g500:#9aa0a6;--g600:#80868b;--g700:#5f6368;
  --g800:#3c4043;--g900:#202124;--w:#fff;
  --sh-sm:0 1px 3px rgba(0,0,0,.08);--sh:0 4px 12px rgba(0,0,0,.08);
  --sh-lg:0 8px 24px rgba(0,0,0,.1);
  --r:12px;--r-sm:8px;--r-lg:16px;
}
*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html,body{height:100%;overflow-x:hidden}
body{font-family:-apple-system,BlinkMacSystemFont,'Segoe UI','Noto Sans Thai',sans-serif;
  background:var(--g50);color:var(--g900);font-size:14px;line-height:1.5;-webkit-font-smoothing:antialiased}

/* ── LOADING ── */
#loading{position:fixed;inset:0;background:#fff;z-index:9999;
  display:flex;flex-direction:column;align-items:center;justify-content:center;gap:14px;
  transition:opacity .35s ease}
#loading.done{opacity:0;pointer-events:none}
.ld-logo{font-size:52px;animation:bob .9s ease-in-out infinite alternate}
@keyframes bob{from{transform:translateY(0)}to{transform:translateY(-8px)}}
.ld-title{font-size:20px;font-weight:700;color:var(--g900)}
.ld-sub{font-size:13px;color:var(--g500);min-height:18px}
.ld-bar{width:180px;height:4px;background:var(--g200);border-radius:2px;overflow:hidden}
.ld-fill{height:100%;background:var(--primary);border-radius:2px;transition:width .3s;width:0%}

/* ── BOTTOM NAV ── */
.bnav{position:fixed;bottom:0;left:0;right:0;z-index:200;
  background:var(--w);border-top:1px solid var(--g200);
  padding:6px 0 calc(6px + env(safe-area-inset-bottom));
  display:grid;grid-template-columns:repeat(5,1fr)}
.bni{display:flex;flex-direction:column;align-items:center;gap:2px;
  padding:5px 4px;cursor:pointer;border:none;background:none;
  color:var(--g500);font-size:10px;font-weight:500;min-height:48px;
  justify-content:center;font-family:inherit;position:relative}
.bni.active{color:var(--primary)}
.bni-icon{font-size:22px;line-height:1}
.bni-badge{position:absolute;top:3px;right:calc(50% - 22px);
  background:var(--danger);color:#fff;border-radius:10px;
  font-size:9px;font-weight:700;padding:1px 5px;min-width:16px;text-align:center}

/* ── SIDEBAR ── */
.sidebar{position:fixed;left:0;top:0;bottom:0;width:260px;background:var(--w);
  border-right:1px solid var(--g200);display:flex;flex-direction:column;
  z-index:300;box-shadow:var(--sh);transition:transform .3s cubic-bezier(.4,0,.2,1)}
.sb-brand{display:flex;align-items:center;gap:10px;
  padding:calc(env(safe-area-inset-top) + 14px) 18px 14px;border-bottom:1px solid var(--g100)}
.sb-icon{width:36px;height:36px;border-radius:10px;flex-shrink:0;
  background:linear-gradient(135deg,var(--primary),#4285f4);
  display:flex;align-items:center;justify-content:center;font-size:18px}
.sb-text{font-size:14px;font-weight:700}
.sb-sub{font-size:11px;color:var(--g500)}
.sb-nav{flex:1;padding:10px 0;overflow-y:auto}
.sb-lbl{font-size:10px;font-weight:700;color:var(--g400);text-transform:uppercase;
  letter-spacing:.8px;padding:4px 18px 6px;margin-top:6px}
.sb-item{display:flex;align-items:center;gap:10px;padding:10px 18px;cursor:pointer;
  border-radius:0 22px 22px 0;margin:1px 8px 1px 0;color:var(--g700);
  font-size:13px;font-weight:500;transition:background .15s}
.sb-item:active,.sb-item:hover{background:var(--g100)}
.sb-item.active{background:var(--primary-light);color:var(--primary)}
.sb-ni{font-size:16px;width:20px;text-align:center;flex-shrink:0}
.sb-badge{margin-left:auto;font-size:11px;font-weight:600;background:var(--danger);
  color:#fff;border-radius:10px;padding:1px 6px}
.sb-foot{padding:10px;border-top:1px solid var(--g100)}
.sb-overlay{display:none;position:fixed;inset:0;background:rgba(0,0,0,.45);z-index:299;backdrop-filter:blur(2px)}
.sb-overlay.on{display:block}

/* ── MAIN ── */
.main{min-height:100vh;display:flex;flex-direction:column}
.topbar{background:var(--w);border-bottom:1px solid var(--g200);
  padding:0 14px;padding-top:env(safe-area-inset-top);
  height:calc(52px + env(safe-area-inset-top));
  display:flex;align-items:flex-end;padding-bottom:8px;gap:8px;
  position:sticky;top:0;z-index:50;box-shadow:var(--sh-sm)}
.tb-menu{width:40px;height:36px;border:none;background:transparent;
  cursor:pointer;font-size:20px;display:flex;align-items:center;justify-content:center;border-radius:8px}
.tb-title{font-size:16px;font-weight:700;flex:1}
.tb-actions{display:flex;gap:6px;align-items:center}

/* ── SYNC BAR ── */
.sync-bar{display:flex;align-items:center;gap:8px;padding:7px 14px;
  font-size:12px;border-bottom:1px solid var(--g200);background:var(--w);flex-shrink:0}
.sbd{width:7px;height:7px;border-radius:50%;flex-shrink:0}
.sbd-ok{background:var(--success)}
.sbd-busy{background:var(--warning);animation:sbp 1s infinite}
.sbd-off{background:var(--g400)}
@keyframes sbp{0%,100%{opacity:1}50%{opacity:.25}}
.sb-txt{flex:1;color:var(--g600)}
.sb-act{background:none;border:none;color:var(--primary);font-size:12px;font-weight:600;
  cursor:pointer;padding:4px 8px;border-radius:6px;font-family:inherit;min-height:auto}

/* ── BUTTONS ── */
.btn{display:inline-flex;align-items:center;justify-content:center;gap:6px;
  padding:10px 18px;border-radius:10px;border:none;font-size:13px;font-weight:600;
  cursor:pointer;white-space:nowrap;min-height:44px;font-family:inherit;-webkit-appearance:none;
  transition:opacity .15s,transform .1s}
.btn:active{opacity:.82;transform:scale(.97)}
.btn-p{background:var(--primary);color:#fff}
.btn-p:disabled{background:var(--g300);cursor:not-allowed}
.btn-o{background:transparent;color:var(--primary);border:1.5px solid var(--primary)}
.btn-g{background:transparent;color:var(--g700);border:1.5px solid var(--g200)}
.btn-d{background:var(--danger);color:#fff}
.btn-sm{padding:8px 14px;font-size:12px;min-height:38px;border-radius:8px}
.btn-xs{padding:5px 10px;font-size:11px;min-height:30px;border-radius:6px}

/* ── PAGES ── */
.page{display:none;padding:14px 14px calc(88px + env(safe-area-inset-bottom)) 14px}
.page.active{display:block}

/* ── STATS ── */
.stats-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:14px}
.stat-card{background:var(--w);border-radius:var(--r);padding:14px;
  box-shadow:var(--sh-sm);border:1px solid var(--g100);display:flex;align-items:center;gap:10px}
.stat-icon{width:38px;height:38px;border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:18px;flex-shrink:0}
.stat-val{font-size:22px;font-weight:700;line-height:1}
.stat-lbl{font-size:11px;color:var(--g500);margin-top:2px}

/* ── CHART CARDS ── */
.cc{background:var(--w);border-radius:var(--r);padding:16px;
  box-shadow:var(--sh-sm);border:1px solid var(--g100);margin-bottom:12px}
.cc-title{font-size:14px;font-weight:600;margin-bottom:12px}

/* ── DONUT ── */
.donut-wrap{position:relative;width:110px;height:110px;flex-shrink:0}
.donut-c{position:absolute;inset:0;display:flex;flex-direction:column;align-items:center;justify-content:center}
.donut-n{font-size:20px;font-weight:700;line-height:1}
.donut-l{font-size:9px;color:var(--g500)}
svg.donut{transform:rotate(-90deg)}
.drow{display:flex;align-items:center;gap:14px}
.dleg{display:flex;flex-direction:column;gap:6px;flex:1}
.dleg-item{display:flex;align-items:center;gap:6px;font-size:12px;color:var(--g700)}
.dleg-dot{width:8px;height:8px;border-radius:50%;flex-shrink:0}

/* ── BARS ── */
.mbars{display:flex;flex-direction:column;gap:10px}
.mbar-row{display:flex;align-items:center;gap:8px}
.mbar-track{flex:1;height:16px;background:var(--g100);border-radius:100px;overflow:hidden;display:flex}
.mbar-seg{height:100%}
.mbar-cnt{font-size:11px;color:var(--g500);width:18px;text-align:right}

/* ── EXPIRY ── */
.exp-list{display:flex;flex-direction:column;gap:8px}
.exp-item{display:flex;align-items:center;gap:10px;padding:10px 12px;
  border-radius:var(--r-sm);background:var(--g50);border:1px solid var(--g100);cursor:pointer}
.exp-av{width:32px;height:32px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:12px;font-weight:700;color:#fff;flex-shrink:0}
.exp-info{flex:1;min-width:0}
.exp-nm{font-size:12px;font-weight:600;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.exp-tp{font-size:11px;color:var(--g500)}
.exp-days{font-size:11px;font-weight:700;padding:4px 7px;border-radius:6px;flex-shrink:0;text-align:center}
.dc{background:var(--danger-light);color:var(--danger)}
.dw{background:var(--warning-light);color:#b06000}
.dok{background:var(--success-light);color:var(--success)}

/* ── AUTH CARD ── */
.auth-card{background:linear-gradient(135deg,#1a73e8,#4285f4);border-radius:var(--r);
  padding:16px;margin-bottom:14px;color:#fff}
.auth-card h3{font-size:14px;font-weight:700;margin-bottom:4px}
.auth-card p{font-size:12px;opacity:.88;margin-bottom:12px;line-height:1.6}
.auth-card-btn{background:#fff;color:var(--primary);border:none;padding:10px 20px;
  border-radius:8px;font-size:13px;font-weight:700;cursor:pointer;
  display:inline-flex;align-items:center;gap:6px;min-height:44px;font-family:inherit}
.auth-signed{background:var(--success-light);border:1px solid var(--success);
  border-radius:var(--r);padding:10px 14px;margin-bottom:14px;
  display:flex;align-items:center;gap:10px}

/* ── POLICY CARDS ── */
.plist{display:flex;flex-direction:column;gap:10px}
.pcard{background:var(--w);border-radius:var(--r);padding:14px;
  box-shadow:var(--sh-sm);border:1px solid var(--g100)}
.pcard:active{opacity:.88}
.pc-top{display:flex;align-items:flex-start;gap:10px;margin-bottom:8px}
.pc-av{width:34px;height:34px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:13px;font-weight:700;color:#fff;flex-shrink:0}
.pc-inf{flex:1;min-width:0}
.pc-nm{font-size:13px;font-weight:700}
.pc-co{font-size:12px;color:var(--g500);overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.pc-bot{display:flex;align-items:center;gap:8px;flex-wrap:wrap;font-size:11px;color:var(--g600)}
.pc-act{display:flex;gap:6px;margin-top:10px;padding-top:10px;border-top:1px solid var(--g100)}

/* ── FILTER ── */
.fscroll{display:flex;gap:8px;overflow-x:auto;padding-bottom:4px;margin-bottom:12px;
  -webkit-overflow-scrolling:touch;scrollbar-width:none}
.fscroll::-webkit-scrollbar{display:none}
.fchip{display:inline-flex;align-items:center;gap:4px;padding:7px 14px;
  border-radius:100px;border:1.5px solid var(--g200);background:var(--w);
  font-size:12px;font-weight:500;color:var(--g700);cursor:pointer;white-space:nowrap;
  flex-shrink:0;min-height:36px}
.fchip.on{background:var(--primary-light);border-color:var(--primary);color:var(--primary)}
.srch{display:flex;align-items:center;gap:8px;background:var(--w);
  border:1.5px solid var(--g200);border-radius:10px;padding:10px 14px;margin-bottom:12px}
.srch:focus-within{border-color:var(--primary)}
.srch input{border:none;outline:none;font-size:16px;background:transparent;width:100%;color:var(--g900);font-family:inherit}

/* ── BADGES ── */
.badge{display:inline-flex;align-items:center;gap:3px;padding:3px 8px;border-radius:100px;font-size:11px;font-weight:600}
.b-health{background:var(--success-light);color:var(--success)}
.b-accident{background:var(--warning-light);color:#c77a00}
.b-life{background:var(--purple-light);color:var(--purple)}
.b-ci{background:var(--orange-light);color:var(--orange)}
.b-other{background:var(--g100);color:var(--g700)}
.sdot{width:7px;height:7px;border-radius:50%;display:inline-block;margin-right:3px}
.s-act{background:var(--success)}.s-exp{background:var(--warning)}.s-end{background:var(--danger)}

/* ── FILE CHIP ── */
.fchip2{display:inline-flex;align-items:center;gap:4px;padding:3px 8px;
  background:var(--primary-light);color:var(--primary);border-radius:6px;font-size:11px;font-weight:500;text-decoration:none}

/* ── UPLOAD ── */
.upzone{border:2px dashed var(--g300);border-radius:var(--r-sm);padding:20px;
  text-align:center;cursor:pointer;background:var(--g50);
  display:flex;flex-direction:column;align-items:center;gap:6px}
.upzone input{display:none}
.flist{display:flex;flex-direction:column;gap:6px;margin-top:8px}
.fitem{display:flex;align-items:center;gap:8px;padding:8px 10px;
  background:var(--w);border:1px solid var(--g200);border-radius:var(--r-sm)}
.fitem-nm{flex:1;font-size:12px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}

/* ── MODAL ── */
.mover{display:none;position:fixed;inset:0;background:rgba(0,0,0,.5);z-index:500;
  align-items:flex-end;justify-content:center;backdrop-filter:blur(3px)}
.mover.on{display:flex;animation:mfi .15s}
@keyframes mfi{from{opacity:0}}
.modal{background:var(--w);border-radius:20px 20px 0 0;width:100%;max-height:93vh;
  overflow-y:auto;animation:msu .25s cubic-bezier(.4,0,.2,1);
  padding-bottom:env(safe-area-inset-bottom);-webkit-overflow-scrolling:touch}
@keyframes msu{from{transform:translateY(100%)}}
.mhandle{width:36px;height:4px;background:var(--g300);border-radius:2px;margin:10px auto 0}
.mhead{display:flex;align-items:center;justify-content:space-between;
  padding:14px 18px 12px;border-bottom:1px solid var(--g100);
  position:sticky;top:0;background:var(--w);z-index:1}
.mtitle{font-size:16px;font-weight:700}
.mclose{width:34px;height:34px;border-radius:50%;border:none;background:var(--g100);
  cursor:pointer;font-size:16px;display:flex;align-items:center;justify-content:center;color:var(--g600)}
.mbody{padding:16px 18px}
.mfoot{display:flex;gap:8px;padding:12px 18px;padding-bottom:calc(12px + env(safe-area-inset-bottom));
  border-top:1px solid var(--g100);position:sticky;bottom:0;background:var(--w)}
.mfoot .btn{flex:1}

/* ── FORM ── */
.fg{display:flex;flex-direction:column;gap:6px;margin-bottom:14px}
.fl{font-size:12px;font-weight:600;color:var(--g700)}
.fl .r{color:var(--danger);margin-left:2px}
.fi{background:var(--w);border:1.5px solid var(--g200);border-radius:var(--r-sm);
  padding:12px 14px;font-size:16px;color:var(--g900);outline:none;width:100%;
  font-family:inherit;-webkit-appearance:none;appearance:none;transition:border-color .2s}
.fi:focus{border-color:var(--primary)}
textarea.fi{resize:vertical;min-height:72px}
select.fi{background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='8' viewBox='0 0 12 8'%3E%3Cpath d='M1 1l5 5 5-5' stroke='%239aa0a6' stroke-width='1.5' fill='none' stroke-linecap='round'/%3E%3C/svg%3E");background-repeat:no-repeat;background-position:right 14px center;padding-right:36px}
.frow{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.fdiv{border:none;border-top:1px solid var(--g100);margin:4px 0 14px}
.fsec{font-size:11px;font-weight:700;color:var(--g500);text-transform:uppercase;letter-spacing:.5px;margin-bottom:10px}

/* ── TYPE CHIPS ── */
.tsel{display:grid;grid-template-columns:repeat(5,1fr);gap:6px}
.tc{display:flex;flex-direction:column;align-items:center;gap:3px;padding:10px 4px;
  border-radius:10px;cursor:pointer;border:1.5px solid var(--g200);background:var(--w);
  font-size:10px;font-weight:600;color:var(--g600);min-height:58px;justify-content:center}
.tc-i{font-size:20px}
.tc-health{border-color:var(--success);background:var(--success-light);color:var(--success)}
.tc-accident{border-color:var(--warning);background:var(--warning-light);color:#c77a00}
.tc-life{border-color:var(--purple);background:var(--purple-light);color:var(--purple)}
.tc-ci{border-color:var(--orange);background:var(--orange-light);color:var(--orange)}
.tc-other{border-color:var(--primary);background:var(--primary-light);color:var(--primary)}

/* ── COV GRID ── */
.cgrid{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.citem{display:flex;align-items:center;gap:8px;padding:8px 10px;
  border:1.5px solid var(--g200);border-radius:8px;cursor:pointer;font-size:12px;color:var(--g700)}
.citem input{width:16px;height:16px;accent-color:var(--primary);flex-shrink:0;cursor:pointer}
.citem:has(input:checked){border-color:var(--primary);background:var(--primary-light);color:var(--primary)}

/* ── DETAIL ── */
.dthero{background:var(--g50);border-radius:var(--r-sm);padding:14px;margin-bottom:14px;display:flex;align-items:center;gap:12px}
.dtav{width:46px;height:46px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:19px;font-weight:700;color:#fff;flex-shrink:0}
.dtrows{display:flex;flex-direction:column;gap:8px}
.dt2{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.dtrow{padding:10px 12px;background:var(--g50);border-radius:8px}
.dtk{font-size:10px;font-weight:600;color:var(--g500);text-transform:uppercase;margin-bottom:3px}
.dtv{font-size:13px;font-weight:600;color:var(--g900)}
.ctags{display:flex;flex-wrap:wrap;gap:5px;margin-top:6px}
.ctag{background:var(--primary-light);color:var(--primary);font-size:11px;padding:3px 7px;border-radius:5px;font-weight:500}

/* ── MEMBER PAGE ── */
.mlist{display:flex;flex-direction:column;gap:10px}
.mitem{background:var(--w);border-radius:var(--r);padding:14px;box-shadow:var(--sh-sm);border:1px solid var(--g100);display:flex;align-items:center;gap:12px}
.mav{width:44px;height:44px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:17px;font-weight:700;color:#fff;flex-shrink:0}
.mi{flex:1;min-width:0}
.mi-nm{font-size:14px;font-weight:700}
.mi-mt{font-size:11px;color:var(--g500);margin-top:2px}
.mi-tags{display:flex;gap:4px;flex-wrap:wrap;margin-top:6px}
.mbadge{padding:2px 6px;border-radius:4px;font-size:10px;font-weight:600}

/* ── SETTINGS ── */
.cfg{background:var(--w);border-radius:var(--r);padding:16px;box-shadow:var(--sh-sm);border:1px solid var(--g100);margin-bottom:12px}
.cfg-t{font-size:14px;font-weight:700;margin-bottom:4px}
.cfg-d{font-size:12px;color:var(--g500);margin-bottom:14px;line-height:1.6}
.steps{list-style:none;counter-reset:s}
.steps li{counter-increment:s;padding:8px 0 8px 32px;position:relative;font-size:13px;color:var(--g700);border-bottom:1px solid var(--g100)}
.steps li:last-child{border-bottom:none}
.steps li::before{content:counter(s);position:absolute;left:0;top:8px;width:22px;height:22px;background:var(--primary);color:#fff;border-radius:50%;font-size:11px;font-weight:700;display:flex;align-items:center;justify-content:center}
.code{background:var(--g900);color:#a8d8a8;padding:10px 12px;border-radius:var(--r-sm);font-size:11px;font-family:'Menlo',monospace;overflow-x:auto;line-height:1.7;margin:8px 0;word-break:break-all}
.srow{display:flex;align-items:center;gap:8px;padding:10px 12px;background:var(--g50);border-radius:8px;border:1px solid var(--g200);font-size:13px;margin-bottom:10px}
.sd2{width:8px;height:8px;border-radius:50%;flex-shrink:0}
.sd2-on{background:var(--success);animation:sdp 2s infinite}
.sd2-off{background:var(--g400)}
@keyframes sdp{0%,100%{opacity:1}50%{opacity:.4}}

/* ── ALERT ── */
.alert{display:flex;align-items:flex-start;gap:10px;padding:12px 14px;border-radius:var(--r-sm);margin-bottom:12px;border:1px solid;font-size:13px;line-height:1.5}
.a-d{background:var(--danger-light);border-color:#f5c6c3;color:#c62828}
.a-w{background:var(--warning-light);border-color:#f5e0a0;color:#b06000}
.a-i{background:var(--primary-light);border-color:#b3cef5;color:var(--primary-dark)}

/* ── TOAST ── */
.twrap{position:fixed;bottom:calc(76px + env(safe-area-inset-bottom));left:12px;right:12px;z-index:999;display:flex;flex-direction:column;gap:6px;pointer-events:none}
.toast{background:var(--g900);color:#fff;padding:12px 14px;border-radius:10px;font-size:13px;display:flex;align-items:center;gap:8px;box-shadow:var(--sh-lg);animation:ti .25s;pointer-events:all}
@keyframes ti{from{transform:translateY(8px);opacity:0}}
.t-ok{background:var(--success)}.t-err{background:var(--danger)}.t-wn{background:#b06000}

/* ── SPINNER ── */
.spin{width:16px;height:16px;border:2px solid rgba(255,255,255,.3);border-top-color:#fff;border-radius:50%;animation:sp .6s linear infinite;flex-shrink:0}
@keyframes sp{to{transform:rotate(360deg)}}

/* ── EMPTY ── */
.empty{text-align:center;padding:48px 20px}
.empty-ico{font-size:44px;margin-bottom:12px;opacity:.4}
.empty-t{font-size:15px;font-weight:600;color:var(--g700);margin-bottom:6px}
.empty-d{font-size:12px;color:var(--g500);max-width:260px;margin:0 auto 16px}

/* ── DRIVE CARD ── */
.drive-card{background:linear-gradient(135deg,#1a73e8,#4285f4);color:#fff;border-radius:var(--r);padding:14px 16px;display:flex;align-items:center;gap:12px;margin-bottom:12px;text-decoration:none}

/* ── DESKTOP ── */
@media(min-width:768px){
  .stats-grid{grid-template-columns:repeat(4,1fr);gap:14px}
  .frow{grid-template-columns:1fr 1fr}
  .cgrid{grid-template-columns:repeat(3,1fr)}
  .dt2{grid-template-columns:1fr 1fr}
  .mlist{display:grid;grid-template-columns:repeat(2,1fr)}
  .modal{border-radius:var(--r-lg);max-width:600px;margin:auto;animation:mdi .2s}
  @keyframes mdi{from{transform:scale(.95);opacity:0}}
  .mhandle{display:none}
  .mover{align-items:center}
  .mfoot{flex-direction:row}
  .mfoot .btn{flex:none}
}
@media(min-width:1024px){
  .bnav{display:none!important}
  .tb-menu{display:none!important}
  .sidebar{transform:none!important}
  .main{margin-left:260px}
  .topbar{height:60px;padding:0 28px}
  .page{padding:24px 28px 32px}
  .twrap{left:auto;right:24px;bottom:24px;width:320px}
}
@media(max-width:1023px){
  .sidebar{transform:translateX(-100%)}
  .sidebar.open{transform:translateX(0)}
}
</style>
</head>
<body>

<div id="loading">
  <div class="ld-logo">🛡️</div>
  <div class="ld-title">Family Insurance</div>
  <div class="ld-sub" id="ld-sub">กำลังเริ่มต้น...</div>
  <div class="ld-bar"><div class="ld-fill" id="ld-fill"></div></div>
</div>

<div class="sb-overlay" id="sb-ov" onclick="closeSB()"></div>

<aside class="sidebar" id="sidebar">
  <div class="sb-brand">
    <div class="sb-icon">🛡️</div>
    <div><div class="sb-text">Insurance Manager</div><div class="sb-sub">Family Policy Tracker</div></div>
  </div>
  <nav class="sb-nav">
    <div class="sb-lbl">ภาพรวม</div>
    <div class="sb-item active" onclick="go('dashboard')"><span class="sb-ni">📊</span>Dashboard</div>
    <div class="sb-item" onclick="go('policies')"><span class="sb-ni">📋</span>กรมธรรม์<span class="sb-badge" id="nb-s" style="display:none">0</span></div>
    <div class="sb-lbl" style="margin-top:8px">ประเภท</div>
    <div class="sb-item" onclick="go('policies');setF2('health')"><span class="sb-ni">❤️‍🩹</span>สุขภาพ</div>
    <div class="sb-item" onclick="go('policies');setF2('accident')"><span class="sb-ni">⚡</span>อุบัติเหตุ</div>
    <div class="sb-item" onclick="go('policies');setF2('life')"><span class="sb-ni">🌿</span>ชีวิต</div>
    <div class="sb-item" onclick="go('policies');setF2('ci')"><span class="sb-ni">🏥</span>โรคร้ายแรง</div>
    <div class="sb-lbl" style="margin-top:8px">จัดการ</div>
    <div class="sb-item" onclick="go('members')"><span class="sb-ni">👨‍👩‍👧‍👦</span>สมาชิก</div>
    <div class="sb-item" onclick="go('settings')"><span class="sb-ni">⚙️</span>ตั้งค่า</div>
  </nav>
  <div class="sb-foot"><div id="sb-auth"></div></div>
</aside>

<div class="main">
  <div class="topbar">
    <button class="tb-menu" onclick="openSB()">☰</button>
    <div class="tb-title" id="pg-title">📊 Dashboard</div>
    <div class="tb-actions">
      <button class="btn btn-p btn-sm" onclick="openAdd()">＋ เพิ่ม</button>
    </div>
  </div>

  <div class="sync-bar" id="sync-bar">
    <div class="sbd sbd-off" id="sb-dot"></div>
    <div class="sb-txt" id="sb-txt">ยังไม่ได้เชื่อมต่อ Google</div>
    <button class="sb-act" id="sb-btn" onclick="syncBarAct()">Login</button>
  </div>

  <!-- DASHBOARD -->
  <div class="page active" id="page-dashboard">
    <div id="alert-area"></div>
    <div id="dash-auth"></div>
    <div class="stats-grid">
      <div class="stat-card"><div class="stat-icon" style="background:#e8f0fe">📋</div><div><div class="stat-val" id="s-tot">0</div><div class="stat-lbl">กรมธรรม์</div></div></div>
      <div class="stat-card"><div class="stat-icon" style="background:#e6f4ea">✅</div><div><div class="stat-val" id="s-act" style="color:var(--success)">0</div><div class="stat-lbl">คุ้มครองอยู่</div></div></div>
      <div class="stat-card"><div class="stat-icon" style="background:#fef9e7">⚠️</div><div><div class="stat-val" id="s-exp" style="color:#c77a00">0</div><div class="stat-lbl">ใกล้หมด</div></div></div>
      <div class="stat-card"><div class="stat-icon" style="background:#fce8e6">💰</div><div><div class="stat-val" id="s-pr" style="color:var(--primary);font-size:17px">-</div><div class="stat-lbl">เบี้ยรวม/ปี ฿</div></div></div>
    </div>
    <div class="cc">
      <div class="cc-title">สัดส่วนประเภทประกัน</div>
      <div class="drow">
        <div class="donut-wrap">
          <svg class="donut" id="dsvg" width="110" height="110" viewBox="0 0 110 110">
            <circle cx="55" cy="55" r="42" fill="none" stroke="#e8eaed" stroke-width="13"/>
          </svg>
          <div class="donut-c"><div class="donut-n" id="d-num">0</div><div class="donut-l">รายการ</div></div>
        </div>
        <div class="dleg" id="d-leg"></div>
      </div>
    </div>
    <div class="cc"><div class="cc-title">กรมธรรม์แต่ละสมาชิก</div><div class="mbars" id="mbars"></div></div>
    <div class="cc"><div class="cc-title">🔔 ใกล้หมดอายุ (90 วัน)</div><div class="exp-list" id="exp-list"></div></div>
  </div>

  <!-- POLICIES -->
  <div class="page" id="page-policies">
    <div class="srch"><span>🔍</span><input type="search" id="q" placeholder="ค้นหา..." oninput="renderP()" autocorrect="off" autocapitalize="off"></div>
    <div class="fscroll">
      <div class="fchip on" data-f="all" onclick="setF(this,'all')">ทั้งหมด</div>
      <div class="fchip" data-f="health" onclick="setF(this,'health')">❤️‍🩹 สุขภาพ</div>
      <div class="fchip" data-f="accident" onclick="setF(this,'accident')">⚡ อุบัติเหตุ</div>
      <div class="fchip" data-f="life" onclick="setF(this,'life')">🌿 ชีวิต</div>
      <div class="fchip" data-f="ci" onclick="setF(this,'ci')">🏥 CI</div>
      <div class="fchip" data-f="expiring" onclick="setF(this,'expiring')">⚠️ ใกล้หมด</div>
    </div>
    <div class="plist" id="plist"></div>
    <div id="empty-p" class="empty" style="display:none">
      <div class="empty-ico">🛡️</div>
      <div class="empty-t">ยังไม่มีกรมธรรม์</div>
      <div class="empty-d">กดปุ่ม ＋ เพิ่ม เพื่อเริ่มบันทึก</div>
      <button class="btn btn-p" onclick="openAdd()">＋ เพิ่มกรมธรรม์แรก</button>
    </div>
  </div>

  <!-- MEMBERS -->
  <div class="page" id="page-members">
    <div style="display:flex;justify-content:flex-end;margin-bottom:12px">
      <button class="btn btn-p btn-sm" onclick="openMemberMod()">＋ เพิ่มสมาชิก</button>
    </div>
    <div class="mlist" id="mlist"></div>
  </div>

  <!-- SETTINGS -->
  <div class="page" id="page-settings">
    <div class="cfg"><div class="cfg-t">🔐 Google Account</div><div id="set-auth"></div></div>
    <div class="cfg">
      <div class="cfg-t">⚙️ OAuth Client ID</div>
      <div class="cfg-d">สร้างจาก Google Cloud Console → Credentials → OAuth 2.0 Client ID (Web App)<br>
        Authorized origins: <code id="curr-org" style="background:var(--g100);padding:2px 5px;border-radius:4px;font-size:11px;word-break:break-all"></code></div>
      <div class="fg"><div class="fl">Client ID</div>
        <input type="text" class="fi" id="cid-input" placeholder="xxx.apps.googleusercontent.com" autocorrect="off" autocapitalize="none"></div>
      <button class="btn btn-p" onclick="saveCID()" style="width:100%">💾 บันทึก Client ID</button>
    </div>
    <div class="cfg" style="border:2px solid var(--primary)">
      <div class="cfg-t" style="color:var(--primary)">📊 Google Sheets — แหล่งข้อมูลหลัก</div>
      <div class="cfg-d">✅ ข้อมูลเหมือนกันทุกเครื่อง (iPhone, iPad, PC)<br>
        วิธีหา ID: <code style="font-size:11px;background:var(--g100);padding:2px 4px;border-radius:3px">docs.google.com/spreadsheets/d/<b style="color:var(--primary)">[ID ตรงนี้]</b>/edit</code></div>
      <div class="fg"><div class="fl">Spreadsheet ID <span class="r">*</span></div>
        <input type="text" class="fi" id="sid" placeholder="1BxiMVs0XRA5..." autocorrect="off" autocapitalize="none"></div>
      <div class="frow">
        <div class="fg"><div class="fl">Sheet กรมธรรม์</div><input type="text" class="fi" id="sname" value="Policies" autocorrect="off"></div>
        <div class="fg"><div class="fl">Sheet สมาชิก</div><input type="text" class="fi" id="msname" value="Members" autocorrect="off"></div>
      </div>
      <div class="srow" id="sh-row"><div class="sd2 sd2-off" id="sh-dot"></div><span id="sh-txt">ยังไม่ได้เชื่อมต่อ</span></div>
      <div style="display:flex;gap:8px;flex-wrap:wrap">
        <button class="btn btn-p btn-sm" onclick="saveSCfg()">💾 บันทึก</button>
        <button class="btn btn-o btn-sm" onclick="pull()">📥 โหลดจาก Sheet</button>
        <button class="btn btn-g btn-sm" onclick="push()">📤 บันทึกขึ้น Sheet</button>
      </div>
      <div class="code" style="margin-top:12px">id | member_id | type | company | policy_no | plan_name | start_date | end_date | premium | sum_insured | coverage | drive_files | notes | updated_at</div>
    </div>
    <div class="cfg">
      <div class="cfg-t">📁 Google Drive</div>
      <div id="drive-area"></div>
      <div class="fg"><div class="fl">Root Folder ID (ปล่อยว่าง = สร้างอัตโนมัติ)</div>
        <input type="text" class="fi" id="dfid" placeholder="ปล่อยว่าง" autocorrect="off" autocapitalize="none"></div>
      <button class="btn btn-o btn-sm" onclick="initDrive()" style="width:100%">📁 สร้าง / เชื่อม Folder</button>
    </div>
    <div class="cfg" style="border-color:var(--danger-light)">
      <div class="cfg-t" style="color:var(--danger)">🗑️ จัดการข้อมูล</div>
      <div style="display:flex;gap:8px;flex-wrap:wrap;margin-top:8px">
        <button class="btn btn-g btn-sm" onclick="doExport()">📥 Export CSV</button>
        <button class="btn btn-d btn-sm" onclick="clearAll()">🗑️ ล้างข้อมูล</button>
      </div>
    </div>
  </div>
</div>

<!-- BOTTOM NAV -->
<nav class="bnav">
  <button class="bni active" data-p="dashboard" onclick="go('dashboard')"><span class="bni-icon">📊</span>หน้าหลัก</button>
  <button class="bni" data-p="policies" onclick="go('policies')"><span class="bni-icon">📋</span>กรมธรรม์<span class="bni-badge" id="nb-b" style="display:none">0</span></button>
  <button class="bni" onclick="openAdd()" style="color:var(--primary)">
    <span class="bni-icon" style="background:var(--primary);color:#fff;border-radius:50%;width:38px;height:38px;display:flex;align-items:center;justify-content:center;font-size:20px">＋</span>เพิ่ม
  </button>
  <button class="bni" data-p="members" onclick="go('members')"><span class="bni-icon">👨‍👩‍👧‍👦</span>สมาชิก</button>
  <button class="bni" data-p="settings" onclick="go('settings')"><span class="bni-icon">⚙️</span>ตั้งค่า</button>
</nav>

<!-- POLICY MODAL -->
<div class="mover" id="pm"><div class="modal">
  <div class="mhandle"></div>
  <div class="mhead"><div class="mtitle" id="pm-t">➕ เพิ่มกรมธรรม์</div><button class="mclose" onclick="closeMod('pm')">✕</button></div>
  <div class="mbody">
    <div class="fg"><div class="fl">ประเภทประกัน <span class="r">*</span></div>
      <div class="tsel">
        <div class="tc" onclick="selT('health')" data-t="health"><div class="tc-i">❤️‍🩹</div>สุขภาพ</div>
        <div class="tc" onclick="selT('accident')" data-t="accident"><div class="tc-i">⚡</div>อุบัติเหตุ</div>
        <div class="tc" onclick="selT('life')" data-t="life"><div class="tc-i">🌿</div>ชีวิต</div>
        <div class="tc" onclick="selT('ci')" data-t="ci"><div class="tc-i">🏥</div>CI</div>
        <div class="tc" onclick="selT('other')" data-t="other"><div class="tc-i">📌</div>อื่นๆ</div>
      </div>
      <input type="hidden" id="f-type">
    </div>
    <div class="fg"><div class="fl">สมาชิก <span class="r">*</span></div><select class="fi" id="f-mem"></select></div>
    <div class="frow">
      <div class="fg"><div class="fl">บริษัทประกัน <span class="r">*</span></div><input type="text" class="fi" id="f-co" placeholder="AIA, เมืองไทย..."></div>
      <div class="fg"><div class="fl">เลขกรมธรรม์</div><input type="text" class="fi" id="f-pno" placeholder="TH-2024-001" autocorrect="off"></div>
    </div>
    <div class="fg"><div class="fl">ชื่อแผน</div><input type="text" class="fi" id="f-plan" placeholder="Health Plus Gold"></div>
    <hr class="fdiv">
    <div class="fsec">📅 ระยะเวลาคุ้มครอง</div>
    <div class="frow">
      <div class="fg"><div class="fl">วันเริ่ม <span class="r">*</span></div><input type="date" class="fi" id="f-s"></div>
      <div class="fg"><div class="fl">วันหมด <span class="r">*</span></div><input type="date" class="fi" id="f-e"></div>
    </div>
    <hr class="fdiv">
    <div class="fsec">💰 การเงิน</div>
    <div class="frow">
      <div class="fg"><div class="fl">เบี้ย/ปี (฿)</div><input type="number" class="fi" id="f-pr" placeholder="0" inputmode="numeric"></div>
      <div class="fg"><div class="fl">ทุนประกัน (฿)</div><input type="number" class="fi" id="f-sum" placeholder="0" inputmode="numeric"></div>
    </div>
    <div class="frow">
      <div class="fg"><div class="fl">ผู้รับผลประโยชน์</div><input type="text" class="fi" id="f-ben" placeholder="ภรรยา, ลูก"></div>
      <div class="fg"><div class="fl">ความถี่ชำระ</div>
        <select class="fi" id="f-freq"><option value="yearly">รายปี</option><option value="halfyearly">ราย 6 เดือน</option><option value="quarterly">รายไตรมาส</option><option value="monthly">รายเดือน</option></select>
      </div>
    </div>
    <hr class="fdiv">
    <div class="fsec">🩺 ความคุ้มครอง</div>
    <div class="cgrid">
      <label class="citem"><input type="checkbox" value="ipd"> 🏥 IPD ผู้ป่วยใน</label>
      <label class="citem"><input type="checkbox" value="opd"> 🩺 OPD ผู้ป่วยนอก</label>
      <label class="citem"><input type="checkbox" value="dental"> 🦷 ทันตกรรม</label>
      <label class="citem"><input type="checkbox" value="vision"> 👁️ สายตา</label>
      <label class="citem"><input type="checkbox" value="maternity"> 🤰 คลอดบุตร</label>
      <label class="citem"><input type="checkbox" value="critical"> 🔴 โรคร้ายแรง</label>
      <label class="citem"><input type="checkbox" value="accident_med"> ⚡ อุบัติเหตุ</label>
      <label class="citem"><input type="checkbox" value="death"> 💐 เสียชีวิต</label>
      <label class="citem"><input type="checkbox" value="disability"> ♿ ทุพพลภาพ</label>
      <label class="citem"><input type="checkbox" value="saving"> 💰 สะสมทรัพย์</label>
      <label class="citem"><input type="checkbox" value="retirement"> 👴 บำนาญ</label>
      <label class="citem"><input type="checkbox" value="other_cov"> 📌 อื่นๆ</label>
    </div>
    <hr class="fdiv">
    <div class="fsec">📎 ไฟล์แนบ → Drive</div>
    <div id="up-warn" class="alert a-i" style="display:none">🔐 Login Google ก่อนอัพโหลดไฟล์</div>
    <div id="up-wrap">
      <div class="upzone" onclick="document.getElementById('fi').click()" ondragover="event.preventDefault()" ondrop="onDrop(event)">
        <input type="file" id="fi" multiple accept=".pdf,.jpg,.jpeg,.png" onchange="onPick(event)">
        <div style="font-size:28px">📎</div>
        <div style="font-size:13px;color:var(--g600)">แตะเพื่อเลือกไฟล์</div>
        <div style="font-size:11px;color:var(--g400)">PDF, JPG, PNG · สูงสุด 20MB</div>
      </div>
      <div class="flist" id="flist"></div>
    </div>
    <div class="fg" style="margin-top:14px"><div class="fl">หมายเหตุ</div><textarea class="fi" id="f-note" placeholder="เงื่อนไขพิเศษ..."></textarea></div>
  </div>
  <div class="mfoot">
    <button class="btn btn-g" onclick="closeMod('pm')">ยกเลิก</button>
    <button class="btn btn-p" id="save-btn" onclick="saveP()">💾 บันทึก</button>
  </div>
</div></div>

<!-- DETAIL MODAL -->
<div class="mover" id="dm"><div class="modal">
  <div class="mhandle"></div>
  <div class="mhead"><div class="mtitle">📋 รายละเอียด</div><button class="mclose" onclick="closeMod('dm')">✕</button></div>
  <div class="mbody" id="dm-body"></div>
  <div class="mfoot">
    <button class="btn btn-g" onclick="closeMod('dm')">ปิด</button>
    <button class="btn btn-o" id="dm-edit">✏️ แก้ไข</button>
    <button class="btn btn-d" id="dm-del">🗑️ ลบ</button>
  </div>
</div></div>

<!-- MEMBER MODAL -->
<div class="mover" id="mm"><div class="modal" style="max-width:440px">
  <div class="mhandle"></div>
  <div class="mhead"><div class="mtitle">👤 เพิ่มสมาชิก</div><button class="mclose" onclick="closeMod('mm')">✕</button></div>
  <div class="mbody">
    <div class="fg"><div class="fl">ชื่อ-นามสกุล <span class="r">*</span></div><input type="text" class="fi" id="m-nm" placeholder="สมชาย ใจดี"></div>
    <div class="frow">
      <div class="fg"><div class="fl">ความสัมพันธ์</div>
        <select class="fi" id="m-role"><option>ตัวเอง</option><option>คู่สมรส</option><option>ลูก</option><option>พ่อ</option><option>แม่</option><option>พ่อตา/แม่ยาย</option><option>อื่นๆ</option></select>
      </div>
      <div class="fg"><div class="fl">วันเกิด</div><input type="date" class="fi" id="m-dob"></div>
    </div>
    <div class="fg"><div class="fl">สีประจำตัว</div><input type="color" class="fi" id="m-col" value="#1a73e8" style="height:48px;cursor:pointer;padding:4px 8px"></div>
  </div>
  <div class="mfoot">
    <button class="btn btn-g" onclick="closeMod('mm')">ยกเลิก</button>
    <button class="btn btn-p" onclick="saveM()">💾 เพิ่มสมาชิก</button>
  </div>
</div></div>

<div class="twrap" id="twrap"></div>

<!-- Load Google libs AFTER page is shown -->
<script src="https://accounts.google.com/gsi/client" async></script>
<script src="https://apis.google.com/js/api.js" async onload="onGapi()"></script>

<script>
// ═══════════════════════
//  CONSTANTS
// ═══════════════════════
const TC={
  health:{l:'สุขภาพ',i:'❤️‍🩹',c:'#34a853',b:'#e6f4ea'},
  accident:{l:'อุบัติเหตุ',i:'⚡',c:'#c77a00',b:'#fef9e7'},
  life:{l:'ชีวิต',i:'🌿',c:'#9c27b0',b:'#f3e5f5'},
  ci:{l:'CI',i:'🏥',c:'#ff6d00',b:'#fff3e0'},
  other:{l:'อื่นๆ',i:'📌',c:'#1a73e8',b:'#e8f0fe'},
};
const CL={ipd:'IPD',opd:'OPD',dental:'ทันตกรรม',vision:'สายตา',maternity:'คลอดบุตร',
  critical:'โรคร้ายแรง',accident_med:'อุบัติเหตุ',death:'เสียชีวิต',
  disability:'ทุพพลภาพ',saving:'สะสมทรัพย์',retirement:'บำนาญ',other_cov:'อื่นๆ'};
const PAL=['#1a73e8','#e91e63','#ff9800','#9c27b0','#00acc1','#34a853','#795548'];
const SCOPE='https://www.googleapis.com/auth/spreadsheets https://www.googleapis.com/auth/drive.file profile email';

// ═══════════════════════
//  STATE
// ═══════════════════════
let P=[],M=[],editId=null,selType='',filt='all';
let files=[],syncTimer=null;
let tok=null,usr=null,gisOk=false;
let cfg={cid:'',sid:'',sn:'Policies',msn:'Members',si:15,dfid:''};

// ═══════════════════════
//  LOADING HELPERS
// ═══════════════════════
function ldSet(pct,msg){
  document.getElementById('ld-fill').style.width=pct+'%';
  document.getElementById('ld-sub').textContent=msg;
}
function ldHide(){
  const el=document.getElementById('loading');
  el.classList.add('done');
  setTimeout(()=>el.style.display='none',400);
}

// ═══════════════════════
//  BOOT — ไม่รอ Google APIs
// ═══════════════════════
function boot(){
  ldSet(20,'อ่านข้อมูลในเครื่อง...');
  loadCfg();
  loadLocal();

  // ตั้งค่า UI settings fields
  const co=document.getElementById('curr-org');
  if(co) co.textContent=location.origin;
  const ci=document.getElementById('cid-input');if(ci&&cfg.cid) ci.value=cfg.cid;
  const si=document.getElementById('sid');if(si&&cfg.sid) si.value=cfg.sid;
  const sn=document.getElementById('sname');if(sn) sn.value=cfg.sn;
  const mn=document.getElementById('msname');if(mn) mn.value=cfg.msn||'Members';
  const df=document.getElementById('dfid');if(df) df.value=cfg.dfid||'';

  ldSet(50,'เตรียม UI...');
  if(!M.length){ M=[{id:uid(),name:'ฉัน (ตัวเอง)',role:'ตัวเอง',color:'#1a73e8',dob:''}]; saveLocal(); }
  populateMSel();
  renderAll(); checkAlerts();

  ldSet(80,'ตรวจสอบ session...');

  // ลอง restore token แบบ non-blocking
  const saved=sessionStorage.getItem('gt');
  if(saved){
    tok=saved;
    verifyTok().then(ok=>{
      if(ok){ fetchUsr(); }
      else{ tok=null; sessionStorage.removeItem('gt'); updateAuthUI(); updateSyncBar(); }
    });
  }

  ldSet(100,'พร้อมใช้งาน!');
  // ซ่อน loading ทันที — ไม่รอ Google
  setTimeout(ldHide, 400);

  updateAuthUI();
  updateSyncBar();
}

// ═══════════════════════
//  LOCAL STORAGE
// ═══════════════════════
function loadLocal(){
  try{ P=JSON.parse(localStorage.getItem('ip')||'[]'); M=JSON.parse(localStorage.getItem('im')||'[]'); }catch(e){P=[];M=[];}
}
function saveLocal(){ localStorage.setItem('ip',JSON.stringify(P)); localStorage.setItem('im',JSON.stringify(M)); }
function loadCfg(){ try{ cfg=Object.assign({cid:'',sid:'',sn:'Policies',msn:'Members',si:15,dfid:''},JSON.parse(localStorage.getItem('ic')||'{}')); }catch(e){} }
function saveCfg(){ localStorage.setItem('ic',JSON.stringify(cfg)); }
function uid(){ return Date.now().toString(36)+Math.random().toString(36).substr(2,5); }

// ═══════════════════════
//  GOOGLE AUTH — safe for iOS
// ═══════════════════════
function onGapi(){
  try{ gapi.load('client',()=>{ try{gapi.client.init({});}catch(e){} }); }catch(e){}
}

// GIS init — try on load + poll fallback
function tryInitGIS(){
  if(!cfg.cid){ gisOk=true; return; }
  if(typeof google==='undefined'||!google.accounts){ setTimeout(tryInitGIS,500); return; }
  try{
    window._tc=google.accounts.oauth2.initTokenClient({
      client_id:cfg.cid, scope:SCOPE,
      callback:onTok,
      error_callback:(e)=>toast('Login ผิดพลาด: '+(e.type||e),'error'),
    });
    gisOk=true;
  }catch(e){ console.warn('GIS:',e); gisOk=true; }
}

function onTok(r){
  if(r.error){ toast('Login ไม่สำเร็จ: '+r.error,'error'); return; }
  tok=r.access_token;
  sessionStorage.setItem('gt',tok);
  fetchUsr().then(()=>{
    if(cfg.sid) pull(false);
    else toast('Login สำเร็จ! กรุณาตั้งค่า Sheet ID ใน ⚙️ ตั้งค่า','warn');
    setupAutoSync();
  });
}

async function verifyTok(){
  try{
    const r=await fetch('https://www.googleapis.com/oauth2/v3/tokeninfo?access_token='+tok);
    return r.ok;
  }catch(e){ return false; }
}

async function fetchUsr(){
  try{
    const r=await fetch('https://www.googleapis.com/oauth2/v3/userinfo',{headers:{Authorization:'Bearer '+tok}});
    if(!r.ok){ tok=null; sessionStorage.removeItem('gt'); updateAuthUI(); updateSyncBar(); return; }
    usr=await r.json();
    updateAuthUI(); updateSyncBar();
    if(cfg.dfid) renderDriveCard(null);
  }catch(e){ console.warn(e); }
}

function signIn(){
  if(!cfg.cid){ toast('กรุณาตั้งค่า Client ID ก่อน','warn'); go('settings'); return; }
  if(!gisOk||!window._tc){ tryInitGIS(); setTimeout(signIn,800); return; }
  try{ window._tc.requestAccessToken({prompt:tok?'':'consent'}); }
  catch(e){ toast('เปิด popup ไม่ได้ — Safari ต้องกดปุ่มโดยตรง','error'); }
}
function signOut(){
  if(tok&&typeof google!=='undefined') try{ google.accounts.oauth2.revoke(tok,()=>{}); }catch(e){}
  tok=null; usr=null; sessionStorage.removeItem('gt');
  if(syncTimer){ clearInterval(syncTimer); syncTimer=null; }
  updateAuthUI(); updateSyncBar(); toast('ออกจากระบบแล้ว','warn');
}

// ═══════════════════════
//  SYNC BAR
// ═══════════════════════
function updateSyncBar(){
  const dot=document.getElementById('sb-dot');
  const txt=document.getElementById('sb-txt');
  const btn=document.getElementById('sb-btn');
  if(!dot) return;
  dot.className='sbd';
  if(!tok){ dot.classList.add('sbd-off'); txt.textContent='ยังไม่ได้ Login Google'; btn.textContent='Login'; }
  else if(!cfg.sid){ dot.classList.add('sbd-off'); txt.textContent='Login แล้ว — ยังไม่ได้ตั้งค่า Sheet ID'; btn.textContent='ตั้งค่า'; }
  else{ dot.classList.add('sbd-ok'); txt.textContent=`✅ Sheet: ${cfg.sn} · ข้อมูลเดียวกันทุกเครื่อง`; btn.textContent='Sync'; }
}
function setSyncing(on,msg){
  const dot=document.getElementById('sb-dot');
  const txt=document.getElementById('sb-txt');
  if(!dot) return;
  dot.className='sbd '+(on?'sbd-busy':'sbd-ok');
  if(msg) txt.textContent=msg;
  else if(!on) txt.textContent=`✅ Sheet: ${cfg.sn}`;
}
function syncBarAct(){
  if(!tok) signIn();
  else if(!cfg.sid) go('settings');
  else pull();
}

// ═══════════════════════
//  SHEETS — fetch only
// ═══════════════════════
async function gsh(method,path,body=null){
  if(!tok) throw new Error('NOT_SIGNED_IN');
  const url=`https://sheets.googleapis.com/v4/spreadsheets/${cfg.sid}${path}`;
  const o={method,headers:{Authorization:'Bearer '+tok,'Content-Type':'application/json'}};
  if(body) o.body=JSON.stringify(body);
  const r=await fetch(url,o);
  if(r.status===401){ tok=null; sessionStorage.removeItem('gt'); usr=null; updateAuthUI(); updateSyncBar(); throw new Error('TOKEN_EXPIRED'); }
  if(!r.ok){ const e=await r.json().catch(()=>({})); throw new Error(e.error?.message||'Sheets error '+r.status); }
  return r.json();
}

async function pull(showToast=true){
  if(!tok){ if(showToast) toast('กรุณา Login ก่อน','warn'); return; }
  if(!cfg.sid){ if(showToast) toast('กรุณาตั้งค่า Sheet ID','warn'); return; }
  setSyncing(true,'กำลังโหลดจาก Sheet...');
  try{
    const pd=await gsh('GET',`/values/${enc(cfg.sn)}?majorDimension=ROWS`);
    if(pd.values&&pd.values.length>1){
      const [h,...rows]=pd.values;
      const x=k=>h.indexOf(k);
      P=rows.filter(r=>r[x('id')]||r[0]).map(r=>({
        id:r[x('id')]||uid(),
        member:r[x('member_id')]||r[x('member')]||'',
        type:r[x('type')]||'other',
        company:r[x('company')]||'',
        policy_no:r[x('policy_no')]||'',
        plan_name:r[x('plan_name')]||'',
        start_date:r[x('start_date')]||'',
        end_date:r[x('end_date')]||'',
        premium:r[x('premium')]||0,
        sum_insured:r[x('sum_insured')]||0,
        payment_freq:r[x('payment_freq')]||'yearly',
        beneficiary:r[x('beneficiary')]||'',
        coverage:(r[x('coverage')]||'').split(',').map(s=>s.trim()).filter(Boolean),
        driveFiles:(()=>{try{return JSON.parse(r[x('drive_files')]||'[]');}catch(e){return[];}})(),
        notes:r[x('notes')]||'',
        created_at:r[x('created_at')]||'',
        updated_at:r[x('updated_at')]||'',
      }));
    }
    try{
      const md=await gsh('GET',`/values/${enc(cfg.msn||'Members')}?majorDimension=ROWS`);
      if(md.values&&md.values.length>1){
        const [h,...rows]=md.values;
        const x=k=>h.indexOf(k);
        const loaded=rows.filter(r=>r[0]).map(r=>({id:r[x('id')]||uid(),name:r[x('name')]||'',role:r[x('role')]||'',dob:r[x('dob')]||'',color:r[x('color')]||'#1a73e8',driveFolderId:r[x('drive_folder_id')]||''}));
        if(loaded.length) M=loaded;
      }
    }catch(e){}
    if(!M.length) M=[{id:uid(),name:'ฉัน (ตัวเอง)',role:'ตัวเอง',color:'#1a73e8',dob:''}];
    saveLocal(); populateMSel(); renderAll(); checkAlerts();
    setSyncing(false);
    if(showToast) toast('โหลดข้อมูลจาก Sheet สำเร็จ ✅','success');
  }catch(e){
    setSyncing(false);
    if(e.message==='TOKEN_EXPIRED') toast('Session หมดอายุ — Login ใหม่','warn');
    else if(showToast) toast('โหลดไม่สำเร็จ: '+e.message,'error');
    else console.warn('pull:',e.message);
  }
}

async function push(showToast=true){
  if(!tok){ if(showToast) toast('กรุณา Login ก่อน','warn'); return; }
  if(!cfg.sid){ if(showToast) toast('กรุณาตั้งค่า Sheet ID','warn'); return; }
  setSyncing(true,'กำลังบันทึกขึ้น Sheet...');
  const PH=['id','member_id','member_name','type','company','policy_no','plan_name','start_date','end_date','premium','sum_insured','payment_freq','beneficiary','coverage','drive_files','notes','created_at','updated_at'];
  const pRows=[PH,...P.map(p=>[p.id,p.member,getMem(p.member).name,p.type,p.company||'',p.policy_no||'',p.plan_name||'',p.start_date||'',p.end_date||'',p.premium||0,p.sum_insured||0,p.payment_freq||'yearly',p.beneficiary||'',(p.coverage||[]).join(','),JSON.stringify(p.driveFiles||[]),p.notes||'',p.created_at||'',p.updated_at||new Date().toISOString()])];
  const MH=['id','name','role','dob','color','drive_folder_id'];
  const mRows=[MH,...M.map(m=>[m.id,m.name,m.role||'',m.dob||'',m.color||'#1a73e8',m.driveFolderId||''])];
  try{
    await gsh('POST',`/values/${enc(cfg.sn+'!A:Z')}:clear`);
    await gsh('PUT',`/values/${enc(cfg.sn+'!A1')}?valueInputOption=RAW`,{values:pRows});
    try{
      await gsh('POST',`/values/${enc((cfg.msn||'Members')+'!A:Z')}:clear`);
      await gsh('PUT',`/values/${enc((cfg.msn||'Members')+'!A1')}?valueInputOption=RAW`,{values:mRows});
    }catch(e){}
    setSyncing(false);
    if(showToast) toast('บันทึกขึ้น Sheet สำเร็จ ✅','success');
    else setSyncing(false);
  }catch(e){
    setSyncing(false);
    if(e.message==='TOKEN_EXPIRED') toast('Session หมดอายุ — Login ใหม่','warn');
    else if(showToast) toast('บันทึกไม่สำเร็จ: '+e.message,'error');
  }
}

function enc(s){ return encodeURIComponent(s); }
function setupAutoSync(){
  if(syncTimer) clearInterval(syncTimer);
  if(tok&&cfg.sid&&cfg.si>0) syncTimer=setInterval(()=>pull(false),cfg.si*60000);
}

// ═══════════════════════
//  DRIVE — fetch only
// ═══════════════════════
async function gdr(method,url,body=null,isForm=false){
  if(!tok) throw new Error('NOT_SIGNED_IN');
  const o={method,headers:{Authorization:'Bearer '+tok}};
  if(body&&!isForm){o.headers['Content-Type']='application/json';o.body=JSON.stringify(body);}
  if(body&&isForm) o.body=body;
  const r=await fetch(url,o);
  if(r.status===401){tok=null;sessionStorage.removeItem('gt');usr=null;updateAuthUI();throw new Error('TOKEN_EXPIRED');}
  if(!r.ok){const e=await r.json().catch(()=>({}));throw new Error(e.error?.message||'Drive error');}
  return r.json();
}
async function initDrive(){
  if(!tok){toast('กรุณา Login ก่อน','warn');return;}
  const inp=document.getElementById('dfid').value.trim();
  if(inp){
    try{ const d=await gdr('GET',`https://www.googleapis.com/drive/v3/files/${inp}?fields=id,name,webViewLink`);
      cfg.dfid=inp;saveCfg();toast(`เชื่อมต่อ "${d.name}" สำเร็จ ✅`,'success');renderDriveCard(d); }
    catch(e){toast('ไม่พบ Folder: '+e.message,'error');}
    return;
  }
  toast('กำลังสร้าง Folder...','warn');
  try{ const d=await gdr('POST','https://www.googleapis.com/drive/v3/files?fields=id,name,webViewLink',{name:'Family Insurance',mimeType:'application/vnd.google-apps.folder'});
    cfg.dfid=d.id;document.getElementById('dfid').value=d.id;saveCfg();renderDriveCard(d);toast('สร้าง Folder เรียบร้อย ✅','success'); }
  catch(e){toast('สร้างไม่สำเร็จ: '+e.message,'error');}
}
function renderDriveCard(f){
  const el=document.getElementById('drive-area');if(!el) return;
  const link=f?.webViewLink||`https://drive.google.com/drive/folders/${cfg.dfid}`;
  el.innerHTML=`<a href="${link}" target="_blank" class="drive-card"><span style="font-size:26px">📁</span><div><div style="font-weight:700">${f?.name||'Family Insurance'}</div><div style="font-size:12px;opacity:.8">แตะเพื่อเปิดใน Drive →</div></div></a>`;
}
async function getMemberFolder(mid){
  const m=getMem(mid);
  if(m.driveFolderId) return m.driveFolderId;
  const d=await gdr('POST','https://www.googleapis.com/drive/v3/files?fields=id',{name:m.name,mimeType:'application/vnd.google-apps.folder',parents:[cfg.dfid]});
  const i=M.findIndex(x=>x.id===mid);if(i!==-1) M[i].driveFolderId=d.id;
  return d.id;
}
async function upFile(f,pid,i){
  files[i].status='uploading';renderFList();
  const meta={name:f.name,parents:[pid]};
  const form=new FormData();
  form.append('metadata',new Blob([JSON.stringify(meta)],{type:'application/json'}));
  form.append('file',f);
  try{ const d=await gdr('POST','https://www.googleapis.com/upload/drive/v3/files?uploadType=multipart&fields=id,name,webViewLink',form,true);
    files[i].status='done';files[i].wvl=d.webViewLink;renderFList();return{id:d.id,name:d.name,webViewLink:d.webViewLink}; }
  catch(e){ files[i].status='error';renderFList();return null; }
}

// ═══════════════════════
//  AUTH UI
// ═══════════════════════
function updateAuthUI(){
  const isIn=!!usr;
  // Sidebar
  const sa=document.getElementById('sb-auth');
  if(sa) sa.innerHTML=isIn
    ?`<div style="display:flex;align-items:center;gap:8px;padding:10px 12px;border-radius:8px;background:var(--success-light);border:1px solid var(--success)">
        ${usr.picture?`<img src="${usr.picture}" style="width:24px;height:24px;border-radius:50%">`:'✅'}
        <div style="flex:1;overflow:hidden"><div style="font-size:12px;font-weight:600;overflow:hidden;text-overflow:ellipsis;white-space:nowrap">${usr.name}</div><div style="font-size:10px;color:var(--g500);overflow:hidden;text-overflow:ellipsis;white-space:nowrap">${usr.email}</div></div>
        <button onclick="signOut()" style="background:none;border:none;cursor:pointer;font-size:14px;color:var(--g500);padding:2px">✕</button>
      </div>`
    :`<button class="btn btn-p" onclick="signIn()" style="width:100%;font-size:12px;min-height:40px">🔐 Login Google</button>`;

  // Dashboard auth area
  const da=document.getElementById('dash-auth');
  if(da) da.innerHTML=isIn
    ?`<div class="auth-signed">
        ${usr.picture?`<img src="${usr.picture}" style="width:30px;height:30px;border-radius:50%">`:''}
        <div style="flex:1"><div style="font-size:13px;font-weight:600;color:var(--success)">${usr.name}</div><div style="font-size:11px;color:var(--g500)">${usr.email}</div></div>
        <button onclick="pull()" style="background:none;border:1.5px solid var(--success);color:var(--success);padding:6px 10px;border-radius:8px;cursor:pointer;font-size:11px;font-weight:600;font-family:inherit">🔄 Sync</button>
      </div>`
    :`<div class="auth-card">
        <h3>🔐 เชื่อมต่อ Google = ข้อมูลเดียวกันทุกเครื่อง</h3>
        <p>iPhone กับ PC จะเห็นข้อมูลเดียวกันทันที<br>หลัง Login และตั้งค่า Google Sheet</p>
        <button class="auth-card-btn" onclick="signIn()">🔐 เข้าสู่ระบบด้วย Google</button>
      </div>`;

  // Settings
  const sa2=document.getElementById('set-auth');
  if(sa2) sa2.innerHTML=isIn
    ?`<div style="display:flex;align-items:center;gap:10px;padding:4px 0 12px">
        ${usr.picture?`<img src="${usr.picture}" style="width:40px;height:40px;border-radius:50%">`:''}
        <div><div style="font-weight:700">${usr.name}</div><div style="font-size:12px;color:var(--g500)">${usr.email}</div></div>
        <button onclick="signOut()" class="btn btn-g btn-sm" style="margin-left:auto">ออก</button>
      </div>`
    :`<div style="padding:4px 0 12px">
        <div style="font-size:13px;color:var(--g600);margin-bottom:10px">ยังไม่ได้ Login — ข้อมูลจะเก็บแค่ในเครื่องนี้</div>
        <button class="btn btn-p" onclick="signIn()" style="width:100%">🔐 Login ด้วย Google</button>
      </div>`;

  // Sheet status
  const sd=document.getElementById('sh-dot');const st=document.getElementById('sh-txt');
  if(sd&&st){
    if(isIn&&cfg.sid){sd.className='sd2 sd2-on';st.textContent='เชื่อมต่อแล้ว: '+cfg.sn+' · ข้อมูลเดียวกันทุกเครื่อง';}
    else if(isIn){sd.className='sd2';sd.style.background='var(--warning)';st.textContent='Login แล้ว — กรุณาตั้งค่า Sheet ID';}
    else{sd.className='sd2 sd2-off';st.textContent='ยังไม่ได้ Login';}
  }
  // Upload
  const uw=document.getElementById('up-warn');const uwp=document.getElementById('up-wrap');
  if(uw&&uwp){uw.style.display=isIn?'none':'flex';uwp.style.display=isIn?'block':'none';}
}

// ═══════════════════════
//  NAVIGATION
// ═══════════════════════
function go(pg){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.getElementById('page-'+pg).classList.add('active');
  document.querySelectorAll('.sb-item,.bni[data-p]').forEach(n=>n.classList.remove('active'));
  document.querySelectorAll(`[data-p="${pg}"]`).forEach(n=>n.classList.add('active'));
  const T={dashboard:'📊 Dashboard',policies:'📋 กรมธรรม์',members:'👨‍👩‍👧‍👦 สมาชิก',settings:'⚙️ ตั้งค่า'};
  document.getElementById('pg-title').textContent=T[pg]||pg;
  if(pg==='policies') renderP();
  if(pg==='members')  renderM();
  if(pg==='dashboard'){renderDash();updateAuthUI();}
  if(pg==='settings') updateAuthUI();
  closeSB();
  window.scrollTo({top:0,behavior:'smooth'});
}
function openSB(){document.getElementById('sidebar').classList.add('open');document.getElementById('sb-ov').classList.add('on');}
function closeSB(){document.getElementById('sidebar').classList.remove('open');document.getElementById('sb-ov').classList.remove('on');}

// ═══════════════════════
//  UTILS
// ═══════════════════════
function dl(d){if(!d) return Infinity;const n=new Date();n.setHours(0,0,0,0);return Math.ceil((new Date(d)-n)/864e5);}
function thd(s){if(!s) return '-';const d=new Date(s);const Mn=['ม.ค.','ก.พ.','มี.ค.','เม.ย.','พ.ค.','มิ.ย.','ก.ค.','ส.ค.','ก.ย.','ต.ค.','พ.ย.','ธ.ค.'];return`${d.getDate()} ${Mn[d.getMonth()]} ${d.getFullYear()+543}`;}
function fm(n){return n?Number(n).toLocaleString('th-TH')+' ฿':'-';}
function pst(p){const d=dl(p.end_date);return d<0?'expired':d<=90?'expiring':'active';}
function getMem(id){return M.find(m=>m.id===id)||{name:id||'?',color:'#9aa0a6'};}
function ini(n){return(n||'?').split(' ').map(w=>w[0]).join('').substr(0,2).toUpperCase();}
function populateMSel(){
  const s=document.getElementById('f-mem');if(!s) return;
  const pv=s.value;s.innerHTML='<option value="">-- เลือกสมาชิก --</option>';
  M.forEach(m=>{const o=document.createElement('option');o.value=m.id;o.textContent=m.name+(m.role?` (${m.role})`:'');s.appendChild(o);});
  if(pv) s.value=pv;
}

// ═══════════════════════
//  RENDER
// ═══════════════════════
function renderAll(){renderDash();renderP();renderM();updBadge();}
function updBadge(){
  const n=P.filter(p=>{const d=dl(p.end_date);return d>=0&&d<=90;}).length;
  ['nb-s','nb-b'].forEach(id=>{const b=document.getElementById(id);if(!b)return;b.style.display=n?'inline':'none';b.textContent=n;});
}
function renderDash(){
  document.getElementById('s-tot').textContent=P.length;
  document.getElementById('s-act').textContent=P.filter(p=>pst(p)==='active').length;
  document.getElementById('s-exp').textContent=P.filter(p=>pst(p)==='expiring').length;
  const pr=P.reduce((a,p)=>a+Number(p.premium||0),0);
  document.getElementById('s-pr').textContent=pr?pr.toLocaleString('th-TH'):'-';
  renderDonut();renderBars();renderExpiry();
}
function renderDonut(){
  const svg=document.getElementById('dsvg');
  document.getElementById('d-num').textContent=P.length;
  svg.querySelectorAll('.ds').forEach(e=>e.remove());
  const lg=document.getElementById('d-leg');
  if(!P.length){lg.innerHTML='<span style="color:var(--g400);font-size:12px">ยังไม่มีข้อมูล</span>';return;}
  const cnt={};P.forEach(p=>{cnt[p.type]=(cnt[p.type]||0)+1;});
  const tot=P.length,r=42,ci=2*Math.PI*r;let off=0;
  Object.entries(cnt).forEach(([t,n])=>{
    const c=TC[t]||TC.other,pc=n/tot,d=pc*ci;
    const el=document.createElementNS('http://www.w3.org/2000/svg','circle');
    el.setAttribute('class','ds');el.setAttribute('cx',55);el.setAttribute('cy',55);el.setAttribute('r',r);
    el.setAttribute('fill','none');el.setAttribute('stroke',c.c);el.setAttribute('stroke-width',13);
    el.setAttribute('stroke-dasharray',`${d} ${ci-d}`);el.setAttribute('stroke-dashoffset',-(off*ci));
    svg.appendChild(el);off+=pc;
  });
  lg.innerHTML=Object.entries(cnt).map(([t,n])=>{const c=TC[t]||TC.other;return`<div class="dleg-item"><div class="dleg-dot" style="background:${c.c}"></div>${c.i} ${c.l} (${n})</div>`;}).join('');
}
function renderBars(){
  const el=document.getElementById('mbars');
  if(!M.length){el.innerHTML='<div style="text-align:center;padding:14px;color:var(--g400);font-size:12px">ยังไม่มีสมาชิก</div>';return;}
  el.innerHTML=M.map(m=>{
    const mp=P.filter(p=>p.member===m.id);
    const tc={};mp.forEach(p=>{tc[p.type]=(tc[p.type]||0)+1;});
    const segs=Object.entries(tc).map(([t,c])=>{const cfg2=TC[t]||TC.other;return`<div class="mbar-seg" style="width:${(c/Math.max(mp.length,1))*100}%;background:${cfg2.c}"></div>`;}).join('');
    return`<div class="mbar-row">
      <div style="display:flex;align-items:center;gap:5px;width:85px;flex-shrink:0">
        <div style="width:22px;height:22px;border-radius:50%;background:${m.color};display:flex;align-items:center;justify-content:center;font-size:9px;font-weight:700;color:#fff;flex-shrink:0">${ini(m.name)}</div>
        <span style="font-size:11px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap">${m.name.split(' ')[0]}</span>
      </div>
      <div class="mbar-track">${segs}</div>
      <div class="mbar-cnt">${mp.length}</div>
    </div>`;
  }).join('');
}
function renderExpiry(){
  const el=document.getElementById('exp-list');
  const ex=P.filter(p=>{const d=dl(p.end_date);return d>=0&&d<=90;}).sort((a,b)=>dl(a.end_date)-dl(b.end_date)).slice(0,8);
  if(!ex.length){el.innerHTML='<div style="text-align:center;padding:14px;color:var(--g400);font-size:12px">ไม่มีกรมธรรม์ที่ใกล้หมดอายุ 🎉</div>';return;}
  el.innerHTML=ex.map(p=>{
    const m=getMem(p.member),c=TC[p.type]||TC.other,d=dl(p.end_date);
    const cls=d<=30?'dc':d<=60?'dw':'dok';
    return`<div class="exp-item" onclick="showD('${p.id}')">
      <div class="exp-av" style="background:${m.color}">${ini(m.name)}</div>
      <div class="exp-info"><div class="exp-nm">${m.name} — ${p.company||'?'}</div><div class="exp-tp">${c.i} ${c.l}</div></div>
      <div class="exp-days ${cls}">${d}ว.<br><span style="font-size:9px;font-weight:400">${thd(p.end_date)}</span></div>
    </div>`;
  }).join('');
}
function checkAlerts(){
  const ar=document.getElementById('alert-area');if(!ar) return;
  const cr=P.filter(p=>{const d=dl(p.end_date);return d>=0&&d<=30;});
  const wa=P.filter(p=>{const d=dl(p.end_date);return d>30&&d<=60;});
  ar.innerHTML=(cr.length?`<div class="alert a-d">🚨 <div><b>ด่วน!</b> ${cr.length} กรมธรรม์หมดอายุใน 30 วัน</div></div>`:'')
    +(wa.length?`<div class="alert a-w">⚠️ ${wa.length} กรมธรรม์หมดอายุใน 31–60 วัน</div>`:'');
}

// ── POLICIES
function setF(el,f){filt=f;document.querySelectorAll('.fchip').forEach(c=>c.classList.remove('on'));el.classList.add('on');renderP();}
function setF2(t){filt=t;document.querySelectorAll('.fchip').forEach(c=>c.classList.toggle('on',c.dataset.f===t));renderP();}
function getFiltered(){
  const q=(document.getElementById('q')?.value||'').toLowerCase();
  return P.filter(p=>{
    const m=getMem(p.member);
    if(q&&![p.company,p.policy_no,p.plan_name,m.name].join(' ').toLowerCase().includes(q)) return false;
    if(filt==='all') return true;
    if(filt==='expiring') return pst(p)==='expiring';
    if(filt==='expired') return pst(p)==='expired';
    return p.type===filt;
  }).sort((a,b)=>new Date(a.end_date||0)-new Date(b.end_date||0));
}
function renderP(){
  const pl=document.getElementById('plist'),ep=document.getElementById('empty-p');
  const rows=getFiltered();
  if(!rows.length){pl.innerHTML='';ep.style.display='block';return;}
  ep.style.display='none';
  pl.innerHTML=rows.map(p=>{
    const m=getMem(p.member),c=TC[p.type]||TC.other,s=pst(p),d=dl(p.end_date);
    const sm={active:['s-act','คุ้มครองอยู่'],expiring:['s-exp','ใกล้หมดอายุ'],expired:['s-end','หมดอายุ']};
    const [dc,sl]=sm[s];
    const fr=(p.driveFiles||[]).length?`<div style="display:flex;gap:4px;flex-wrap:wrap;margin-top:6px">${(p.driveFiles||[]).map(f=>`<a class="fchip2" href="${f.webViewLink||'#'}" target="_blank">📎 ${f.name}</a>`).join('')}</div>`:'';
    return`<div class="pcard">
      <div class="pc-top">
        <div class="pc-av" style="background:${m.color}">${ini(m.name)}</div>
        <div class="pc-inf"><div class="pc-nm">${m.name}</div><div class="pc-co">${p.company||'-'}${p.plan_name?' · '+p.plan_name:''}</div></div>
        <span class="badge b-${p.type}">${c.i} ${c.l}</span>
      </div>
      <div class="pc-bot">
        <span class="sdot ${dc}"></span><span>${sl}</span>
        <span>หมด: ${thd(p.end_date)}${s==='expiring'?` <b style="color:var(--warning)">(${d}ว.)</b>`:''}</span>
        ${p.premium?`<span style="color:var(--primary);font-weight:600">${fm(p.premium)}/ปี</span>`:''}
      </div>${fr}
      <div class="pc-act">
        <button class="btn btn-g btn-sm" onclick="showD('${p.id}')" style="flex:1">👁️ ดู</button>
        <button class="btn btn-o btn-sm" onclick="editP('${p.id}')">✏️</button>
        <button class="btn btn-d btn-sm" onclick="delP('${p.id}')">🗑️</button>
      </div>
    </div>`;
  }).join('');
}

// ── POLICY CRUD
function openAdd(){
  editId=null;files=[];
  document.getElementById('pm-t').textContent='➕ เพิ่มกรมธรรม์';
  clearF();populateMSel();updUpload();openMod('pm');
}
function clearF(){
  selType='';document.querySelectorAll('.tc').forEach(c=>c.className='tc');
  ['f-type','f-co','f-pno','f-plan','f-s','f-e','f-pr','f-sum','f-ben','f-note'].forEach(id=>{const el=document.getElementById(id);if(el) el.value='';});
  document.getElementById('f-mem').value='';document.getElementById('f-freq').value='yearly';
  document.querySelectorAll('.cgrid input').forEach(cb=>cb.checked=false);
  files=[];renderFList();
}
function updUpload(){
  const w=document.getElementById('up-warn'),u=document.getElementById('up-wrap');
  if(w&&u){w.style.display=tok?'none':'flex';u.style.display=tok?'block':'none';}
}
function selT(t){
  selType=t;document.getElementById('f-type').value=t;
  document.querySelectorAll('.tc').forEach(c=>{c.className='tc';if(c.dataset.t===t) c.classList.add('tc-'+t);});
}
async function saveP(){
  const mem=document.getElementById('f-mem').value;
  const co=document.getElementById('f-co').value.trim();
  const s=document.getElementById('f-s').value;
  const e=document.getElementById('f-e').value;
  const ty=selType;
  if(!mem){toast('กรุณาเลือกสมาชิก','error');return;}
  if(!co){toast('กรุณากรอกบริษัท','error');return;}
  if(!ty){toast('กรุณาเลือกประเภทประกัน','error');return;}
  if(!s||!e){toast('กรุณากรอกวันคุ้มครอง','error');return;}
  if(new Date(e)<=new Date(s)){toast('วันหมดต้องหลังวันเริ่ม','error');return;}
  const btn=document.getElementById('save-btn');
  btn.disabled=true;btn.innerHTML='<div class="spin"></div> กำลังบันทึก...';
  let dfs=editId?(P.find(p=>p.id===editId)?.driveFiles||[]):[];
  if(tok&&files.length&&cfg.dfid){
    try{ const fid=await getMemberFolder(mem);
      for(let i=0;i<files.length;i++){if(files[i].status==='pending'){const r=await upFile(files[i].file,fid,i);if(r) dfs.push(r);}}
    }catch(e){toast('อัพโหลดบางไฟล์ไม่สำเร็จ','warn');}
  }
  const cov=[...document.querySelectorAll('.cgrid input:checked')].map(cb=>cb.value);
  const pol={id:editId||uid(),member:mem,type:ty,company:co,
    policy_no:document.getElementById('f-pno').value.trim(),
    plan_name:document.getElementById('f-plan').value.trim(),
    start_date:s,end_date:e,
    premium:document.getElementById('f-pr').value||0,
    sum_insured:document.getElementById('f-sum').value||0,
    payment_freq:document.getElementById('f-freq').value,
    beneficiary:document.getElementById('f-ben').value.trim(),
    coverage:cov,driveFiles:dfs,
    notes:document.getElementById('f-note').value.trim(),
    created_at:editId?(P.find(p=>p.id===editId)?.created_at||new Date().toISOString()):new Date().toISOString(),
    updated_at:new Date().toISOString()};
  if(editId){const i=P.findIndex(p=>p.id===editId);if(i!==-1) P[i]=pol;}
  else P.push(pol);
  saveLocal();closeMod('pm');renderAll();checkAlerts();
  btn.disabled=false;btn.innerHTML='💾 บันทึก';
  toast(editId?'อัพเดทเรียบร้อย ✅':'บันทึกเรียบร้อย ✅','success');
  if(tok&&cfg.sid) push(false);
}
function editP(id){
  const p=P.find(p=>p.id===id);if(!p) return;
  editId=id;files=[];
  document.getElementById('pm-t').textContent='✏️ แก้ไขกรมธรรม์';
  clearF();populateMSel();selT(p.type);
  document.getElementById('f-mem').value=p.member;
  document.getElementById('f-co').value=p.company||'';
  document.getElementById('f-pno').value=p.policy_no||'';
  document.getElementById('f-plan').value=p.plan_name||'';
  document.getElementById('f-s').value=p.start_date||'';
  document.getElementById('f-e').value=p.end_date||'';
  document.getElementById('f-pr').value=p.premium||'';
  document.getElementById('f-sum').value=p.sum_insured||'';
  document.getElementById('f-freq').value=p.payment_freq||'yearly';
  document.getElementById('f-ben').value=p.beneficiary||'';
  document.getElementById('f-note').value=p.notes||'';
  if(p.coverage) p.coverage.forEach(v=>{const cb=document.querySelector(`.cgrid input[value="${v}"]`);if(cb) cb.checked=true;});
  updUpload();closeMod('dm');openMod('pm');
}
function delP(id){
  if(!confirm('ต้องการลบกรมธรรม์นี้?')) return;
  P=P.filter(p=>p.id!==id);
  saveLocal();renderAll();checkAlerts();closeMod('dm');
  toast('ลบเรียบร้อย','warn');
  if(tok&&cfg.sid) push(false);
}
function showD(id){
  const p=P.find(p=>p.id===id);if(!p) return;
  const m=getMem(p.member),c=TC[p.type]||TC.other,s=pst(p),d=dl(p.end_date);
  const stxt={active:'✅ คุ้มครองอยู่',expiring:'⚠️ ใกล้หมดอายุ',expired:'❌ หมดอายุ'};
  const ftxt={yearly:'รายปี',halfyearly:'ราย 6 เดือน',quarterly:'รายไตรมาส',monthly:'รายเดือน'};
  const ct=(p.coverage||[]).map(cv=>`<div class="ctag">${CL[cv]||cv}</div>`).join('');
  const fh=(p.driveFiles||[]).map(f=>`<div style="display:flex;align-items:center;gap:8px;padding:8px 10px;background:var(--w);border:1px solid var(--g200);border-radius:8px;margin-bottom:6px">
    <span style="font-size:18px">${f.name?.endsWith('.pdf')?'📄':'🖼️'}</span>
    <div style="flex:1;min-width:0"><div style="font-size:12px;font-weight:600;overflow:hidden;text-overflow:ellipsis;white-space:nowrap">${f.name}</div><div style="font-size:11px;color:var(--g500)">Google Drive</div></div>
    <a href="${f.webViewLink||'#'}" target="_blank" class="btn btn-o btn-xs">เปิด</a>
  </div>`).join('');
  document.getElementById('dm-body').innerHTML=`
  <div class="dthero">
    <div class="dtav" style="background:${m.color}">${ini(m.name)}</div>
    <div><div style="font-size:15px;font-weight:700">${m.name}</div>
    <div style="margin-top:4px"><span class="badge b-${p.type}">${c.i} ${c.l}</span> <span style="font-size:12px;color:var(--g500)">${p.company||''}</span></div></div>
  </div>
  <div class="dtrows">
    <div class="dt2">
      <div class="dtrow"><div class="dtk">เลขกรมธรรม์</div><div class="dtv" style="font-family:monospace;font-size:12px">${p.policy_no||'-'}</div></div>
      <div class="dtrow"><div class="dtk">สถานะ</div><div class="dtv" style="font-size:12px">${stxt[s]}${s==='expiring'?` (${d}ว.)`:''}</div></div>
    </div>
    <div class="dt2">
      <div class="dtrow"><div class="dtk">วันเริ่ม</div><div class="dtv">${thd(p.start_date)}</div></div>
      <div class="dtrow"><div class="dtk">วันหมด</div><div class="dtv">${thd(p.end_date)}</div></div>
    </div>
    <div class="dt2">
      <div class="dtrow"><div class="dtk">เบี้ย/ปี</div><div class="dtv">${fm(p.premium)}</div></div>
      <div class="dtrow"><div class="dtk">ทุนประกัน</div><div class="dtv">${fm(p.sum_insured)}</div></div>
    </div>
    <div class="dt2">
      <div class="dtrow"><div class="dtk">ความถี่ชำระ</div><div class="dtv">${ftxt[p.payment_freq]||'-'}</div></div>
      <div class="dtrow"><div class="dtk">ผู้รับผลประโยชน์</div><div class="dtv">${p.beneficiary||'-'}</div></div>
    </div>
    ${ct?`<div style="padding:10px 12px;background:var(--g50);border-radius:8px"><div class="dtk" style="margin-bottom:6px">ความคุ้มครอง</div><div class="ctags">${ct}</div></div>`:''}
    ${fh?`<div><div class="dtk" style="margin-bottom:6px;padding:0 2px">📎 ไฟล์แนบ</div>${fh}</div>`:''}
    ${p.notes?`<div class="dtrow"><div class="dtk">หมายเหตุ</div><div class="dtv" style="font-size:12px;font-weight:400">${p.notes}</div></div>`:''}
  </div>`;
  document.getElementById('dm-edit').onclick=()=>editP(id);
  document.getElementById('dm-del').onclick=()=>delP(id);
  openMod('dm');
}

// ── MEMBERS
function openMemberMod(){
  document.getElementById('m-nm').value='';
  document.getElementById('m-role').value='ตัวเอง';
  document.getElementById('m-dob').value='';
  document.getElementById('m-col').value=PAL[M.length%PAL.length];
  openMod('mm');
}
function saveM(){
  const nm=document.getElementById('m-nm').value.trim();
  if(!nm){toast('กรุณากรอกชื่อ','error');return;}
  M.push({id:uid(),name:nm,role:document.getElementById('m-role').value,dob:document.getElementById('m-dob').value,color:document.getElementById('m-col').value});
  saveLocal();populateMSel();renderM();renderDash();
  closeMod('mm');toast(`เพิ่ม "${nm}" เรียบร้อย`,'success');
  if(tok&&cfg.sid) push(false);
}
function delMember(id){
  if(!confirm('ลบสมาชิกนี้?')) return;
  M=M.filter(m=>m.id!==id);
  saveLocal();populateMSel();renderM();renderDash();
  toast('ลบเรียบร้อย','warn');
  if(tok&&cfg.sid) push(false);
}
function renderM(){
  const el=document.getElementById('mlist');if(!el) return;
  if(!M.length){el.innerHTML='<div class="empty"><div class="empty-ico">👨‍👩‍👧‍👦</div><div class="empty-t">ยังไม่มีสมาชิก</div></div>';return;}
  el.innerHTML=M.map(m=>{
    const mp=P.filter(p=>p.member===m.id);
    const age=m.dob?Math.floor((Date.now()-new Date(m.dob))/315576e5):null;
    const tb=[...new Set(mp.map(p=>p.type))].map(t=>{const c=TC[t]||TC.other;return`<div class="mbadge" style="background:${c.b};color:${c.c}">${c.i} ${c.l}</div>`;}).join('');
    const drv=m.driveFolderId?`<a href="https://drive.google.com/drive/folders/${m.driveFolderId}" target="_blank" class="btn btn-g btn-xs">📁</a>`:'';
    return`<div class="mitem">
      <div class="mav" style="background:${m.color}">${ini(m.name)}</div>
      <div class="mi">
        <div class="mi-nm">${m.name}</div>
        <div class="mi-mt">${m.role||''}${age?' · '+age+' ปี':''} · ${mp.length} กรมธรรม์</div>
        <div class="mi-tags">${tb||'<span style="font-size:11px;color:var(--g400)">ยังไม่มีกรมธรรม์</span>'}</div>
      </div>
      <div style="display:flex;flex-direction:column;gap:5px">${drv}<button class="btn btn-d btn-xs" onclick="delMember('${m.id}')">🗑️</button></div>
    </div>`;
  }).join('');
}

// ── SETTINGS
function saveCID(){
  const id=document.getElementById('cid-input').value.trim();
  if(!id){toast('กรุณากรอก Client ID','error');return;}
  cfg.cid=id;saveCfg();toast('บันทึกแล้ว กำลัง Refresh...','success');
  setTimeout(()=>location.reload(),1500);
}
function saveSCfg(){
  cfg.sid=document.getElementById('sid').value.trim();
  cfg.sn=document.getElementById('sname').value.trim()||'Policies';
  cfg.msn=document.getElementById('msname').value.trim()||'Members';
  saveCfg();updateSyncBar();updateAuthUI();
  toast('บันทึกการตั้งค่า Sheet เรียบร้อย','success');
  if(tok&&cfg.sid) pull();
}
function doExport(){
  const H=['สมาชิก','ประเภท','บริษัท','เลขกรมธรรม์','ชื่อแผน','วันเริ่ม','วันหมด','เบี้ย','ทุน','ความคุ้มครอง','ผู้รับ','หมายเหตุ'];
  const rows=P.map(p=>[getMem(p.member).name,(TC[p.type]||TC.other).l,p.company,p.policy_no,p.plan_name,p.start_date,p.end_date,p.premium,p.sum_insured,(p.coverage||[]).map(c=>CL[c]||c).join('; '),p.beneficiary,p.notes]);
  const csv=[H,...rows].map(r=>r.map(c=>'"'+String(c||'').replace(/"/g,'""')+'"').join(',')).join('\n');
  const a=document.createElement('a');a.href=URL.createObjectURL(new Blob(['\uFEFF'+csv],{type:'text/csv;charset=utf-8;'}));
  a.download=`insurance_${new Date().toISOString().slice(0,10)}.csv`;a.click();toast('Export CSV เรียบร้อย','success');
}
function clearAll(){
  if(!confirm('ลบข้อมูลทั้งหมดในเครื่องนี้?'))return;
  P=[];M=[{id:uid(),name:'ฉัน (ตัวเอง)',role:'ตัวเอง',color:'#1a73e8',dob:''}];
  saveLocal();populateMSel();renderAll();toast('ล้างข้อมูลเรียบร้อย','warn');
}

// ── FILES
function onPick(e){addF([...e.target.files]);e.target.value='';}
function onDrop(e){e.preventDefault();addF([...e.dataTransfer.files]);}
function addF(fs){fs.forEach(f=>{if(f.size>20*1024*1024){toast(`"${f.name}" ใหญ่เกิน 20MB`,'error');return;}if(!files.find(x=>x.file.name===f.name&&x.file.size===f.size)) files.push({file:f,status:'pending'});});renderFList();}
function removeF(i){files.splice(i,1);renderFList();}
function renderFList(){
  const el=document.getElementById('flist');if(!el) return;
  el.innerHTML=files.map((pf,i)=>{
    const ic=pf.file.name.endsWith('.pdf')?'📄':'🖼️';
    const sz=(pf.file.size/1024).toFixed(0)+' KB';
    const st=pf.status==='done'?'✅':pf.status==='uploading'?'⏳':pf.status==='error'?'❌':'📌';
    return`<div class="fitem"><span style="font-size:16px">${ic}</span><div class="fitem-nm">${pf.file.name}</div><span style="font-size:11px;color:var(--g500);flex-shrink:0">${sz}</span><span>${st}</span>${pf.status==='pending'?`<button onclick="removeF(${i})" style="background:none;border:none;cursor:pointer;color:var(--g400);font-size:16px;padding:2px">✕</button>`:''}</div>`;
  }).join('');
}

// ── MODAL
function openMod(id){document.getElementById(id).classList.add('on');}
function closeMod(id){document.getElementById(id).classList.remove('on');}
document.querySelectorAll('.mover').forEach(o=>o.addEventListener('click',e=>{if(e.target===o) o.classList.remove('on');}));
document.querySelectorAll('.modal').forEach(modal=>{
  let sy=0;
  modal.addEventListener('touchstart',e=>{sy=e.touches[0].clientY;},{passive:true});
  modal.addEventListener('touchend',e=>{if(e.changedTouches[0].clientY-sy>80&&modal.scrollTop===0) modal.closest('.mover').classList.remove('on');},{passive:true});
});

// ── TOAST
function toast(msg,type=''){
  const c=document.getElementById('twrap');
  const t=document.createElement('div');
  t.className='toast'+(type?' t-'+({success:'ok',error:'err',warn:'wn'}[type]||type):'');
  t.innerHTML=(type==='success'?'✅ ':type==='error'?'❌ ':type==='warn'?'⚠️ ':'ℹ️ ')+msg;
  c.appendChild(t);
  setTimeout(()=>{t.style.cssText='opacity:0;transform:translateY(6px);transition:all .3s';setTimeout(()=>t.remove(),300);},3200);
}

// ═══════════════════════
//  START — boot ทันที ไม่รอ Google
// ═══════════════════════
document.addEventListener('DOMContentLoaded', ()=>{
  boot();          // แสดง App ทันที
  tryInitGIS();    // init GIS แบบ non-blocking
});
</script>
</body>
</html>
