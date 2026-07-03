
<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="theme-color" content="#1a73e8">
<title>Family Insurance</title>
<style>
:root{
  --pri:#1a73e8;--pri-dk:#1557b0;--pri-lt:#e8f0fe;
  --ok:#34a853;--ok-lt:#e6f4ea;
  --warn:#fbbc04;--warn-lt:#fef9e7;
  --err:#ea4335;--err-lt:#fce8e6;
  --pur:#9c27b0;--pur-lt:#f3e5f5;
  --org:#ff6d00;--org-lt:#fff3e0;
  --g50:#f8f9fa;--g100:#f1f3f4;--g200:#e8eaed;--g300:#dadce0;
  --g400:#bdc1c6;--g500:#9aa0a6;--g600:#80868b;--g700:#5f6368;
  --g800:#3c4043;--g900:#202124;--w:#fff;
  --sh0:0 1px 3px rgba(0,0,0,.08);--sh1:0 4px 12px rgba(0,0,0,.08);--sh2:0 8px 24px rgba(0,0,0,.1);
  --r:12px;--rs:8px;--rl:16px;
}
*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html,body{height:100%;overflow-x:hidden}
body{font-family:-apple-system,BlinkMacSystemFont,'Segoe UI','Noto Sans Thai',sans-serif;
  background:var(--g50);color:var(--g900);font-size:14px;line-height:1.5;-webkit-font-smoothing:antialiased}

/* ── LOADING ── */
#ld{position:fixed;inset:0;background:#fff;z-index:9999;
  display:flex;flex-direction:column;align-items:center;justify-content:center;gap:14px;transition:opacity .35s}
#ld.gone{opacity:0;pointer-events:none}
.ld-logo{font-size:52px;animation:bob .9s ease-in-out infinite alternate}
@keyframes bob{to{transform:translateY(-8px)}}
.ld-bar{width:180px;height:4px;background:var(--g200);border-radius:2px;overflow:hidden}
.ld-fill{height:100%;background:var(--pri);border-radius:2px;transition:width .25s;width:0}

/* ── SIDEBAR ── */
.sidebar{position:fixed;left:0;top:0;bottom:0;width:260px;background:var(--w);
  border-right:1px solid var(--g200);display:flex;flex-direction:column;
  z-index:300;box-shadow:var(--sh1);transition:transform .28s cubic-bezier(.4,0,.2,1)}
.sb-brand{display:flex;align-items:center;gap:10px;
  padding:calc(env(safe-area-inset-top)+14px) 18px 14px;border-bottom:1px solid var(--g100)}
.sb-icon{width:36px;height:36px;border-radius:10px;flex-shrink:0;
  background:linear-gradient(135deg,var(--pri),#4285f4);display:flex;align-items:center;justify-content:center;font-size:18px}
.sb-name{font-size:14px;font-weight:700}.sb-sub{font-size:11px;color:var(--g500)}
.sb-nav{flex:1;padding:10px 0;overflow-y:auto}
.sb-lbl{font-size:10px;font-weight:700;color:var(--g400);text-transform:uppercase;letter-spacing:.8px;padding:6px 18px 5px;margin-top:4px}
.sb-row{display:flex;align-items:center;gap:9px;padding:10px 18px;cursor:pointer;
  border-radius:0 22px 22px 0;margin:1px 8px 1px 0;color:var(--g700);font-size:13px;font-weight:500;transition:background .15s}
.sb-row:active,.sb-row:hover{background:var(--g100)}
.sb-row.on{background:var(--pri-lt);color:var(--pri)}
.sb-ic{font-size:16px;width:20px;text-align:center;flex-shrink:0}
.sb-badge{margin-left:auto;background:var(--err);color:#fff;border-radius:10px;font-size:11px;font-weight:600;padding:1px 6px}
.sb-foot{padding:10px;border-top:1px solid var(--g100)}
.sb-ov{display:none;position:fixed;inset:0;background:rgba(0,0,0,.45);z-index:299;backdrop-filter:blur(2px)}
.sb-ov.on{display:block}

/* ── MAIN ── */
.main{min-height:100vh;display:flex;flex-direction:column}
.topbar{background:var(--w);border-bottom:1px solid var(--g200);
  padding:0 14px;padding-top:env(safe-area-inset-top);
  height:calc(52px + env(safe-area-inset-top));
  display:flex;align-items:flex-end;padding-bottom:8px;gap:8px;
  position:sticky;top:0;z-index:50;box-shadow:var(--sh0)}
.tb-menu{width:40px;height:36px;border:none;background:transparent;cursor:pointer;font-size:22px;
  display:flex;align-items:center;justify-content:center;border-radius:8px;flex-shrink:0}
.tb-title{font-size:16px;font-weight:700;flex:1}
.tb-act{display:flex;gap:6px;align-items:center}

/* ── SYNC STATUS BAR ── */
.sync-bar{display:flex;align-items:center;gap:8px;padding:7px 14px;font-size:12px;
  border-bottom:1px solid var(--g200);background:var(--w);flex-shrink:0;min-height:36px}
.sd{width:8px;height:8px;border-radius:50%;flex-shrink:0}
.sd-ok{background:var(--ok)}.sd-busy{background:var(--warn);animation:pulse 1s infinite}
.sd-off{background:var(--g400)}.sd-err{background:var(--err)}
@keyframes pulse{0%,100%{opacity:1}50%{opacity:.2}}
.sb-txt{flex:1;color:var(--g600)}.sb-act-btn{background:none;border:none;color:var(--pri);
  font-size:12px;font-weight:600;cursor:pointer;padding:4px 8px;border-radius:6px;font-family:inherit}

/* ── PAGES ── */
.page{display:none;padding:14px 14px calc(86px + env(safe-area-inset-bottom)) 14px}
.page.active{display:block}

/* ── BUTTONS ── */
.btn{display:inline-flex;align-items:center;justify-content:center;gap:6px;
  padding:10px 18px;border-radius:10px;border:none;font-size:13px;font-weight:600;
  cursor:pointer;white-space:nowrap;min-height:44px;font-family:inherit;-webkit-appearance:none;transition:opacity .15s}
.btn:active{opacity:.78}
.bp{background:var(--pri);color:#fff}.bp:disabled{background:var(--g300);cursor:not-allowed}
.bo{background:transparent;color:var(--pri);border:1.5px solid var(--pri)}
.bg{background:transparent;color:var(--g700);border:1.5px solid var(--g200)}
.bd{background:var(--err);color:#fff}
.bs{padding:8px 14px;font-size:12px;min-height:38px;border-radius:8px}
.bx{padding:5px 10px;font-size:11px;min-height:30px;border-radius:6px}

/* ── STATS ── */
.sg{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:14px}
.sc{background:var(--w);border-radius:var(--r);padding:14px;box-shadow:var(--sh0);border:1px solid var(--g100);display:flex;align-items:center;gap:10px}
.si{width:38px;height:38px;border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:18px;flex-shrink:0}
.sv{font-size:22px;font-weight:700;line-height:1}.sl{font-size:11px;color:var(--g500);margin-top:2px}

/* ── CHART CARD ── */
.cc{background:var(--w);border-radius:var(--r);padding:16px;box-shadow:var(--sh0);border:1px solid var(--g100);margin-bottom:12px}
.cc-t{font-size:14px;font-weight:600;margin-bottom:12px;display:flex;align-items:center;justify-content:space-between}

/* ── MEMBER INSURANCE SECTION (Dashboard) ── */
.mem-section{background:var(--w);border-radius:var(--r);box-shadow:var(--sh0);border:1px solid var(--g100);margin-bottom:12px;overflow:hidden}
.mem-header{display:flex;align-items:center;gap:10px;padding:14px 16px;cursor:pointer;
  border-bottom:1px solid var(--g100);background:var(--g50);transition:background .15s}
.mem-header:active{background:var(--g100)}
.mem-av{width:38px;height:38px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:15px;font-weight:700;color:#fff;flex-shrink:0}
.mem-hinfo{flex:1;min-width:0}
.mem-hname{font-size:14px;font-weight:700}
.mem-hrole{font-size:11px;color:var(--g500)}
.mem-hcount{font-size:12px;font-weight:600;color:var(--pri);background:var(--pri-lt);padding:3px 10px;border-radius:100px}
.mem-hchev{font-size:12px;color:var(--g400);transition:transform .2s;flex-shrink:0}
.mem-header.open .mem-hchev{transform:rotate(180deg)}
.mem-body{display:none;padding:12px 12px 8px}
.mem-body.open{display:block}
.ins-row{display:flex;align-items:center;gap:10px;padding:10px 12px;border-radius:var(--rs);
  border:1px solid var(--g100);margin-bottom:8px;cursor:pointer;background:var(--g50);transition:background .15s}
.ins-row:active{background:var(--g100)}
.ins-row:last-child{margin-bottom:0}
.ins-type-icon{width:34px;height:34px;border-radius:8px;display:flex;align-items:center;justify-content:center;font-size:16px;flex-shrink:0}
.ins-info{flex:1;min-width:0}
.ins-company{font-size:13px;font-weight:600;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.ins-plan{font-size:11px;color:var(--g500);white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.ins-right{text-align:right;flex-shrink:0}
.ins-exp{font-size:11px;font-weight:600;padding:3px 8px;border-radius:6px}
.ic{background:var(--err-lt);color:var(--err)}
.iw{background:var(--warn-lt);color:#b06000}
.iok{background:var(--ok-lt);color:var(--ok)}
.iend{background:var(--g100);color:var(--g600)}
.ins-prem{font-size:11px;color:var(--g500);margin-top:2px}
.mem-add-btn{display:flex;align-items:center;gap:6px;padding:8px 12px;border-radius:var(--rs);
  border:1.5px dashed var(--g300);color:var(--g500);font-size:12px;cursor:pointer;
  width:100%;justify-content:center;background:transparent;font-family:inherit;margin-top:4px;min-height:40px}
.mem-add-btn:active{background:var(--g100)}

/* ── DONUT ── */
.donut-wrap{position:relative;width:100px;height:100px;flex-shrink:0}
.dc{position:absolute;inset:0;display:flex;flex-direction:column;align-items:center;justify-content:center}
.dn{font-size:20px;font-weight:700;line-height:1}.dl{font-size:9px;color:var(--g500)}
svg.donut{transform:rotate(-90deg)}
.drow{display:flex;align-items:center;gap:12px}
.dleg{display:flex;flex-direction:column;gap:5px;flex:1}
.dli{display:flex;align-items:center;gap:5px;font-size:11px;color:var(--g700)}
.dld{width:8px;height:8px;border-radius:50%;flex-shrink:0}

/* ── EXPIRY LIST ── */
.exp-list{display:flex;flex-direction:column;gap:8px}
.exp-row{display:flex;align-items:center;gap:10px;padding:10px 12px;
  border-radius:var(--rs);background:var(--g50);border:1px solid var(--g100);cursor:pointer}
.exp-av2{width:30px;height:30px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:700;color:#fff;flex-shrink:0}
.exp-inf{flex:1;min-width:0}
.exp-nm{font-size:12px;font-weight:600;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.exp-tp{font-size:10px;color:var(--g500)}
.exp-d{font-size:11px;font-weight:700;padding:3px 7px;border-radius:6px;text-align:center;flex-shrink:0}

/* ── POLICY LIST ── */
.plist{display:flex;flex-direction:column;gap:10px}
.pcard{background:var(--w);border-radius:var(--r);padding:14px;box-shadow:var(--sh0);border:1px solid var(--g100)}
.pcard:active{opacity:.85}
.pc-top{display:flex;align-items:flex-start;gap:10px;margin-bottom:8px}
.pc-av{width:34px;height:34px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:13px;font-weight:700;color:#fff;flex-shrink:0}
.pc-inf{flex:1;min-width:0}
.pc-nm{font-size:13px;font-weight:700}
.pc-co{font-size:12px;color:var(--g500);overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.pc-bot{display:flex;align-items:center;gap:8px;flex-wrap:wrap;font-size:11px;color:var(--g600)}
.pc-act{display:flex;gap:6px;margin-top:10px;padding-top:10px;border-top:1px solid var(--g100)}

/* ── FILTER ── */
.fscroll{display:flex;gap:8px;overflow-x:auto;padding-bottom:4px;margin-bottom:12px;-webkit-overflow-scrolling:touch;scrollbar-width:none}
.fscroll::-webkit-scrollbar{display:none}
.fc{display:inline-flex;align-items:center;gap:4px;padding:7px 14px;border-radius:100px;
  border:1.5px solid var(--g200);background:var(--w);font-size:12px;font-weight:500;
  color:var(--g700);cursor:pointer;white-space:nowrap;flex-shrink:0;min-height:36px}
.fc.on{background:var(--pri-lt);border-color:var(--pri);color:var(--pri)}
.srch{display:flex;align-items:center;gap:8px;background:var(--w);
  border:1.5px solid var(--g200);border-radius:10px;padding:10px 14px;margin-bottom:12px}
.srch:focus-within{border-color:var(--pri)}
.srch input{border:none;outline:none;font-size:16px;background:transparent;width:100%;color:var(--g900);font-family:inherit}

/* ── BADGES ── */
.badge{display:inline-flex;align-items:center;gap:3px;padding:3px 8px;border-radius:100px;font-size:11px;font-weight:600}
.bh{background:var(--ok-lt);color:var(--ok)}.ba{background:var(--warn-lt);color:#c77a00}
.bl{background:var(--pur-lt);color:var(--pur)}.bc{background:var(--org-lt);color:var(--org)}.bo2{background:var(--g100);color:var(--g700)}
.sdot{width:7px;height:7px;border-radius:50%;display:inline-block;margin-right:3px}
.sa{background:var(--ok)}.se{background:var(--warn)}.sx{background:var(--err)}

/* ── FILE CHIP ── */
.fchip{display:inline-flex;align-items:center;gap:4px;padding:3px 8px;background:var(--pri-lt);color:var(--pri);border-radius:6px;font-size:11px;font-weight:500;text-decoration:none}

/* ── UPLOAD ── */
.upzone{border:2px dashed var(--g300);border-radius:var(--rs);padding:20px;text-align:center;cursor:pointer;background:var(--g50);display:flex;flex-direction:column;align-items:center;gap:6px}
.upzone input{display:none}
.flist2{display:flex;flex-direction:column;gap:6px;margin-top:8px}
.fitem{display:flex;align-items:center;gap:8px;padding:8px 10px;background:var(--w);border:1px solid var(--g200);border-radius:var(--rs)}
.fitem-nm{flex:1;font-size:12px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}

/* ── MODAL ── */
.mover{display:none;position:fixed;inset:0;background:rgba(0,0,0,.5);z-index:500;align-items:flex-end;justify-content:center;backdrop-filter:blur(3px)}
.mover.on{display:flex;animation:mfi .15s}
@keyframes mfi{from{opacity:0}}
.modal{background:var(--w);border-radius:20px 20px 0 0;width:100%;max-height:93vh;overflow-y:auto;animation:msu .25s cubic-bezier(.4,0,.2,1);padding-bottom:env(safe-area-inset-bottom);-webkit-overflow-scrolling:touch}
@keyframes msu{from{transform:translateY(100%)}}
.mhandle{width:36px;height:4px;background:var(--g300);border-radius:2px;margin:10px auto 0}
.mhead{display:flex;align-items:center;justify-content:space-between;padding:14px 18px 12px;border-bottom:1px solid var(--g100);position:sticky;top:0;background:var(--w);z-index:1}
.mtitle{font-size:16px;font-weight:700}
.mclose{width:34px;height:34px;border-radius:50%;border:none;background:var(--g100);cursor:pointer;font-size:16px;display:flex;align-items:center;justify-content:center;color:var(--g600)}
.mbody{padding:16px 18px}
.mfoot{display:flex;gap:8px;padding:12px 18px;padding-bottom:calc(12px + env(safe-area-inset-bottom));border-top:1px solid var(--g100);position:sticky;bottom:0;background:var(--w)}
.mfoot .btn{flex:1}

/* ── FORM ── */
.fg{display:flex;flex-direction:column;gap:6px;margin-bottom:14px}
.fl{font-size:12px;font-weight:600;color:var(--g700)}
.fl .r{color:var(--err);margin-left:2px}
.fi{background:var(--w);border:1.5px solid var(--g200);border-radius:var(--rs);padding:12px 14px;font-size:16px;color:var(--g900);outline:none;width:100%;font-family:inherit;-webkit-appearance:none;transition:border-color .2s}
.fi:focus{border-color:var(--pri)}
textarea.fi{resize:vertical;min-height:72px}
select.fi{background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='8' viewBox='0 0 12 8'%3E%3Cpath d='M1 1l5 5 5-5' stroke='%239aa0a6' stroke-width='1.5' fill='none' stroke-linecap='round'/%3E%3C/svg%3E");background-repeat:no-repeat;background-position:right 14px center;padding-right:36px}
.frow{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.fdiv{border:none;border-top:1px solid var(--g100);margin:4px 0 14px}
.fsec{font-size:11px;font-weight:700;color:var(--g500);text-transform:uppercase;letter-spacing:.5px;margin-bottom:10px}
.tsel{display:grid;grid-template-columns:repeat(5,1fr);gap:6px}
.tc2{display:flex;flex-direction:column;align-items:center;gap:3px;padding:10px 4px;border-radius:10px;cursor:pointer;border:1.5px solid var(--g200);background:var(--w);font-size:10px;font-weight:600;color:var(--g600);min-height:58px;justify-content:center}
.tc2-i{font-size:20px}
.t-health{border-color:var(--ok);background:var(--ok-lt);color:var(--ok)}
.t-accident{border-color:var(--warn);background:var(--warn-lt);color:#c77a00}
.t-life{border-color:var(--pur);background:var(--pur-lt);color:var(--pur)}
.t-ci{border-color:var(--org);background:var(--org-lt);color:var(--org)}
.t-other{border-color:var(--pri);background:var(--pri-lt);color:var(--pri)}
.cgrid{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.citem{display:flex;align-items:center;gap:8px;padding:8px 10px;border:1.5px solid var(--g200);border-radius:8px;cursor:pointer;font-size:12px;color:var(--g700)}
.citem input{width:16px;height:16px;accent-color:var(--pri);flex-shrink:0;cursor:pointer}
.citem:has(input:checked){border-color:var(--pri);background:var(--pri-lt);color:var(--pri)}

/* ── DETAIL MODAL ── */
.dthero{background:var(--g50);border-radius:var(--rs);padding:14px;margin-bottom:14px;display:flex;align-items:center;gap:12px}
.dtav{width:46px;height:46px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:19px;font-weight:700;color:#fff;flex-shrink:0}
.dtrows{display:flex;flex-direction:column;gap:8px}
.dt2{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.dtrow{padding:10px 12px;background:var(--g50);border-radius:8px}
.dtk{font-size:10px;font-weight:600;color:var(--g500);text-transform:uppercase;margin-bottom:3px}
.dtv{font-size:13px;font-weight:600;color:var(--g900)}
.ctags{display:flex;flex-wrap:wrap;gap:5px;margin-top:6px}
.ctag{background:var(--pri-lt);color:var(--pri);font-size:11px;padding:3px 7px;border-radius:5px;font-weight:500}

/* ── MEMBER PAGE ── */
.mlist{display:flex;flex-direction:column;gap:10px}
.mitem{background:var(--w);border-radius:var(--r);padding:14px;box-shadow:var(--sh0);border:1px solid var(--g100);display:flex;align-items:center;gap:12px}
.mav2{width:44px;height:44px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:17px;font-weight:700;color:#fff;flex-shrink:0}
.mi{flex:1;min-width:0}
.mi-nm{font-size:14px;font-weight:700}
.mi-mt{font-size:11px;color:var(--g500);margin-top:2px}
.mi-tags{display:flex;gap:4px;flex-wrap:wrap;margin-top:6px}
.mb{padding:2px 6px;border-radius:4px;font-size:10px;font-weight:600}

/* ── AUTH CARD ── */
.auth-card{background:linear-gradient(135deg,#1a73e8,#4285f4);border-radius:var(--r);padding:16px;margin-bottom:14px;color:#fff}
.auth-card h3{font-size:14px;font-weight:700;margin-bottom:4px}
.auth-card p{font-size:12px;opacity:.88;margin-bottom:12px;line-height:1.6}
.auth-card-btn{background:#fff;color:var(--pri);border:none;padding:10px 20px;border-radius:8px;font-size:13px;font-weight:700;cursor:pointer;display:inline-flex;align-items:center;gap:6px;min-height:44px;font-family:inherit}
.auth-signed{background:var(--ok-lt);border:1px solid var(--ok);border-radius:var(--r);padding:10px 14px;margin-bottom:14px;display:flex;align-items:center;gap:10px}

/* ── SETTINGS ── */
.cfg{background:var(--w);border-radius:var(--r);padding:16px;box-shadow:var(--sh0);border:1px solid var(--g100);margin-bottom:12px}
.cfg-t{font-size:14px;font-weight:700;margin-bottom:4px}
.cfg-d{font-size:12px;color:var(--g500);margin-bottom:14px;line-height:1.6}
.srow2{display:flex;align-items:center;gap:8px;padding:10px 12px;background:var(--g50);border-radius:8px;border:1px solid var(--g200);font-size:13px;margin-bottom:10px}
.sd2{width:8px;height:8px;border-radius:50%;flex-shrink:0}
.sd2-ok{background:var(--ok);animation:pulse 2s infinite}
.sd2-off{background:var(--g400)}
.code{background:var(--g900);color:#a8d8a8;padding:10px 12px;border-radius:var(--rs);font-size:11px;font-family:'Menlo',monospace;overflow-x:auto;line-height:1.7;margin:8px 0;word-break:break-all}
.steps{list-style:none;counter-reset:s}
.steps li{counter-increment:s;padding:8px 0 8px 32px;position:relative;font-size:13px;color:var(--g700);border-bottom:1px solid var(--g100)}
.steps li:last-child{border-bottom:none}
.steps li::before{content:counter(s);position:absolute;left:0;top:8px;width:22px;height:22px;background:var(--pri);color:#fff;border-radius:50%;font-size:11px;font-weight:700;display:flex;align-items:center;justify-content:center}
.drive-card{background:linear-gradient(135deg,#1a73e8,#4285f4);color:#fff;border-radius:var(--r);padding:14px 16px;display:flex;align-items:center;gap:12px;margin-bottom:12px;text-decoration:none}

/* ── ALERTS ── */
.alert{display:flex;align-items:flex-start;gap:10px;padding:12px 14px;border-radius:var(--rs);margin-bottom:12px;border:1px solid;font-size:13px;line-height:1.5}
.a-d{background:var(--err-lt);border-color:#f5c6c3;color:#c62828}
.a-w{background:var(--warn-lt);border-color:#f5e0a0;color:#b06000}
.a-i{background:var(--pri-lt);border-color:#b3cef5;color:var(--pri-dk)}

/* ── BOTTOM NAV ── */
.bnav{position:fixed;bottom:0;left:0;right:0;z-index:200;background:var(--w);border-top:1px solid var(--g200);
  padding:6px 0 calc(6px + env(safe-area-inset-bottom));display:grid;grid-template-columns:repeat(5,1fr)}
.bni{display:flex;flex-direction:column;align-items:center;gap:2px;padding:5px 4px;cursor:pointer;
  border:none;background:none;color:var(--g500);font-size:10px;font-weight:500;
  min-height:48px;justify-content:center;font-family:inherit;position:relative}
.bni.on{color:var(--pri)}
.bni-i{font-size:22px;line-height:1}
.bni-b{position:absolute;top:3px;right:calc(50% - 22px);background:var(--err);color:#fff;border-radius:10px;font-size:9px;font-weight:700;padding:1px 5px}

/* ── TOAST ── */
.twrap{position:fixed;bottom:calc(76px + env(safe-area-inset-bottom));left:12px;right:12px;z-index:999;display:flex;flex-direction:column;gap:6px;pointer-events:none}
.toast{background:var(--g900);color:#fff;padding:12px 14px;border-radius:10px;font-size:13px;display:flex;align-items:center;gap:8px;box-shadow:var(--sh2);animation:ti .25s;pointer-events:all}
@keyframes ti{from{transform:translateY(8px);opacity:0}}
.t-ok{background:var(--ok)}.t-err{background:var(--err)}.t-wn{background:#b06000}

/* ── SPINNER ── */
.spin{width:16px;height:16px;border:2px solid rgba(255,255,255,.3);border-top-color:#fff;border-radius:50%;animation:sp .6s linear infinite;flex-shrink:0}
@keyframes sp{to{transform:rotate(360deg)}}

/* ── EMPTY ── */
.empty{text-align:center;padding:48px 20px}
.empty-i{font-size:44px;margin-bottom:12px;opacity:.4}
.empty-t{font-size:15px;font-weight:600;color:var(--g700);margin-bottom:6px}
.empty-d{font-size:12px;color:var(--g500);max-width:260px;margin:0 auto 16px}

/* ── DESKTOP ── */
@media(min-width:768px){
  .sg{grid-template-columns:repeat(4,1fr);gap:14px}
  .frow{grid-template-columns:1fr 1fr}
  .cgrid{grid-template-columns:repeat(3,1fr)}
  .dt2{grid-template-columns:1fr 1fr}
  .mlist{display:grid;grid-template-columns:repeat(2,1fr)}
  .modal{border-radius:var(--rl);max-width:620px;margin:auto;animation:mdi .2s}
  @keyframes mdi{from{transform:scale(.95);opacity:0}}
  .mhandle{display:none}
  .mover{align-items:center}
  .mfoot{flex-direction:row}
  .mfoot .btn{flex:none}
  .tsel{grid-template-columns:repeat(5,1fr)}
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

<!-- LOADING -->
<div id="ld">
  <div class="ld-logo">🛡️</div>
  <div style="font-size:20px;font-weight:700">Family Insurance</div>
  <div style="font-size:13px;color:var(--g500)" id="ld-sub">กำลังเริ่มต้น...</div>
  <div class="ld-bar"><div class="ld-fill" id="ld-fill"></div></div>
</div>

<div class="sb-ov" id="sb-ov" onclick="closeSB()"></div>

<!-- SIDEBAR -->
<aside class="sidebar" id="sidebar">
  <div class="sb-brand">
    <div class="sb-icon">🛡️</div>
    <div><div class="sb-name">Insurance Manager</div><div class="sb-sub">Family Policy Tracker</div></div>
  </div>
  <nav class="sb-nav">
    <div class="sb-lbl">ภาพรวม</div>
    <div class="sb-row on" onclick="go('dashboard')"><span class="sb-ic">📊</span>Dashboard</div>
    <div class="sb-row" onclick="go('policies')"><span class="sb-ic">📋</span>กรมธรรม์<span class="sb-badge" id="nb-s" style="display:none">0</span></div>
    <div class="sb-lbl" style="margin-top:6px">ประเภท</div>
    <div class="sb-row" onclick="go('policies');setF2('health')"><span class="sb-ic">❤️‍🩹</span>สุขภาพ</div>
    <div class="sb-row" onclick="go('policies');setF2('accident')"><span class="sb-ic">⚡</span>อุบัติเหตุ</div>
    <div class="sb-row" onclick="go('policies');setF2('life')"><span class="sb-ic">🌿</span>ชีวิต</div>
    <div class="sb-row" onclick="go('policies');setF2('ci')"><span class="sb-ic">🏥</span>โรคร้ายแรง</div>
    <div class="sb-lbl" style="margin-top:6px">จัดการ</div>
    <div class="sb-row" onclick="go('members')"><span class="sb-ic">👨‍👩‍👧‍👦</span>สมาชิก</div>
    <div class="sb-row" onclick="go('settings')"><span class="sb-ic">⚙️</span>ตั้งค่า</div>
  </nav>
  <div class="sb-foot"><div id="sb-auth"></div></div>
</aside>

<!-- MAIN -->
<div class="main">
  <div class="topbar">
    <button class="tb-menu" onclick="openSB()">☰</button>
    <div class="tb-title" id="pg-t">📊 Dashboard</div>
    <div class="tb-act">
      <button class="btn bp bs" onclick="openAdd()">＋ เพิ่ม</button>
    </div>
  </div>

  <!-- SYNC BAR -->
  <div class="sync-bar" id="sync-bar">
    <div class="sd sd-off" id="sb-dot"></div>
    <div class="sb-txt" id="sb-txt">ยังไม่ได้เชื่อมต่อ</div>
    <button class="sb-act-btn" id="sb-btn" onclick="syncBarClick()">Login</button>
  </div>

  <!-- DASHBOARD -->
  <div class="page active" id="page-dashboard">
    <div id="alert-area"></div>
    <div id="dash-auth-area"></div>

    <!-- Stats Row -->
    <div class="sg">
      <div class="sc"><div class="si" style="background:#e8f0fe">📋</div><div><div class="sv" id="s-tot">0</div><div class="sl">กรมธรรม์</div></div></div>
      <div class="sc"><div class="si" style="background:#e6f4ea">✅</div><div><div class="sv" id="s-act" style="color:var(--ok)">0</div><div class="sl">คุ้มครองอยู่</div></div></div>
      <div class="sc"><div class="si" style="background:#fef9e7">⚠️</div><div><div class="sv" id="s-exp" style="color:#c77a00">0</div><div class="sl">ใกล้หมด</div></div></div>
      <div class="sc"><div class="si" style="background:#fce8e6">💰</div><div><div class="sv" id="s-pr" style="color:var(--pri);font-size:17px">-</div><div class="sl">เบี้ยรวม/ปี ฿</div></div></div>
    </div>

    <!-- ประกันของแต่ละคน (หลัก) -->
    <div class="cc-t" style="margin-bottom:8px">
      <span style="font-size:14px;font-weight:700">👨‍👩‍👧‍👦 ประกันของแต่ละคน</span>
      <span style="font-size:11px;color:var(--g500)">แตะเพื่อดูรายละเอียด</span>
    </div>
    <div id="member-ins-area"></div>

    <!-- Donut + Expiry -->
    <div class="cc">
      <div class="cc-t"><span>สัดส่วนประเภทประกัน</span></div>
      <div class="drow">
        <div class="donut-wrap">
          <svg class="donut" id="dsvg" width="100" height="100" viewBox="0 0 100 100">
            <circle cx="50" cy="50" r="38" fill="none" stroke="#e8eaed" stroke-width="12"/>
          </svg>
          <div class="dc"><div class="dn" id="d-num">0</div><div class="dl">รายการ</div></div>
        </div>
        <div class="dleg" id="d-leg"><span style="color:var(--g400);font-size:12px">ยังไม่มีข้อมูล</span></div>
      </div>
    </div>

    <div class="cc">
      <div class="cc-t"><span>🔔 ใกล้หมดอายุ (90 วัน)</span></div>
      <div class="exp-list" id="exp-list"></div>
    </div>
  </div>

  <!-- POLICIES -->
  <div class="page" id="page-policies">
    <div class="srch"><span>🔍</span><input type="search" id="q" placeholder="ค้นหา..." oninput="renderP()" autocorrect="off" autocapitalize="off"></div>
    <div class="fscroll">
      <div class="fc on" data-f="all" onclick="setF(this,'all')">ทั้งหมด</div>
      <div class="fc" data-f="health" onclick="setF(this,'health')">❤️‍🩹 สุขภาพ</div>
      <div class="fc" data-f="accident" onclick="setF(this,'accident')">⚡ อุบัติเหตุ</div>
      <div class="fc" data-f="life" onclick="setF(this,'life')">🌿 ชีวิต</div>
      <div class="fc" data-f="ci" onclick="setF(this,'ci')">🏥 CI</div>
      <div class="fc" data-f="expiring" onclick="setF(this,'expiring')">⚠️ ใกล้หมด</div>
    </div>
    <div class="plist" id="plist"></div>
    <div id="empty-p" class="empty" style="display:none">
      <div class="empty-i">🛡️</div>
      <div class="empty-t">ยังไม่มีกรมธรรม์</div>
      <div class="empty-d">กดปุ่ม ＋ เพิ่ม เพื่อเริ่มบันทึก</div>
      <button class="btn bp" onclick="openAdd()">＋ เพิ่มกรมธรรม์แรก</button>
    </div>
  </div>

  <!-- MEMBERS -->
  <div class="page" id="page-members">
    <div style="display:flex;justify-content:flex-end;margin-bottom:12px">
      <button class="btn bp bs" onclick="openMemMod()">＋ เพิ่มสมาชิก</button>
    </div>
    <div class="mlist" id="mlist"></div>
  </div>

  <!-- SETTINGS -->
  <div class="page" id="page-settings">
    <div class="cfg"><div class="cfg-t">🔐 Google Account</div><div id="set-auth"></div></div>

    <div class="cfg">
      <div class="cfg-t">⚙️ OAuth Client ID</div>
      <div class="cfg-d">สร้างจาก Google Cloud Console → Credentials → OAuth 2.0 Client ID (Web App)<br>
        เพิ่ม Authorized origins: <code id="curr-org" style="background:var(--g100);padding:2px 5px;border-radius:4px;font-size:11px;word-break:break-all"></code></div>
      <div class="fg"><div class="fl">Client ID</div>
        <input type="text" class="fi" id="cid-in" placeholder="xxx.apps.googleusercontent.com" autocorrect="off" autocapitalize="none"></div>
      <button class="btn bp" onclick="saveCID()" style="width:100%">💾 บันทึก Client ID</button>
    </div>

    <div class="cfg" style="border:2px solid var(--pri)">
      <div class="cfg-t" style="color:var(--pri)">📊 Google Sheets — แหล่งข้อมูลหลัก</div>
      <div class="cfg-d">
        ✅ <strong>ข้อมูลเหมือนกันทุกเครื่อง</strong> — iPhone, iPad, PC อ่านจาก Sheet เดียวกัน<br><br>
        วิธีหา Spreadsheet ID:<br>
        <code style="font-size:11px;background:var(--g100);padding:4px 8px;border-radius:4px;display:block;margin-top:6px;word-break:break-all">docs.google.com/spreadsheets/d/<strong style="color:var(--pri)">[ID ตรงนี้]</strong>/edit</code>
      </div>
      <div class="fg"><div class="fl">Spreadsheet ID <span class="r">*</span></div>
        <input type="text" class="fi" id="sid-in" placeholder="1BxiMVs0XRA5..." autocorrect="off" autocapitalize="none"></div>
      <div class="frow">
        <div class="fg"><div class="fl">Sheet กรมธรรม์</div><input type="text" class="fi" id="sn-in" value="Policies" autocorrect="off"></div>
        <div class="fg"><div class="fl">Sheet สมาชิก</div><input type="text" class="fi" id="msn-in" value="Members" autocorrect="off"></div>
      </div>
      <div class="srow2" id="sh-row">
        <div class="sd2 sd2-off" id="sh-dot"></div><span id="sh-txt">ยังไม่ได้เชื่อมต่อ</span>
      </div>
      <div style="display:flex;gap:8px;flex-wrap:wrap">
        <button class="btn bp bs" onclick="saveSCfg()">💾 บันทึก</button>
        <button class="btn bo bs" onclick="pull()">📥 โหลดจาก Sheet</button>
        <button class="btn bg bs" onclick="push()">📤 บันทึกขึ้น Sheet</button>
      </div>
      <div class="code" style="margin-top:12px;font-size:10px">Columns: id | member_id | type | company | policy_no | plan_name | start_date | end_date | premium | sum_insured | payment_freq | beneficiary | coverage | drive_files | notes | updated_at</div>
    </div>

    <div class="cfg">
      <div class="cfg-t">📁 Google Drive — ไฟล์กรมธรรม์</div>
      <div class="cfg-d">ไฟล์แนบถูกเก็บใน Drive → Family Insurance → [ชื่อสมาชิก]<br>
        <strong>ทุกเครื่องใช้ Folder เดียวกัน</strong> เพราะ Folder ID ถูกเก็บใน Google Sheet</div>
      <div id="drive-area"></div>
      <div class="fg"><div class="fl">Root Folder ID (ปล่อยว่าง = สร้างอัตโนมัติ)</div>
        <input type="text" class="fi" id="dfid-in" placeholder="ปล่อยว่าง" autocorrect="off" autocapitalize="none"></div>
      <button class="btn bo bs" onclick="initDrive()" style="width:100%">📁 สร้าง / เชื่อม Folder</button>
    </div>

    <div class="cfg" style="border-color:var(--err-lt)">
      <div class="cfg-t" style="color:var(--err)">🗑️ จัดการข้อมูล</div>
      <div style="display:flex;gap:8px;flex-wrap:wrap;margin-top:8px">
        <button class="btn bg bs" onclick="doExport()">📥 Export CSV</button>
        <button class="btn bd bs" onclick="clearAll()">🗑️ ล้างข้อมูล (เครื่องนี้)</button>
      </div>
    </div>
  </div>
</div>

<!-- BOTTOM NAV -->
<nav class="bnav">
  <button class="bni on" data-p="dashboard" onclick="go('dashboard')"><span class="bni-i">📊</span>หน้าหลัก</button>
  <button class="bni" data-p="policies" onclick="go('policies')"><span class="bni-i">📋</span>กรมธรรม์<span class="bni-b" id="nb-b" style="display:none">0</span></button>
  <button class="bni" onclick="openAdd()" style="color:var(--pri)">
    <span class="bni-i" style="background:var(--pri);color:#fff;border-radius:50%;width:38px;height:38px;display:flex;align-items:center;justify-content:center;font-size:20px">＋</span>เพิ่ม
  </button>
  <button class="bni" data-p="members" onclick="go('members')"><span class="bni-i">👨‍👩‍👧‍👦</span>สมาชิก</button>
  <button class="bni" data-p="settings" onclick="go('settings')"><span class="bni-i">⚙️</span>ตั้งค่า</button>
</nav>

<!-- POLICY MODAL -->
<div class="mover" id="pm">
  <div class="modal">
    <div class="mhandle"></div>
    <div class="mhead"><div class="mtitle" id="pm-t">➕ เพิ่มกรมธรรม์</div><button class="mclose" onclick="closeMod('pm')">✕</button></div>
    <div class="mbody">
      <div class="fg">
        <div class="fl">ประเภทประกัน <span class="r">*</span></div>
        <div class="tsel">
          <div class="tc2" onclick="selT('health')" data-t="health"><div class="tc2-i">❤️‍🩹</div>สุขภาพ</div>
          <div class="tc2" onclick="selT('accident')" data-t="accident"><div class="tc2-i">⚡</div>อุบัติเหตุ</div>
          <div class="tc2" onclick="selT('life')" data-t="life"><div class="tc2-i">🌿</div>ชีวิต</div>
          <div class="tc2" onclick="selT('ci')" data-t="ci"><div class="tc2-i">🏥</div>CI</div>
          <div class="tc2" onclick="selT('other')" data-t="other"><div class="tc2-i">📌</div>อื่นๆ</div>
        </div>
        <input type="hidden" id="f-type">
      </div>
      <div class="fg"><div class="fl">สมาชิก <span class="r">*</span></div><select class="fi" id="f-mem"></select></div>
      <div class="frow">
        <div class="fg"><div class="fl">บริษัทประกัน <span class="r">*</span></div><input type="text" class="fi" id="f-co" placeholder="AIA, เมืองไทย..."></div>
        <div class="fg"><div class="fl">เลขกรมธรรม์</div><input type="text" class="fi" id="f-pno" placeholder="TH-001" autocorrect="off"></div>
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
          <select class="fi" id="f-freq">
            <option value="yearly">รายปี</option><option value="halfyearly">ราย 6 เดือน</option>
            <option value="quarterly">รายไตรมาส</option><option value="monthly">รายเดือน</option>
          </select>
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
      <div class="fsec">📎 ไฟล์แนบ → Google Drive</div>
      <div id="up-warn" class="alert a-i" style="display:none">🔐 Login Google ก่อนอัพโหลดไฟล์</div>
      <div id="up-wrap">
        <div class="upzone" onclick="document.getElementById('fi').click()" ondragover="event.preventDefault()" ondrop="onDrop(event)">
          <input type="file" id="fi" multiple accept=".pdf,.jpg,.jpeg,.png" onchange="onPick(event)">
          <div style="font-size:28px">📎</div>
          <div style="font-size:13px;color:var(--g600)">แตะเลือกไฟล์</div>
          <div style="font-size:11px;color:var(--g400)">PDF, JPG, PNG · สูงสุด 20MB</div>
        </div>
        <div class="flist2" id="flist2"></div>
      </div>
      <div class="fg" style="margin-top:14px"><div class="fl">หมายเหตุ</div><textarea class="fi" id="f-note" placeholder="เงื่อนไขพิเศษ..."></textarea></div>
    </div>
    <div class="mfoot">
      <button class="btn bg" onclick="closeMod('pm')">ยกเลิก</button>
      <button class="btn bp" id="save-btn" onclick="saveP()">💾 บันทึก</button>
    </div>
  </div>
</div>

<!-- DETAIL MODAL -->
<div class="mover" id="dm">
  <div class="modal">
    <div class="mhandle"></div>
    <div class="mhead"><div class="mtitle">📋 รายละเอียด</div><button class="mclose" onclick="closeMod('dm')">✕</button></div>
    <div class="mbody" id="dm-body"></div>
    <div class="mfoot">
      <button class="btn bg" onclick="closeMod('dm')">ปิด</button>
      <button class="btn bo" id="dm-edit">✏️ แก้ไข</button>
      <button class="btn bd" id="dm-del">🗑️ ลบ</button>
    </div>
  </div>
</div>

<!-- MEMBER MODAL -->
<div class="mover" id="mm">
  <div class="modal" style="max-width:440px">
    <div class="mhandle"></div>
    <div class="mhead"><div class="mtitle">👤 เพิ่มสมาชิก</div><button class="mclose" onclick="closeMod('mm')">✕</button></div>
    <div class="mbody">
      <div class="fg"><div class="fl">ชื่อ-นามสกุล <span class="r">*</span></div><input type="text" class="fi" id="m-nm" placeholder="สมชาย ใจดี"></div>
      <div class="frow">
        <div class="fg"><div class="fl">ความสัมพันธ์</div>
          <select class="fi" id="m-role">
            <option>ตัวเอง</option><option>คู่สมรส</option><option>ลูก</option>
            <option>พ่อ</option><option>แม่</option><option>พ่อตา/แม่ยาย</option><option>อื่นๆ</option>
          </select>
        </div>
        <div class="fg"><div class="fl">วันเกิด</div><input type="date" class="fi" id="m-dob"></div>
      </div>
      <div class="fg"><div class="fl">สีประจำตัว</div><input type="color" class="fi" id="m-col" value="#1a73e8" style="height:48px;cursor:pointer;padding:4px 8px"></div>
    </div>
    <div class="mfoot">
      <button class="btn bg" onclick="closeMod('mm')">ยกเลิก</button>
      <button class="btn bp" onclick="saveM()">💾 เพิ่มสมาชิก</button>
    </div>
  </div>
</div>

<div class="twrap" id="twrap"></div>

<script src="https://accounts.google.com/gsi/client" async></script>
<script src="https://apis.google.com/js/api.js" async onload="onGapi()"></script>
<script>
// ═══════════════════════════════════════
//  CONSTANTS
// ═══════════════════════════════════════
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

// ═══════════════════════════════════════
//  STATE
// ═══════════════════════════════════════
let P=[],M=[],editId=null,selType='',filt='all';
let pFiles=[],syncTimer=null;
let tok=null,usr=null,gisOk=false;
// cfg เก็บเฉพาะ clientId ใน localStorage — Sheet ID + Drive Folder ID ถูกดึงจาก Sheet
let cfg={cid:'',sid:'',sn:'Policies',msn:'Members',si:15};
// driveFolderId จะถูก sync ผ่าน Sheet (ไม่ใช่ localStorage)
let sharedDriveFolderId='';

// ═══════════════════════════════════════
//  BOOT
// ═══════════════════════════════════════
function ldSet(p,t){document.getElementById('ld-fill').style.width=p+'%';document.getElementById('ld-sub').textContent=t;}
function ldHide(){const e=document.getElementById('ld');e.classList.add('gone');setTimeout(()=>e.style.display='none',400);}

function boot(){
  ldSet(15,'อ่านการตั้งค่า...');
  loadCfg(); loadLocal();

  // ตั้งค่า UI fields
  const co=document.getElementById('curr-org');if(co) co.textContent=location.origin;
  const ci=document.getElementById('cid-in');if(ci&&cfg.cid) ci.value=cfg.cid;
  const si=document.getElementById('sid-in');if(si&&cfg.sid) si.value=cfg.sid;
  const sn=document.getElementById('sn-in');if(sn) sn.value=cfg.sn||'Policies';
  const mn=document.getElementById('msn-in');if(mn) mn.value=cfg.msn||'Members';

  ldSet(40,'เตรียมข้อมูล...');
  if(!M.length){ M=[{id:uid(),name:'ฉัน (ตัวเอง)',role:'ตัวเอง',color:'#1a73e8',dob:''}]; saveLocal(); }
  populateMSel(); renderAll(); checkAlerts();

  ldSet(70,'ตรวจสอบ session...');
  const saved=sessionStorage.getItem('gt');
  if(saved){
    tok=saved;
    verifyTok().then(ok=>{
      if(ok){ fetchUsr(); }
      else { tok=null; sessionStorage.removeItem('gt'); updateAuthUI(); updateSyncBar(); }
    });
  }

  ldSet(100,'พร้อมแล้ว!');
  // ซ่อน loading ทันที — ไม่รอ Google
  setTimeout(ldHide,350);
  updateAuthUI(); updateSyncBar();
}

// ═══════════════════════════════════════
//  LOCAL STORAGE (cache offline)
// ═══════════════════════════════════════
function loadLocal(){ try{P=JSON.parse(localStorage.getItem('ip')||'[]');M=JSON.parse(localStorage.getItem('im')||'[]');}catch(e){P=[];M=[];} }
function saveLocal(){ localStorage.setItem('ip',JSON.stringify(P));localStorage.setItem('im',JSON.stringify(M)); }
function loadCfg(){ try{cfg=Object.assign({cid:'',sid:'',sn:'Policies',msn:'Members',si:15},JSON.parse(localStorage.getItem('ic')||'{}'));}catch(e){} }
function saveCfg(){ localStorage.setItem('ic',JSON.stringify(cfg)); }
function uid(){ return Date.now().toString(36)+Math.random().toString(36).substr(2,5); }

// ═══════════════════════════════════════
//  GOOGLE AUTH (iOS-safe fetch only)
// ═══════════════════════════════════════
function onGapi(){ try{gapi.load('client',()=>{try{gapi.client.init({});}catch(e){}});}catch(e){} }

function tryGIS(){
  if(!cfg.cid){gisOk=true;return;}
  if(typeof google==='undefined'||!google.accounts){setTimeout(tryGIS,500);return;}
  try{
    window._tc=google.accounts.oauth2.initTokenClient({
      client_id:cfg.cid,scope:SCOPE,
      callback:onTok,
      error_callback:(e)=>toast('Login ผิดพลาด: '+(e.type||e),'error'),
    });
    gisOk=true;
  }catch(e){console.warn('GIS:',e);gisOk=true;}
}

function onTok(r){
  if(r.error){toast('Login ไม่สำเร็จ: '+r.error,'error');return;}
  tok=r.access_token;
  sessionStorage.setItem('gt',tok);
  fetchUsr().then(()=>{
    // ดึง Drive Folder ID จาก Sheet ก่อน แล้วค่อย pull ข้อมูล
    if(cfg.sid) pull(false).then(()=>{ updateDriveFolderUI(); });
    else toast('Login สำเร็จ! กรุณาตั้งค่า Sheet ID','warn');
    setupAutoSync();
  });
}

async function verifyTok(){
  try{const r=await fetch('https://www.googleapis.com/oauth2/v3/tokeninfo?access_token='+tok);return r.ok;}
  catch(e){return false;}
}
async function fetchUsr(){
  try{
    const r=await fetch('https://www.googleapis.com/oauth2/v3/userinfo',{headers:{Authorization:'Bearer '+tok}});
    if(!r.ok){tok=null;sessionStorage.removeItem('gt');updateAuthUI();updateSyncBar();return;}
    usr=await r.json(); updateAuthUI(); updateSyncBar();
  }catch(e){console.warn(e);}
}
function signIn(){
  if(!cfg.cid){toast('กรุณาตั้งค่า Client ID ก่อน','warn');go('settings');return;}
  if(!gisOk||!window._tc){tryGIS();setTimeout(signIn,800);return;}
  try{window._tc.requestAccessToken({prompt:tok?'':'consent'});}
  catch(e){toast('ไม่สามารถเปิด Login ได้ — ลองกดปุ่มอีกครั้ง','error');}
}
function signOut(){
  if(tok&&typeof google!=='undefined') try{google.accounts.oauth2.revoke(tok,()=>{});}catch(e){}
  tok=null;usr=null;sessionStorage.removeItem('gt');
  if(syncTimer){clearInterval(syncTimer);syncTimer=null;}
  updateAuthUI();updateSyncBar();toast('ออกจากระบบแล้ว','warn');
}

// ═══════════════════════════════════════
//  SYNC BAR
// ═══════════════════════════════════════
function updateSyncBar(){
  const dot=document.getElementById('sb-dot'),txt=document.getElementById('sb-txt'),btn=document.getElementById('sb-btn');
  if(!dot)return;
  dot.className='sd';
  if(!tok){dot.classList.add('sd-off');txt.textContent='ยังไม่ได้ Login Google';btn.textContent='Login';}
  else if(!cfg.sid){dot.classList.add('sd-off');txt.textContent='Login แล้ว — ยังไม่ได้ตั้งค่า Sheet ID';btn.textContent='ตั้งค่า';}
  else{dot.classList.add('sd-ok');txt.textContent=`✅ Sync กับ Sheet: ${cfg.sn} · ข้อมูลเดียวกันทุกเครื่อง`;btn.textContent='Sync';}
}
function setSyncing(on,msg){
  const dot=document.getElementById('sb-dot'),txt=document.getElementById('sb-txt');
  if(!dot)return;
  dot.className='sd '+(on?'sd-busy':'sd-ok');
  if(msg) txt.textContent=msg;
  else if(!on) txt.textContent=`✅ Sheet: ${cfg.sn}`;
}
function syncBarClick(){if(!tok)signIn();else if(!cfg.sid)go('settings');else pull();}

// ═══════════════════════════════════════
//  GOOGLE SHEETS — fetch REST (iOS-safe)
//  Drive Folder ID ถูกเก็บใน Sheet "Config"
// ═══════════════════════════════════════
async function gsh(method,path,body=null){
  if(!tok)throw new Error('NOT_SIGNED_IN');
  const url=`https://sheets.googleapis.com/v4/spreadsheets/${cfg.sid}${path}`;
  const o={method,headers:{Authorization:'Bearer '+tok,'Content-Type':'application/json'}};
  if(body) o.body=JSON.stringify(body);
  const r=await fetch(url,o);
  if(r.status===401){tok=null;sessionStorage.removeItem('gt');usr=null;updateAuthUI();updateSyncBar();throw new Error('TOKEN_EXPIRED');}
  if(!r.ok){const e=await r.json().catch(()=>({}));throw new Error(e.error?.message||'Sheets '+r.status);}
  return r.json();
}

// ── PULL: Sheet → App ──────────────────
async function pull(showMsg=true){
  if(!tok){if(showMsg)toast('กรุณา Login ก่อน','warn');return;}
  if(!cfg.sid){if(showMsg)toast('กรุณาตั้งค่า Sheet ID','warn');return;}
  setSyncing(true,'กำลังโหลดจาก Sheet...');
  try{
    // 1. โหลด Config Sheet (Drive Folder ID ที่แชร์ทุกเครื่อง)
    try{
      const cd=await gsh('GET',`/values/${enc('Config')}?majorDimension=ROWS`);
      if(cd.values&&cd.values.length>1){
        const [h,...rows]=cd.values;
        const xi=k=>h.indexOf(k);
        rows.forEach(r=>{
          if(r[xi('key')]==='drive_folder_id') sharedDriveFolderId=r[xi('value')]||'';
        });
        document.getElementById('dfid-in').value=sharedDriveFolderId;
      }
    }catch(e){/* Config sheet อาจยังไม่มี */}

    // 2. โหลด Policies
    const pd=await gsh('GET',`/values/${enc(cfg.sn)}?majorDimension=ROWS`);
    if(pd.values&&pd.values.length>1){
      const [h,...rows]=pd.values;
      const xi=k=>h.indexOf(k);
      P=rows.filter(r=>r[xi('id')]||r[0]).map(r=>({
        id:r[xi('id')]||uid(),
        member:r[xi('member_id')]||'',
        type:r[xi('type')]||'other',
        company:r[xi('company')]||'',
        policy_no:r[xi('policy_no')]||'',
        plan_name:r[xi('plan_name')]||'',
        start_date:r[xi('start_date')]||'',
        end_date:r[xi('end_date')]||'',
        premium:r[xi('premium')]||0,
        sum_insured:r[xi('sum_insured')]||0,
        payment_freq:r[xi('payment_freq')]||'yearly',
        beneficiary:r[xi('beneficiary')]||'',
        coverage:(r[xi('coverage')]||'').split(',').map(s=>s.trim()).filter(Boolean),
        driveFiles:(()=>{try{return JSON.parse(r[xi('drive_files')]||'[]');}catch(e){return[];}})(),
        notes:r[xi('notes')]||'',
        created_at:r[xi('created_at')]||'',
        updated_at:r[xi('updated_at')]||'',
      }));
    }

    // 3. โหลด Members (รวม driveFolderId ของแต่ละคน)
    try{
      const md=await gsh('GET',`/values/${enc(cfg.msn||'Members')}?majorDimension=ROWS`);
      if(md.values&&md.values.length>1){
        const [h,...rows]=md.values;
        const xi=k=>h.indexOf(k);
        const loaded=rows.filter(r=>r[0]).map(r=>({
          id:r[xi('id')]||uid(),
          name:r[xi('name')]||'',
          role:r[xi('role')]||'',
          dob:r[xi('dob')]||'',
          color:r[xi('color')]||'#1a73e8',
          driveFolderId:r[xi('drive_folder_id')]||'', // sub-folder ของแต่ละคนใน Drive
        }));
        if(loaded.length) M=loaded;
      }
    }catch(e){}

    if(!M.length) M=[{id:uid(),name:'ฉัน (ตัวเอง)',role:'ตัวเอง',color:'#1a73e8',dob:''}];
    saveLocal(); populateMSel(); renderAll(); checkAlerts();
    setSyncing(false);
    if(showMsg) toast('โหลดข้อมูลจาก Sheet สำเร็จ ✅','success');
    updateDriveFolderUI();
  }catch(e){
    setSyncing(false);
    if(e.message==='TOKEN_EXPIRED') toast('Session หมดอายุ — Login ใหม่','warn');
    else if(showMsg) toast('โหลดไม่สำเร็จ: '+e.message,'error');
    else console.warn('pull:',e.message);
  }
}

// ── PUSH: App → Sheet ──────────────────
async function push(showMsg=true){
  if(!tok){if(showMsg)toast('กรุณา Login ก่อน','warn');return;}
  if(!cfg.sid){if(showMsg)toast('กรุณาตั้งค่า Sheet ID','warn');return;}
  setSyncing(true,'กำลังบันทึกขึ้น Sheet...');

  // Policies
  const PH=['id','member_id','member_name','type','company','policy_no','plan_name',
    'start_date','end_date','premium','sum_insured','payment_freq','beneficiary',
    'coverage','drive_files','notes','created_at','updated_at'];
  const pRows=[PH,...P.map(p=>[
    p.id,p.member,getMem(p.member).name,p.type,p.company||'',p.policy_no||'',p.plan_name||'',
    p.start_date||'',p.end_date||'',p.premium||0,p.sum_insured||0,p.payment_freq||'yearly',p.beneficiary||'',
    (p.coverage||[]).join(','),JSON.stringify(p.driveFiles||[]),p.notes||'',p.created_at||'',p.updated_at||new Date().toISOString(),
  ])];

  // Members (รวม driveFolderId ของแต่ละคน)
  const MH=['id','name','role','dob','color','drive_folder_id'];
  const mRows=[MH,...M.map(m=>[m.id,m.name,m.role||'',m.dob||'',m.color||'#1a73e8',m.driveFolderId||''])];

  // Config (Drive Folder ID ที่แชร์)
  const CH=['key','value'];
  const cRows=[CH,['drive_folder_id',sharedDriveFolderId||'']];

  try{
    await gsh('POST',`/values/${enc(cfg.sn+'!A:Z')}:clear`);
    await gsh('PUT',`/values/${enc(cfg.sn+'!A1')}?valueInputOption=RAW`,{values:pRows});
    try{
      await gsh('POST',`/values/${enc((cfg.msn||'Members')+'!A:Z')}:clear`);
      await gsh('PUT',`/values/${enc((cfg.msn||'Members')+'!A1')}?valueInputOption=RAW`,{values:mRows});
    }catch(e){}
    // เขียน Config sheet
    try{
      await gsh('POST',`/values/${enc('Config!A:Z')}:clear`);
      await gsh('PUT',`/values/${enc('Config!A1')}?valueInputOption=RAW`,{values:cRows});
    }catch(e){}
    setSyncing(false);
    if(showMsg) toast('บันทึกขึ้น Sheet สำเร็จ ✅','success');
    else setSyncing(false);
  }catch(e){
    setSyncing(false);
    if(e.message==='TOKEN_EXPIRED') toast('Session หมดอายุ — Login ใหม่','warn');
    else if(showMsg) toast('บันทึกไม่สำเร็จ: '+e.message,'error');
  }
}

function enc(s){return encodeURIComponent(s);}
function setupAutoSync(){
  if(syncTimer) clearInterval(syncTimer);
  if(tok&&cfg.sid&&cfg.si>0) syncTimer=setInterval(()=>pull(false),cfg.si*60000);
}

// ═══════════════════════════════════════
//  GOOGLE DRIVE — fetch REST
//  Folder ID ถูกแชร์ผ่าน Sheet (Config)
//  ทุกเครื่องจึงใช้ Folder เดียวกัน
// ═══════════════════════════════════════
async function gdr(method,url,body=null,isForm=false){
  if(!tok)throw new Error('NOT_SIGNED_IN');
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
  const inp=document.getElementById('dfid-in').value.trim();
  if(inp){
    try{
      const d=await gdr('GET',`https://www.googleapis.com/drive/v3/files/${inp}?fields=id,name,webViewLink`);
      sharedDriveFolderId=inp;
      // บันทึกขึ้น Config Sheet ทันที → ทุกเครื่องจะอ่านได้
      if(cfg.sid) await saveDriveFolderToSheet(inp);
      toast(`เชื่อมต่อ "${d.name}" สำเร็จ — บันทึกขึ้น Sheet แล้ว ✅`,'success');
      renderDriveCard(d);
    }catch(e){toast('ไม่พบ Folder: '+e.message,'error');}
    return;
  }
  toast('กำลังสร้าง Folder Family Insurance...','warn');
  try{
    const d=await gdr('POST','https://www.googleapis.com/drive/v3/files?fields=id,name,webViewLink',
      {name:'Family Insurance',mimeType:'application/vnd.google-apps.folder'});
    sharedDriveFolderId=d.id;
    document.getElementById('dfid-in').value=d.id;
    // บันทึก Folder ID ขึ้น Config Sheet → ทุกเครื่องอ่านได้
    if(cfg.sid) await saveDriveFolderToSheet(d.id);
    toast('สร้าง Folder เรียบร้อย บันทึกขึ้น Sheet แล้ว ✅','success');
    renderDriveCard(d);
  }catch(e){toast('สร้างไม่สำเร็จ: '+e.message,'error');}
}

async function saveDriveFolderToSheet(folderId){
  try{
    await gsh('POST',`/values/${enc('Config!A:Z')}:clear`);
    await gsh('PUT',`/values/${enc('Config!A1')}?valueInputOption=RAW`,
      {values:[['key','value'],['drive_folder_id',folderId]]});
  }catch(e){console.warn('save drive folder:',e.message);}
}

function updateDriveFolderUI(){
  if(sharedDriveFolderId){
    document.getElementById('dfid-in').value=sharedDriveFolderId;
    renderDriveCard(null);
  }
}

function renderDriveCard(f){
  const el=document.getElementById('drive-area');if(!el)return;
  const link=f?.webViewLink||`https://drive.google.com/drive/folders/${sharedDriveFolderId}`;
  const name=f?.name||'Family Insurance';
  el.innerHTML=`<a href="${link}" target="_blank" class="drive-card"><span style="font-size:26px">📁</span><div><div style="font-weight:700">${name}</div><div style="font-size:12px;opacity:.8">แตะเพื่อเปิดใน Google Drive → ใช้ร่วมกันทุกเครื่อง</div></div></a>`;
}

// Sub-folder ของแต่ละสมาชิก (ID ถูกเก็บใน Members Sheet)
async function getMemberFolder(memberId){
  const mi=M.findIndex(m=>m.id===memberId);
  if(mi!==-1&&M[mi].driveFolderId) return M[mi].driveFolderId;
  const mem=getMem(memberId);
  const d=await gdr('POST','https://www.googleapis.com/drive/v3/files?fields=id',
    {name:mem.name,mimeType:'application/vnd.google-apps.folder',parents:[sharedDriveFolderId]});
  if(mi!==-1) M[mi].driveFolderId=d.id;
  saveLocal();
  // Push Members sheet ทันทีเพื่อให้ทุกเครื่องรู้ folder ID
  if(tok&&cfg.sid) push(false);
  return d.id;
}

async function upFile(f,pid,i){
  pFiles[i].status='uploading';renderFList();
  const meta={name:f.name,parents:[pid]};
  const form=new FormData();
  form.append('metadata',new Blob([JSON.stringify(meta)],{type:'application/json'}));
  form.append('file',f);
  try{
    const d=await gdr('POST','https://www.googleapis.com/upload/drive/v3/files?uploadType=multipart&fields=id,name,webViewLink',form,true);
    pFiles[i].status='done';pFiles[i].wvl=d.webViewLink;renderFList();
    return{id:d.id,name:d.name,webViewLink:d.webViewLink};
  }catch(e){pFiles[i].status='error';renderFList();return null;}
}

// ═══════════════════════════════════════
//  AUTH UI
// ═══════════════════════════════════════
function updateAuthUI(){
  const isIn=!!usr;

  // Sidebar
  const sa=document.getElementById('sb-auth');
  if(sa) sa.innerHTML=isIn
    ?`<div style="display:flex;align-items:center;gap:8px;padding:10px 12px;border-radius:8px;background:var(--ok-lt);border:1px solid var(--ok)">
        ${usr.picture?`<img src="${usr.picture}" style="width:24px;height:24px;border-radius:50%">`:'✅'}
        <div style="flex:1;overflow:hidden"><div style="font-size:12px;font-weight:600;overflow:hidden;text-overflow:ellipsis;white-space:nowrap">${usr.name}</div>
        <div style="font-size:10px;color:var(--g500);overflow:hidden;text-overflow:ellipsis;white-space:nowrap">${usr.email}</div></div>
        <button onclick="signOut()" style="background:none;border:none;cursor:pointer;font-size:14px;color:var(--g500);padding:2px">✕</button>
      </div>`
    :`<button class="btn bp" onclick="signIn()" style="width:100%;font-size:12px;min-height:40px">🔐 Login Google</button>`;

  // Dashboard
  const da=document.getElementById('dash-auth-area');
  if(da) da.innerHTML=isIn
    ?`<div class="auth-signed">
        ${usr.picture?`<img src="${usr.picture}" style="width:28px;height:28px;border-radius:50%">`:''}
        <div style="flex:1"><div style="font-size:13px;font-weight:600;color:var(--ok)">${usr.name}</div>
        <div style="font-size:11px;color:var(--g500)">${usr.email} · ข้อมูลเดียวกันทุกเครื่อง</div></div>
        <button onclick="pull()" style="background:none;border:1.5px solid var(--ok);color:var(--ok);padding:6px 10px;border-radius:8px;cursor:pointer;font-size:11px;font-weight:600;font-family:inherit">🔄 Sync</button>
      </div>`
    :`<div class="auth-card">
        <h3>🔐 เชื่อมต่อ Google = ข้อมูลเดียวกันทุกเครื่อง</h3>
        <p>iPhone กับ PC จะเห็นข้อมูลเดียวกันทันที หลัง Login และตั้งค่า Google Sheet</p>
        <button class="auth-card-btn" onclick="signIn()">🔐 เข้าสู่ระบบด้วย Google</button>
      </div>`;

  // Settings
  const sa2=document.getElementById('set-auth');
  if(sa2) sa2.innerHTML=isIn
    ?`<div style="display:flex;align-items:center;gap:10px;padding:4px 0 12px">
        ${usr.picture?`<img src="${usr.picture}" style="width:40px;height:40px;border-radius:50%">`:''}
        <div><div style="font-weight:700">${usr.name}</div><div style="font-size:12px;color:var(--g500)">${usr.email}</div></div>
        <button onclick="signOut()" class="btn bg bs" style="margin-left:auto">ออก</button>
      </div>`
    :`<div style="padding:4px 0 12px">
        <div style="font-size:13px;color:var(--g600);margin-bottom:10px">ยังไม่ได้ Login — ข้อมูลจะเก็บแค่ในเครื่องนี้</div>
        <button class="btn bp" onclick="signIn()" style="width:100%">🔐 Login ด้วย Google</button>
      </div>`;

  // Sheet status
  const sd=document.getElementById('sh-dot'),st=document.getElementById('sh-txt');
  if(sd&&st){
    if(isIn&&cfg.sid){sd.className='sd2 sd2-ok';st.textContent=`เชื่อมต่อแล้ว: ${cfg.sn} · ข้อมูลเดียวกันทุกเครื่อง`;}
    else if(isIn){sd.className='sd2';sd.style.background='var(--warn)';st.textContent='Login แล้ว — กรุณาตั้งค่า Sheet ID';}
    else{sd.className='sd2 sd2-off';st.textContent='ยังไม่ได้ Login';}
  }
  // Upload area
  const uw=document.getElementById('up-warn'),uwp=document.getElementById('up-wrap');
  if(uw&&uwp){uw.style.display=isIn?'none':'flex';uwp.style.display=isIn?'block':'none';}
  if(isIn&&sharedDriveFolderId) renderDriveCard(null);
}

// ═══════════════════════════════════════
//  NAVIGATION
// ═══════════════════════════════════════
function go(pg){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.getElementById('page-'+pg).classList.add('active');
  document.querySelectorAll('.sb-row,.bni[data-p]').forEach(n=>n.classList.remove('on'));
  document.querySelectorAll(`[data-p="${pg}"]`).forEach(n=>n.classList.add('on'));
  const T={dashboard:'📊 Dashboard',policies:'📋 กรมธรรม์',members:'👨‍👩‍👧‍👦 สมาชิก',settings:'⚙️ ตั้งค่า'};
  document.getElementById('pg-t').textContent=T[pg]||pg;
  if(pg==='policies') renderP();
  if(pg==='members')  renderMems();
  if(pg==='dashboard'){renderDash();updateAuthUI();}
  if(pg==='settings') {updateAuthUI();updateDriveFolderUI();}
  closeSB();window.scrollTo({top:0,behavior:'smooth'});
}
function openSB(){document.getElementById('sidebar').classList.add('open');document.getElementById('sb-ov').classList.add('on');}
function closeSB(){document.getElementById('sidebar').classList.remove('open');document.getElementById('sb-ov').classList.remove('on');}

// ═══════════════════════════════════════
//  UTILS
// ═══════════════════════════════════════
function dl(d){if(!d)return Infinity;const n=new Date();n.setHours(0,0,0,0);return Math.ceil((new Date(d)-n)/864e5);}
function thd(s){
  if(!s)return '-';const d=new Date(s);
  const Mn=['ม.ค.','ก.พ.','มี.ค.','เม.ย.','พ.ค.','มิ.ย.','ก.ค.','ส.ค.','ก.ย.','ต.ค.','พ.ย.','ธ.ค.'];
  return`${d.getDate()} ${Mn[d.getMonth()]} ${d.getFullYear()+543}`;
}
function fm(n){return n?Number(n).toLocaleString('th-TH')+' ฿':'-';}
function pst(p){const d=dl(p.end_date);return d<0?'expired':d<=90?'expiring':'active';}
function getMem(id){return M.find(m=>m.id===id)||{name:id||'?',color:'#9aa0a6'};}
function ini(n){return(n||'?').split(' ').map(w=>w[0]).join('').substr(0,2).toUpperCase();}
function populateMSel(){
  const s=document.getElementById('f-mem');if(!s)return;
  const pv=s.value;
  s.innerHTML='<option value="">-- เลือกสมาชิก --</option>';
  M.forEach(m=>{const o=document.createElement('option');o.value=m.id;o.textContent=m.name+(m.role?` (${m.role})`:'');s.appendChild(o);});
  if(pv) s.value=pv;
}

// ═══════════════════════════════════════
//  RENDER ALL
// ═══════════════════════════════════════
function renderAll(){renderDash();renderP();renderMems();updBadge();}
function updBadge(){
  const n=P.filter(p=>{const d=dl(p.end_date);return d>=0&&d<=90;}).length;
  ['nb-s','nb-b'].forEach(id=>{const b=document.getElementById(id);if(!b)return;b.style.display=n?'inline':'none';b.textContent=n;});
}

// ── DASHBOARD ──────────────────────────
function renderDash(){
  document.getElementById('s-tot').textContent=P.length;
  document.getElementById('s-act').textContent=P.filter(p=>pst(p)==='active').length;
  document.getElementById('s-exp').textContent=P.filter(p=>pst(p)==='expiring').length;
  const pr=P.reduce((a,p)=>a+Number(p.premium||0),0);
  document.getElementById('s-pr').textContent=pr?pr.toLocaleString('th-TH'):'-';
  renderMemberIns();
  renderDonut();
  renderExpiry();
}

// ── ประกันของแต่ละคน (Feature ใหม่) ──
function renderMemberIns(){
  const area=document.getElementById('member-ins-area');
  if(!area)return;
  if(!M.length){area.innerHTML='<div class="empty"><div class="empty-i">👨‍👩‍👧‍👦</div><div class="empty-t">ยังไม่มีสมาชิก</div><button class="btn bp bs" onclick="openMemMod()">＋ เพิ่มสมาชิก</button></div>';return;}

  area.innerHTML=M.map(m=>{
    const mp=P.filter(p=>p.member===m.id).sort((a,b)=>new Date(a.end_date||0)-new Date(b.end_date||0));
    const expCount=mp.filter(p=>pst(p)==='expiring').length;
    const expiredCount=mp.filter(p=>pst(p)==='expired').length;
    const headerExtra=expCount?`<span style="font-size:10px;background:var(--warn-lt);color:#b06000;padding:2px 6px;border-radius:4px;font-weight:600;margin-left:4px">⚠️ ${expCount} ใกล้หมด</span>`:
      expiredCount?`<span style="font-size:10px;background:var(--err-lt);color:var(--err);padding:2px 6px;border-radius:4px;font-weight:600;margin-left:4px">❌ ${expiredCount} หมดแล้ว</span>`:'';

    const insRows=mp.map(p=>{
      const c=TC[p.type]||TC.other;
      const s=pst(p);
      const d=dl(p.end_date);
      let expCls='iok',expTxt=`${thd(p.end_date)}`;
      if(s==='expired'){expCls='iend';expTxt='หมดอายุแล้ว';}
      else if(d<=30){expCls='ic';expTxt=`🔴 อีก ${d} วัน`;}
      else if(d<=90){expCls='iw';expTxt=`⚠️ อีก ${d} วัน`;}
      else expTxt=`${thd(p.end_date)}`;
      return`<div class="ins-row" onclick="showD('${p.id}')">
        <div class="ins-type-icon" style="background:${c.b}">${c.i}</div>
        <div class="ins-info">
          <div class="ins-company">${p.company||'-'}${p.plan_name?` · ${p.plan_name}`:''}</div>
          <div class="ins-plan">${c.l}${p.policy_no?' · '+p.policy_no:''}</div>
        </div>
        <div class="ins-right">
          <div class="ins-exp ${expCls}">${expTxt}</div>
          ${p.premium?`<div class="ins-prem">${fm(p.premium)}/ปี</div>`:''}
        </div>
      </div>`;
    }).join('');

    const addBtn=`<button class="mem-add-btn" onclick="openAddForMember('${m.id}')">＋ เพิ่มกรมธรรม์ให้ ${m.name.split(' ')[0]}</button>`;

    return`<div class="mem-section">
      <div class="mem-header" onclick="toggleMem('mem-${m.id}',this)" id="mh-${m.id}">
        <div class="mem-av" style="background:${m.color}">${ini(m.name)}</div>
        <div class="mem-hinfo">
          <div class="mem-hname">${m.name}${headerExtra}</div>
          <div class="mem-hrole">${m.role||''}${m.dob?' · '+(new Date().getFullYear()-new Date(m.dob).getFullYear())+' ปี':''}</div>
        </div>
        <div class="mem-hcount">${mp.length} กรมธรรม์</div>
        <div class="mem-hchev">▼</div>
      </div>
      <div class="mem-body" id="mem-${m.id}">
        ${mp.length?insRows:'<div style="text-align:center;padding:12px 0;font-size:12px;color:var(--g400)">ยังไม่มีกรมธรรม์</div>'}
        ${addBtn}
      </div>
    </div>`;
  }).join('');

  // Auto-expand ถ้ามีกรมธรรม์ใกล้หมด
  M.forEach(m=>{
    const mp=P.filter(p=>p.member===m.id);
    const hasUrgent=mp.some(p=>pst(p)==='expiring'||pst(p)==='expired');
    if(hasUrgent||mp.length>0){
      const body=document.getElementById('mem-'+m.id);
      const header=document.getElementById('mh-'+m.id);
      if(body&&header){body.classList.add('open');header.classList.add('open');}
    }
  });
}

function toggleMem(bodyId,header){
  const body=document.getElementById(bodyId);
  if(!body)return;
  body.classList.toggle('open');
  header.classList.toggle('open');
}

function openAddForMember(memberId){
  openAdd();
  setTimeout(()=>{
    const sel=document.getElementById('f-mem');
    if(sel) sel.value=memberId;
  },100);
}

function renderDonut(){
  const svg=document.getElementById('dsvg');
  document.getElementById('d-num').textContent=P.length;
  svg.querySelectorAll('.ds').forEach(e=>e.remove());
  const lg=document.getElementById('d-leg');
  if(!P.length){lg.innerHTML='<span style="color:var(--g400);font-size:12px">ยังไม่มีข้อมูล</span>';return;}
  const cnt={};P.forEach(p=>{cnt[p.type]=(cnt[p.type]||0)+1;});
  const tot=P.length,r=38,ci=2*Math.PI*r;let off=0;
  Object.entries(cnt).forEach(([t,n])=>{
    const c=TC[t]||TC.other,pc=n/tot,d=pc*ci;
    const el=document.createElementNS('http://www.w3.org/2000/svg','circle');
    el.setAttribute('class','ds');el.setAttribute('cx',50);el.setAttribute('cy',50);el.setAttribute('r',r);
    el.setAttribute('fill','none');el.setAttribute('stroke',c.c);el.setAttribute('stroke-width',12);
    el.setAttribute('stroke-dasharray',`${d} ${ci-d}`);el.setAttribute('stroke-dashoffset',-(off*ci));
    svg.appendChild(el);off+=pc;
  });
  lg.innerHTML=Object.entries(cnt).map(([t,n])=>{const c=TC[t]||TC.other;return`<div class="dli"><div class="dld" style="background:${c.c}"></div>${c.i} ${c.l} (${n})</div>`;}).join('');
}

function renderExpiry(){
  const el=document.getElementById('exp-list');
  const ex=P.filter(p=>{const d=dl(p.end_date);return d>=0&&d<=90;}).sort((a,b)=>dl(a.end_date)-dl(b.end_date)).slice(0,6);
  if(!ex.length){el.innerHTML='<div style="text-align:center;padding:14px;color:var(--g400);font-size:12px">ไม่มีกรมธรรม์ที่ใกล้หมดอายุ 🎉</div>';return;}
  el.innerHTML=ex.map(p=>{
    const m=getMem(p.member),c=TC[p.type]||TC.other,d=dl(p.end_date);
    const cls=d<=30?'ic':d<=60?'iw':'iok';
    return`<div class="exp-row" onclick="showD('${p.id}')">
      <div class="exp-av2" style="background:${m.color}">${ini(m.name)}</div>
      <div class="exp-inf"><div class="exp-nm">${m.name} — ${p.company||'?'}</div><div class="exp-tp">${c.i} ${c.l}</div></div>
      <div class="exp-d ${cls}">${d}ว.<br><span style="font-size:9px;font-weight:400">${thd(p.end_date)}</span></div>
    </div>`;
  }).join('');
}

function checkAlerts(){
  const ar=document.getElementById('alert-area');if(!ar)return;
  const cr=P.filter(p=>{const d=dl(p.end_date);return d>=0&&d<=30;});
  const wa=P.filter(p=>{const d=dl(p.end_date);return d>30&&d<=60;});
  ar.innerHTML=(cr.length?`<div class="alert a-d">🚨 <div><b>ด่วน!</b> ${cr.length} กรมธรรม์หมดอายุใน 30 วัน</div></div>`:'')
    +(wa.length?`<div class="alert a-w">⚠️ ${wa.length} กรมธรรม์หมดอายุใน 31–60 วัน</div>`:'');
}

// ── POLICIES PAGE ───────────────────────
function setF(el,f){filt=f;document.querySelectorAll('.fc').forEach(c=>c.classList.remove('on'));el.classList.add('on');renderP();}
function setF2(t){filt=t;document.querySelectorAll('.fc').forEach(c=>c.classList.toggle('on',c.dataset.f===t));renderP();}
function getFiltered(){
  const q=(document.getElementById('q')?.value||'').toLowerCase();
  return P.filter(p=>{
    const m=getMem(p.member);
    if(q&&![p.company,p.policy_no,p.plan_name,m.name].join(' ').toLowerCase().includes(q))return false;
    if(filt==='all')return true;
    if(filt==='expiring')return pst(p)==='expiring';
    if(filt==='expired')return pst(p)==='expired';
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
    const sm={active:['sa','คุ้มครองอยู่'],expiring:['se','ใกล้หมดอายุ'],expired:['sx','หมดอายุ']};
    const [dc,sl]=sm[s];
    const fr=(p.driveFiles||[]).length?`<div style="display:flex;gap:4px;flex-wrap:wrap;margin-top:6px">${(p.driveFiles||[]).map(f=>`<a class="fchip" href="${f.webViewLink||'#'}" target="_blank">📎 ${f.name}</a>`).join('')}</div>`:'';
    return`<div class="pcard">
      <div class="pc-top">
        <div class="pc-av" style="background:${m.color}">${ini(m.name)}</div>
        <div class="pc-inf"><div class="pc-nm">${m.name}</div><div class="pc-co">${p.company||'-'}${p.plan_name?' · '+p.plan_name:''}</div></div>
        <span class="badge ${p.type==='health'?'bh':p.type==='accident'?'ba':p.type==='life'?'bl':p.type==='ci'?'bc':'bo2'}">${c.i} ${c.l}</span>
      </div>
      <div class="pc-bot">
        <span class="sdot ${dc}"></span><span>${sl}</span>
        <span>หมด: ${thd(p.end_date)}${s==='expiring'?` <b style="color:var(--warn)">(${d}ว.)</b>`:''}</span>
        ${p.premium?`<span style="color:var(--pri);font-weight:600">${fm(p.premium)}/ปี</span>`:''}
      </div>${fr}
      <div class="pc-act">
        <button class="btn bg bs" onclick="showD('${p.id}')" style="flex:1">👁️ ดู</button>
        <button class="btn bo bs" onclick="editP('${p.id}')">✏️</button>
        <button class="btn bd bs" onclick="delP('${p.id}')">🗑️</button>
      </div>
    </div>`;
  }).join('');
}

// ── POLICY CRUD ─────────────────────────
function openAdd(){
  editId=null;pFiles=[];
  document.getElementById('pm-t').textContent='➕ เพิ่มกรมธรรม์';
  clearF();populateMSel();updUpload();openMod('pm');
}
function clearF(){
  selType='';document.querySelectorAll('.tc2').forEach(c=>c.className='tc2');
  ['f-type','f-co','f-pno','f-plan','f-s','f-e','f-pr','f-sum','f-ben','f-note'].forEach(id=>{const el=document.getElementById(id);if(el)el.value='';});
  document.getElementById('f-mem').value='';document.getElementById('f-freq').value='yearly';
  document.querySelectorAll('.cgrid input').forEach(cb=>cb.checked=false);
  pFiles=[];renderFList();
}
function updUpload(){
  const w=document.getElementById('up-warn'),u=document.getElementById('up-wrap');
  if(w&&u){w.style.display=tok?'none':'flex';u.style.display=tok?'block':'none';}
}
function selT(t){
  selType=t;document.getElementById('f-type').value=t;
  document.querySelectorAll('.tc2').forEach(c=>{c.className='tc2';if(c.dataset.t===t)c.classList.add('t-'+t);});
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
  if(tok&&pFiles.length&&sharedDriveFolderId){
    try{
      const fid=await getMemberFolder(mem);
      for(let i=0;i<pFiles.length;i++){if(pFiles[i].status==='pending'){const r=await upFile(pFiles[i].file,fid,i);if(r)dfs.push(r);}}
    }catch(e){toast('อัพโหลดบางไฟล์ไม่สำเร็จ','warn');}
  }

  const cov=[...document.querySelectorAll('.cgrid input:checked')].map(cb=>cb.value);
  const pol={
    id:editId||uid(),member:mem,type:ty,company:co,
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
    updated_at:new Date().toISOString(),
  };
  if(editId){const i=P.findIndex(p=>p.id===editId);if(i!==-1)P[i]=pol;}
  else P.push(pol);
  saveLocal();closeMod('pm');renderAll();checkAlerts();
  btn.disabled=false;btn.innerHTML='💾 บันทึก';
  toast(editId?'อัพเดทเรียบร้อย ✅':'บันทึกเรียบร้อย ✅','success');
  if(tok&&cfg.sid) push(false);
}
function editP(id){
  const p=P.find(p=>p.id===id);if(!p)return;
  editId=id;pFiles=[];
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
  if(p.coverage)p.coverage.forEach(v=>{const cb=document.querySelector(`.cgrid input[value="${v}"]`);if(cb)cb.checked=true;});
  updUpload();closeMod('dm');openMod('pm');
}
function delP(id){
  if(!confirm('ต้องการลบกรมธรรม์นี้?'))return;
  P=P.filter(p=>p.id!==id);
  saveLocal();renderAll();checkAlerts();closeMod('dm');
  toast('ลบเรียบร้อย','warn');
  if(tok&&cfg.sid) push(false);
}
function showD(id){
  const p=P.find(p=>p.id===id);if(!p)return;
  const m=getMem(p.member),c=TC[p.type]||TC.other,s=pst(p),d=dl(p.end_date);
  const stxt={active:'✅ คุ้มครองอยู่',expiring:'⚠️ ใกล้หมดอายุ',expired:'❌ หมดอายุ'};
  const ftxt={yearly:'รายปี',halfyearly:'ราย 6 เดือน',quarterly:'รายไตรมาส',monthly:'รายเดือน'};
  const ct=(p.coverage||[]).map(cv=>`<div class="ctag">${CL[cv]||cv}</div>`).join('');
  const fh=(p.driveFiles||[]).map(f=>`<div style="display:flex;align-items:center;gap:8px;padding:8px 10px;background:var(--w);border:1px solid var(--g200);border-radius:8px;margin-bottom:6px">
    <span style="font-size:18px">${f.name?.endsWith('.pdf')?'📄':'🖼️'}</span>
    <div style="flex:1;min-width:0"><div style="font-size:12px;font-weight:600;overflow:hidden;text-overflow:ellipsis;white-space:nowrap">${f.name}</div>
    <div style="font-size:11px;color:var(--g500)">Google Drive</div></div>
    <a href="${f.webViewLink||'#'}" target="_blank" class="btn bo bx">เปิด</a>
  </div>`).join('');
  document.getElementById('dm-body').innerHTML=`
  <div class="dthero">
    <div class="dtav" style="background:${m.color}">${ini(m.name)}</div>
    <div><div style="font-size:15px;font-weight:700">${m.name}</div>
    <div style="margin-top:4px"><span class="badge ${p.type==='health'?'bh':p.type==='accident'?'ba':p.type==='life'?'bl':p.type==='ci'?'bc':'bo2'}">${c.i} ${c.l}</span> <span style="font-size:12px;color:var(--g500)">${p.company||''}</span></div></div>
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
      <div class="dtrow"><div class="dtk">ความถี่</div><div class="dtv">${ftxt[p.payment_freq]||'-'}</div></div>
      <div class="dtrow"><div class="dtk">ผู้รับผลประโยชน์</div><div class="dtv">${p.beneficiary||'-'}</div></div>
    </div>
    ${ct?`<div style="padding:10px 12px;background:var(--g50);border-radius:8px"><div class="dtk" style="margin-bottom:6px">ความคุ้มครอง</div><div class="ctags">${ct}</div></div>`:''}
    ${fh?`<div><div class="dtk" style="margin-bottom:6px">📎 ไฟล์แนบ</div>${fh}</div>`:''}
    ${p.notes?`<div class="dtrow"><div class="dtk">หมายเหตุ</div><div class="dtv" style="font-size:12px;font-weight:400">${p.notes}</div></div>`:''}
  </div>`;
  document.getElementById('dm-edit').onclick=()=>editP(id);
  document.getElementById('dm-del').onclick=()=>delP(id);
  openMod('dm');
}

// ── MEMBERS ─────────────────────────────
function openMemMod(){
  document.getElementById('m-nm').value='';
  document.getElementById('m-role').value='ตัวเอง';
  document.getElementById('m-dob').value='';
  document.getElementById('m-col').value=PAL[M.length%PAL.length];
  openMod('mm');
}
function saveM(){
  const nm=document.getElementById('m-nm').value.trim();
  if(!nm){toast('กรุณากรอกชื่อ','error');return;}
  M.push({id:uid(),name:nm,role:document.getElementById('m-role').value,
    dob:document.getElementById('m-dob').value,color:document.getElementById('m-col').value});
  saveLocal();populateMSel();renderMems();renderDash();
  closeMod('mm');toast(`เพิ่ม "${nm}" เรียบร้อย`,'success');
  if(tok&&cfg.sid)push(false);
}
function delMem(id){
  if(!confirm('ลบสมาชิกนี้?'))return;
  M=M.filter(m=>m.id!==id);
  saveLocal();populateMSel();renderMems();renderDash();
  toast('ลบเรียบร้อย','warn');
  if(tok&&cfg.sid)push(false);
}
function renderMems(){
  const el=document.getElementById('mlist');if(!el)return;
  if(!M.length){el.innerHTML='<div class="empty"><div class="empty-i">👨‍👩‍👧‍👦</div><div class="empty-t">ยังไม่มีสมาชิก</div></div>';return;}
  el.innerHTML=M.map(m=>{
    const mp=P.filter(p=>p.member===m.id);
    const age=m.dob?Math.floor((Date.now()-new Date(m.dob))/315576e5):null;
    const tb=[...new Set(mp.map(p=>p.type))].map(t=>{const c=TC[t]||TC.other;return`<div class="mb" style="background:${c.b};color:${c.c}">${c.i} ${c.l}</div>`;}).join('');
    const drv=m.driveFolderId?`<a href="https://drive.google.com/drive/folders/${m.driveFolderId}" target="_blank" class="btn bg bx">📁</a>`:'';
    return`<div class="mitem">
      <div class="mav2" style="background:${m.color}">${ini(m.name)}</div>
      <div class="mi">
        <div class="mi-nm">${m.name}</div>
        <div class="mi-mt">${m.role||''}${age?' · '+age+' ปี':''} · ${mp.length} กรมธรรม์</div>
        <div class="mi-tags">${tb||'<span style="font-size:11px;color:var(--g400)">ยังไม่มีกรมธรรม์</span>'}</div>
      </div>
      <div style="display:flex;flex-direction:column;gap:5px">${drv}<button class="btn bd bx" onclick="delMem('${m.id}')">🗑️</button></div>
    </div>`;
  }).join('');
}

// ── SETTINGS ────────────────────────────
function saveCID(){
  const id=document.getElementById('cid-in').value.trim();
  if(!id){toast('กรุณากรอก Client ID','error');return;}
  cfg.cid=id;saveCfg();toast('บันทึกแล้ว กำลัง Refresh...','success');
  setTimeout(()=>location.reload(),1500);
}
function saveSCfg(){
  cfg.sid=document.getElementById('sid-in').value.trim();
  cfg.sn=document.getElementById('sn-in').value.trim()||'Policies';
  cfg.msn=document.getElementById('msn-in').value.trim()||'Members';
  saveCfg();updateSyncBar();updateAuthUI();
  toast('บันทึกการตั้งค่า Sheet เรียบร้อย','success');
  if(tok&&cfg.sid) pull();
}
function doExport(){
  const H=['สมาชิก','ประเภท','บริษัท','เลขกรมธรรม์','ชื่อแผน','วันเริ่ม','วันหมด','เบี้ย','ทุน','ความคุ้มครอง','ผู้รับ','หมายเหตุ'];
  const rows=P.map(p=>[getMem(p.member).name,(TC[p.type]||TC.other).l,p.company,p.policy_no,p.plan_name,p.start_date,p.end_date,p.premium,p.sum_insured,(p.coverage||[]).map(c=>CL[c]||c).join('; '),p.beneficiary,p.notes]);
  const csv=[H,...rows].map(r=>r.map(c=>'"'+String(c||'').replace(/"/g,'""')+'"').join(',')).join('\n');
  const a=document.createElement('a');
  a.href=URL.createObjectURL(new Blob(['\uFEFF'+csv],{type:'text/csv;charset=utf-8;'}));
  a.download=`insurance_${new Date().toISOString().slice(0,10)}.csv`;a.click();
  toast('Export CSV เรียบร้อย','success');
}
function clearAll(){
  if(!confirm('ล้างข้อมูลในเครื่องนี้?'))return;
  P=[];M=[{id:uid(),name:'ฉัน (ตัวเอง)',role:'ตัวเอง',color:'#1a73e8',dob:''}];
  saveLocal();populateMSel();renderAll();toast('ล้างข้อมูลเรียบร้อย','warn');
}

// ── FILES ────────────────────────────────
function onPick(e){addF([...e.target.files]);e.target.value='';}
function onDrop(e){e.preventDefault();addF([...e.dataTransfer.files]);}
function addF(fs){
  fs.forEach(f=>{
    if(f.size>20*1024*1024){toast(`"${f.name}" ใหญ่เกิน 20MB`,'error');return;}
    if(!pFiles.find(x=>x.file.name===f.name&&x.file.size===f.size))pFiles.push({file:f,status:'pending'});
  });renderFList();
}
function removeF(i){pFiles.splice(i,1);renderFList();}
function renderFList(){
  const el=document.getElementById('flist2');if(!el)return;
  el.innerHTML=pFiles.map((pf,i)=>{
    const ic=pf.file.name.endsWith('.pdf')?'📄':'🖼️';
    const sz=(pf.file.size/1024).toFixed(0)+' KB';
    const st=pf.status==='done'?'✅':pf.status==='uploading'?'⏳':pf.status==='error'?'❌':'📌';
    return`<div class="fitem"><span style="font-size:16px">${ic}</span><div class="fitem-nm">${pf.file.name}</div>
      <span style="font-size:11px;color:var(--g500);flex-shrink:0">${sz}</span><span>${st}</span>
      ${pf.status==='pending'?`<button onclick="removeF(${i})" style="background:none;border:none;cursor:pointer;color:var(--g400);font-size:16px;padding:2px">✕</button>`:''}</div>`;
  }).join('');
}

// ── MODAL ────────────────────────────────
function openMod(id){document.getElementById(id).classList.add('on');}
function closeMod(id){document.getElementById(id).classList.remove('on');}
document.querySelectorAll('.mover').forEach(o=>o.addEventListener('click',e=>{if(e.target===o)o.classList.remove('on');}));
document.querySelectorAll('.modal').forEach(modal=>{
  let sy=0;
  modal.addEventListener('touchstart',e=>{sy=e.touches[0].clientY;},{passive:true});
  modal.addEventListener('touchend',e=>{if(e.changedTouches[0].clientY-sy>80&&modal.scrollTop===0)modal.closest('.mover').classList.remove('on');},{passive:true});
});

// ── TOAST ────────────────────────────────
function toast(msg,type=''){
  const c=document.getElementById('twrap');
  const t=document.createElement('div');
  t.className='toast'+(type?(' t-'+({success:'ok',error:'err',warn:'wn'}[type]||type)):'');
  t.innerHTML=(type==='success'?'✅ ':type==='error'?'❌ ':type==='warn'?'⚠️ ':'ℹ️ ')+msg;
  c.appendChild(t);
  setTimeout(()=>{t.style.cssText='opacity:0;transform:translateY(6px);transition:all .3s';setTimeout(()=>t.remove(),300);},3200);
}

// ═══════════════════════════════════════
//  START
// ═══════════════════════════════════════
document.addEventListener('DOMContentLoaded',()=>{
  boot();       // แสดง App ทันที ไม่รอ Google
  tryGIS();     // init GIS แบบ non-blocking
});
</script>
</body>
</html>
