#Wandee
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
  --primary:#1a73e8; --primary-dark:#1557b0; --primary-light:#e8f0fe;
  --success:#34a853; --success-light:#e6f4ea;
  --warning:#fbbc04; --warning-light:#fef9e7;
  --danger:#ea4335; --danger-light:#fce8e6;
  --purple:#9c27b0; --purple-light:#f3e5f5;
  --orange:#ff6d00; --orange-light:#fff3e0;
  --g50:#f8f9fa; --g100:#f1f3f4; --g200:#e8eaed; --g300:#dadce0;
  --g400:#bdc1c6; --g500:#9aa0a6; --g600:#80868b; --g700:#5f6368;
  --g800:#3c4043; --g900:#202124; --white:#fff;
  --sh-sm:0 1px 3px rgba(0,0,0,.08); --sh:0 4px 12px rgba(0,0,0,.08);
  --sh-lg:0 8px 24px rgba(0,0,0,.1);
  --r:12px; --r-sm:8px; --r-lg:16px;
  --ease:all .2s cubic-bezier(.4,0,.2,1);
  --safe-top: env(safe-area-inset-top);
  --safe-bottom: env(safe-area-inset-bottom);
  --safe-left: env(safe-area-inset-left);
  --safe-right: env(safe-area-inset-right);
}
*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html{height:100%}
body{
  font-family:-apple-system,BlinkMacSystemFont,'Segoe UI','Noto Sans Thai',sans-serif;
  background:var(--g50);color:var(--g900);min-height:100vh;font-size:14px;
  line-height:1.5;-webkit-font-smoothing:antialiased;overflow-x:hidden;
}

/* ── BOTTOM NAV (Mobile) ── */
.bottom-nav{
  display:none;position:fixed;bottom:0;left:0;right:0;z-index:200;
  background:var(--white);border-top:1px solid var(--g200);
  padding:8px 0 calc(8px + var(--safe-bottom));
  display:none;grid-template-columns:repeat(5,1fr);
}
.bn-item{
  display:flex;flex-direction:column;align-items:center;gap:3px;
  padding:6px 4px;cursor:pointer;border:none;background:none;
  color:var(--g500);transition:var(--ease);position:relative;
  font-size:10px;font-weight:500;min-height:44px;justify-content:center;
}
.bn-item.active{color:var(--primary)}
.bn-item .bn-icon{font-size:20px;line-height:1}
.bn-badge{
  position:absolute;top:4px;right:calc(50% - 18px);
  background:var(--danger);color:white;border-radius:10px;
  font-size:9px;font-weight:700;padding:1px 5px;min-width:16px;text-align:center;
}

/* ── SIDEBAR (Desktop) ── */
.sidebar{
  position:fixed;left:0;top:0;bottom:0;width:240px;background:var(--white);
  border-right:1px solid var(--g200);display:flex;flex-direction:column;
  z-index:100;box-shadow:var(--sh-sm);transition:transform .3s;
}
.sidebar-brand{
  display:flex;align-items:center;gap:10px;
  padding:20px 20px 16px;border-bottom:1px solid var(--g100);
}
.brand-icon{
  width:36px;height:36px;border-radius:10px;flex-shrink:0;
  background:linear-gradient(135deg,var(--primary),#4285f4);
  display:flex;align-items:center;justify-content:center;font-size:18px;
}
.brand-text{font-size:14px;font-weight:700;line-height:1.2}
.brand-sub{font-size:11px;color:var(--g500)}
.sidebar-nav{flex:1;padding:12px 0;overflow-y:auto}
.nav-label{font-size:10px;font-weight:700;color:var(--g400);text-transform:uppercase;
  letter-spacing:.8px;padding:4px 20px 8px;margin-top:4px}
.nav-item{
  display:flex;align-items:center;gap:10px;padding:10px 20px;cursor:pointer;
  border-radius:0 24px 24px 0;margin:1px 8px 1px 0;color:var(--g700);
  font-size:13.5px;font-weight:500;transition:var(--ease);
}
.nav-item:hover{background:var(--g100)}
.nav-item.active{background:var(--primary-light);color:var(--primary)}
.nav-icon{font-size:16px;width:20px;text-align:center;flex-shrink:0}
.nav-badge{
  margin-left:auto;font-size:11px;font-weight:600;background:var(--danger);
  color:white;border-radius:10px;padding:1px 6px;min-width:18px;text-align:center;
}
.sidebar-footer{padding:12px;border-top:1px solid var(--g100)}
.sidebar-overlay{
  display:none;position:fixed;inset:0;background:rgba(0,0,0,.4);
  z-index:99;backdrop-filter:blur(2px);
}

/* ── MAIN ── */
.main{margin-left:240px;min-height:100vh;display:flex;flex-direction:column}
.topbar{
  background:var(--white);border-bottom:1px solid var(--g200);
  padding:0 24px;height:60px;display:flex;align-items:center;gap:12px;
  position:sticky;top:0;z-index:50;box-shadow:var(--sh-sm);
}
.topbar-menu-btn{
  display:none;width:40px;height:40px;border-radius:8px;border:none;
  background:transparent;cursor:pointer;font-size:20px;align-items:center;justify-content:center;
}
.topbar-title{font-size:17px;font-weight:700;flex:1}
.topbar-actions{display:flex;gap:8px;align-items:center}

/* ── BUTTONS ── */
.btn{
  display:inline-flex;align-items:center;justify-content:center;gap:6px;
  padding:10px 18px;border-radius:10px;border:none;font-size:13px;font-weight:600;
  cursor:pointer;transition:var(--ease);white-space:nowrap;
  min-height:44px; /* iOS min touch target */
  font-family:inherit;
}
.btn-primary{background:var(--primary);color:white}
.btn-primary:hover{background:var(--primary-dark)}
.btn-primary:active{transform:scale(.97)}
.btn-primary:disabled{background:var(--g300);cursor:not-allowed}
.btn-outline{background:transparent;color:var(--primary);border:1.5px solid var(--primary)}
.btn-outline:hover{background:var(--primary-light)}
.btn-ghost{background:transparent;color:var(--g700);border:1.5px solid var(--g200)}
.btn-ghost:hover{background:var(--g100)}
.btn-danger{background:var(--danger);color:white}
.btn-success{background:var(--success);color:white}
.btn-sm{padding:8px 14px;font-size:12px;min-height:36px;border-radius:8px}
.btn-xs{padding:5px 10px;font-size:11px;min-height:30px;border-radius:6px}
.btn-icon{padding:10px;min-width:44px;width:44px}

/* ── PAGES ── */
.page{display:none;flex:1;padding:20px 20px 24px}
.page.active{display:block}

/* ── GOOGLE AUTH ── */
.gauth-btn{
  display:flex;align-items:center;gap:8px;padding:10px 12px;border-radius:var(--r-sm);
  background:var(--white);color:var(--g800);cursor:pointer;border:1.5px solid var(--g200);
  width:100%;font-size:12.5px;font-weight:500;transition:var(--ease);font-family:inherit;
}
.gauth-btn:hover{background:var(--g50)}
.gauth-btn.signed-in{background:var(--success-light);border-color:var(--success);color:var(--success)}
.gauth-avatar{width:22px;height:22px;border-radius:50%;object-fit:cover}
.gauth-info{display:flex;flex-direction:column;text-align:left;flex:1;overflow:hidden}
.gauth-name{font-size:12px;font-weight:600;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.gauth-email{font-size:10px;color:var(--g500);white-space:nowrap;overflow:hidden;text-overflow:ellipsis}

/* ── MOBILE AUTH CARD ── */
.mobile-auth-card{
  background:linear-gradient(135deg,#1a73e8,#4285f4);
  border-radius:var(--r);padding:16px;margin-bottom:16px;color:white;
}
.mobile-auth-card-title{font-size:14px;font-weight:700;margin-bottom:4px}
.mobile-auth-card-desc{font-size:12px;opacity:.85;margin-bottom:12px}
.mobile-auth-card-btn{
  background:white;color:var(--primary);border:none;padding:10px 16px;
  border-radius:8px;font-size:13px;font-weight:700;cursor:pointer;
  display:inline-flex;align-items:center;gap:6px;min-height:44px;font-family:inherit;
}
.mobile-auth-signed{
  background:var(--success-light);border:1px solid var(--success);
  border-radius:var(--r);padding:12px 14px;margin-bottom:16px;
  display:flex;align-items:center;gap:10px;font-size:13px;
}

/* ── STATS ── */
.stats-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:12px;margin-bottom:16px}
.stat-card{
  background:var(--white);border-radius:var(--r);padding:14px 16px;
  box-shadow:var(--sh-sm);border:1px solid var(--g100);
  display:flex;align-items:center;gap:12px;
}
.stat-icon{width:40px;height:40px;border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:18px;flex-shrink:0}
.stat-value{font-size:22px;font-weight:700;line-height:1}
.stat-label{font-size:11px;color:var(--g500);margin-top:2px}

/* ── CHART CARDS ── */
.chart-card{
  background:var(--white);border-radius:var(--r);padding:16px;
  box-shadow:var(--sh-sm);border:1px solid var(--g100);margin-bottom:16px;
}
.card-title{font-size:14px;font-weight:600;color:var(--g800);margin-bottom:12px}
.card-subtitle{font-size:12px;color:var(--g500);margin-top:-8px;margin-bottom:12px}

/* ── DONUT ── */
.donut-wrap{position:relative;width:120px;height:120px;margin:0 auto 10px;flex-shrink:0}
.donut-center{position:absolute;inset:0;display:flex;flex-direction:column;align-items:center;justify-content:center}
.donut-num{font-size:22px;font-weight:700;line-height:1}
.donut-lbl{font-size:10px;color:var(--g500)}
svg.donut{transform:rotate(-90deg)}
.donut-row{display:flex;align-items:center;gap:16px}
.donut-legend{display:flex;flex-direction:column;gap:6px;flex:1}
.legend-item{display:flex;align-items:center;gap:6px;font-size:12px;color:var(--g700)}
.legend-dot{width:8px;height:8px;border-radius:50%;flex-shrink:0}

/* ── MEMBER BARS ── */
.member-bars{display:flex;flex-direction:column;gap:10px}
.member-bar-row{display:flex;align-items:center;gap:8px}
.bar-track{flex:1;height:18px;background:var(--g100);border-radius:100px;overflow:hidden;display:flex;gap:1px}
.bar-seg{height:100%;transition:width .4s}
.bar-count{font-size:12px;color:var(--g500);width:20px;text-align:right;flex-shrink:0}

/* ── EXPIRY ── */
.expiry-list{display:flex;flex-direction:column;gap:8px}
.expiry-item{
  display:flex;align-items:center;gap:10px;padding:10px 12px;
  border-radius:var(--r-sm);background:var(--g50);border:1px solid var(--g100);cursor:pointer;
}
.expiry-avatar{width:34px;height:34px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:13px;font-weight:700;color:white;flex-shrink:0}
.expiry-info{flex:1;min-width:0}
.expiry-name{font-size:13px;font-weight:600;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.expiry-type{font-size:11px;color:var(--g500)}
.expiry-days{font-size:12px;font-weight:700;padding:4px 8px;border-radius:6px;flex-shrink:0;text-align:center;white-space:nowrap}
.days-critical{background:var(--danger-light);color:var(--danger)}
.days-warning{background:var(--warning-light);color:#c77a00}
.days-ok{background:var(--success-light);color:var(--success)}

/* ── POLICY CARDS (Mobile list) ── */
.policy-list{display:flex;flex-direction:column;gap:10px}
.policy-card{
  background:var(--white);border-radius:var(--r);padding:14px 16px;
  box-shadow:var(--sh-sm);border:1px solid var(--g100);cursor:pointer;
  transition:var(--ease);
}
.policy-card:active{transform:scale(.98)}
.policy-card-top{display:flex;align-items:flex-start;gap:10px;margin-bottom:8px}
.policy-card-avatar{width:36px;height:36px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:14px;font-weight:700;color:white;flex-shrink:0}
.policy-card-info{flex:1;min-width:0}
.policy-card-name{font-size:14px;font-weight:700;color:var(--g900)}
.policy-card-company{font-size:12px;color:var(--g500)}
.policy-card-bottom{display:flex;align-items:center;gap:8px;flex-wrap:wrap}
.policy-card-date{font-size:11px;color:var(--g600)}
.policy-card-premium{font-size:12px;font-weight:600;color:var(--primary)}
.pc-actions{display:flex;gap:6px;margin-top:10px;padding-top:10px;border-top:1px solid var(--g100)}

/* ── FILTER BAR ── */
.filter-bar{display:flex;gap:8px;margin-bottom:14px;overflow-x:auto;padding-bottom:4px;-webkit-overflow-scrolling:touch}
.filter-bar::-webkit-scrollbar{display:none}
.filter-chip{
  display:inline-flex;align-items:center;gap:5px;padding:8px 14px;
  border-radius:100px;border:1.5px solid var(--g200);background:var(--white);
  font-size:12px;font-weight:500;color:var(--g700);cursor:pointer;
  white-space:nowrap;flex-shrink:0;transition:var(--ease);min-height:36px;
}
.filter-chip.active{background:var(--primary-light);border-color:var(--primary);color:var(--primary)}
.search-wrap{
  display:flex;align-items:center;gap:8px;background:var(--white);
  border:1.5px solid var(--g200);border-radius:10px;padding:10px 14px;
  margin-bottom:12px;
}
.search-wrap:focus-within{border-color:var(--primary);box-shadow:0 0 0 3px rgba(26,115,232,.1)}
.search-wrap input{border:none;outline:none;font-size:14px;background:transparent;width:100%;color:var(--g900);font-family:inherit}

/* ── BADGES ── */
.badge{display:inline-flex;align-items:center;gap:3px;padding:3px 8px;border-radius:100px;font-size:11px;font-weight:600}
.badge-health{background:var(--success-light);color:var(--success)}
.badge-accident{background:var(--warning-light);color:#c77a00}
.badge-life{background:var(--purple-light);color:var(--purple)}
.badge-ci{background:var(--orange-light);color:var(--orange)}
.badge-other{background:var(--g100);color:var(--g700)}
.status-dot{width:7px;height:7px;border-radius:50%;display:inline-block;margin-right:3px}
.status-active{background:var(--success)}
.status-expiring{background:var(--warning)}
.status-expired{background:var(--danger)}

/* ── FILE CHIP ── */
.file-chip{
  display:inline-flex;align-items:center;gap:4px;padding:4px 8px;
  background:var(--primary-light);color:var(--primary);border-radius:6px;
  font-size:11px;font-weight:500;text-decoration:none;max-width:130px;
  white-space:nowrap;overflow:hidden;text-overflow:ellipsis;
}

/* ── UPLOAD AREA ── */
.upload-area{
  border:2px dashed var(--g300);border-radius:var(--r-sm);padding:20px;
  text-align:center;cursor:pointer;background:var(--g50);min-height:80px;
  display:flex;flex-direction:column;align-items:center;justify-content:center;gap:6px;
}
.upload-area input{display:none}
.file-list{display:flex;flex-direction:column;gap:6px;margin-top:10px}
.file-item{
  display:flex;align-items:center;gap:8px;padding:8px 10px;
  background:var(--white);border:1px solid var(--g200);border-radius:var(--r-sm);
}
.file-item-name{flex:1;font-size:12px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.file-item-size{font-size:11px;color:var(--g500);flex-shrink:0}

/* ── ALERT ── */
.alert{
  display:flex;align-items:flex-start;gap:10px;padding:12px 14px;
  border-radius:var(--r-sm);margin-bottom:12px;border:1px solid;font-size:13px;
}
.alert-danger{background:var(--danger-light);border-color:#f5c6c3;color:#c62828}
.alert-warning{background:var(--warning-light);border-color:#f5e0a0;color:#b06000}
.alert-info{background:var(--primary-light);border-color:#b3cef5;color:var(--primary-dark)}
.alert-success{background:var(--success-light);border-color:#a8d8b2;color:#1e6e37}

/* ── MODAL ── */
.modal-overlay{
  display:none;position:fixed;inset:0;background:rgba(0,0,0,.5);
  z-index:500;align-items:flex-end;justify-content:center;
  backdrop-filter:blur(3px);
}
.modal-overlay.open{display:flex;animation:fadeIn .15s}
@keyframes fadeIn{from{opacity:0}}
.modal{
  background:var(--white);border-radius:var(--r-lg) var(--r-lg) 0 0;
  width:100%;max-height:92vh;overflow-y:auto;
  animation:slideUp .25s cubic-bezier(.4,0,.2,1);
  padding-bottom:calc(env(safe-area-inset-bottom));
}
@keyframes slideUp{from{transform:translateY(100%)}}
.modal-handle{
  width:36px;height:4px;background:var(--g300);border-radius:2px;
  margin:10px auto 0;
}
.modal-header{
  display:flex;align-items:center;justify-content:space-between;
  padding:16px 20px 14px;border-bottom:1px solid var(--g100);
  position:sticky;top:0;background:var(--white);z-index:1;
}
.modal-title{font-size:16px;font-weight:700}
.modal-close{
  width:36px;height:36px;border-radius:50%;border:none;background:var(--g100);
  cursor:pointer;font-size:16px;display:flex;align-items:center;justify-content:center;
  color:var(--g600);
}
.modal-body{padding:16px 20px}
.modal-footer{
  display:flex;gap:10px;padding:14px 20px;border-top:1px solid var(--g100);
  position:sticky;bottom:0;background:var(--white);
  padding-bottom:calc(14px + env(safe-area-inset-bottom));
}

/* ── FORM ── */
.form-group{display:flex;flex-direction:column;gap:6px;margin-bottom:14px}
label.form-label{font-size:12px;font-weight:600;color:var(--g700)}
.form-label span.req{color:var(--danger);margin-left:2px}
input.form-input,select.form-input,textarea.form-input{
  background:var(--white);border:1.5px solid var(--g200);border-radius:var(--r-sm);
  padding:12px 14px;font-size:16px; /* 16px prevents iOS zoom */
  color:var(--g900);transition:var(--ease);outline:none;width:100%;font-family:inherit;
  -webkit-appearance:none;appearance:none;
}
input.form-input:focus,select.form-input:focus,textarea.form-input:focus{
  border-color:var(--primary);box-shadow:0 0 0 3px rgba(26,115,232,.1);
}
textarea.form-input{resize:vertical;min-height:72px}
select.form-input{
  background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='8' viewBox='0 0 12 8'%3E%3Cpath d='M1 1l5 5 5-5' stroke='%239aa0a6' stroke-width='1.5' fill='none' stroke-linecap='round'/%3E%3C/svg%3E");
  background-repeat:no-repeat;background-position:right 14px center;padding-right:36px;
}
.form-row{display:grid;grid-template-columns:1fr 1fr;gap:12px}
.form-divider{border:none;border-top:1px solid var(--g100);margin:8px 0 14px}
.form-section-title{font-size:11px;font-weight:700;color:var(--g500);text-transform:uppercase;letter-spacing:.5px;margin-bottom:10px}

/* ── TYPE SELECTOR ── */
.type-selector{display:grid;grid-template-columns:repeat(3,1fr);gap:8px}
.type-chip{
  display:flex;flex-direction:column;align-items:center;gap:4px;
  padding:10px 8px;border-radius:10px;cursor:pointer;
  border:1.5px solid var(--g200);background:var(--white);
  font-size:11px;font-weight:600;color:var(--g600);transition:var(--ease);
  min-height:60px;justify-content:center;
}
.type-chip-icon{font-size:20px}
.type-chip.sel-health{border-color:var(--success);background:var(--success-light);color:var(--success)}
.type-chip.sel-accident{border-color:var(--warning);background:var(--warning-light);color:#c77a00}
.type-chip.sel-life{border-color:var(--purple);background:var(--purple-light);color:var(--purple)}
.type-chip.sel-ci{border-color:var(--orange);background:var(--orange-light);color:var(--orange)}
.type-chip.sel-other{border-color:var(--primary);background:var(--primary-light);color:var(--primary)}

/* ── COVERAGE GRID ── */
.coverage-grid{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.coverage-check{
  display:flex;align-items:center;gap:8px;padding:8px 10px;
  border:1.5px solid var(--g200);border-radius:8px;cursor:pointer;
  font-size:12.5px;color:var(--g700);transition:var(--ease);
}
.coverage-check input{
  width:16px;height:16px;cursor:pointer;accent-color:var(--primary);flex-shrink:0;
}
.coverage-check:has(input:checked){border-color:var(--primary);background:var(--primary-light);color:var(--primary)}

/* ── DETAIL VIEW ── */
.detail-hero{
  background:var(--g50);border-radius:var(--r-sm);padding:14px;margin-bottom:14px;
  display:flex;align-items:center;gap:12px;
}
.detail-avatar{width:48px;height:48px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:20px;font-weight:700;color:white;flex-shrink:0}
.detail-rows{display:flex;flex-direction:column;gap:10px}
.detail-row{display:flex;flex-direction:column;gap:3px;padding:10px 12px;background:var(--g50);border-radius:8px}
.detail-key{font-size:11px;font-weight:600;color:var(--g500);text-transform:uppercase;letter-spacing:.4px}
.detail-val{font-size:14px;font-weight:600;color:var(--g900)}
.detail-2col{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.coverage-tags{display:flex;flex-wrap:wrap;gap:5px;margin-top:6px}
.coverage-tag{background:var(--primary-light);color:var(--primary);font-size:11px;font-weight:500;padding:3px 7px;border-radius:5px}

/* ── MEMBER PAGE ── */
.members-list{display:flex;flex-direction:column;gap:10px}
.member-item{
  background:var(--white);border-radius:var(--r);padding:14px 16px;
  box-shadow:var(--sh-sm);border:1px solid var(--g100);
  display:flex;align-items:center;gap:12px;
}
.member-avatar{width:44px;height:44px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:17px;font-weight:700;color:white;flex-shrink:0}
.member-info{flex:1;min-width:0}
.member-name{font-size:14px;font-weight:700}
.member-meta{font-size:12px;color:var(--g500);margin-top:2px}
.member-tags{display:flex;gap:4px;flex-wrap:wrap;margin-top:6px}
.mini-badge{padding:2px 6px;border-radius:4px;font-size:10px;font-weight:600}

/* ── SETTINGS ── */
.config-card{
  background:var(--white);border-radius:var(--r);padding:16px;
  box-shadow:var(--sh-sm);border:1px solid var(--g100);margin-bottom:14px;
}
.config-title{font-size:14px;font-weight:700;margin-bottom:4px}
.config-desc{font-size:12px;color:var(--g500);margin-bottom:14px}
.step-list{list-style:none;counter-reset:step}
.step-list li{
  counter-increment:step;padding:8px 0 8px 34px;position:relative;
  font-size:13px;color:var(--g700);border-bottom:1px solid var(--g100);
}
.step-list li:last-child{border-bottom:none}
.step-list li::before{
  content:counter(step);position:absolute;left:0;top:8px;
  width:22px;height:22px;background:var(--primary);color:white;
  border-radius:50%;font-size:11px;font-weight:700;
  display:flex;align-items:center;justify-content:center;
}
.code-block{
  background:var(--g900);color:#a8d8a8;padding:10px 12px;border-radius:var(--r-sm);
  font-size:11px;font-family:'Menlo','Consolas',monospace;overflow-x:auto;
  line-height:1.7;margin:8px 0;word-break:break-all;
}
.sync-row{display:flex;align-items:center;gap:8px;padding:10px 12px;background:var(--g50);border-radius:8px;border:1px solid var(--g200);font-size:13px}
.sync-dot{width:8px;height:8px;border-radius:50%;flex-shrink:0}
.sync-active{background:var(--success);animation:pulse 2s infinite}
.sync-inactive{background:var(--g400)}
@keyframes pulse{0%,100%{opacity:1}50%{opacity:.4}}

/* ── DRIVE FOLDER CARD ── */
.drive-folder-card{
  background:linear-gradient(135deg,#1a73e8,#4285f4);color:white;
  border-radius:var(--r);padding:14px 16px;display:flex;align-items:center;gap:12px;
  margin-bottom:12px;text-decoration:none;
}
.attached-file{
  display:flex;align-items:center;gap:8px;padding:8px 10px;
  background:var(--white);border:1px solid var(--g200);border-radius:8px;margin-bottom:6px;
}
.attached-file-info{flex:1;min-width:0}
.attached-file-name{font-size:12.5px;font-weight:600;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.attached-file-meta{font-size:11px;color:var(--g500)}

/* ── TOAST ── */
.toast-container{position:fixed;bottom:calc(80px + var(--safe-bottom));right:16px;left:16px;z-index:999;display:flex;flex-direction:column;gap:8px;pointer-events:none}
.toast{
  background:var(--g900);color:white;padding:12px 14px;border-radius:10px;
  font-size:13px;display:flex;align-items:center;gap:8px;
  box-shadow:var(--sh-lg);animation:toastIn .3s;pointer-events:all;
}
@keyframes toastIn{from{transform:translateY(20px);opacity:0}}
.toast-success{background:var(--success)}
.toast-error{background:var(--danger)}
.toast-warn{background:#c77a00}

/* ── SPINNER ── */
.spinner{width:16px;height:16px;border:2px solid rgba(255,255,255,.3);border-top-color:white;border-radius:50%;animation:spin .6s linear infinite;flex-shrink:0}
.spinner-dark{border-color:rgba(26,115,232,.2);border-top-color:var(--primary)}
@keyframes spin{to{transform:rotate(360deg)}}

/* ── EMPTY STATE ── */
.empty-state{text-align:center;padding:48px 24px}
.empty-icon{font-size:44px;margin-bottom:12px;opacity:.4}
.empty-title{font-size:15px;font-weight:600;color:var(--g700);margin-bottom:6px}
.empty-desc{font-size:12px;color:var(--g500);max-width:280px;margin:0 auto 16px}

/* ── SCROLLBAR ── */
::-webkit-scrollbar{width:4px;height:4px}
::-webkit-scrollbar-thumb{background:var(--g300);border-radius:2px}

/* ═══════════════════════════════
   RESPONSIVE BREAKPOINTS
═══════════════════════════════ */

/* ── Tablet (768px+) ── */
@media (min-width:768px){
  .stats-grid{grid-template-columns:repeat(4,1fr)}
  .form-row{grid-template-columns:1fr 1fr}
  .modal{border-radius:var(--r-lg);max-width:600px;margin:auto;animation:modalIn .2s}
  @keyframes modalIn{from{transform:scale(.95);opacity:0}}
  .modal-handle{display:none}
  .modal-overlay{align-items:center}
  .coverage-grid{grid-template-columns:repeat(3,1fr)}
  .type-selector{grid-template-columns:repeat(5,1fr)}
  .detail-2col{grid-template-columns:1fr 1fr}
  .members-list{display:grid;grid-template-columns:repeat(2,1fr)}
}

/* ── Desktop (1024px+) ── */
@media (min-width:1024px){
  .bottom-nav{display:none!important}
  .topbar-menu-btn{display:none!important}
  .sidebar{transform:translateX(0)!important}
  .main{margin-left:240px}
  .topbar{padding:0 28px}
  .page{padding:24px 28px}
  .stats-grid{grid-template-columns:repeat(4,1fr);gap:16px}
  .toast-container{left:auto;width:320px;bottom:24px}
}

/* ── Mobile only (< 768px) ── */
@media (max-width:767px){
  .sidebar{transform:translateX(-100%);width:280px}
  .sidebar.open{transform:translateX(0)}
  .sidebar-overlay.open{display:block}
  .topbar-menu-btn{display:flex}
  .main{margin-left:0}
  .page{padding:14px 14px calc(80px + var(--safe-bottom)) 14px}
  .bottom-nav{display:grid}
  .topbar{height:54px;padding:0 14px;padding-left:calc(14px + var(--safe-left));padding-right:calc(14px + var(--safe-right))}
  .topbar-title{font-size:15px}
  .btn-primary .btn-label-long{display:none}
  .modal-footer{flex-direction:column}
  .modal-footer .btn{width:100%}
}
</style>
</head>
<body>

<!-- SIDEBAR OVERLAY -->
<div class="sidebar-overlay" id="sidebar-overlay" onclick="closeSidebar()"></div>

<!-- SIDEBAR -->
<aside class="sidebar" id="sidebar">
  <div class="sidebar-brand">
    <div class="brand-icon">🛡️</div>
    <div><div class="brand-text">Insurance Manager</div><div class="brand-sub">Family Policy Tracker</div></div>
  </div>
  <nav class="sidebar-nav">
    <div class="nav-label">ภาพรวม</div>
    <div class="nav-item active" onclick="navigate('dashboard');closeSidebar()"><span class="nav-icon">📊</span>Dashboard</div>
    <div class="nav-item" onclick="navigate('policies');closeSidebar()">
      <span class="nav-icon">📋</span>กรมธรรม์ทั้งหมด
      <span class="nav-badge" id="expiring-count-side" style="display:none">0</span>
    </div>
    <div class="nav-label" style="margin-top:8px">ประเภทประกัน</div>
    <div class="nav-item" onclick="navigate('policies');setTypeFilter('health');closeSidebar()"><span class="nav-icon">❤️‍🩹</span>ประกันสุขภาพ</div>
    <div class="nav-item" onclick="navigate('policies');setTypeFilter('accident');closeSidebar()"><span class="nav-icon">⚡</span>ประกันอุบัติเหตุ</div>
    <div class="nav-item" onclick="navigate('policies');setTypeFilter('life');closeSidebar()"><span class="nav-icon">🌿</span>ประกันชีวิต</div>
    <div class="nav-item" onclick="navigate('policies');setTypeFilter('ci');closeSidebar()"><span class="nav-icon">🏥</span>โรคร้ายแรง</div>
    <div class="nav-label" style="margin-top:8px">จัดการ</div>
    <div class="nav-item" onclick="navigate('members');closeSidebar()"><span class="nav-icon">👨‍👩‍👧‍👦</span>สมาชิกครอบครัว</div>
    <div class="nav-item" onclick="navigate('settings');closeSidebar()"><span class="nav-icon">⚙️</span>ตั้งค่า Google</div>
  </nav>
  <div class="sidebar-footer">
    <div id="sidebar-auth-area">
      <button class="gauth-btn" onclick="handleSignIn()">
        <span style="font-size:16px">🔐</span>
        <div class="gauth-info"><div class="gauth-name">เข้าสู่ระบบ Google</div><div class="gauth-email">Sheets & Drive</div></div>
      </button>
    </div>
  </div>
</aside>

<!-- MAIN -->
<div class="main">
  <!-- TOPBAR -->
  <div class="topbar">
    <button class="topbar-menu-btn" onclick="openSidebar()">☰</button>
    <div class="topbar-title" id="page-title">📊 Dashboard</div>
    <div class="topbar-actions">
      <div id="sync-indicator" style="display:none;align-items:center;gap:6px;font-size:12px;color:var(--g600)">
        <div class="spinner spinner-dark"></div>
      </div>
      <button class="btn btn-primary btn-sm" onclick="openAddModal()">
        <span>＋</span><span class="btn-label-long">เพิ่มกรมธรรม์</span>
      </button>
    </div>
  </div>

  <!-- ══ DASHBOARD ══ -->
  <div class="page active" id="page-dashboard">
    <div id="alert-area"></div>
    <div id="mobile-auth-area"></div>
    <div class="stats-grid">
      <div class="stat-card"><div class="stat-icon" style="background:#e8f0fe">📋</div><div><div class="stat-value" id="s-total">0</div><div class="stat-label">กรมธรรม์</div></div></div>
      <div class="stat-card"><div class="stat-icon" style="background:#e6f4ea">✅</div><div><div class="stat-value" id="s-active" style="color:var(--success)">0</div><div class="stat-label">คุ้มครองอยู่</div></div></div>
      <div class="stat-card"><div class="stat-icon" style="background:#fef9e7">⚠️</div><div><div class="stat-value" id="s-expiring" style="color:#c77a00">0</div><div class="stat-label">ใกล้หมดอายุ</div></div></div>
      <div class="stat-card"><div class="stat-icon" style="background:#fce8e6">💰</div><div><div class="stat-value" id="s-premium" style="color:var(--primary);font-size:18px">-</div><div class="stat-label">เบี้ยรวม/ปี ฿</div></div></div>
    </div>
    <div class="chart-card">
      <div class="card-title">สัดส่วนประเภทประกัน</div>
      <div class="donut-row">
        <div class="donut-wrap">
          <svg class="donut" id="donut-svg" width="120" height="120" viewBox="0 0 120 120">
            <circle cx="60" cy="60" r="46" fill="none" stroke="#e8eaed" stroke-width="14"/>
          </svg>
          <div class="donut-center"><div class="donut-num" id="donut-num">0</div><div class="donut-lbl">รายการ</div></div>
        </div>
        <div class="donut-legend" id="donut-legend"><span style="color:var(--g400);font-size:12px">ยังไม่มีข้อมูล</span></div>
      </div>
    </div>
    <div class="chart-card">
      <div class="card-title">กรมธรรม์แต่ละสมาชิก</div>
      <div class="member-bars" id="member-bars"><div style="text-align:center;padding:16px;color:var(--g400);font-size:13px">ยังไม่มีข้อมูล</div></div>
    </div>
    <div class="chart-card">
      <div class="card-title">🔔 ใกล้หมดอายุ (90 วัน)</div>
      <div class="expiry-list" id="expiry-list"></div>
    </div>
  </div>

  <!-- ══ POLICIES ══ -->
  <div class="page" id="page-policies">
    <div class="search-wrap">
      <span>🔍</span>
      <input type="search" id="search-input" placeholder="ค้นหาชื่อ, บริษัท, เลขกรมธรรม์..." oninput="renderPolicies()" autocorrect="off" autocapitalize="off">
    </div>
    <div class="filter-bar" id="filter-bar">
      <div class="filter-chip active" data-filter="all" onclick="setFilter(this,'all')">ทั้งหมด</div>
      <div class="filter-chip" data-filter="health" onclick="setFilter(this,'health')">❤️‍🩹 สุขภาพ</div>
      <div class="filter-chip" data-filter="accident" onclick="setFilter(this,'accident')">⚡ อุบัติเหตุ</div>
      <div class="filter-chip" data-filter="life" onclick="setFilter(this,'life')">🌿 ชีวิต</div>
      <div class="filter-chip" data-filter="ci" onclick="setFilter(this,'ci')">🏥 CI</div>
      <div class="filter-chip" data-filter="expiring" onclick="setFilter(this,'expiring')">⚠️ ใกล้หมด</div>
      <div class="filter-chip" data-filter="expired" onclick="setFilter(this,'expired')">❌ หมดแล้ว</div>
    </div>
    <div class="policy-list" id="policy-list"></div>
    <div id="empty-state" class="empty-state" style="display:none">
      <div class="empty-icon">🛡️</div>
      <div class="empty-title">ยังไม่มีกรมธรรม์</div>
      <div class="empty-desc">กดปุ่ม ＋ เพื่อเริ่มบันทึกกรมธรรม์ของครอบครัว</div>
      <button class="btn btn-primary" onclick="openAddModal()">＋ เพิ่มกรมธรรม์แรก</button>
    </div>
  </div>

  <!-- ══ MEMBERS ══ -->
  <div class="page" id="page-members">
    <div style="display:flex;justify-content:flex-end;margin-bottom:14px">
      <button class="btn btn-primary btn-sm" onclick="openMemberModal()">＋ เพิ่มสมาชิก</button>
    </div>
    <div class="members-list" id="members-list"></div>
  </div>

  <!-- ══ SETTINGS ══ -->
  <div class="page" id="page-settings">
    <!-- Auth status -->
    <div class="config-card">
      <div class="config-title">🔐 Google Account</div>
      <div id="settings-auth"></div>
    </div>
    <!-- Client ID -->
    <div class="config-card">
      <div class="config-title">⚙️ ตั้งค่า OAuth Client ID</div>
      <div class="config-desc">สร้างจาก Google Cloud Console → OAuth 2.0 Client ID (Web Application)</div>
      <ol class="step-list">
        <li>ไปที่ <strong>console.cloud.google.com</strong> → New Project</li>
        <li>Enable <strong>Google Sheets API</strong> + <strong>Google Drive API</strong></li>
        <li>Credentials → OAuth 2.0 Client ID → Web Application</li>
        <li>Authorized origins: <code id="current-origin" style="background:var(--g100);padding:2px 6px;border-radius:4px;font-size:11px;word-break:break-all"></code></li>
        <li>คัดลอก <strong>Client ID</strong> มาวางด้านล่าง</li>
      </ol>
      <div class="form-group" style="margin-top:14px">
        <label class="form-label">Google OAuth Client ID</label>
        <input type="text" class="form-input" id="client-id-input" placeholder="xxx.apps.googleusercontent.com" autocorrect="off" autocapitalize="none">
      </div>
      <button class="btn btn-primary" onclick="saveClientId()" style="width:100%">💾 บันทึก Client ID</button>
    </div>
    <!-- Sheets -->
    <div class="config-card">
      <div class="config-title">📊 Google Sheets — ข้อมูลกรมธรรม์</div>
      <div class="config-desc">
        วิธีหา Spreadsheet ID: เปิด Google Sheet แล้วดูจาก URL<br>
        <code style="font-size:11px;word-break:break-all;background:var(--g100);padding:2px 4px;border-radius:3px">docs.google.com/spreadsheets/d/<strong style="color:var(--primary)">[ID อยู่ตรงนี้]</strong>/edit</code>
      </div>
      <div class="form-group">
        <label class="form-label">Spreadsheet ID <span class="req">*</span></label>
        <input type="text" class="form-input" id="sheet-id" placeholder="1BxiMVs0XRA5nFMdKvBdBZjg..." autocorrect="off" autocapitalize="none">
      </div>
      <div class="form-row">
        <div class="form-group">
          <label class="form-label">Sheet Name</label>
          <input type="text" class="form-input" id="sheet-name" value="Policies" autocorrect="off">
        </div>
        <div class="form-group">
          <label class="form-label">Auto-sync ทุก (นาที)</label>
          <select class="form-input" id="sync-interval">
            <option value="0">ปิด</option><option value="5">5</option>
            <option value="15" selected>15</option><option value="30">30</option><option value="60">60</option>
          </select>
        </div>
      </div>
      <div id="sheet-sync-status" class="sync-row" style="margin-bottom:12px">
        <div class="sync-dot sync-inactive"></div><span>ยังไม่ได้เชื่อมต่อ</span>
      </div>
      <div style="display:flex;gap:8px;flex-wrap:wrap">
        <button class="btn btn-primary btn-sm" onclick="saveSheetConfig()">💾 บันทึก</button>
        <button class="btn btn-outline btn-sm" onclick="syncToSheet()">🔄 Sync ตอนนี้</button>
        <button class="btn btn-ghost btn-sm" onclick="importFromSheet()">📥 Import</button>
      </div>
      <div class="code-block" style="margin-top:12px">id | member | type | company | policy_no | plan_name | start_date | end_date | premium | sum_insured | coverage | beneficiary | drive_files | notes | updated_at</div>
    </div>
    <!-- Drive -->
    <div class="config-card">
      <div class="config-title">📁 Google Drive — ไฟล์กรมธรรม์</div>
      <div class="config-desc">ไฟล์แนบจะถูกอัพโหลดไปยัง Drive → Family Insurance → [ชื่อสมาชิก]</div>
      <div id="drive-folder-display"></div>
      <div class="form-group">
        <label class="form-label">Root Folder ID (ปล่อยว่าง = สร้างใหม่อัตโนมัติ)</label>
        <input type="text" class="form-input" id="drive-folder-id" placeholder="ปล่อยว่างแล้วกดสร้าง" autocorrect="off" autocapitalize="none">
      </div>
      <button class="btn btn-outline btn-sm" onclick="initDriveFolder()" style="width:100%">📁 สร้าง / เชื่อม Folder</button>
    </div>
    <!-- Data mgmt -->
    <div class="config-card" style="border-color:#fce8e6">
      <div class="config-title" style="color:var(--danger)">🗑️ จัดการข้อมูล</div>
      <div style="display:flex;gap:8px;flex-wrap:wrap;margin-top:8px">
        <button class="btn btn-ghost btn-sm" onclick="exportCSV()">📥 Export CSV</button>
        <button class="btn btn-danger btn-sm" onclick="clearAllData()">🗑️ ล้างข้อมูล</button>
      </div>
    </div>
  </div>
</div>

<!-- BOTTOM NAV -->
<nav class="bottom-nav" id="bottom-nav">
  <button class="bn-item active" data-page="dashboard" onclick="navigate('dashboard')">
    <span class="bn-icon">📊</span>หน้าหลัก
  </button>
  <button class="bn-item" data-page="policies" onclick="navigate('policies')">
    <span class="bn-icon">📋</span>กรมธรรม์
    <span class="bn-badge" id="expiring-count-bn" style="display:none">0</span>
  </button>
  <button class="bn-item" onclick="openAddModal()" style="color:var(--primary)">
    <span class="bn-icon" style="background:var(--primary);color:white;border-radius:50%;width:36px;height:36px;display:flex;align-items:center;justify-content:center;font-size:18px">＋</span>
    <span style="margin-top:2px">เพิ่ม</span>
  </button>
  <button class="bn-item" data-page="members" onclick="navigate('members')">
    <span class="bn-icon">👨‍👩‍👧‍👦</span>สมาชิก
  </button>
  <button class="bn-item" data-page="settings" onclick="navigate('settings')">
    <span class="bn-icon">⚙️</span>ตั้งค่า
  </button>
</nav>

<!-- ADD/EDIT MODAL -->
<div class="modal-overlay" id="policy-modal">
  <div class="modal">
    <div class="modal-handle"></div>
    <div class="modal-header">
      <div class="modal-title" id="modal-title">➕ เพิ่มกรมธรรม์</div>
      <button class="modal-close" onclick="closeModal('policy-modal')">✕</button>
    </div>
    <div class="modal-body">
      <div class="form-group">
        <label class="form-label">ประเภทประกัน <span class="req">*</span></label>
        <div class="type-selector">
          <div class="type-chip" onclick="selectType('health')" data-type="health"><div class="type-chip-icon">❤️‍🩹</div>สุขภาพ</div>
          <div class="type-chip" onclick="selectType('accident')" data-type="accident"><div class="type-chip-icon">⚡</div>อุบัติเหตุ</div>
          <div class="type-chip" onclick="selectType('life')" data-type="life"><div class="type-chip-icon">🌿</div>ชีวิต</div>
          <div class="type-chip" onclick="selectType('ci')" data-type="ci"><div class="type-chip-icon">🏥</div>CI</div>
          <div class="type-chip" onclick="selectType('other')" data-type="other"><div class="type-chip-icon">📌</div>อื่นๆ</div>
        </div>
        <input type="hidden" id="f-type">
      </div>
      <div class="form-group">
        <label class="form-label">สมาชิก <span class="req">*</span></label>
        <select class="form-input" id="f-member"></select>
      </div>
      <div class="form-row">
        <div class="form-group">
          <label class="form-label">บริษัทประกัน <span class="req">*</span></label>
          <input type="text" class="form-input" id="f-company" placeholder="AIA, เมืองไทย...">
        </div>
        <div class="form-group">
          <label class="form-label">เลขกรมธรรม์</label>
          <input type="text" class="form-input" id="f-policy-no" placeholder="TH-2024-001" autocorrect="off">
        </div>
      </div>
      <div class="form-group">
        <label class="form-label">ชื่อแผน</label>
        <input type="text" class="form-input" id="f-plan" placeholder="เช่น Health Plus Gold">
      </div>
      <hr class="form-divider">
      <div class="form-section-title">📅 ระยะเวลาคุ้มครอง</div>
      <div class="form-row">
        <div class="form-group">
          <label class="form-label">วันเริ่มคุ้มครอง <span class="req">*</span></label>
          <input type="date" class="form-input" id="f-start">
        </div>
        <div class="form-group">
          <label class="form-label">วันหมดอายุ <span class="req">*</span></label>
          <input type="date" class="form-input" id="f-end">
        </div>
      </div>
      <hr class="form-divider">
      <div class="form-section-title">💰 การเงิน</div>
      <div class="form-row">
        <div class="form-group">
          <label class="form-label">เบี้ยประกัน/ปี (฿)</label>
          <input type="number" class="form-input" id="f-premium" placeholder="0" inputmode="numeric">
        </div>
        <div class="form-group">
          <label class="form-label">ทุนประกันรวม (฿)</label>
          <input type="number" class="form-input" id="f-sum" placeholder="0" inputmode="numeric">
        </div>
      </div>
      <div class="form-row">
        <div class="form-group">
          <label class="form-label">ผู้รับผลประโยชน์</label>
          <input type="text" class="form-input" id="f-beneficiary" placeholder="ภรรยา, ลูก">
        </div>
        <div class="form-group">
          <label class="form-label">ความถี่ชำระ</label>
          <select class="form-input" id="f-freq">
            <option value="yearly">รายปี</option>
            <option value="halfyearly">ราย 6 เดือน</option>
            <option value="quarterly">รายไตรมาส</option>
            <option value="monthly">รายเดือน</option>
          </select>
        </div>
      </div>
      <hr class="form-divider">
      <div class="form-section-title">🩺 ความคุ้มครอง</div>
      <div class="coverage-grid" id="coverage-grid">
        <label class="coverage-check"><input type="checkbox" value="ipd"> 🏥 ผู้ป่วยใน IPD</label>
        <label class="coverage-check"><input type="checkbox" value="opd"> 🩺 ผู้ป่วยนอก OPD</label>
        <label class="coverage-check"><input type="checkbox" value="dental"> 🦷 ทันตกรรม</label>
        <label class="coverage-check"><input type="checkbox" value="vision"> 👁️ สายตา</label>
        <label class="coverage-check"><input type="checkbox" value="maternity"> 🤰 คลอดบุตร</label>
        <label class="coverage-check"><input type="checkbox" value="critical"> 🔴 โรคร้ายแรง</label>
        <label class="coverage-check"><input type="checkbox" value="accident_med"> ⚡ อุบัติเหตุ</label>
        <label class="coverage-check"><input type="checkbox" value="death"> 💐 เสียชีวิต</label>
        <label class="coverage-check"><input type="checkbox" value="disability"> ♿ ทุพพลภาพ</label>
        <label class="coverage-check"><input type="checkbox" value="saving"> 💰 สะสมทรัพย์</label>
        <label class="coverage-check"><input type="checkbox" value="retirement"> 👴 บำนาญ</label>
        <label class="coverage-check"><input type="checkbox" value="other_cov"> 📌 อื่นๆ</label>
      </div>
      <hr class="form-divider">
      <div class="form-section-title">📎 ไฟล์แนบ → Google Drive</div>
      <div id="upload-not-auth" class="alert alert-info" style="display:none;margin-bottom:10px">
        🔐 Login Google ก่อนเพื่ออัพโหลดไฟล์
      </div>
      <div id="upload-wrap">
        <div class="upload-area" onclick="document.getElementById('file-input').click()"
          ondragover="event.preventDefault()" ondrop="handleDrop(event)">
          <input type="file" id="file-input" multiple accept=".pdf,.jpg,.jpeg,.png" onchange="handleFileSelect(event)">
          <div style="font-size:28px">📎</div>
          <div style="font-size:13px;color:var(--g600)">แตะเพื่อเลือกไฟล์</div>
          <div style="font-size:11px;color:var(--g400)">PDF, JPG, PNG (สูงสุด 20MB)</div>
        </div>
        <div class="file-list" id="file-list"></div>
      </div>
      <div class="form-group" style="margin-top:14px">
        <label class="form-label">หมายเหตุ</label>
        <textarea class="form-input" id="f-notes" placeholder="เงื่อนไขพิเศษ, contact agent..."></textarea>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-ghost" onclick="closeModal('policy-modal')">ยกเลิก</button>
      <button class="btn btn-primary" id="save-btn" onclick="savePolicy()">💾 บันทึกกรมธรรม์</button>
    </div>
  </div>
</div>

<!-- DETAIL MODAL -->
<div class="modal-overlay" id="detail-modal">
  <div class="modal" style="max-width:600px">
    <div class="modal-handle"></div>
    <div class="modal-header">
      <div class="modal-title">📋 รายละเอียด</div>
      <button class="modal-close" onclick="closeModal('detail-modal')">✕</button>
    </div>
    <div class="modal-body" id="detail-content"></div>
    <div class="modal-footer">
      <button class="btn btn-ghost btn-sm" onclick="closeModal('detail-modal')">ปิด</button>
      <button class="btn btn-outline btn-sm" id="detail-edit-btn">✏️ แก้ไข</button>
      <button class="btn btn-danger btn-sm" id="detail-del-btn">🗑️ ลบ</button>
    </div>
  </div>
</div>

<!-- MEMBER MODAL -->
<div class="modal-overlay" id="member-modal">
  <div class="modal" style="max-width:440px">
    <div class="modal-handle"></div>
    <div class="modal-header">
      <div class="modal-title">👤 เพิ่มสมาชิก</div>
      <button class="modal-close" onclick="closeModal('member-modal')">✕</button>
    </div>
    <div class="modal-body">
      <div class="form-group">
        <label class="form-label">ชื่อ-นามสกุล <span class="req">*</span></label>
        <input type="text" class="form-input" id="m-name" placeholder="เช่น สมชาย ใจดี">
      </div>
      <div class="form-row">
        <div class="form-group">
          <label class="form-label">ความสัมพันธ์</label>
          <select class="form-input" id="m-role">
            <option>ตัวเอง</option><option>คู่สมรส</option><option>ลูก</option>
            <option>พ่อ</option><option>แม่</option><option>พ่อตา/แม่ยาย</option><option>อื่นๆ</option>
          </select>
        </div>
        <div class="form-group">
          <label class="form-label">วันเกิด</label>
          <input type="date" class="form-input" id="m-dob">
        </div>
      </div>
      <div class="form-group">
        <label class="form-label">สีประจำตัว</label>
        <input type="color" class="form-input" id="m-color" value="#1a73e8" style="height:48px;cursor:pointer;padding:4px 8px">
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-ghost" onclick="closeModal('member-modal')">ยกเลิก</button>
      <button class="btn btn-primary" onclick="saveMember()">💾 เพิ่มสมาชิก</button>
    </div>
  </div>
</div>

<div class="toast-container" id="toast-container"></div>

<!-- Google Identity Services (GIS) — ไม่ block render -->
<script src="https://accounts.google.com/gsi/client" async></script>
<script src="https://apis.google.com/js/api.js" async
  onload="onGapiLoad()" onerror="console.warn('GAPI load failed')"></script>

<script>
// ══════════════════════════════════════════════
//  CONSTANTS
// ══════════════════════════════════════════════
const TYPE_CFG = {
  health  :{ label:'สุขภาพ',     icon:'❤️‍🩹', color:'#34a853', bg:'#e6f4ea' },
  accident:{ label:'อุบัติเหตุ', icon:'⚡',   color:'#c77a00', bg:'#fef9e7' },
  life    :{ label:'ชีวิต',      icon:'🌿',   color:'#9c27b0', bg:'#f3e5f5' },
  ci      :{ label:'CI',         icon:'🏥',   color:'#ff6d00', bg:'#fff3e0' },
  other   :{ label:'อื่นๆ',      icon:'📌',   color:'#1a73e8', bg:'#e8f0fe' },
};
const COV_LBL = {
  ipd:'ผู้ป่วยใน',opd:'ผู้ป่วยนอก',dental:'ทันตกรรม',vision:'สายตา',
  maternity:'คลอดบุตร',critical:'โรคร้ายแรง',accident_med:'อุบัติเหตุ',
  death:'เสียชีวิต',disability:'ทุพพลภาพ',saving:'สะสมทรัพย์',
  retirement:'บำนาญ',other_cov:'อื่นๆ',
};
const PALETTE=['#1a73e8','#e91e63','#ff9800','#9c27b0','#00acc1','#34a853','#f06292','#8d6e63'];
const SCOPES=[
  'https://www.googleapis.com/auth/spreadsheets',
  'https://www.googleapis.com/auth/drive.file',
  'profile','email',
].join(' ');

// ══════════════════════════════════════════════
//  STATE
// ══════════════════════════════════════════════
let policies=[], members=[], editingId=null, selectedType='';
let activeFilter='all', syncTimer=null;
let pendingFiles=[];

// Google auth state
let gapiReady=false, gisReady=false, tokenClient=null, accessToken=null, currentUser=null;

let cfg={clientId:'',sheetId:'',sheetName:'Policies',syncInterval:15,driveFolderId:''};

// ══════════════════════════════════════════════
//  BOOT
// ══════════════════════════════════════════════
function init(){
  loadLocal();
  document.getElementById('current-origin').textContent=location.origin;
  if(cfg.clientId) document.getElementById('client-id-input').value=cfg.clientId;
  if(cfg.sheetId)  document.getElementById('sheet-id').value=cfg.sheetId;
  document.getElementById('sheet-name').value=cfg.sheetName||'Policies';
  document.getElementById('drive-folder-id').value=cfg.driveFolderId||'';
  if(!members.length){ members=[{id:uid(),name:'ฉัน (ตัวเอง)',role:'ตัวเอง',color:'#1a73e8',dob:''}]; saveLocal(); }
  populateMemberDropdowns();
  renderAll(); checkAlerts();
  updateAuthUI();
  // Try silent token restore from sessionStorage
  const savedToken=sessionStorage.getItem('gtoken');
  if(savedToken){ accessToken=savedToken; tryRestoreUser(); }
}

function loadLocal(){
  try{
    policies=JSON.parse(localStorage.getItem('ins_policies')||'[]');
    members=JSON.parse(localStorage.getItem('ins_members')||'[]');
    cfg=Object.assign({clientId:'',sheetId:'',sheetName:'Policies',syncInterval:15,driveFolderId:''},
      JSON.parse(localStorage.getItem('ins_cfg')||'{}'));
  }catch(e){policies=[];members=[];}
}
function saveLocal(){
  localStorage.setItem('ins_policies',JSON.stringify(policies));
  localStorage.setItem('ins_members',JSON.stringify(members));
  localStorage.setItem('ins_cfg',JSON.stringify(cfg));
}
function uid(){ return Date.now().toString(36)+Math.random().toString(36).substr(2,5); }

// ══════════════════════════════════════════════
//  GOOGLE APIS — iOS-compatible approach
//  Uses fetch() + REST API directly instead of
//  gapi.client (which fails on Safari/iOS)
// ══════════════════════════════════════════════
function onGapiLoad(){
  gapi.load('client',async()=>{
    try{
      await gapi.client.init({});
      gapiReady=true;
    }catch(e){ console.warn('gapi init warn:',e); gapiReady=true; }
    tryInitGIS();
  });
}

function tryInitGIS(){
  if(typeof google==='undefined'||!google.accounts){ setTimeout(tryInitGIS,500); return; }
  if(!cfg.clientId){ gisReady=true; return; }
  tokenClient=google.accounts.oauth2.initTokenClient({
    client_id:cfg.clientId, scope:SCOPES,
    callback:handleTokenResponse,
    error_callback:(e)=>{ showToast('Login ผิดพลาด: '+(e.type||e),'error'); },
  });
  gisReady=true;
}

function handleTokenResponse(resp){
  if(resp.error){ showToast('Login ไม่สำเร็จ: '+resp.error,'error'); return; }
  accessToken=resp.access_token;
  sessionStorage.setItem('gtoken',accessToken);
  fetchUserProfile();
}

async function fetchUserProfile(){
  try{
    const r=await fetch('https://www.googleapis.com/oauth2/v3/userinfo',
      {headers:{Authorization:'Bearer '+accessToken}});
    if(!r.ok){ accessToken=null; sessionStorage.removeItem('gtoken'); updateAuthUI(); return; }
    currentUser=await r.json();
    updateAuthUI();
    showToast('สวัสดี '+currentUser.name+' 👋','success');
    if(!cfg.driveFolderId) initDriveFolder();
    setupAutoSync();
  }catch(e){ console.warn('profile fetch failed',e); }
}

async function tryRestoreUser(){
  // Verify token is still valid
  try{
    const r=await fetch('https://www.googleapis.com/oauth2/v3/tokeninfo?access_token='+accessToken);
    if(!r.ok){ accessToken=null; sessionStorage.removeItem('gtoken'); return; }
    fetchUserProfile();
  }catch(e){ accessToken=null; sessionStorage.removeItem('gtoken'); }
}

function handleSignIn(){
  if(!cfg.clientId){
    showToast('กรุณาตั้งค่า Client ID ก่อน → ⚙️ ตั้งค่า','warn');
    navigate('settings'); return;
  }
  if(!gisReady||!tokenClient){ tryInitGIS(); setTimeout(handleSignIn,800); return; }
  // For iOS Safari: must be triggered directly from user gesture
  tokenClient.requestAccessToken({prompt: accessToken?'':'consent'});
}

function handleSignOut(){
  if(accessToken && typeof google!=='undefined'){
    google.accounts.oauth2.revoke(accessToken,()=>{});
  }
  accessToken=null; currentUser=null;
  sessionStorage.removeItem('gtoken');
  if(syncTimer){ clearInterval(syncTimer); syncTimer=null; }
  updateAuthUI();
  showToast('ออกจากระบบแล้ว','warn');
}

function updateAuthUI(){
  const isIn=!!currentUser;
  // Sidebar
  const sa=document.getElementById('sidebar-auth-area');
  if(isIn){
    sa.innerHTML=`<div class="gauth-btn signed-in">
      ${currentUser.picture?`<img class="gauth-avatar" src="${currentUser.picture}">`:'✅'}
      <div class="gauth-info"><div class="gauth-name">${currentUser.name}</div><div class="gauth-email">${currentUser.email}</div></div>
      <button onclick="handleSignOut()" style="background:none;border:none;cursor:pointer;font-size:14px;padding:4px;min-height:auto" title="ออก">✕</button>
    </div>`;
  } else {
    sa.innerHTML=`<button class="gauth-btn" onclick="handleSignIn()">
      <span style="font-size:16px">🔐</span>
      <div class="gauth-info"><div class="gauth-name">เข้าสู่ระบบ Google</div><div class="gauth-email">Sheets & Drive</div></div>
    </button>`;
  }
  // Mobile auth card on dashboard
  const ma=document.getElementById('mobile-auth-area');
  if(ma){
    if(isIn){
      ma.innerHTML=`<div class="mobile-auth-signed">
        ${currentUser.picture?`<img class="gauth-avatar" src="${currentUser.picture}" style="width:32px;height:32px">`:'✅'}
        <div><div style="font-size:13px;font-weight:600;color:var(--success)">${currentUser.name}</div><div style="font-size:11px;color:var(--g500)">${currentUser.email}</div></div>
        <button onclick="syncToSheet()" style="margin-left:auto;background:none;border:1.5px solid var(--success);color:var(--success);padding:6px 10px;border-radius:8px;cursor:pointer;font-size:11px;font-weight:600;font-family:inherit;min-height:auto">🔄 Sync</button>
      </div>`;
    } else {
      ma.innerHTML=`<div class="mobile-auth-card">
        <div class="mobile-auth-card-title">🔐 เชื่อมต่อ Google</div>
        <div class="mobile-auth-card-desc">Login เพื่อ Sync ข้อมูลขึ้น Google Sheets และอัพโหลดไฟล์ไปยัง Drive</div>
        <button class="mobile-auth-card-btn" onclick="handleSignIn()">🔐 เข้าสู่ระบบด้วย Google</button>
      </div>`;
    }
  }
  // Settings page
  const ss=document.getElementById('settings-auth');
  if(ss){
    if(isIn){
      ss.innerHTML=`<div style="display:flex;align-items:center;gap:10px;padding:10px 0">
        ${currentUser.picture?`<img src="${currentUser.picture}" style="width:40px;height:40px;border-radius:50%">`:''}
        <div><div style="font-size:14px;font-weight:700">${currentUser.name}</div><div style="font-size:12px;color:var(--g500)">${currentUser.email}</div></div>
        <button onclick="handleSignOut()" class="btn btn-ghost btn-sm" style="margin-left:auto">ออก</button>
      </div>`;
    } else {
      ss.innerHTML=`<div style="padding:8px 0 14px"><div style="font-size:13px;color:var(--g600);margin-bottom:10px">ยังไม่ได้ Login — ข้อมูลจะเก็บแค่ใน Browser เท่านั้น</div>
        <button class="btn btn-primary" onclick="handleSignIn()" style="width:100%">🔐 เข้าสู่ระบบด้วย Google</button></div>`;
    }
  }
  // Sheet sync status
  const sss=document.getElementById('sheet-sync-status');
  if(sss){
    if(isIn && cfg.sheetId){
      sss.innerHTML=`<div class="sync-dot sync-active"></div><span>เชื่อมต่อแล้ว: ${cfg.sheetName}</span>`;
    } else if(isIn){
      sss.innerHTML=`<div class="sync-dot" style="background:var(--warning)"></div><span>Login แล้ว — ยังไม่ได้ตั้งค่า Sheet ID</span>`;
    } else {
      sss.innerHTML=`<div class="sync-dot sync-inactive"></div><span>ยังไม่ได้ Login Google</span>`;
    }
  }
  // Upload area in modal
  const ua=document.getElementById('upload-not-auth');
  const uw=document.getElementById('upload-wrap');
  if(ua && uw){ ua.style.display=isIn?'none':'flex'; uw.style.display=isIn?'block':'none'; }
  // Drive folder
  if(isIn && cfg.driveFolderId) renderDriveFolderCard();
}

// ══════════════════════════════════════════════
//  GOOGLE SHEETS — pure fetch (works on iOS)
// ══════════════════════════════════════════════
async function sheetsRequest(method, path, body=null){
  if(!accessToken) throw new Error('NOT_SIGNED_IN');
  const url=`https://sheets.googleapis.com/v4/spreadsheets/${cfg.sheetId}${path}`;
  const opts={method, headers:{Authorization:'Bearer '+accessToken,'Content-Type':'application/json'}};
  if(body) opts.body=JSON.stringify(body);
  const r=await fetch(url,opts);
  if(r.status===401){ accessToken=null; sessionStorage.removeItem('gtoken'); updateAuthUI(); throw new Error('TOKEN_EXPIRED'); }
  if(!r.ok){ const e=await r.json(); throw new Error(e.error?.message||'Sheets error'); }
  return r.json();
}

async function syncToSheet(silent=false){
  if(!accessToken){if(!silent) showToast('กรุณา Login Google ก่อน','warn'); return;}
  if(!cfg.sheetId){if(!silent) showToast('กรุณาตั้งค่า Spreadsheet ID','warn'); return;}
  if(!silent) showSyncLoader(true);

  const H=['id','สมาชิก','ประเภท','บริษัทประกัน','เลขกรมธรรม์','ชื่อแผน',
    'วันเริ่ม','วันหมดอายุ','เบี้ย/ปี','ทุนประกัน','ความคุ้มครอง',
    'ผู้รับผลประโยชน์','ไฟล์ Drive','หมายเหตุ','อัพเดทล่าสุด'];
  const rows=[H,...policies.map(p=>[
    p.id, getMember(p.member).name,(TYPE_CFG[p.type]||TYPE_CFG.other).label,
    p.company||'',p.policy_no||'',p.plan_name||'',
    p.start_date||'',p.end_date||'',p.premium||'',p.sum_insured||'',
    (p.coverage||[]).map(c=>COV_LBL[c]||c).join(', '),
    p.beneficiary||'',
    (p.driveFiles||[]).map(f=>f.webViewLink||f.name).join(', '),
    p.notes||'',p.updated_at||'',
  ])];

  try{
    // Clear then write
    await sheetsRequest('POST',`/values/${encodeURIComponent(cfg.sheetName+'!A:Z')}:clear`);
    await sheetsRequest('PUT',`/values/${encodeURIComponent(cfg.sheetName+'!A1')}?valueInputOption=RAW`,{values:rows});
    if(!silent){ showSyncLoader(false); showToast('Sync ขึ้น Sheets สำเร็จ ✅','success'); }
    else showSyncLoader(false);
    // Update status badge
    updateAuthUI();
  }catch(e){
    showSyncLoader(false);
    if(!silent) showToast('Sync ไม่สำเร็จ: '+e.message,'error');
    if(e.message==='TOKEN_EXPIRED') showToast('Session หมดอายุ — กรุณา Login ใหม่','warn');
  }
}

async function importFromSheet(){
  if(!accessToken){showToast('กรุณา Login Google ก่อน','warn');return;}
  if(!cfg.sheetId){showToast('กรุณาตั้งค่า Spreadsheet ID','warn');return;}
  showToast('กำลัง Import...','warn'); showSyncLoader(true);
  try{
    const d=await sheetsRequest('GET',`/values/${encodeURIComponent(cfg.sheetName)}?majorDimension=ROWS`);
    showSyncLoader(false);
    const [hdrs,...rows]=d.values||[];
    if(!hdrs){showToast('ไม่พบข้อมูลใน Sheet','warn');return;}
    showToast(`Import สำเร็จ ${rows.length} แถว ✅`,'success');
  }catch(e){showSyncLoader(false);showToast('Import ไม่สำเร็จ: '+e.message,'error');}
}

// ══════════════════════════════════════════════
//  GOOGLE DRIVE — pure fetch (works on iOS)
// ══════════════════════════════════════════════
async function driveRequest(method,url,body=null,isUpload=false){
  if(!accessToken) throw new Error('NOT_SIGNED_IN');
  const opts={method,headers:{Authorization:'Bearer '+accessToken}};
  if(body && !isUpload){ opts.headers['Content-Type']='application/json'; opts.body=JSON.stringify(body); }
  if(body && isUpload){ opts.body=body; } // FormData
  const r=await fetch(url,opts);
  if(r.status===401){ accessToken=null; sessionStorage.removeItem('gtoken'); updateAuthUI(); throw new Error('TOKEN_EXPIRED'); }
  if(!r.ok){ let e; try{e=await r.json();}catch(x){e={error:{message:r.statusText}};} throw new Error(e.error?.message||'Drive error'); }
  return r.json();
}

async function initDriveFolder(){
  if(!accessToken){showToast('กรุณา Login Google ก่อน','warn');return;}
  const inputId=document.getElementById('drive-folder-id').value.trim();
  if(inputId){
    try{
      const d=await driveRequest('GET',`https://www.googleapis.com/drive/v3/files/${inputId}?fields=id,name,webViewLink`);
      cfg.driveFolderId=inputId; saveLocal();
      showToast(`เชื่อมต่อ "${d.name}" สำเร็จ ✅`,'success');
      renderDriveFolderCard(d);
    }catch(e){showToast('ไม่พบ Folder: '+e.message,'error');}
    return;
  }
  showToast('กำลังสร้าง Folder...','warn');
  try{
    const d=await driveRequest('POST','https://www.googleapis.com/drive/v3/files?fields=id,name,webViewLink',
      {name:'Family Insurance',mimeType:'application/vnd.google-apps.folder'});
    cfg.driveFolderId=d.id;
    document.getElementById('drive-folder-id').value=d.id;
    saveLocal();
    showToast('สร้าง Folder "Family Insurance" เรียบร้อย ✅','success');
    renderDriveFolderCard(d);
  }catch(e){showToast('สร้าง Folder ไม่สำเร็จ: '+e.message,'error');}
}

function renderDriveFolderCard(folder){
  const el=document.getElementById('drive-folder-display'); if(!el) return;
  const name=folder?.name||'Family Insurance';
  const link=folder?.webViewLink||`https://drive.google.com/drive/folders/${cfg.driveFolderId}`;
  el.innerHTML=`<a href="${link}" target="_blank" class="drive-folder-card" style="text-decoration:none;display:flex;align-items:center;gap:12px">
    <span style="font-size:28px">📁</span>
    <div><div style="font-size:14px;font-weight:700">${name}</div><div style="font-size:12px;opacity:.85;margin-top:2px">แตะเพื่อเปิดใน Google Drive →</div></div>
  </a>`;
}

async function getOrCreateMemberFolder(memberId){
  const mem=getMember(memberId);
  if(mem.driveFolderId) return mem.driveFolderId;
  const d=await driveRequest('POST','https://www.googleapis.com/drive/v3/files?fields=id',
    {name:mem.name,mimeType:'application/vnd.google-apps.folder',parents:[cfg.driveFolderId]});
  const idx=members.findIndex(m=>m.id===memberId);
  if(idx!==-1){members[idx].driveFolderId=d.id; saveLocal();}
  return d.id;
}

async function uploadFileToDrive(fileObj,parentId,i){
  pendingFiles[i].status='uploading'; renderFileList();
  const meta={name:fileObj.name,parents:[parentId]};
  const form=new FormData();
  form.append('metadata',new Blob([JSON.stringify(meta)],{type:'application/json'}));
  form.append('file',fileObj);
  try{
    const d=await driveRequest('POST',
      'https://www.googleapis.com/upload/drive/v3/files?uploadType=multipart&fields=id,name,webViewLink',
      form,true);
    pendingFiles[i].status='done';
    pendingFiles[i].driveId=d.id;
    pendingFiles[i].webViewLink=d.webViewLink;
    renderFileList();
    return {id:d.id,name:d.name,webViewLink:d.webViewLink};
  }catch(e){
    pendingFiles[i].status='error'; renderFileList();
    return null;
  }
}

// ══════════════════════════════════════════════
//  AUTO SYNC
// ══════════════════════════════════════════════
function setupAutoSync(){
  if(syncTimer) clearInterval(syncTimer);
  if(accessToken && cfg.sheetId && cfg.syncInterval>0)
    syncTimer=setInterval(()=>syncToSheet(true),cfg.syncInterval*60000);
}

// ══════════════════════════════════════════════
//  NAVIGATION
// ══════════════════════════════════════════════
function navigate(page){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.getElementById('page-'+page).classList.add('active');
  document.querySelectorAll('.nav-item').forEach(n=>n.classList.remove('active'));
  document.querySelectorAll('.bn-item[data-page]').forEach(b=>b.classList.remove('active'));
  const titles={dashboard:'📊 Dashboard',policies:'📋 กรมธรรม์',members:'👨‍👩‍👧‍👦 สมาชิก',settings:'⚙️ ตั้งค่า'};
  document.getElementById('page-title').textContent=titles[page]||page;
  document.querySelectorAll(`.bn-item[data-page="${page}"]`).forEach(b=>b.classList.add('active'));
  if(page==='policies') renderPolicies();
  if(page==='members')  renderMembers();
  if(page==='dashboard'){renderDashboard();updateAuthUI();}
  if(page==='settings') updateAuthUI();
  // Scroll to top
  window.scrollTo({top:0,behavior:'smooth'});
}

function openSidebar(){
  document.getElementById('sidebar').classList.add('open');
  document.getElementById('sidebar-overlay').classList.add('open');
}
function closeSidebar(){
  document.getElementById('sidebar').classList.remove('open');
  document.getElementById('sidebar-overlay').classList.remove('open');
}

// ══════════════════════════════════════════════
//  DATE & FORMAT UTILS
// ══════════════════════════════════════════════
function daysLeft(d){
  if(!d) return Infinity;
  const now=new Date(); now.setHours(0,0,0,0);
  return Math.ceil((new Date(d)-now)/86400000);
}
function thaiDate(s){
  if(!s) return '-';
  const d=new Date(s);
  const M=['ม.ค.','ก.พ.','มี.ค.','เม.ย.','พ.ค.','มิ.ย.','ก.ค.','ส.ค.','ก.ย.','ต.ค.','พ.ย.','ธ.ค.'];
  return `${d.getDate()} ${M[d.getMonth()]} ${d.getFullYear()+543}`;
}
function fmtMoney(n){return n?Number(n).toLocaleString('th-TH')+' ฿':'-';}
function getStatus(p){const d=daysLeft(p.end_date);return d<0?'expired':d<=90?'expiring':'active';}
function getMember(id){return members.find(m=>m.id===id)||{name:id||'?',color:'#9aa0a6'};}
function getInitials(n){return(n||'?').split(' ').map(w=>w[0]).join('').substr(0,2).toUpperCase();}

function populateMemberDropdowns(){
  ['f-member'].forEach(id=>{
    const sel=document.getElementById(id); if(!sel) return;
    const prev=sel.value;
    sel.innerHTML='<option value="">-- เลือกสมาชิก --</option>';
    members.forEach(m=>{const o=document.createElement('option');o.value=m.id;o.textContent=m.name+(m.role?` (${m.role})`:'');sel.appendChild(o);});
    sel.value=prev;
  });
}

// ══════════════════════════════════════════════
//  RENDER ALL
// ══════════════════════════════════════════════
function renderAll(){renderDashboard();renderPolicies();renderMembers();updateExpiringBadge();}

// ══════════════════════════════════════════════
//  DASHBOARD
// ══════════════════════════════════════════════
function renderDashboard(){
  document.getElementById('s-total').textContent=policies.length;
  document.getElementById('s-active').textContent=policies.filter(p=>getStatus(p)==='active').length;
  document.getElementById('s-expiring').textContent=policies.filter(p=>getStatus(p)==='expiring').length;
  const prem=policies.reduce((a,p)=>a+Number(p.premium||0),0);
  document.getElementById('s-premium').textContent=prem?prem.toLocaleString('th-TH'):'-';
  renderDonut(); renderBars(); renderExpiry();
}
function renderDonut(){
  const svg=document.getElementById('donut-svg');
  const legend=document.getElementById('donut-legend');
  document.getElementById('donut-num').textContent=policies.length;
  svg.querySelectorAll('.ds').forEach(e=>e.remove());
  if(!policies.length){legend.innerHTML='<span style="color:var(--g400);font-size:12px">ยังไม่มีข้อมูล</span>';return;}
  const counts={};
  policies.forEach(p=>{counts[p.type]=(counts[p.type]||0)+1;});
  const total=policies.length,r=46,circ=2*Math.PI*r; let off=0;
  Object.entries(counts).forEach(([t,n])=>{
    const c=TYPE_CFG[t]||TYPE_CFG.other,pct=n/total,dash=pct*circ;
    const ci=document.createElementNS('http://www.w3.org/2000/svg','circle');
    ci.setAttribute('class','ds');ci.setAttribute('cx',60);ci.setAttribute('cy',60);ci.setAttribute('r',r);
    ci.setAttribute('fill','none');ci.setAttribute('stroke',c.color);ci.setAttribute('stroke-width',14);
    ci.setAttribute('stroke-dasharray',`${dash} ${circ-dash}`);
    ci.setAttribute('stroke-dashoffset',-(off*circ)); svg.appendChild(ci); off+=pct;
  });
  legend.innerHTML=Object.entries(counts).map(([t,n])=>{
    const c=TYPE_CFG[t]||TYPE_CFG.other;
    return`<div class="legend-item"><div class="legend-dot" style="background:${c.color}"></div>${c.icon} ${c.label} (${n})</div>`;
  }).join('');
}
function renderBars(){
  const el=document.getElementById('member-bars');
  if(!members.length){el.innerHTML='<div style="text-align:center;padding:16px;color:var(--g400);font-size:13px">ยังไม่มีสมาชิก</div>';return;}
  el.innerHTML=members.map(m=>{
    const mp=policies.filter(p=>p.member===m.id);
    const tc={};mp.forEach(p=>{tc[p.type]=(tc[p.type]||0)+1;});
    const segs=Object.entries(tc).map(([t,c2])=>{
      const c=TYPE_CFG[t]||TYPE_CFG.other;
      return`<div class="bar-seg" style="width:${(c2/Math.max(mp.length,1))*100}%;background:${c.color}"></div>`;
    }).join('');
    return`<div class="member-bar-row">
      <div style="display:flex;align-items:center;gap:6px;width:100px;flex-shrink:0">
        <div style="width:26px;height:26px;border-radius:50%;background:${m.color};display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:700;color:white;flex-shrink:0">${getInitials(m.name)}</div>
        <span style="font-size:12px;font-weight:500;overflow:hidden;text-overflow:ellipsis;white-space:nowrap">${m.name.split(' ')[0]}</span>
      </div>
      <div class="bar-track">${mp.length?segs:'<div style="width:100%"></div>'}</div>
      <div class="bar-count">${mp.length}</div>
    </div>`;
  }).join('');
}
function renderExpiry(){
  const el=document.getElementById('expiry-list');
  const exp=policies.filter(p=>{const d=daysLeft(p.end_date);return d>=0&&d<=90;})
    .sort((a,b)=>daysLeft(a.end_date)-daysLeft(b.end_date)).slice(0,8);
  if(!exp.length){el.innerHTML='<div style="text-align:center;padding:16px;color:var(--g400);font-size:13px">ไม่มีกรมธรรม์ที่ใกล้หมดอายุ 🎉</div>';return;}
  el.innerHTML=exp.map(p=>{
    const mem=getMember(p.member),c=TYPE_CFG[p.type]||TYPE_CFG.other,d=daysLeft(p.end_date);
    const cls=d<=30?'days-critical':d<=60?'days-warning':'days-ok';
    return`<div class="expiry-item" onclick="showDetail('${p.id}')">
      <div class="expiry-avatar" style="background:${mem.color}">${getInitials(mem.name)}</div>
      <div class="expiry-info">
        <div class="expiry-name">${mem.name} — ${p.company||'(ไม่ระบุ)'}</div>
        <div class="expiry-type">${c.icon} ${c.label}${p.plan_name?' · '+p.plan_name:''}</div>
      </div>
      <div class="expiry-days ${cls}">${d}ว.<br><span style="font-size:9px;font-weight:400">${thaiDate(p.end_date)}</span></div>
    </div>`;
  }).join('');
}
function checkAlerts(){
  const area=document.getElementById('alert-area');
  const crit=policies.filter(p=>{const d=daysLeft(p.end_date);return d>=0&&d<=30;});
  const warn=policies.filter(p=>{const d=daysLeft(p.end_date);return d>30&&d<=60;});
  let html='';
  if(crit.length) html+=`<div class="alert alert-danger">🚨 <div><strong>ด่วน!</strong> มี ${crit.length} กรมธรรม์หมดอายุใน 30 วัน</div></div>`;
  if(warn.length) html+=`<div class="alert alert-warning">⚠️ มี ${warn.length} กรมธรรม์หมดอายุใน 31–60 วัน</div>`;
  area.innerHTML=html;
}
function updateExpiringBadge(){
  const n=policies.filter(p=>{const d=daysLeft(p.end_date);return d>=0&&d<=90;}).length;
  ['expiring-count-side','expiring-count-bn'].forEach(id=>{
    const b=document.getElementById(id); if(!b) return;
    b.style.display=n?'inline':'none'; b.textContent=n;
  });
}

// ══════════════════════════════════════════════
//  POLICIES PAGE
// ══════════════════════════════════════════════
function setFilter(el,filter){
  activeFilter=filter;
  document.querySelectorAll('.filter-chip').forEach(c=>c.classList.remove('active'));
  el.classList.add('active');
  renderPolicies();
}
function setTypeFilter(type){
  activeFilter=type;
  document.querySelectorAll('.filter-chip').forEach(c=>{
    c.classList.toggle('active',c.dataset.filter===type);
  });
}
function getFiltered(){
  const q=(document.getElementById('search-input')?.value||'').toLowerCase();
  return policies.filter(p=>{
    const mem=getMember(p.member);
    const str=[p.company,p.policy_no,p.plan_name,mem.name].join(' ').toLowerCase();
    if(q && !str.includes(q)) return false;
    if(activeFilter==='all') return true;
    if(activeFilter==='expiring') return getStatus(p)==='expiring';
    if(activeFilter==='expired')  return getStatus(p)==='expired';
    return p.type===activeFilter;
  }).sort((a,b)=>new Date(a.end_date||0)-new Date(b.end_date||0));
}
function renderPolicies(){
  const list=document.getElementById('policy-list');
  const empty=document.getElementById('empty-state');
  const rows=getFiltered();
  if(!rows.length){list.innerHTML='';empty.style.display='block';return;}
  empty.style.display='none';
  list.innerHTML=rows.map(p=>{
    const mem=getMember(p.member),c=TYPE_CFG[p.type]||TYPE_CFG.other;
    const st=getStatus(p),d=daysLeft(p.end_date);
    const stMap={active:['status-active','คุ้มครองอยู่'],expiring:['status-expiring','ใกล้หมดอายุ'],expired:['status-expired','หมดอายุ']};
    const [dc,sl]=stMap[st];
    const files=(p.driveFiles||[]);
    const fileRow=files.length?`<div style="display:flex;gap:4px;flex-wrap:wrap;margin-top:6px">${files.map(f=>`<a class="file-chip" href="${f.webViewLink||'#'}" target="_blank">📎 ${f.name}</a>`).join('')}</div>`:'';
    return`<div class="policy-card">
      <div class="policy-card-top">
        <div class="policy-card-avatar" style="background:${mem.color}">${getInitials(mem.name)}</div>
        <div class="policy-card-info">
          <div class="policy-card-name">${mem.name}</div>
          <div class="policy-card-company">${p.company||'-'}${p.plan_name?' · '+p.plan_name:''}</div>
        </div>
        <span class="badge badge-${p.type}">${c.icon} ${c.label}</span>
      </div>
      <div class="policy-card-bottom">
        <span class="status-dot ${dc}"></span><span style="font-size:12px;color:var(--g600)">${sl}</span>
        <span class="policy-card-date">หมดอายุ: ${thaiDate(p.end_date)}${st==='expiring'?' <strong style="color:var(--warning)">('+d+'วัน)</strong>':''}</span>
        ${p.premium?`<span class="policy-card-premium">${fmtMoney(p.premium)}/ปี</span>`:''}
      </div>
      ${fileRow}
      <div class="pc-actions">
        <button class="btn btn-ghost btn-sm" onclick="showDetail('${p.id}')" style="flex:1">👁️ ดูรายละเอียด</button>
        <button class="btn btn-outline btn-sm" onclick="editPolicy('${p.id}')">✏️</button>
        <button class="btn btn-danger btn-sm" onclick="deletePolicy('${p.id}')">🗑️</button>
      </div>
    </div>`;
  }).join('');
}

// ══════════════════════════════════════════════
//  ADD / EDIT POLICY
// ══════════════════════════════════════════════
function openAddModal(){
  editingId=null; pendingFiles=[];
  document.getElementById('modal-title').textContent='➕ เพิ่มกรมธรรม์';
  clearForm(); populateMemberDropdowns();
  updateUploadArea();
  openModal('policy-modal');
}
function clearForm(){
  selectedType='';
  document.querySelectorAll('.type-chip').forEach(c=>c.className='type-chip');
  ['f-type','f-company','f-policy-no','f-plan','f-start','f-end','f-premium','f-sum','f-beneficiary','f-notes']
    .forEach(id=>{const el=document.getElementById(id);if(el) el.value='';});
  document.getElementById('f-member').value='';
  document.getElementById('f-freq').value='yearly';
  document.querySelectorAll('#coverage-grid input').forEach(cb=>cb.checked=false);
  pendingFiles=[]; renderFileList();
}
function updateUploadArea(){
  const ua=document.getElementById('upload-not-auth');
  const uw=document.getElementById('upload-wrap');
  if(ua&&uw){ua.style.display=accessToken?'none':'flex';uw.style.display=accessToken?'block':'none';}
}
function selectType(type){
  selectedType=type;
  document.getElementById('f-type').value=type;
  document.querySelectorAll('.type-chip').forEach(c=>{c.className='type-chip';if(c.dataset.type===type) c.className=`type-chip sel-${type}`;});
}

async function savePolicy(){
  const member=document.getElementById('f-member').value;
  const company=document.getElementById('f-company').value.trim();
  const start=document.getElementById('f-start').value;
  const end=document.getElementById('f-end').value;
  const type=selectedType;
  if(!member){showToast('กรุณาเลือกสมาชิก','error');return;}
  if(!company){showToast('กรุณากรอกบริษัทประกัน','error');return;}
  if(!type){showToast('กรุณาเลือกประเภทประกัน','error');return;}
  if(!start||!end){showToast('กรุณากรอกวันคุ้มครอง','error');return;}
  if(new Date(end)<=new Date(start)){showToast('วันหมดอายุต้องหลังวันเริ่ม','error');return;}

  const btn=document.getElementById('save-btn');
  btn.disabled=true; btn.innerHTML='<div class="spinner"></div> กำลังบันทึก...';

  // Upload files
  let driveFiles=editingId?(policies.find(p=>p.id===editingId)?.driveFiles||[]):[];
  if(accessToken && pendingFiles.length && cfg.driveFolderId){
    showSyncLoader(true);
    try{
      const folderId=await getOrCreateMemberFolder(member);
      for(let i=0;i<pendingFiles.length;i++){
        if(pendingFiles[i].status==='pending'){
          const r=await uploadFileToDrive(pendingFiles[i].file,folderId,i);
          if(r) driveFiles.push(r);
        }
      }
    }catch(e){showToast('อัพโหลดบางไฟล์ไม่สำเร็จ','warn');}
    showSyncLoader(false);
  }

  const cov=[...document.querySelectorAll('#coverage-grid input:checked')].map(cb=>cb.value);
  const policy={
    id:editingId||uid(),member,type,company,
    policy_no:document.getElementById('f-policy-no').value.trim(),
    plan_name:document.getElementById('f-plan').value.trim(),
    start_date:start,end_date:end,
    premium:document.getElementById('f-premium').value||0,
    sum_insured:document.getElementById('f-sum').value||0,
    payment_freq:document.getElementById('f-freq').value,
    beneficiary:document.getElementById('f-beneficiary').value.trim(),
    coverage:cov,driveFiles,
    notes:document.getElementById('f-notes').value.trim(),
    created_at:editingId?(policies.find(p=>p.id===editingId)?.created_at||new Date().toISOString()):new Date().toISOString(),
    updated_at:new Date().toISOString(),
  };

  if(editingId){const i=policies.findIndex(p=>p.id===editingId);if(i!==-1)policies[i]=policy;}
  else policies.push(policy);

  saveLocal(); closeModal('policy-modal');
  renderAll(); checkAlerts();
  btn.disabled=false; btn.innerHTML='💾 บันทึกกรมธรรม์';
  showToast(editingId?'อัพเดทเรียบร้อย ✅':'บันทึกเรียบร้อย ✅','success');

  if(accessToken && cfg.sheetId) syncToSheet(true);
}

function editPolicy(id){
  const p=policies.find(p=>p.id===id); if(!p) return;
  editingId=id; pendingFiles=[];
  document.getElementById('modal-title').textContent='✏️ แก้ไขกรมธรรม์';
  clearForm(); populateMemberDropdowns();
  selectType(p.type);
  document.getElementById('f-member').value=p.member;
  ['f-company','f-policy-no','f-plan','f-start','f-end','f-premium','f-sum','f-beneficiary','f-notes']
    .forEach(id=>{const k=id.replace('f-','').replace('-','_').replace('policy_no','policy_no').replace('f_','');});
  document.getElementById('f-company').value=p.company||'';
  document.getElementById('f-policy-no').value=p.policy_no||'';
  document.getElementById('f-plan').value=p.plan_name||'';
  document.getElementById('f-start').value=p.start_date||'';
  document.getElementById('f-end').value=p.end_date||'';
  document.getElementById('f-premium').value=p.premium||'';
  document.getElementById('f-sum').value=p.sum_insured||'';
  document.getElementById('f-freq').value=p.payment_freq||'yearly';
  document.getElementById('f-beneficiary').value=p.beneficiary||'';
  document.getElementById('f-notes').value=p.notes||'';
  if(p.coverage) p.coverage.forEach(v=>{const cb=document.querySelector(`#coverage-grid input[value="${v}"]`);if(cb) cb.checked=true;});
  updateUploadArea();
  closeModal('detail-modal');
  openModal('policy-modal');
}

function deletePolicy(id){
  if(!confirm('ต้องการลบกรมธรรม์นี้?')) return;
  policies=policies.filter(p=>p.id!==id);
  saveLocal(); renderAll(); checkAlerts(); closeModal('detail-modal');
  showToast('ลบเรียบร้อย','warn');
  if(accessToken && cfg.sheetId) syncToSheet(true);
}

function showDetail(id){
  const p=policies.find(p=>p.id===id); if(!p) return;
  const mem=getMember(p.member),c=TYPE_CFG[p.type]||TYPE_CFG.other;
  const st=getStatus(p),d=daysLeft(p.end_date);
  const stTxt={active:'✅ คุ้มครองอยู่',expiring:'⚠️ ใกล้หมดอายุ',expired:'❌ หมดอายุ'};
  const freqTxt={yearly:'รายปี',halfyearly:'ราย 6 เดือน',quarterly:'รายไตรมาส',monthly:'รายเดือน'};
  const covTags=(p.coverage||[]).map(cv=>`<div class="coverage-tag">${COV_LBL[cv]||cv}</div>`).join('');
  const filesHTML=(p.driveFiles||[]).map(f=>`<div class="attached-file">
    <span style="font-size:20px">${f.name?.endsWith('.pdf')?'📄':'🖼️'}</span>
    <div class="attached-file-info"><div class="attached-file-name">${f.name}</div><div class="attached-file-meta">Google Drive</div></div>
    <a href="${f.webViewLink||'#'}" target="_blank" class="btn btn-outline btn-xs">เปิด</a>
  </div>`).join('');

  document.getElementById('detail-content').innerHTML=`
  <div class="detail-hero">
    <div class="detail-avatar" style="background:${mem.color}">${getInitials(mem.name)}</div>
    <div>
      <div style="font-size:15px;font-weight:700">${mem.name}</div>
      <div style="margin-top:4px"><span class="badge badge-${p.type}">${c.icon} ${c.label}</span> <span style="font-size:12px;color:var(--g500)">${p.company||''}</span></div>
    </div>
  </div>
  <div class="detail-rows">
    <div class="detail-2col">
      <div class="detail-row"><div class="detail-key">เลขกรมธรรม์</div><div class="detail-val" style="font-family:monospace;font-size:13px">${p.policy_no||'-'}</div></div>
      <div class="detail-row"><div class="detail-key">สถานะ</div><div class="detail-val" style="font-size:13px">${stTxt[st]}${st==='expiring'?' ('+d+'วัน)':''}</div></div>
    </div>
    <div class="detail-2col">
      <div class="detail-row"><div class="detail-key">วันเริ่มคุ้มครอง</div><div class="detail-val">${thaiDate(p.start_date)}</div></div>
      <div class="detail-row"><div class="detail-key">วันหมดอายุ</div><div class="detail-val">${thaiDate(p.end_date)}</div></div>
    </div>
    <div class="detail-2col">
      <div class="detail-row"><div class="detail-key">เบี้ยประกัน/ปี</div><div class="detail-val">${fmtMoney(p.premium)}</div></div>
      <div class="detail-row"><div class="detail-key">ทุนประกัน</div><div class="detail-val">${fmtMoney(p.sum_insured)}</div></div>
    </div>
    <div class="detail-2col">
      <div class="detail-row"><div class="detail-key">ความถี่ชำระ</div><div class="detail-val">${freqTxt[p.payment_freq]||'-'}</div></div>
      <div class="detail-row"><div class="detail-key">ผู้รับผลประโยชน์</div><div class="detail-val">${p.beneficiary||'-'}</div></div>
    </div>
    ${p.plan_name?`<div class="detail-row"><div class="detail-key">ชื่อแผน</div><div class="detail-val">${p.plan_name}</div></div>`:''}
    ${covTags?`<div style="padding:10px 12px;background:var(--g50);border-radius:8px"><div class="detail-key" style="margin-bottom:6px">ความคุ้มครอง</div><div class="coverage-tags">${covTags}</div></div>`:''}
    ${filesHTML?`<div><div class="detail-key" style="margin-bottom:6px;padding:0 2px">📎 ไฟล์แนบ</div>${filesHTML}</div>`:''}
    ${p.notes?`<div class="detail-row"><div class="detail-key">หมายเหตุ</div><div class="detail-val" style="font-size:13px;font-weight:400">${p.notes}</div></div>`:''}
  </div>`;
  document.getElementById('detail-edit-btn').onclick=()=>editPolicy(id);
  document.getElementById('detail-del-btn').onclick=()=>deletePolicy(id);
  openModal('detail-modal');
}

// ══════════════════════════════════════════════
//  FILE HANDLING
// ══════════════════════════════════════════════
function handleFileSelect(e){addFiles([...e.target.files]);e.target.value='';}
function handleDrop(e){e.preventDefault();addFiles([...e.dataTransfer.files]);}
function addFiles(files){
  files.forEach(f=>{
    if(f.size>20*1024*1024){showToast(`"${f.name}" ใหญ่เกิน 20MB`,'error');return;}
    if(!pendingFiles.find(x=>x.file.name===f.name&&x.file.size===f.size))
      pendingFiles.push({file:f,status:'pending'});
  });
  renderFileList();
}
function removeFile(i){pendingFiles.splice(i,1);renderFileList();}
function renderFileList(){
  const el=document.getElementById('file-list');if(!el) return;
  el.innerHTML=pendingFiles.map((pf,i)=>{
    const icon=pf.file.name.endsWith('.pdf')?'📄':'🖼️';
    const sz=(pf.file.size/1024).toFixed(0)+' KB';
    const stIcon=pf.status==='done'?'✅':pf.status==='uploading'?'⏳':pf.status==='error'?'❌':'📌';
    return`<div class="file-item">
      <span style="font-size:18px">${icon}</span>
      <div class="file-item-name">${pf.file.name}</div>
      <div class="file-item-size">${sz}</div>
      <span>${stIcon}</span>
      ${pf.status==='pending'?`<button onclick="removeFile(${i})" style="background:none;border:none;cursor:pointer;color:var(--g400);font-size:16px;padding:4px;min-height:auto">✕</button>`:''}
    </div>`;
  }).join('');
}

// ══════════════════════════════════════════════
//  MEMBERS
// ══════════════════════════════════════════════
function openMemberModal(){
  document.getElementById('m-name').value='';
  document.getElementById('m-role').value='ตัวเอง';
  document.getElementById('m-dob').value='';
  document.getElementById('m-color').value=PALETTE[members.length%PALETTE.length];
  openModal('member-modal');
}
function saveMember(){
  const name=document.getElementById('m-name').value.trim();
  if(!name){showToast('กรุณากรอกชื่อ','error');return;}
  members.push({id:uid(),name,role:document.getElementById('m-role').value,
    dob:document.getElementById('m-dob').value,color:document.getElementById('m-color').value});
  saveLocal();populateMemberDropdowns();renderMembers();renderDashboard();
  closeModal('member-modal');showToast(`เพิ่ม "${name}" เรียบร้อย`,'success');
}
function deleteMember(id){
  if(!confirm('ลบสมาชิกนี้?')) return;
  members=members.filter(m=>m.id!==id);
  saveLocal();populateMemberDropdowns();renderMembers();renderDashboard();
  showToast('ลบสมาชิกเรียบร้อย','warn');
}
function renderMembers(){
  const el=document.getElementById('members-list');if(!el) return;
  if(!members.length){el.innerHTML='<div class="empty-state"><div class="empty-icon">👨‍👩‍👧‍👦</div><div class="empty-title">ยังไม่มีสมาชิก</div></div>';return;}
  el.innerHTML=members.map(m=>{
    const mp=policies.filter(p=>p.member===m.id);
    const age=m.dob?Math.floor((Date.now()-new Date(m.dob))/31557600000):null;
    const tBadges=[...new Set(mp.map(p=>p.type))].map(t=>{const c=TYPE_CFG[t]||TYPE_CFG.other;return`<div class="mini-badge" style="background:${c.bg};color:${c.color}">${c.icon} ${c.label}</div>`;}).join('');
    const driveLink=m.driveFolderId?`<a href="https://drive.google.com/drive/folders/${m.driveFolderId}" target="_blank" class="btn btn-ghost btn-xs">📁 Drive</a>`:'';
    return`<div class="member-item">
      <div class="member-avatar" style="background:${m.color}">${getInitials(m.name)}</div>
      <div class="member-info">
        <div class="member-name">${m.name}</div>
        <div class="member-meta">${m.role||''}${age?' · '+age+' ปี':''} · ${mp.length} กรมธรรม์</div>
        <div class="member-tags" style="margin-top:6px">${tBadges||'<span style="font-size:11px;color:var(--g400)">ยังไม่มีกรมธรรม์</span>'}</div>
      </div>
      <div style="display:flex;flex-direction:column;gap:6px;flex-shrink:0">
        ${driveLink}
        <button class="btn btn-danger btn-xs" onclick="deleteMember('${m.id}')">🗑️</button>
      </div>
    </div>`;
  }).join('');
}

// ══════════════════════════════════════════════
//  SETTINGS
// ══════════════════════════════════════════════
function saveClientId(){
  const id=document.getElementById('client-id-input').value.trim();
  if(!id){showToast('กรุณากรอก Client ID','error');return;}
  cfg.clientId=id;saveLocal();
  showToast('บันทึกแล้ว — กำลัง Refresh...','success');
  setTimeout(()=>location.reload(),1500);
}
function saveSheetConfig(){
  cfg.sheetId=document.getElementById('sheet-id').value.trim();
  cfg.sheetName=document.getElementById('sheet-name').value.trim()||'Policies';
  cfg.syncInterval=parseInt(document.getElementById('sync-interval').value)||0;
  saveLocal();setupAutoSync();updateAuthUI();
  showToast('บันทึกการตั้งค่า Sheet เรียบร้อย','success');
}
function exportCSV(){
  const H=['สมาชิก','ประเภท','บริษัท','เลขกรมธรรม์','ชื่อแผน','วันเริ่ม','วันหมด','เบี้ย','ทุน','ความคุ้มครอง','ผู้รับผลประโยชน์','หมายเหตุ'];
  const rows=policies.map(p=>[
    getMember(p.member).name,(TYPE_CFG[p.type]||TYPE_CFG.other).label,
    p.company,p.policy_no,p.plan_name,p.start_date,p.end_date,p.premium,p.sum_insured,
    (p.coverage||[]).map(c=>COV_LBL[c]||c).join('; '),p.beneficiary,p.notes,
  ]);
  const csv=[H,...rows].map(r=>r.map(c=>'"'+String(c||'').replace(/"/g,'""')+'"').join(',')).join('\n');
  const a=document.createElement('a');
  a.href=URL.createObjectURL(new Blob(['\uFEFF'+csv],{type:'text/csv;charset=utf-8;'}));
  a.download=`family_insurance_${new Date().toISOString().slice(0,10)}.csv`;
  a.click();showToast('Export CSV เรียบร้อย','success');
}
function clearAllData(){
  if(!confirm('ลบข้อมูลทั้งหมด?'))return;
  if(!confirm('ยืนยัน — ลบทั้งหมด?'))return;
  policies=[];members=[{id:uid(),name:'ฉัน (ตัวเอง)',role:'ตัวเอง',color:'#1a73e8',dob:''}];
  saveLocal();populateMemberDropdowns();renderAll();showToast('ล้างข้อมูลเรียบร้อย','warn');
}

// ══════════════════════════════════════════════
//  UI HELPERS
// ══════════════════════════════════════════════
function showSyncLoader(show){
  document.getElementById('sync-indicator').style.display=show?'flex':'none';
}
function openModal(id){document.getElementById(id).classList.add('open');}
function closeModal(id){document.getElementById(id).classList.remove('open');}
document.querySelectorAll('.modal-overlay').forEach(o=>{
  o.addEventListener('click',e=>{if(e.target===o) o.classList.remove('open');});
});
// Swipe down to close modal on mobile
document.querySelectorAll('.modal').forEach(modal=>{
  let startY=0;
  modal.addEventListener('touchstart',e=>{startY=e.touches[0].clientY;},{passive:true});
  modal.addEventListener('touchend',e=>{
    const diff=e.changedTouches[0].clientY-startY;
    if(diff>80 && modal.scrollTop===0) modal.closest('.modal-overlay').classList.remove('open');
  },{passive:true});
});

function showToast(msg,type=''){
  const c=document.getElementById('toast-container');
  const t=document.createElement('div');
  t.className='toast'+(type?' toast-'+type:'');
  t.innerHTML=(type==='success'?'✅ ':type==='error'?'❌ ':type==='warn'?'⚠️ ':'ℹ️ ')+msg;
  c.appendChild(t);
  setTimeout(()=>{t.style.cssText='opacity:0;transform:translateY(10px);transition:all .3s';setTimeout(()=>t.remove(),300);},3000);
}

// ══════════════════════════════════════════════
//  START
// ══════════════════════════════════════════════
init();
setTimeout(()=>{if(!policies.length) loadDemo();},400);

function loadDemo(){
  const me=members[0];
  const sp={id:uid(),name:'สมหญิง รักครอบครัว',role:'คู่สมรส',color:'#e91e63',dob:'1990-05-15'};
  const ch={id:uid(),name:'น้องน้ำตาล',role:'ลูก',color:'#ff9800',dob:'2015-09-20'};
  members.push(sp,ch);
  const add=n=>{const d=new Date();d.setDate(d.getDate()+n);return d.toISOString().slice(0,10);};
  policies=[
    {id:uid(),member:me.id,type:'health',company:'เมืองไทยประกันชีวิต',policy_no:'MTL-2024-001',plan_name:'Health Plus Gold',start_date:add(-180),end_date:add(185),premium:25000,sum_insured:3000000,coverage:['ipd','opd','dental'],beneficiary:'ภรรยา',driveFiles:[],notes:'',created_at:new Date().toISOString(),updated_at:new Date().toISOString()},
    {id:uid(),member:me.id,type:'life',company:'AIA',policy_no:'AIA-LIFE-2022',plan_name:'Life Protect 20/20',start_date:add(-730),end_date:add(2555),premium:48000,sum_insured:5000000,coverage:['death','disability','saving'],beneficiary:'ภรรยาและลูก',driveFiles:[],notes:'',created_at:new Date().toISOString(),updated_at:new Date().toISOString()},
    {id:uid(),member:me.id,type:'accident',company:'Allianz Ayudhya',policy_no:'AA-ACC-2024',plan_name:'PA Master',start_date:add(-60),end_date:add(25),premium:3500,sum_insured:500000,coverage:['accident_med','death'],beneficiary:'ภรรยา',driveFiles:[],notes:'',created_at:new Date().toISOString(),updated_at:new Date().toISOString()},
    {id:uid(),member:sp.id,type:'health',company:'Cigna',policy_no:'CIGNA-2024',plan_name:'Smart Health',start_date:add(-90),end_date:add(55),premium:20000,sum_insured:2000000,coverage:['ipd','opd','maternity'],beneficiary:'สามี',driveFiles:[],notes:'',created_at:new Date().toISOString(),updated_at:new Date().toISOString()},
    {id:uid(),member:ch.id,type:'health',company:'เมืองไทยประกันชีวิต',policy_no:'MTL-CHILD-001',plan_name:'Child Health Star',start_date:add(-30),end_date:add(335),premium:12000,sum_insured:1000000,coverage:['ipd','opd'],beneficiary:'พ่อแม่',driveFiles:[],notes:'',created_at:new Date().toISOString(),updated_at:new Date().toISOString()},
  ];
  saveLocal();populateMemberDropdowns();renderAll();checkAlerts();
  showToast('โหลดข้อมูลตัวอย่าง 🎉','success');
}
</script>
</body>
</html>
