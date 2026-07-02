# Family-Insurance
<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Family Insurance Manager</title>
<!-- Google Identity Services -->
<script src="https://accounts.google.com/gsi/client" async defer></script>
<!-- Google API Client -->
<script src="https://apis.google.com/js/api.js" async defer></script>
<style>
  :root {
    --primary:#1a73e8;--primary-dark:#1557b0;--primary-light:#e8f0fe;
    --success:#34a853;--success-light:#e6f4ea;
    --warning:#fbbc04;--warning-light:#fef9e7;
    --danger:#ea4335;--danger-light:#fce8e6;
    --purple:#9c27b0;--purple-light:#f3e5f5;
    --orange:#ff6d00;--orange-light:#fff3e0;
    --gray-50:#f8f9fa;--gray-100:#f1f3f4;--gray-200:#e8eaed;
    --gray-300:#dadce0;--gray-400:#bdc1c6;--gray-500:#9aa0a6;
    --gray-600:#80868b;--gray-700:#5f6368;--gray-800:#3c4043;--gray-900:#202124;
    --white:#ffffff;
    --shadow-sm:0 1px 3px rgba(0,0,0,.08),0 1px 2px rgba(0,0,0,.06);
    --shadow:0 4px 12px rgba(0,0,0,.08),0 2px 4px rgba(0,0,0,.06);
    --shadow-lg:0 8px 24px rgba(0,0,0,.1),0 4px 8px rgba(0,0,0,.06);
    --radius:12px;--radius-sm:8px;--radius-lg:16px;
    --transition:all .2s cubic-bezier(.4,0,.2,1);
  }
  *{margin:0;padding:0;box-sizing:border-box}
  body{font-family:'Segoe UI',-apple-system,BlinkMacSystemFont,'Noto Sans Thai',sans-serif;
    background:var(--gray-50);color:var(--gray-900);min-height:100vh;font-size:14px;line-height:1.5}

  /* ── SIDEBAR ── */
  .sidebar{position:fixed;left:0;top:0;bottom:0;width:240px;background:var(--white);
    border-right:1px solid var(--gray-200);display:flex;flex-direction:column;
    z-index:100;box-shadow:var(--shadow-sm)}
  .sidebar-brand{display:flex;align-items:center;gap:10px;padding:20px 20px 16px;
    border-bottom:1px solid var(--gray-100)}
  .brand-icon{width:36px;height:36px;border-radius:10px;
    background:linear-gradient(135deg,var(--primary),#4285f4);
    display:flex;align-items:center;justify-content:center;font-size:18px}
  .brand-text{font-size:14px;font-weight:700;line-height:1.2}
  .brand-sub{font-size:11px;color:var(--gray-500)}
  .sidebar-nav{flex:1;padding:12px 0;overflow-y:auto}
  .nav-label{font-size:10px;font-weight:700;color:var(--gray-400);text-transform:uppercase;
    letter-spacing:.8px;padding:4px 20px 8px;margin-top:4px}
  .nav-item{display:flex;align-items:center;gap:10px;padding:10px 20px;cursor:pointer;
    border-radius:0 24px 24px 0;margin:1px 8px 1px 0;color:var(--gray-700);
    font-size:13.5px;font-weight:500;transition:var(--transition)}
  .nav-item:hover{background:var(--gray-100);color:var(--gray-900)}
  .nav-item.active{background:var(--primary-light);color:var(--primary)}
  .nav-icon{font-size:16px;width:20px;text-align:center;flex-shrink:0}
  .nav-badge{margin-left:auto;font-size:11px;font-weight:600;background:var(--danger);
    color:white;border-radius:10px;padding:1px 6px;min-width:18px;text-align:center}
  .sidebar-footer{padding:12px;border-top:1px solid var(--gray-100);display:flex;flex-direction:column;gap:8px}

  /* ── GOOGLE AUTH BUTTON ── */
  .gauth-btn{display:flex;align-items:center;gap:8px;padding:10px 12px;border-radius:var(--radius-sm);
    background:var(--white);color:var(--gray-800);cursor:pointer;border:1.5px solid var(--gray-200);
    width:100%;font-size:12.5px;font-weight:500;transition:var(--transition)}
  .gauth-btn:hover{background:var(--gray-50);border-color:var(--gray-300)}
  .gauth-btn.signed-in{background:var(--success-light);border-color:var(--success);color:var(--success)}
  .gauth-avatar{width:22px;height:22px;border-radius:50%;object-fit:cover}
  .gauth-info{display:flex;flex-direction:column;text-align:left;flex:1;overflow:hidden}
  .gauth-name{font-size:12px;font-weight:600;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
  .gauth-email{font-size:10px;color:var(--gray-500);white-space:nowrap;overflow:hidden;text-overflow:ellipsis}

  /* ── MAIN ── */
  .main{margin-left:240px;min-height:100vh;display:flex;flex-direction:column}
  .topbar{background:var(--white);border-bottom:1px solid var(--gray-200);
    padding:0 28px;height:60px;display:flex;align-items:center;gap:16px;
    position:sticky;top:0;z-index:50;box-shadow:var(--shadow-sm)}
  .topbar-title{font-size:17px;font-weight:700;flex:1}
  .topbar-actions{display:flex;gap:10px;align-items:center}
  .btn{display:inline-flex;align-items:center;gap:6px;padding:8px 16px;border-radius:8px;
    border:none;font-size:13px;font-weight:500;cursor:pointer;transition:var(--transition);white-space:nowrap}
  .btn-primary{background:var(--primary);color:white}
  .btn-primary:hover{background:var(--primary-dark);box-shadow:0 2px 8px rgba(26,115,232,.3)}
  .btn-primary:disabled{background:var(--gray-300);cursor:not-allowed}
  .btn-outline{background:transparent;color:var(--primary);border:1.5px solid var(--primary)}
  .btn-outline:hover{background:var(--primary-light)}
  .btn-ghost{background:transparent;color:var(--gray-700);border:1.5px solid var(--gray-200)}
  .btn-ghost:hover{background:var(--gray-100)}
  .btn-danger{background:var(--danger);color:white}
  .btn-sm{padding:6px 12px;font-size:12px;border-radius:6px}

  .page{display:none;flex:1;padding:24px 28px}
  .page.active{display:block}

  /* ── STATS ── */
  .stats-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:16px;margin-bottom:24px}
  .stat-card{background:var(--white);border-radius:var(--radius);padding:18px 20px;
    box-shadow:var(--shadow-sm);border:1px solid var(--gray-100);
    display:flex;align-items:center;gap:14px;transition:var(--transition)}
  .stat-card:hover{box-shadow:var(--shadow);transform:translateY(-1px)}
  .stat-icon{width:44px;height:44px;border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:20px;flex-shrink:0}
  .stat-value{font-size:24px;font-weight:700;line-height:1}
  .stat-label{font-size:12px;color:var(--gray-500);margin-top:3px}

  /* ── DASHBOARD GRID ── */
  .dashboard-grid{display:grid;grid-template-columns:1fr 1fr;gap:16px;margin-bottom:24px}
  .chart-card{background:var(--white);border-radius:var(--radius);padding:20px;
    box-shadow:var(--shadow-sm);border:1px solid var(--gray-100)}
  .card-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:16px}
  .card-title{font-size:14px;font-weight:600;color:var(--gray-800)}
  .card-subtitle{font-size:12px;color:var(--gray-500);margin-top:2px}

  /* ── DONUT ── */
  .donut-wrap{position:relative;width:140px;height:140px;margin:0 auto 12px}
  .donut-center{position:absolute;inset:0;display:flex;flex-direction:column;align-items:center;justify-content:center}
  .donut-num{font-size:24px;font-weight:700;line-height:1}
  .donut-lbl{font-size:10px;color:var(--gray-500)}
  svg.donut{transform:rotate(-90deg)}
  .donut-legend{display:flex;flex-wrap:wrap;gap:8px;justify-content:center;margin-top:8px}
  .legend-item{display:flex;align-items:center;gap:5px;font-size:12px;color:var(--gray-700)}
  .legend-dot{width:8px;height:8px;border-radius:50%;flex-shrink:0}

  /* ── MEMBER BARS ── */
  .member-bars{display:flex;flex-direction:column;gap:10px}
  .member-bar-row{display:flex;align-items:center;gap:10px}
  .bar-track{flex:1;height:20px;background:var(--gray-100);border-radius:100px;overflow:hidden;display:flex;gap:2px}
  .bar-seg{height:100%;transition:width .4s}
  .bar-count{font-size:12px;color:var(--gray-500);width:28px;text-align:right}

  /* ── EXPIRY ── */
  .expiry-list{display:flex;flex-direction:column;gap:8px}
  .expiry-item{display:flex;align-items:center;gap:12px;padding:10px 12px;border-radius:var(--radius-sm);
    background:var(--gray-50);border:1px solid var(--gray-100);transition:var(--transition);cursor:pointer}
  .expiry-item:hover{background:var(--gray-100)}
  .expiry-avatar{width:32px;height:32px;border-radius:50%;display:flex;align-items:center;justify-content:center;
    font-size:13px;font-weight:700;color:white;flex-shrink:0}
  .expiry-info{flex:1;min-width:0}
  .expiry-name{font-size:13px;font-weight:600;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
  .expiry-type{font-size:11px;color:var(--gray-500)}
  .expiry-days{font-size:12px;font-weight:700;padding:4px 8px;border-radius:6px;flex-shrink:0;text-align:center}
  .days-critical{background:var(--danger-light);color:var(--danger)}
  .days-warning{background:var(--warning-light);color:#c77a00}
  .days-ok{background:var(--success-light);color:var(--success)}

  /* ── FILTER ── */
  .filter-bar{display:flex;gap:10px;align-items:center;margin-bottom:18px;flex-wrap:wrap}
  .search-box{display:flex;align-items:center;gap:8px;background:var(--white);
    border:1.5px solid var(--gray-200);border-radius:8px;padding:8px 12px;flex:1;min-width:200px;max-width:320px;transition:var(--transition)}
  .search-box:focus-within{border-color:var(--primary);box-shadow:0 0 0 3px rgba(26,115,232,.1)}
  .search-box input{border:none;outline:none;font-size:13px;background:transparent;width:100%;color:var(--gray-900)}
  select.filter-select{background:var(--white);border:1.5px solid var(--gray-200);border-radius:8px;
    padding:8px 28px 8px 12px;font-size:13px;color:var(--gray-700);cursor:pointer;appearance:none;
    background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='8' viewBox='0 0 12 8'%3E%3Cpath d='M1 1l5 5 5-5' stroke='%239aa0a6' stroke-width='1.5' fill='none' stroke-linecap='round'/%3E%3C/svg%3E");
    background-repeat:no-repeat;background-position:right 10px center;outline:none}

  /* ── TABLE ── */
  .table-card{background:var(--white);border-radius:var(--radius);overflow:hidden;
    box-shadow:var(--shadow-sm);border:1px solid var(--gray-100)}
  .table-wrap{overflow-x:auto}
  table{width:100%;border-collapse:collapse}
  thead th{background:var(--gray-50);padding:12px 16px;text-align:left;font-size:12px;
    font-weight:600;color:var(--gray-600);text-transform:uppercase;letter-spacing:.5px;
    border-bottom:1px solid var(--gray-200);white-space:nowrap;cursor:pointer;user-select:none}
  thead th:hover{background:var(--gray-100)}
  tbody tr{border-bottom:1px solid var(--gray-100);transition:var(--transition)}
  tbody tr:hover{background:var(--primary-light)}
  tbody tr:last-child{border-bottom:none}
  tbody td{padding:12px 16px;font-size:13px;color:var(--gray-800);vertical-align:middle}
  .td-member{display:flex;align-items:center;gap:8px}
  .member-avatar{width:28px;height:28px;border-radius:50%;display:flex;align-items:center;
    justify-content:center;font-size:12px;font-weight:700;color:white;flex-shrink:0}
  .badge{display:inline-flex;align-items:center;gap:4px;padding:3px 8px;border-radius:100px;font-size:11px;font-weight:600}
  .badge-health{background:var(--success-light);color:var(--success)}
  .badge-accident{background:var(--warning-light);color:#c77a00}
  .badge-life{background:var(--purple-light);color:var(--purple)}
  .badge-ci{background:var(--orange-light);color:var(--orange)}
  .badge-other{background:var(--gray-100);color:var(--gray-700)}
  .status-dot{width:8px;height:8px;border-radius:50%;display:inline-block;margin-right:4px}
  .status-active{background:var(--success)}
  .status-expiring{background:var(--warning)}
  .status-expired{background:var(--danger)}
  .row-actions{display:flex;gap:4px}

  /* ── FILE CHIP ── */
  .file-chip{display:inline-flex;align-items:center;gap:5px;padding:3px 8px;
    background:var(--primary-light);color:var(--primary);border-radius:6px;
    font-size:11px;font-weight:500;cursor:pointer;text-decoration:none;max-width:140px;
    white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
  .file-chip:hover{background:#c5d8fb}

  /* ── UPLOAD AREA ── */
  .upload-area{border:2px dashed var(--gray-300);border-radius:var(--radius-sm);
    padding:24px;text-align:center;cursor:pointer;transition:var(--transition);background:var(--gray-50)}
  .upload-area:hover,.upload-area.dragover{border-color:var(--primary);background:var(--primary-light)}
  .upload-area input{display:none}
  .upload-icon{font-size:28px;margin-bottom:8px}
  .upload-text{font-size:13px;color:var(--gray-600)}
  .upload-sub{font-size:11px;color:var(--gray-400);margin-top:4px}
  .file-list{display:flex;flex-direction:column;gap:6px;margin-top:12px}
  .file-item{display:flex;align-items:center;gap:8px;padding:8px 10px;
    background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-sm)}
  .file-item-name{flex:1;font-size:12px;color:var(--gray-800);white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
  .file-item-size{font-size:11px;color:var(--gray-500);flex-shrink:0}
  .file-item-status{font-size:11px;flex-shrink:0;font-weight:600}
  .file-uploading{color:var(--warning)}
  .file-done{color:var(--success)}
  .file-error{color:var(--danger)}

  /* ── MODAL ── */
  .modal-overlay{display:none;position:fixed;inset:0;background:rgba(0,0,0,.45);z-index:500;
    align-items:center;justify-content:center;padding:16px;backdrop-filter:blur(2px)}
  .modal-overlay.open{display:flex;animation:fadeIn .15s}
  @keyframes fadeIn{from{opacity:0}}
  .modal{background:var(--white);border-radius:var(--radius-lg);width:100%;max-width:700px;
    max-height:90vh;overflow-y:auto;box-shadow:var(--shadow-lg);animation:slideUp .2s}
  @keyframes slideUp{from{transform:translateY(20px);opacity:0}}
  .modal-header{display:flex;align-items:center;justify-content:space-between;
    padding:20px 24px 16px;border-bottom:1px solid var(--gray-100);
    position:sticky;top:0;background:var(--white);z-index:1}
  .modal-title{font-size:16px;font-weight:700}
  .modal-close{width:32px;height:32px;border-radius:50%;border:none;background:var(--gray-100);
    cursor:pointer;font-size:16px;display:flex;align-items:center;justify-content:center;
    transition:var(--transition);color:var(--gray-600)}
  .modal-close:hover{background:var(--gray-200)}
  .modal-body{padding:20px 24px}
  .modal-footer{display:flex;gap:10px;justify-content:flex-end;padding:16px 24px;
    border-top:1px solid var(--gray-100);position:sticky;bottom:0;background:var(--white)}

  /* ── FORM ── */
  .form-grid{display:grid;grid-template-columns:1fr 1fr;gap:16px}
  .form-group{display:flex;flex-direction:column;gap:6px}
  .form-group.full{grid-column:1/-1}
  label.form-label{font-size:12px;font-weight:600;color:var(--gray-700)}
  .form-label span.req{color:var(--danger);margin-left:2px}
  input.form-input,select.form-input,textarea.form-input{background:var(--white);
    border:1.5px solid var(--gray-200);border-radius:var(--radius-sm);padding:9px 12px;
    font-size:13.5px;color:var(--gray-900);transition:var(--transition);outline:none;
    width:100%;font-family:inherit}
  input.form-input:focus,select.form-input:focus,textarea.form-input:focus{
    border-color:var(--primary);box-shadow:0 0 0 3px rgba(26,115,232,.1)}
  textarea.form-input{resize:vertical;min-height:72px}
  .form-divider{grid-column:1/-1;border:none;border-top:1px solid var(--gray-100);margin:4px 0}
  .form-section-title{grid-column:1/-1;font-size:11px;font-weight:700;color:var(--gray-500);text-transform:uppercase;letter-spacing:.5px}
  .type-selector{display:flex;gap:8px;flex-wrap:wrap}
  .type-chip{display:flex;align-items:center;gap:6px;padding:7px 12px;border-radius:8px;
    cursor:pointer;border:1.5px solid var(--gray-200);background:var(--white);
    font-size:12.5px;font-weight:500;transition:var(--transition);color:var(--gray-700)}
  .type-chip:hover{border-color:var(--gray-300);background:var(--gray-50)}
  .type-chip.sel-health{border-color:var(--success);background:var(--success-light);color:var(--success)}
  .type-chip.sel-accident{border-color:var(--warning);background:var(--warning-light);color:#c77a00}
  .type-chip.sel-life{border-color:var(--purple);background:var(--purple-light);color:var(--purple)}
  .type-chip.sel-ci{border-color:var(--orange);background:var(--orange-light);color:var(--orange)}
  .type-chip.sel-other{border-color:var(--primary);background:var(--primary-light);color:var(--primary)}
  .coverage-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:8px}
  .coverage-check{display:flex;align-items:center;gap:6px;cursor:pointer;font-size:12.5px;color:var(--gray-700)}
  .coverage-check input{cursor:pointer;accent-color:var(--primary)}

  /* ── ALERT ── */
  .alert-banner{display:flex;align-items:flex-start;gap:12px;padding:12px 16px;
    border-radius:var(--radius-sm);margin-bottom:16px;border:1px solid;font-size:13px}
  .alert-danger{background:var(--danger-light);border-color:#f5c6c3;color:#c62828}
  .alert-warning{background:var(--warning-light);border-color:#f5e0a0;color:#b06000}
  .alert-info{background:var(--primary-light);border-color:#b3cef5;color:var(--primary-dark)}

  /* ── DETAIL ── */
  .detail-header{display:flex;align-items:center;gap:14px;margin-bottom:20px;
    padding:16px;background:var(--gray-50);border-radius:var(--radius-sm)}
  .detail-avatar{width:48px;height:48px;border-radius:50%;display:flex;align-items:center;
    justify-content:center;font-size:20px;font-weight:700;color:white}
  .detail-grid{display:grid;grid-template-columns:1fr 1fr;gap:12px}
  .detail-item{background:var(--gray-50);border-radius:8px;padding:10px 12px}
  .detail-key{font-size:11px;font-weight:600;color:var(--gray-500);text-transform:uppercase;letter-spacing:.4px;margin-bottom:4px}
  .detail-val{font-size:14px;font-weight:600;color:var(--gray-900)}
  .coverage-tags{display:flex;flex-wrap:wrap;gap:6px;margin-top:8px}
  .coverage-tag{background:var(--primary-light);color:var(--primary);font-size:12px;font-weight:500;padding:3px 8px;border-radius:6px}
  .attached-files{display:flex;flex-direction:column;gap:6px;margin-top:8px}
  .attached-file-row{display:flex;align-items:center;gap:8px;padding:8px 10px;
    background:var(--white);border:1px solid var(--gray-200);border-radius:8px}
  .attached-file-icon{font-size:18px;flex-shrink:0}
  .attached-file-info{flex:1;min-width:0}
  .attached-file-name{font-size:12.5px;font-weight:600;color:var(--gray-800);
    white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
  .attached-file-meta{font-size:11px;color:var(--gray-500)}

  /* ── SETTINGS ── */
  .config-section{background:var(--white);border-radius:var(--radius);padding:20px;
    box-shadow:var(--shadow-sm);border:1px solid var(--gray-100);margin-bottom:16px}
  .config-title{font-size:14px;font-weight:700;margin-bottom:4px}
  .config-desc{font-size:12.5px;color:var(--gray-500);margin-bottom:16px}
  .step-list{list-style:none;counter-reset:step}
  .step-list li{counter-increment:step;padding:8px 0 8px 36px;position:relative;
    font-size:13px;color:var(--gray-700);border-bottom:1px solid var(--gray-100)}
  .step-list li:last-child{border-bottom:none}
  .step-list li::before{content:counter(step);position:absolute;left:0;top:8px;
    width:24px;height:24px;background:var(--primary);color:white;border-radius:50%;
    font-size:11px;font-weight:700;display:flex;align-items:center;justify-content:center}
  .code-block{background:var(--gray-900);color:#a8d8a8;padding:12px 14px;
    border-radius:var(--radius-sm);font-size:12px;font-family:'Consolas',monospace;
    overflow-x:auto;line-height:1.7;margin:10px 0;user-select:all}
  .sync-status{display:flex;align-items:center;gap:8px;font-size:12.5px;padding:10px 14px;
    border-radius:8px;background:var(--gray-50);border:1px solid var(--gray-200)}
  .sync-dot{width:8px;height:8px;border-radius:50%;flex-shrink:0}
  .sync-active{background:var(--success);animation:pulse 2s infinite}
  .sync-inactive{background:var(--gray-400)}
  @keyframes pulse{0%,100%{opacity:1}50%{opacity:.4}}

  /* ── DRIVE FOLDER ── */
  .drive-folder-card{background:linear-gradient(135deg,#1a73e8,#4285f4);color:white;
    border-radius:var(--radius);padding:16px 20px;display:flex;align-items:center;gap:14px;
    margin-bottom:16px;cursor:pointer;transition:var(--transition)}
  .drive-folder-card:hover{transform:translateY(-1px);box-shadow:var(--shadow)}
  .drive-folder-icon{font-size:28px;flex-shrink:0}
  .drive-folder-info{}
  .drive-folder-name{font-size:14px;font-weight:700}
  .drive-folder-sub{font-size:12px;opacity:.8;margin-top:2px}

  /* ── MEMBER CARDS ── */
  .member-summary-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(200px,1fr));gap:12px;margin-bottom:20px}
  .member-card{background:var(--white);border-radius:var(--radius);padding:16px;
    border:1px solid var(--gray-100);box-shadow:var(--shadow-sm);cursor:pointer;transition:var(--transition)}
  .member-card:hover{box-shadow:var(--shadow);transform:translateY(-1px)}
  .mini-badge{padding:2px 6px;border-radius:4px;font-size:10px;font-weight:600}
  .member-policy-types{display:flex;gap:4px;flex-wrap:wrap}

  /* ── MEMBER PAGE ── */
  .members-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(260px,1fr));gap:16px}
  .member-full-card{background:var(--white);border-radius:var(--radius);padding:20px;
    box-shadow:var(--shadow-sm);border:1px solid var(--gray-100)}
  .member-full-top{display:flex;align-items:center;gap:12px;margin-bottom:14px}
  .member-full-avatar{width:44px;height:44px;border-radius:50%;display:flex;align-items:center;
    justify-content:center;font-size:18px;font-weight:700;color:white;flex-shrink:0}
  .member-full-name{font-size:15px;font-weight:700}
  .member-full-role{font-size:12px;color:var(--gray-500)}

  /* ── EMPTY STATE ── */
  .empty-state{text-align:center;padding:64px 24px}
  .empty-icon{font-size:48px;margin-bottom:16px;opacity:.4}
  .empty-title{font-size:16px;font-weight:600;color:var(--gray-700);margin-bottom:8px}
  .empty-desc{font-size:13px;color:var(--gray-500);max-width:320px;margin:0 auto 20px}

  /* ── TOAST ── */
  .toast-container{position:fixed;bottom:24px;right:24px;z-index:999;display:flex;flex-direction:column;gap:8px}
  .toast{background:var(--gray-900);color:white;padding:12px 16px;border-radius:10px;min-width:260px;
    font-size:13px;display:flex;align-items:center;gap:8px;box-shadow:var(--shadow-lg);animation:toastIn .3s}
  @keyframes toastIn{from{transform:translateX(100%);opacity:0}}
  .toast-success{background:var(--success)}
  .toast-error{background:var(--danger)}
  .toast-warn{background:#c77a00}

  /* ── PROGRESS BAR ── */
  .progress-bar{height:4px;background:var(--gray-200);border-radius:2px;overflow:hidden;margin-top:6px}
  .progress-fill{height:100%;background:var(--primary);border-radius:2px;transition:width .3s}

  /* ── LOADING SPINNER ── */
  .spinner{width:18px;height:18px;border:2px solid rgba(255,255,255,.3);
    border-top-color:white;border-radius:50%;animation:spin .6s linear infinite;flex-shrink:0}
  .spinner-dark{border-color:rgba(26,115,232,.2);border-top-color:var(--primary)}
  @keyframes spin{to{transform:rotate(360deg)}}

  @media(max-width:768px){
    .sidebar{transform:translateX(-100%)}.sidebar.open{transform:translateX(0)}
    .main{margin-left:0}.stats-grid{grid-template-columns:1fr 1fr}
    .dashboard-grid{grid-template-columns:1fr}.form-grid{grid-template-columns:1fr}
    .topbar{padding:0 16px}.page{padding:16px}.coverage-grid{grid-template-columns:1fr 1fr}
    .detail-grid{grid-template-columns:1fr}
  }
  ::-webkit-scrollbar{width:6px;height:6px}
  ::-webkit-scrollbar-thumb{background:var(--gray-300);border-radius:3px}
</style>
</head>
<body>

<!-- SIDEBAR -->
<aside class="sidebar" id="sidebar">
  <div class="sidebar-brand">
    <div class="brand-icon">🛡️</div>
    <div><div class="brand-text">Insurance Manager</div><div class="brand-sub">Family Policy Tracker</div></div>
  </div>
  <nav class="sidebar-nav">
    <div class="nav-label">ภาพรวม</div>
    <div class="nav-item active" onclick="navigate('dashboard')"><span class="nav-icon">📊</span>Dashboard</div>
    <div class="nav-item" onclick="navigate('policies')">
      <span class="nav-icon">📋</span>กรมธรรม์ทั้งหมด
      <span class="nav-badge" id="expiring-count" style="display:none">0</span>
    </div>
    <div class="nav-label" style="margin-top:8px">ประเภทประกัน</div>
    <div class="nav-item" onclick="navigate('policies');filterByType('health')"><span class="nav-icon">❤️‍🩹</span>ประกันสุขภาพ</div>
    <div class="nav-item" onclick="navigate('policies');filterByType('accident')"><span class="nav-icon">⚡</span>ประกันอุบัติเหตุ</div>
    <div class="nav-item" onclick="navigate('policies');filterByType('life')"><span class="nav-icon">🌿</span>ประกันชีวิต</div>
    <div class="nav-item" onclick="navigate('policies');filterByType('ci')"><span class="nav-icon">🏥</span>โรคร้ายแรง (CI)</div>
    <div class="nav-label" style="margin-top:8px">จัดการ</div>
    <div class="nav-item" onclick="navigate('members')"><span class="nav-icon">👨‍👩‍👧‍👦</span>สมาชิกครอบครัว</div>
    <div class="nav-item" onclick="navigate('settings')"><span class="nav-icon">⚙️</span>ตั้งค่า Google</div>
  </nav>
  <div class="sidebar-footer">
    <!-- Google Sign-In -->
    <div id="auth-area">
      <button class="gauth-btn" id="signin-btn" onclick="handleSignIn()">
        <span style="font-size:16px">🔐</span>
        <div class="gauth-info"><div class="gauth-name">เข้าสู่ระบบ Google</div><div class="gauth-email">เพื่อใช้ Sheets & Drive</div></div>
      </button>
    </div>
  </div>
</aside>

<!-- MAIN -->
<div class="main">
  <div class="topbar">
    <div class="topbar-title" id="page-title">📊 Dashboard</div>
    <div class="topbar-actions">
      <div id="sync-indicator" style="display:none;align-items:center;gap:6px;font-size:12px;color:var(--gray-600)">
        <div class="spinner spinner-dark"></div> กำลัง Sync...
      </div>
      <button class="btn btn-ghost btn-sm" onclick="exportCSV()">📥 CSV</button>
      <button class="btn btn-primary" id="add-btn" onclick="openAddModal()">＋ เพิ่มกรมธรรม์</button>
    </div>
  </div>

  <!-- DASHBOARD -->
  <div class="page active" id="page-dashboard">
    <div id="alert-area"></div>
    <div id="auth-notice" class="alert-banner alert-info" style="display:none">
      🔐 <div><strong>เชื่อมต่อ Google เพื่อใช้งานเต็มรูปแบบ</strong> — กดปุ่ม "เข้าสู่ระบบ Google" ที่แถบซ้ายเพื่อ Sync ข้อมูลขึ้น Google Sheets และอัพโหลดไฟล์ไปยัง Google Drive</div>
    </div>
    <div class="stats-grid">
      <div class="stat-card"><div class="stat-icon" style="background:#e8f0fe">📋</div>
        <div><div class="stat-value" id="stat-total">0</div><div class="stat-label">กรมธรรม์ทั้งหมด</div></div></div>
      <div class="stat-card"><div class="stat-icon" style="background:#e6f4ea">✅</div>
        <div><div class="stat-value" id="stat-active" style="color:var(--success)">0</div><div class="stat-label">กำลังคุ้มครอง</div></div></div>
      <div class="stat-card"><div class="stat-icon" style="background:#fef9e7">⚠️</div>
        <div><div class="stat-value" id="stat-expiring" style="color:#c77a00">0</div><div class="stat-label">ใกล้หมดอายุ (90 วัน)</div></div></div>
      <div class="stat-card"><div class="stat-icon" style="background:#fce8e6">💰</div>
        <div><div class="stat-value" id="stat-premium" style="color:var(--primary);font-size:18px">-</div><div class="stat-label">เบี้ยรวมต่อปี (฿)</div></div></div>
    </div>
    <div class="dashboard-grid">
      <div class="chart-card">
        <div class="card-header"><div><div class="card-title">สัดส่วนตามประเภทประกัน</div><div class="card-subtitle">จากกรมธรรม์ทั้งหมด</div></div></div>
        <div class="donut-wrap">
          <svg class="donut" id="donut-svg" width="140" height="140" viewBox="0 0 140 140">
            <circle cx="70" cy="70" r="54" fill="none" stroke="#e8eaed" stroke-width="16"/>
          </svg>
          <div class="donut-center"><div class="donut-num" id="donut-num">0</div><div class="donut-lbl">กรมธรรม์</div></div>
        </div>
        <div class="donut-legend" id="donut-legend"></div>
      </div>
      <div class="chart-card">
        <div class="card-header"><div><div class="card-title">กรมธรรม์แต่ละสมาชิก</div><div class="card-subtitle">จำแนกตามประเภท</div></div></div>
        <div class="member-bars" id="member-bars"><div style="text-align:center;padding:20px 0;color:var(--gray-400);font-size:13px">ยังไม่มีข้อมูล</div></div>
      </div>
    </div>
    <div class="dashboard-grid">
      <div class="chart-card">
        <div class="card-header"><div><div class="card-title">🔔 ใกล้หมดอายุ</div><div class="card-subtitle">ภายใน 90 วันข้างหน้า</div></div></div>
        <div class="expiry-list" id="expiry-list"></div>
      </div>
      <div class="chart-card">
        <div class="card-header"><div><div class="card-title">👨‍👩‍👧‍👦 สรุปต่อสมาชิก</div><div class="card-subtitle">คลิกเพื่อกรองในตาราง</div></div></div>
        <div class="member-summary-grid" id="member-summary-cards"></div>
      </div>
    </div>
  </div>

  <!-- POLICIES PAGE -->
  <div class="page" id="page-policies">
    <div class="filter-bar">
      <div class="search-box"><span>🔍</span><input type="text" placeholder="ค้นหา..." id="search-input" oninput="renderTable()"></div>
      <select class="filter-select" id="filter-member" onchange="renderTable()"><option value="">👤 ทุกสมาชิก</option></select>
      <select class="filter-select" id="filter-type" onchange="renderTable()">
        <option value="">📋 ทุกประเภท</option>
        <option value="health">❤️‍🩹 สุขภาพ</option>
        <option value="accident">⚡ อุบัติเหตุ</option>
        <option value="life">🌿 ชีวิต</option>
        <option value="ci">🏥 โรคร้ายแรง</option>
        <option value="other">📌 อื่นๆ</option>
      </select>
      <select class="filter-select" id="filter-status" onchange="renderTable()">
        <option value="">📍 ทุกสถานะ</option>
        <option value="active">✅ คุ้มครองอยู่</option>
        <option value="expiring">⚠️ ใกล้หมดอายุ</option>
        <option value="expired">❌ หมดอายุ</option>
      </select>
      <button class="btn btn-ghost btn-sm" onclick="clearFilters()">✕ ล้าง</button>
    </div>
    <div class="table-card">
      <div class="table-wrap">
        <table>
          <thead><tr>
            <th onclick="sortTable('member')">สมาชิก</th>
            <th onclick="sortTable('type')">ประเภท</th>
            <th onclick="sortTable('company')">บริษัทประกัน</th>
            <th onclick="sortTable('policy_no')">เลขกรมธรรม์</th>
            <th onclick="sortTable('end_date')">หมดอายุ</th>
            <th onclick="sortTable('premium')">เบี้ย/ปี</th>
            <th>ไฟล์แนบ</th>
            <th>สถานะ</th>
            <th>จัดการ</th>
          </tr></thead>
          <tbody id="policy-tbody"></tbody>
        </table>
      </div>
      <div id="empty-state" class="empty-state" style="display:none">
        <div class="empty-icon">🛡️</div><div class="empty-title">ยังไม่มีกรมธรรม์</div>
        <div class="empty-desc">กดปุ่ม "＋ เพิ่มกรมธรรม์" เพื่อเริ่มบันทึก</div>
        <button class="btn btn-primary" onclick="openAddModal()">＋ เพิ่มกรมธรรม์แรก</button>
      </div>
    </div>
  </div>

  <!-- MEMBERS PAGE -->
  <div class="page" id="page-members">
    <div style="display:flex;justify-content:flex-end;margin-bottom:16px">
      <button class="btn btn-primary" onclick="openMemberModal()">＋ เพิ่มสมาชิก</button>
    </div>
    <div class="members-grid" id="members-grid"></div>
  </div>

  <!-- SETTINGS PAGE -->
  <div class="page" id="page-settings">
    <!-- Google Account Status -->
    <div class="config-section">
      <div class="config-title">🔐 สถานะ Google Account</div>
      <div class="config-desc">ต้อง Login ด้วย Google ก่อนจึงจะ Sync ขึ้น Sheets และอัพโหลดไฟล์ไปยัง Drive ได้</div>
      <div id="settings-auth-status" class="sync-status">
        <div class="sync-dot sync-inactive"></div><span>ยังไม่ได้ Login</span>
      </div>
    </div>

    <!-- Google Client ID -->
    <div class="config-section">
      <div class="config-title">⚙️ ตั้งค่า OAuth Client ID</div>
      <div class="config-desc">สร้างจาก Google Cloud Console → APIs & Services → Credentials → OAuth 2.0 Client ID (Web Application)</div>
      <ol class="step-list">
        <li>ไปที่ <strong>console.cloud.google.com</strong> → สร้าง Project ใหม่</li>
        <li>เปิด <strong>Google Sheets API</strong> และ <strong>Google Drive API</strong></li>
        <li>สร้าง <strong>OAuth 2.0 Client ID</strong> ประเภท Web Application</li>
        <li>เพิ่ม Authorized JavaScript origins: <code style="background:var(--gray-100);padding:2px 6px;border-radius:4px" id="current-origin"></code></li>
        <li>คัดลอก <strong>Client ID</strong> มาวางด้านล่าง แล้วกด Save</li>
      </ol>
      <div class="form-group" style="margin-top:16px">
        <label class="form-label">Google OAuth Client ID</label>
        <div style="display:flex;gap:8px">
          <input type="text" class="form-input" id="client-id-input" placeholder="xxxxxxxxxxxx-xxxxxxxxxxxxxxxx.apps.googleusercontent.com">
          <button class="btn btn-primary" onclick="saveClientId()">💾 Save</button>
        </div>
      </div>
    </div>

    <!-- Google Sheets Config -->
    <div class="config-section">
      <div class="config-title">📊 Google Sheets — เก็บข้อมูลกรมธรรม์</div>
      <div class="config-desc">ข้อมูลที่กรอกในฟอร์มจะ Sync ขึ้น Google Sheets อัตโนมัติทุกครั้งที่บันทึก</div>
      <div class="form-grid">
        <div class="form-group full">
          <label class="form-label">Spreadsheet ID (จาก URL ของ Sheet)</label>
          <input type="text" class="form-input" id="sheet-id" placeholder="1BxiMVs0XRA5nFMdKvBdBZjgmUUqptlbs74OgVE2upms">
        </div>
        <div class="form-group">
          <label class="form-label">Sheet Name</label>
          <input type="text" class="form-input" id="sheet-name" value="Policies">
        </div>
        <div class="form-group">
          <label class="form-label">Auto-sync ทุก (นาที)</label>
          <select class="form-input" id="sync-interval">
            <option value="0">ปิด</option><option value="5">5</option>
            <option value="15" selected>15</option><option value="30">30</option><option value="60">60</option>
          </select>
        </div>
        <div class="form-group full" style="flex-direction:row;gap:10px;flex-wrap:wrap">
          <button class="btn btn-primary" onclick="saveSheetConfig()">💾 บันทึก</button>
          <button class="btn btn-outline" onclick="syncToSheet()">🔄 Sync ตอนนี้</button>
          <button class="btn btn-ghost" onclick="importFromSheet()">📥 Import จาก Sheet</button>
        </div>
      </div>
      <div class="code-block" style="margin-top:12px;font-size:11px">
Columns: id | member | type | company | policy_no | plan_name | start_date | end_date | premium | sum_insured | coverage | beneficiary | drive_folder_id | notes | updated_at
      </div>
    </div>

    <!-- Google Drive Config -->
    <div class="config-section">
      <div class="config-title">📁 Google Drive — เก็บไฟล์กรมธรรม์</div>
      <div class="config-desc">ไฟล์ PDF และเอกสารแนบจะถูกอัพโหลดไปยัง Google Drive โดยอัตโนมัติเมื่อบันทึกกรมธรรม์</div>
      <div id="drive-folder-display"></div>
      <div class="form-group">
        <label class="form-label">Root Folder ID (ปล่อยว่าง = สร้างใหม่อัตโนมัติชื่อ "Family Insurance")</label>
        <div style="display:flex;gap:8px">
          <input type="text" class="form-input" id="drive-folder-id" placeholder="ใส่ Folder ID หรือปล่อยว่างให้สร้างอัตโนมัติ">
          <button class="btn btn-outline" onclick="initDriveFolder()">📁 สร้าง/เชื่อม Folder</button>
        </div>
      </div>
    </div>

    <!-- Danger Zone -->
    <div class="config-section" style="border-color:var(--danger-light)">
      <div class="config-title" style="color:var(--danger)">🗑️ จัดการข้อมูล</div>
      <div style="display:flex;gap:10px;flex-wrap:wrap;margin-top:8px">
        <button class="btn btn-ghost" onclick="exportCSV()">📥 Export CSV</button>
        <button class="btn btn-danger" onclick="clearAllData()">🗑️ ล้างข้อมูลทั้งหมด</button>
      </div>
    </div>
  </div>
</div>

<!-- ADD/EDIT POLICY MODAL -->
<div class="modal-overlay" id="policy-modal">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title" id="modal-title">➕ เพิ่มกรมธรรม์ใหม่</div>
      <button class="modal-close" onclick="closeModal('policy-modal')">✕</button>
    </div>
    <div class="modal-body">
      <div class="form-grid">
        <div class="form-group full">
          <label class="form-label">ประเภทประกัน <span class="req">*</span></label>
          <div class="type-selector">
            <div class="type-chip" onclick="selectType('health')" data-type="health">❤️‍🩹 สุขภาพ</div>
            <div class="type-chip" onclick="selectType('accident')" data-type="accident">⚡ อุบัติเหตุ</div>
            <div class="type-chip" onclick="selectType('life')" data-type="life">🌿 ชีวิต</div>
            <div class="type-chip" onclick="selectType('ci')" data-type="ci">🏥 โรคร้ายแรง</div>
            <div class="type-chip" onclick="selectType('other')" data-type="other">📌 อื่นๆ</div>
          </div>
          <input type="hidden" id="f-type">
        </div>
        <div class="form-group">
          <label class="form-label">สมาชิก <span class="req">*</span></label>
          <select class="form-input" id="f-member"></select>
        </div>
        <div class="form-group">
          <label class="form-label">บริษัทประกัน <span class="req">*</span></label>
          <input type="text" class="form-input" id="f-company" placeholder="เช่น AIA, เมืองไทย, Allianz">
        </div>
        <div class="form-group">
          <label class="form-label">เลขกรมธรรม์</label>
          <input type="text" class="form-input" id="f-policy-no" placeholder="TH-2024-001">
        </div>
        <div class="form-group">
          <label class="form-label">ชื่อแผน</label>
          <input type="text" class="form-input" id="f-plan" placeholder="เช่น Health Plus Gold">
        </div>
        <hr class="form-divider">
        <div class="form-section-title">📅 ระยะเวลาคุ้มครอง</div>
        <div class="form-group">
          <label class="form-label">วันเริ่มคุ้มครอง <span class="req">*</span></label>
          <input type="date" class="form-input" id="f-start">
        </div>
        <div class="form-group">
          <label class="form-label">วันหมดอายุ <span class="req">*</span></label>
          <input type="date" class="form-input" id="f-end">
        </div>
        <hr class="form-divider">
        <div class="form-section-title">💰 การเงิน</div>
        <div class="form-group">
          <label class="form-label">เบี้ยประกัน/ปี (฿)</label>
          <input type="number" class="form-input" id="f-premium" placeholder="0">
        </div>
        <div class="form-group">
          <label class="form-label">ทุนประกันรวม (฿)</label>
          <input type="number" class="form-input" id="f-sum" placeholder="0">
        </div>
        <div class="form-group">
          <label class="form-label">ผู้รับผลประโยชน์</label>
          <input type="text" class="form-input" id="f-beneficiary" placeholder="เช่น ภรรยา, ลูก">
        </div>
        <div class="form-group">
          <label class="form-label">ความถี่ชำระ</label>
          <select class="form-input" id="f-freq">
            <option value="yearly">รายปี</option><option value="halfyearly">ราย 6 เดือน</option>
            <option value="quarterly">รายไตรมาส</option><option value="monthly">รายเดือน</option>
          </select>
        </div>
        <hr class="form-divider">
        <div class="form-section-title">🩺 ความคุ้มครอง</div>
        <div class="form-group full">
          <div class="coverage-grid">
            <label class="coverage-check"><input type="checkbox" value="ipd"> 🏥 ผู้ป่วยใน (IPD)</label>
            <label class="coverage-check"><input type="checkbox" value="opd"> 🩺 ผู้ป่วยนอก (OPD)</label>
            <label class="coverage-check"><input type="checkbox" value="dental"> 🦷 ทันตกรรม</label>
            <label class="coverage-check"><input type="checkbox" value="vision"> 👁️ สายตา</label>
            <label class="coverage-check"><input type="checkbox" value="maternity"> 🤰 คลอดบุตร</label>
            <label class="coverage-check"><input type="checkbox" value="critical"> 🔴 โรคร้ายแรง</label>
            <label class="coverage-check"><input type="checkbox" value="accident_med"> ⚡ ค่ารักษาอุบัติเหตุ</label>
            <label class="coverage-check"><input type="checkbox" value="death"> 💐 เสียชีวิต</label>
            <label class="coverage-check"><input type="checkbox" value="disability"> ♿ ทุพพลภาพ</label>
            <label class="coverage-check"><input type="checkbox" value="saving"> 💰 สะสมทรัพย์</label>
            <label class="coverage-check"><input type="checkbox" value="retirement"> 👴 บำนาญ</label>
            <label class="coverage-check"><input type="checkbox" value="other_cov"> 📌 อื่นๆ</label>
          </div>
        </div>
        <hr class="form-divider">
        <div class="form-section-title">📎 ไฟล์แนบ → Google Drive</div>
        <div class="form-group full">
          <div id="upload-not-signed-in" style="display:none" class="alert-banner alert-info" style="margin:0">
            🔐 กรุณา Login ด้วย Google ก่อนเพื่ออัพโหลดไฟล์ไปยัง Google Drive
          </div>
          <div id="upload-area-wrap">
            <div class="upload-area" id="upload-area" onclick="document.getElementById('file-input').click()"
              ondragover="event.preventDefault();this.classList.add('dragover')"
              ondragleave="this.classList.remove('dragover')"
              ondrop="handleDrop(event)">
              <input type="file" id="file-input" multiple accept=".pdf,.jpg,.jpeg,.png,.gif" onchange="handleFileSelect(event)">
              <div class="upload-icon">📎</div>
              <div class="upload-text">คลิกหรือลากไฟล์มาวางที่นี่</div>
              <div class="upload-sub">รองรับ PDF, JPG, PNG (ไฟล์ละสูงสุด 20MB)</div>
            </div>
            <div class="file-list" id="file-list"></div>
          </div>
        </div>
        <div class="form-group full">
          <label class="form-label">หมายเหตุ</label>
          <textarea class="form-input" id="f-notes" placeholder="เช่น เงื่อนไขพิเศษ, contact agent..."></textarea>
        </div>
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
  <div class="modal" style="max-width:620px">
    <div class="modal-header">
      <div class="modal-title">📋 รายละเอียดกรมธรรม์</div>
      <button class="modal-close" onclick="closeModal('detail-modal')">✕</button>
    </div>
    <div class="modal-body" id="detail-content"></div>
    <div class="modal-footer">
      <button class="btn btn-ghost" onclick="closeModal('detail-modal')">ปิด</button>
      <button class="btn btn-outline" id="detail-edit-btn">✏️ แก้ไข</button>
      <button class="btn btn-danger btn-sm" id="detail-delete-btn">🗑️ ลบ</button>
    </div>
  </div>
</div>

<!-- MEMBER MODAL -->
<div class="modal-overlay" id="member-modal">
  <div class="modal" style="max-width:440px">
    <div class="modal-header">
      <div class="modal-title">👤 เพิ่มสมาชิกครอบครัว</div>
      <button class="modal-close" onclick="closeModal('member-modal')">✕</button>
    </div>
    <div class="modal-body">
      <div class="form-grid">
        <div class="form-group full">
          <label class="form-label">ชื่อ-นามสกุล <span class="req">*</span></label>
          <input type="text" class="form-input" id="m-name" placeholder="เช่น สมชาย ใจดี">
        </div>
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
        <div class="form-group">
          <label class="form-label">สีประจำตัว</label>
          <input type="color" class="form-input" id="m-color" value="#1a73e8" style="height:40px;cursor:pointer">
        </div>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-ghost" onclick="closeModal('member-modal')">ยกเลิก</button>
      <button class="btn btn-primary" onclick="saveMember()">💾 เพิ่มสมาชิก</button>
    </div>
  </div>
</div>

<div class="toast-container" id="toast-container"></div>

<script>
// ═══════════════════════════════════════════════════════════
//  STATE
// ═══════════════════════════════════════════════════════════
let policies = [];
let members  = [];
let editingId = null;
let selectedType = '';
let sortField = 'end_date', sortDir = 1;
let pendingFiles = [];   // files waiting to upload
let syncTimer = null;

// Google Auth state
let gapiInited = false;
let gisInited  = false;
let tokenClient = null;
let accessToken = null;
let currentUser = null;

// Config (persisted)
let cfg = {
  clientId    : '',
  sheetId     : '',
  sheetName   : 'Policies',
  syncInterval: 15,
  driveFolderId: '',
};

const TYPE_CFG = {
  health  : { label:'สุขภาพ',     icon:'❤️‍🩹', color:'#34a853', bg:'#e6f4ea' },
  accident: { label:'อุบัติเหตุ', icon:'⚡',   color:'#c77a00', bg:'#fef9e7' },
  life    : { label:'ชีวิต',      icon:'🌿',   color:'#9c27b0', bg:'#f3e5f5' },
  ci      : { label:'โรคร้ายแรง', icon:'🏥',  color:'#ff6d00', bg:'#fff3e0' },
  other   : { label:'อื่นๆ',      icon:'📌',   color:'#1a73e8', bg:'#e8f0fe' },
};
const COV_LBL = {
  ipd:'ผู้ป่วยใน (IPD)', opd:'ผู้ป่วยนอก (OPD)', dental:'ทันตกรรม',
  vision:'สายตา', maternity:'คลอดบุตร', critical:'โรคร้ายแรง',
  accident_med:'ค่ารักษาอุบัติเหตุ', death:'เสียชีวิต',
  disability:'ทุพพลภาพ', saving:'สะสมทรัพย์', retirement:'บำนาญ', other_cov:'อื่นๆ',
};
const PALETTE = ['#1a73e8','#34a853','#9c27b0','#ff6d00','#ea4335','#00acc1','#f06292','#8d6e63'];

// ═══════════════════════════════════════════════════════════
//  INIT
// ═══════════════════════════════════════════════════════════
function init() {
  loadLocal();
  document.getElementById('current-origin').textContent = location.origin;
  if (cfg.clientId) document.getElementById('client-id-input').value = cfg.clientId;
  if (cfg.sheetId)  document.getElementById('sheet-id').value = cfg.sheetId;
  document.getElementById('sheet-name').value = cfg.sheetName;
  document.getElementById('drive-folder-id').value = cfg.driveFolderId || '';

  if (!members.length) {
    members = [{ id:uid(), name:'ฉัน (ตัวเอง)', role:'ตัวเอง', color:'#1a73e8', dob:'' }];
    saveLocal();
  }
  populateMemberDropdowns();
  renderAll();
  checkAlerts();

  // Init Google APIs
  loadGoogleAPIs();

  // Show auth notice if not signed in
  updateAuthUI();
}

function loadLocal() {
  try {
    policies = JSON.parse(localStorage.getItem('ins_policies') || '[]');
    members  = JSON.parse(localStorage.getItem('ins_members')  || '[]');
    cfg      = Object.assign({clientId:'',sheetId:'',sheetName:'Policies',syncInterval:15,driveFolderId:''},
                JSON.parse(localStorage.getItem('ins_cfg') || '{}'));
  } catch(e) { policies=[]; members=[]; }
}
function saveLocal() {
  localStorage.setItem('ins_policies', JSON.stringify(policies));
  localStorage.setItem('ins_members',  JSON.stringify(members));
  localStorage.setItem('ins_cfg',      JSON.stringify(cfg));
}
function uid() { return Date.now().toString(36)+Math.random().toString(36).substr(2,5); }

// ═══════════════════════════════════════════════════════════
//  GOOGLE APIS BOOTSTRAP
// ═══════════════════════════════════════════════════════════
function loadGoogleAPIs() {
  if (!cfg.clientId) return;

  // Load GAPI (for Sheets & Drive REST)
  if (typeof gapi !== 'undefined') {
    gapi.load('client', initGapiClient);
  } else {
    window.gapiLoadCallback = () => gapi.load('client', initGapiClient);
  }

  // Load GIS token client
  if (typeof google !== 'undefined' && google.accounts) {
    initTokenClient();
  } else {
    window.gisLoadCallback = initTokenClient;
  }
}

async function initGapiClient() {
  await gapi.client.init({
    discoveryDocs: [
      'https://sheets.googleapis.com/$discovery/rest?version=v4',
      'https://www.googleapis.com/discovery/v1/apis/drive/v3/rest',
    ],
  });
  gapiInited = true;
  maybeEnableUI();
}

function initTokenClient() {
  if (!cfg.clientId) return;
  tokenClient = google.accounts.oauth2.initTokenClient({
    client_id: cfg.clientId,
    scope: [
      'https://www.googleapis.com/auth/spreadsheets',
      'https://www.googleapis.com/auth/drive.file',
      'profile', 'email',
    ].join(' '),
    callback: handleTokenResponse,
  });
  gisInited = true;
  maybeEnableUI();
}

function maybeEnableUI() {
  if (gapiInited && gisInited) {
    console.log('Google APIs ready');
  }
}

function handleTokenResponse(resp) {
  if (resp.error) { showToast('Login ไม่สำเร็จ: ' + resp.error, 'error'); return; }
  accessToken = resp.access_token;
  gapi.client.setToken({ access_token: accessToken });

  // Fetch profile via tokeninfo
  fetch(`https://www.googleapis.com/oauth2/v3/userinfo`, {
    headers: { Authorization: 'Bearer ' + accessToken }
  }).then(r=>r.json()).then(profile => {
    currentUser = profile;
    updateAuthUI();
    showToast(`สวัสดี ${profile.name} 👋`, 'success');
    // Auto-init Drive folder
    if (!cfg.driveFolderId) initDriveFolder();
  });
}

function handleSignIn() {
  if (!cfg.clientId) {
    showToast('กรุณาตั้งค่า Client ID ก่อนครับ (ไปที่ ⚙️ ตั้งค่า Google)', 'warn');
    navigate('settings'); return;
  }
  if (!tokenClient) { initTokenClient(); }
  if (!gapi.client) {
    gapi.load('client', async () => { await initGapiClient(); tokenClient.requestAccessToken(); });
  } else {
    tokenClient.requestAccessToken({ prompt: accessToken ? '' : 'consent' });
  }
}

function handleSignOut() {
  if (accessToken) google.accounts.oauth2.revoke(accessToken, ()=>{});
  accessToken = null; currentUser = null;
  gapi.client.setToken(null);
  updateAuthUI();
  showToast('ออกจากระบบแล้ว', 'warn');
}

function updateAuthUI() {
  const authArea = document.getElementById('auth-area');
  const notice   = document.getElementById('auth-notice');
  const settingsStatus = document.getElementById('settings-auth-status');
  const uploadWarn = document.getElementById('upload-not-signed-in');

  if (currentUser) {
    authArea.innerHTML = `
      <div class="gauth-btn signed-in">
        ${currentUser.picture ? `<img class="gauth-avatar" src="${currentUser.picture}">` : '✅'}
        <div class="gauth-info">
          <div class="gauth-name">${currentUser.name}</div>
          <div class="gauth-email">${currentUser.email}</div>
        </div>
        <button onclick="handleSignOut()" style="background:none;border:none;cursor:pointer;color:inherit;font-size:14px" title="ออกจากระบบ">✕</button>
      </div>`;
    if (notice) notice.style.display = 'none';
    if (settingsStatus) settingsStatus.innerHTML = `<div class="sync-dot sync-active"></div><span>Login แล้ว: <strong>${currentUser.email}</strong></span>`;
    if (uploadWarn) uploadWarn.style.display = 'none';
    if (cfg.driveFolderId) renderDriveFolderCard();
    setupAutoSync();
  } else {
    authArea.innerHTML = `
      <button class="gauth-btn" onclick="handleSignIn()">
        <span style="font-size:16px">🔐</span>
        <div class="gauth-info"><div class="gauth-name">เข้าสู่ระบบ Google</div><div class="gauth-email">เพื่อใช้ Sheets & Drive</div></div>
      </button>`;
    if (notice) notice.style.display = 'flex';
    if (settingsStatus) settingsStatus.innerHTML = `<div class="sync-dot sync-inactive"></div><span>ยังไม่ได้ Login</span>`;
    if (uploadWarn) uploadWarn.style.display = 'flex';
  }
}

// ═══════════════════════════════════════════════════════════
//  NAVIGATION
// ═══════════════════════════════════════════════════════════
function navigate(page) {
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.nav-item').forEach(n=>n.classList.remove('active'));
  document.getElementById('page-'+page).classList.add('active');
  const T = {dashboard:'📊 Dashboard',policies:'📋 กรมธรรม์ทั้งหมด',members:'👨‍👩‍👧‍👦 สมาชิกครอบครัว',settings:'⚙️ ตั้งค่า Google'};
  document.getElementById('page-title').textContent = T[page]||page;
  if (page==='policies') renderTable();
  if (page==='members')  renderMembers();
  if (page==='dashboard') renderDashboard();
}
function filterByType(t) { document.getElementById('filter-type').value=t; renderTable(); }
function clearFilters() {
  ['search-input','filter-member','filter-type','filter-status'].forEach(id=>{
    const el=document.getElementById(id); if(el) el.value='';
  }); renderTable();
}

// ═══════════════════════════════════════════════════════════
//  DATE UTILS
// ═══════════════════════════════════════════════════════════
function daysLeft(d) {
  if (!d) return Infinity;
  const now=new Date(); now.setHours(0,0,0,0);
  return Math.ceil((new Date(d)-now)/86400000);
}
function thaiDate(s) {
  if (!s) return '-';
  const d=new Date(s);
  const m=['ม.ค.','ก.พ.','มี.ค.','เม.ย.','พ.ค.','มิ.ย.','ก.ค.','ส.ค.','ก.ย.','ต.ค.','พ.ย.','ธ.ค.'];
  return `${d.getDate()} ${m[d.getMonth()]} ${d.getFullYear()+543}`;
}
function fmtMoney(n) { return n?Number(n).toLocaleString('th-TH')+' ฿':'-'; }
function getStatus(p) { const d=daysLeft(p.end_date); return d<0?'expired':d<=90?'expiring':'active'; }
function getMember(id) { return members.find(m=>m.id===id)||{name:id,color:'#9aa0a6'}; }
function getInitials(n) { return (n||'?').split(' ').map(w=>w[0]).join('').substr(0,2).toUpperCase(); }

function populateMemberDropdowns() {
  ['f-member','filter-member'].forEach(id=>{
    const sel=document.getElementById(id); if(!sel) return;
    const prev=sel.value;
    sel.innerHTML = id==='filter-member'
      ? '<option value="">👤 ทุกสมาชิก</option>'
      : '<option value="">-- เลือกสมาชิก --</option>';
    members.forEach(m=>{ const o=document.createElement('option'); o.value=m.id; o.textContent=m.name+(m.role?` (${m.role})`:''); sel.appendChild(o); });
    sel.value=prev;
  });
}

// ═══════════════════════════════════════════════════════════
//  RENDER ALL
// ═══════════════════════════════════════════════════════════
function renderAll() { renderDashboard(); renderTable(); renderMembers(); updateExpiringBadge(); }

// ═══════════════════════════════════════════════════════════
//  DASHBOARD
// ═══════════════════════════════════════════════════════════
function renderDashboard() {
  const total    = policies.length;
  const active   = policies.filter(p=>getStatus(p)==='active').length;
  const expiring = policies.filter(p=>getStatus(p)==='expiring').length;
  const premium  = policies.reduce((a,p)=>a+Number(p.premium||0),0);
  document.getElementById('stat-total').textContent   = total;
  document.getElementById('stat-active').textContent  = active;
  document.getElementById('stat-expiring').textContent= expiring;
  document.getElementById('stat-premium').textContent = premium?premium.toLocaleString('th-TH'):'-';
  renderDonut(); renderMemberBars(); renderExpiryList(); renderMemberCards();
}

function renderDonut() {
  const svg=document.getElementById('donut-svg');
  const legend=document.getElementById('donut-legend');
  document.getElementById('donut-num').textContent=policies.length;
  svg.querySelectorAll('.dseg').forEach(e=>e.remove());
  if (!policies.length) { legend.innerHTML='<span style="color:var(--gray-400);font-size:12px">ยังไม่มีข้อมูล</span>'; return; }
  const counts={};
  policies.forEach(p=>{ counts[p.type]=(counts[p.type]||0)+1; });
  const total=policies.length, r=54, circ=2*Math.PI*r;
  let off=0;
  Object.entries(counts).forEach(([type,n])=>{
    const cfg2=TYPE_CFG[type]||TYPE_CFG.other, pct=n/total, dash=pct*circ;
    const c=document.createElementNS('http://www.w3.org/2000/svg','circle');
    c.setAttribute('class','dseg'); c.setAttribute('cx',70); c.setAttribute('cy',70); c.setAttribute('r',r);
    c.setAttribute('fill','none'); c.setAttribute('stroke',cfg2.color); c.setAttribute('stroke-width',16);
    c.setAttribute('stroke-dasharray',`${dash} ${circ-dash}`);
    c.setAttribute('stroke-dashoffset',-(off*circ));
    svg.appendChild(c); off+=pct;
  });
  legend.innerHTML=Object.entries(counts).map(([t,n])=>{
    const c=TYPE_CFG[t]||TYPE_CFG.other;
    return `<div class="legend-item"><div class="legend-dot" style="background:${c.color}"></div>${c.icon} ${c.label} (${n})</div>`;
  }).join('');
}

function renderMemberBars() {
  const el=document.getElementById('member-bars');
  if (!members.length) { el.innerHTML='<div style="text-align:center;padding:20px;color:var(--gray-400);font-size:13px">ยังไม่มีสมาชิก</div>'; return; }
  el.innerHTML=members.map(m=>{
    const mp=policies.filter(p=>p.member===m.id);
    const tc={};
    mp.forEach(p=>{ tc[p.type]=(tc[p.type]||0)+1; });
    const segs=Object.entries(tc).map(([t,c])=>{
      const cfg2=TYPE_CFG[t]||TYPE_CFG.other, w=(c/Math.max(mp.length,1))*100;
      return `<div class="bar-seg" style="width:${w}%;background:${cfg2.color}"></div>`;
    }).join('');
    return `<div class="member-bar-row">
      <div style="display:flex;align-items:center;gap:6px;width:110px;flex-shrink:0">
        <div class="member-avatar" style="background:${m.color};width:26px;height:26px;font-size:11px">${getInitials(m.name)}</div>
        <span style="font-size:12px;font-weight:500;color:var(--gray-800)">${m.name.split(' ')[0]}</span>
      </div>
      <div class="bar-track">${mp.length?segs:'<div style="width:100%;border-radius:100px"></div>'}</div>
      <div class="bar-count">${mp.length}</div>
    </div>`;
  }).join('');
}

function renderExpiryList() {
  const el=document.getElementById('expiry-list');
  const exp=policies.filter(p=>{ const d=daysLeft(p.end_date); return d>=0&&d<=90; })
    .sort((a,b)=>daysLeft(a.end_date)-daysLeft(b.end_date)).slice(0,8);
  if (!exp.length) { el.innerHTML='<div style="text-align:center;padding:16px;color:var(--gray-400);font-size:13px">ไม่มีกรมธรรม์ที่ใกล้หมดอายุ 🎉</div>'; return; }
  el.innerHTML=exp.map(p=>{
    const mem=getMember(p.member), cfg2=TYPE_CFG[p.type]||TYPE_CFG.other, d=daysLeft(p.end_date);
    const cls=d<=30?'days-critical':d<=60?'days-warning':'days-ok';
    return `<div class="expiry-item" onclick="showDetail('${p.id}')">
      <div class="expiry-avatar" style="background:${mem.color}">${getInitials(mem.name)}</div>
      <div class="expiry-info">
        <div class="expiry-name">${mem.name} — ${p.company||'(ไม่ระบุ)'}</div>
        <div class="expiry-type">${cfg2.icon} ${cfg2.label} · ${p.plan_name||''}</div>
      </div>
      <div class="expiry-days ${cls}">${d} วัน<br><span style="font-size:9px;font-weight:400">${thaiDate(p.end_date)}</span></div>
    </div>`;
  }).join('');
}

function renderMemberCards() {
  const el=document.getElementById('member-summary-cards');
  el.innerHTML=members.map(m=>{
    const mp=policies.filter(p=>p.member===m.id);
    const types=[...new Set(mp.map(p=>p.type))];
    const badges=types.map(t=>{ const c=TYPE_CFG[t]||TYPE_CFG.other; return `<div class="mini-badge" style="background:${c.bg};color:${c.color}">${c.icon} ${c.label}</div>`; }).join('');
    return `<div class="member-card" onclick="filterByMember('${m.id}')">
      <div style="display:flex;align-items:center;gap:8px;margin-bottom:10px">
        <div class="member-avatar" style="background:${m.color};width:34px;height:34px;font-size:13px">${getInitials(m.name)}</div>
        <div><div style="font-size:13px;font-weight:700">${m.name}</div><div style="font-size:11px;color:var(--gray-500)">${m.role||''} · ${mp.length} กรมธรรม์</div></div>
      </div>
      <div class="member-policy-types">${badges||'<span style="font-size:11px;color:var(--gray-400)">ยังไม่มีกรมธรรม์</span>'}</div>
    </div>`;
  }).join('');
}

function filterByMember(id) { navigate('policies'); document.getElementById('filter-member').value=id; renderTable(); }

function checkAlerts() {
  const area=document.getElementById('alert-area');
  const crit=policies.filter(p=>{ const d=daysLeft(p.end_date); return d>=0&&d<=30; });
  const warn=policies.filter(p=>{ const d=daysLeft(p.end_date); return d>30&&d<=60; });
  let html='';
  if (crit.length) html+=`<div class="alert-banner alert-danger">🚨 <div><strong>แจ้งเตือนด่วน:</strong> มี ${crit.length} กรมธรรม์จะหมดอายุใน 30 วัน — ตรวจสอบและต่ออายุโดยเร็ว</div></div>`;
  if (warn.length) html+=`<div class="alert-banner alert-warning">⚠️ มี ${warn.length} กรมธรรม์จะหมดอายุใน 31–60 วัน</div>`;
  area.innerHTML=html;
}

function updateExpiringBadge() {
  const n=policies.filter(p=>{ const d=daysLeft(p.end_date); return d>=0&&d<=90; }).length;
  const b=document.getElementById('expiring-count');
  b.style.display=n?'inline':'none'; b.textContent=n;
}

// ═══════════════════════════════════════════════════════════
//  TABLE
// ═══════════════════════════════════════════════════════════
function getFiltered() {
  const q=(document.getElementById('search-input')?.value||'').toLowerCase();
  const mf=document.getElementById('filter-member')?.value||'';
  const tf=document.getElementById('filter-type')?.value||'';
  const sf=document.getElementById('filter-status')?.value||'';
  return policies.filter(p=>{
    const mem=getMember(p.member);
    const str=[p.company,p.policy_no,p.plan_name,mem.name].join(' ').toLowerCase();
    if (q&&!str.includes(q)) return false;
    if (mf&&p.member!==mf) return false;
    if (tf&&p.type!==tf) return false;
    if (sf&&getStatus(p)!==sf) return false;
    return true;
  }).sort((a,b)=>{
    let va=a[sortField]||'', vb=b[sortField]||'';
    if (sortField==='premium'){ va=Number(va)||0; vb=Number(vb)||0; }
    return va<vb?-sortDir:va>vb?sortDir:0;
  });
}

function renderTable() {
  const tbody=document.getElementById('policy-tbody');
  const empty=document.getElementById('empty-state');
  const rows=getFiltered();
  if (!rows.length) { tbody.innerHTML=''; empty.style.display='block'; return; }
  empty.style.display='none';
  tbody.innerHTML=rows.map(p=>{
    const mem=getMember(p.member), c=TYPE_CFG[p.type]||TYPE_CFG.other;
    const st=getStatus(p), d=daysLeft(p.end_date);
    const stMap={active:['status-active','คุ้มครองอยู่'],expiring:['status-expiring','ใกล้หมดอายุ'],expired:['status-expired','หมดอายุ']};
    const [dc,sl]=stMap[st];
    let endCell=thaiDate(p.end_date);
    if (st==='expiring') endCell+=` <small style="color:var(--warning);font-weight:600">(${d}ว.)</small>`;
    if (st==='expired')  endCell+=` <small style="color:var(--danger);font-weight:600">(หมดแล้ว)</small>`;

    // File chips
    const files=p.driveFiles||[];
    const fileChips=files.length
      ? files.map(f=>`<a class="file-chip" href="${f.webViewLink||'#'}" target="_blank" title="${f.name}">📎 ${f.name}</a>`).join('')
      : `<span style="font-size:11px;color:var(--gray-400)">ไม่มีไฟล์</span>`;

    return `<tr>
      <td><div class="td-member"><div class="member-avatar" style="background:${mem.color}">${getInitials(mem.name)}</div>${mem.name}</div></td>
      <td><span class="badge badge-${p.type}">${c.icon} ${c.label}</span></td>
      <td>${p.company||'-'}</td>
      <td><span style="font-family:monospace;font-size:11px;color:var(--gray-600)">${p.policy_no||'-'}</span></td>
      <td>${endCell}</td>
      <td style="font-weight:600">${fmtMoney(p.premium)}</td>
      <td style="max-width:160px">${fileChips}</td>
      <td><span class="status-dot ${dc}"></span>${sl}</td>
      <td><div class="row-actions">
        <button class="btn btn-ghost btn-sm" onclick="showDetail('${p.id}')">👁️</button>
        <button class="btn btn-ghost btn-sm" onclick="editPolicy('${p.id}')">✏️</button>
        <button class="btn btn-ghost btn-sm" style="color:var(--danger)" onclick="deletePolicy('${p.id}')">🗑️</button>
      </div></td>
    </tr>`;
  }).join('');
}

function sortTable(f) {
  sortDir=sortField===f?-sortDir:1; sortField=f; renderTable();
}

// ═══════════════════════════════════════════════════════════
//  FILE HANDLING (UI)
// ═══════════════════════════════════════════════════════════
function handleFileSelect(e) { addFiles([...e.target.files]); e.target.value=''; }
function handleDrop(e) {
  e.preventDefault();
  document.getElementById('upload-area').classList.remove('dragover');
  addFiles([...e.dataTransfer.files]);
}
function addFiles(files) {
  files.forEach(f=>{
    if (f.size>20*1024*1024) { showToast(`"${f.name}" ใหญ่เกิน 20MB`, 'error'); return; }
    if (!pendingFiles.find(x=>x.file.name===f.name&&x.file.size===f.size))
      pendingFiles.push({ file:f, status:'pending', driveId:null, webViewLink:null });
  });
  renderFileList();
}
function removeFile(i) { pendingFiles.splice(i,1); renderFileList(); }
function renderFileList() {
  const el=document.getElementById('file-list'); if(!el) return;
  el.innerHTML=pendingFiles.map((pf,i)=>{
    const icon=pf.file.name.endsWith('.pdf')?'📄':'🖼️';
    const sz=(pf.file.size/1024).toFixed(0)+' KB';
    const stIcon=pf.status==='done'?'✅':pf.status==='uploading'?'⏳':pf.status==='error'?'❌':'📌';
    const stCls=pf.status==='done'?'file-done':pf.status==='uploading'?'file-uploading':pf.status==='error'?'file-error':'';
    return `<div class="file-item">
      <span style="font-size:18px">${icon}</span>
      <div class="file-item-name">${pf.file.name}</div>
      <div class="file-item-size">${sz}</div>
      <div class="file-item-status ${stCls}">${stIcon}</div>
      ${pf.status==='pending'?`<button onclick="removeFile(${i})" style="background:none;border:none;cursor:pointer;color:var(--gray-400);font-size:14px">✕</button>`:''}
    </div>`;
  }).join('');
}

// ═══════════════════════════════════════════════════════════
//  GOOGLE DRIVE — FOLDER
// ═══════════════════════════════════════════════════════════
async function initDriveFolder() {
  if (!accessToken) { showToast('กรุณา Login ด้วย Google ก่อนครับ', 'warn'); return; }
  const inputId=document.getElementById('drive-folder-id').value.trim();

  if (inputId) {
    // Verify existing folder
    try {
      const r=await gapi.client.drive.files.get({ fileId:inputId, fields:'id,name,webViewLink' });
      cfg.driveFolderId=inputId; saveLocal();
      showToast(`เชื่อมต่อ Folder "${r.result.name}" สำเร็จ ✅`, 'success');
      renderDriveFolderCard(r.result);
    } catch(e) { showToast('ไม่พบ Folder นี้ใน Drive ของคุณ', 'error'); }
    return;
  }

  // Create new root folder
  showToast('กำลังสร้าง Folder "Family Insurance" ใน Drive...', 'warn');
  try {
    const r=await gapi.client.drive.files.create({
      resource:{ name:'Family Insurance', mimeType:'application/vnd.google-apps.folder' },
      fields:'id,name,webViewLink',
    });
    cfg.driveFolderId=r.result.id;
    document.getElementById('drive-folder-id').value=r.result.id;
    saveLocal();
    showToast('สร้าง Folder เรียบร้อย ✅', 'success');
    renderDriveFolderCard(r.result);
  } catch(e) { showToast('สร้าง Folder ไม่สำเร็จ: '+e.result?.error?.message, 'error'); }
}

function renderDriveFolderCard(folder) {
  const el=document.getElementById('drive-folder-display');
  if (!el||!cfg.driveFolderId) return;
  const name=folder?.name||'Family Insurance';
  const link=folder?.webViewLink||`https://drive.google.com/drive/folders/${cfg.driveFolderId}`;
  el.innerHTML=`<a href="${link}" target="_blank" class="drive-folder-card" style="text-decoration:none">
    <div class="drive-folder-icon">📁</div>
    <div class="drive-folder-info">
      <div class="drive-folder-name">${name}</div>
      <div class="drive-folder-sub">คลิกเพื่อเปิดใน Google Drive →</div>
    </div>
  </a>`;
}

// Create sub-folder per member if not exists (cached in member.driveFolderId)
async function getOrCreateMemberFolder(memberId) {
  const mem=getMember(memberId);
  if (mem.driveFolderId) return mem.driveFolderId;

  const r=await gapi.client.drive.files.create({
    resource:{
      name:mem.name, mimeType:'application/vnd.google-apps.folder',
      parents:[cfg.driveFolderId],
    },
    fields:'id',
  });
  const idx=members.findIndex(m=>m.id===memberId);
  if (idx!==-1) { members[idx].driveFolderId=r.result.id; saveLocal(); }
  return r.result.id;
}

// Upload a single file to Drive
async function uploadFileToDrive(fileObj, parentId, i) {
  pendingFiles[i].status='uploading'; renderFileList();
  const meta={ name:fileObj.name, parents:[parentId] };
  const form=new FormData();
  form.append('metadata',new Blob([JSON.stringify(meta)],{type:'application/json'}));
  form.append('file',fileObj);
  const resp=await fetch('https://www.googleapis.com/upload/drive/v3/files?uploadType=multipart&fields=id,name,webViewLink',{
    method:'POST',
    headers:{ Authorization:'Bearer '+accessToken },
    body:form,
  });
  if (!resp.ok) { pendingFiles[i].status='error'; renderFileList(); return null; }
  const data=await resp.json();
  pendingFiles[i].status='done'; pendingFiles[i].driveId=data.id; pendingFiles[i].webViewLink=data.webViewLink;
  renderFileList();
  return { id:data.id, name:data.name, webViewLink:data.webViewLink };
}

// ═══════════════════════════════════════════════════════════
//  POLICY CRUD
// ═══════════════════════════════════════════════════════════
function openAddModal() {
  editingId=null; pendingFiles=[];
  document.getElementById('modal-title').textContent='➕ เพิ่มกรมธรรม์ใหม่';
  clearForm(); populateMemberDropdowns();
  updateUploadArea();
  openModal('policy-modal');
}

function updateUploadArea() {
  const warn=document.getElementById('upload-not-signed-in');
  const wrap=document.getElementById('upload-area-wrap');
  if (!accessToken) { if(warn) warn.style.display='flex'; if(wrap) wrap.style.display='none'; }
  else { if(warn) warn.style.display='none'; if(wrap) wrap.style.display='block'; }
}

function clearForm() {
  selectedType='';
  document.querySelectorAll('.type-chip').forEach(c=>c.className='type-chip');
  ['f-type','f-company','f-policy-no','f-plan','f-start','f-end','f-premium','f-sum','f-beneficiary','f-notes']
    .forEach(id=>{ const el=document.getElementById(id); if(el) el.value=''; });
  document.getElementById('f-member').value='';
  document.getElementById('f-freq').value='yearly';
  document.querySelectorAll('.coverage-grid input').forEach(cb=>cb.checked=false);
  pendingFiles=[]; renderFileList();
}

function selectType(type) {
  selectedType=type;
  document.getElementById('f-type').value=type;
  document.querySelectorAll('.type-chip').forEach(c=>{ c.className='type-chip'; if(c.dataset.type===type) c.className=`type-chip sel-${type}`; });
}

async function savePolicy() {
  const member=document.getElementById('f-member').value;
  const company=document.getElementById('f-company').value.trim();
  const start=document.getElementById('f-start').value;
  const end=document.getElementById('f-end').value;
  const type=selectedType;
  if (!member)  { showToast('กรุณาเลือกสมาชิก','error'); return; }
  if (!company) { showToast('กรุณากรอกบริษัทประกัน','error'); return; }
  if (!type)    { showToast('กรุณาเลือกประเภทประกัน','error'); return; }
  if (!start||!end) { showToast('กรุณากรอกวันเริ่มและวันหมดอายุ','error'); return; }
  if (new Date(end)<=new Date(start)) { showToast('วันหมดอายุต้องหลังวันเริ่ม','error'); return; }

  const saveBtn=document.getElementById('save-btn');
  saveBtn.disabled=true; saveBtn.innerHTML='<div class="spinner"></div> กำลังบันทึก...';

  // Upload files to Drive
  let driveFiles=editingId ? (policies.find(p=>p.id===editingId)?.driveFiles||[]) : [];
  if (accessToken && pendingFiles.length && cfg.driveFolderId) {
    showSyncIndicator(true);
    try {
      const memberFolderId=await getOrCreateMemberFolder(member);
      for (let i=0;i<pendingFiles.length;i++) {
        const pf=pendingFiles[i];
        if (pf.status==='pending') {
          const result=await uploadFileToDrive(pf.file, memberFolderId, i);
          if (result) driveFiles.push(result);
        }
      }
    } catch(e) { showToast('อัพโหลดไฟล์บางรายการไม่สำเร็จ','warn'); }
    showSyncIndicator(false);
  }

  const coverage=[...document.querySelectorAll('.coverage-grid input:checked')].map(cb=>cb.value);
  const policy={
    id:editingId||uid(), member, type, company,
    policy_no:document.getElementById('f-policy-no').value.trim(),
    plan_name:document.getElementById('f-plan').value.trim(),
    start_date:start, end_date:end,
    premium:document.getElementById('f-premium').value||0,
    sum_insured:document.getElementById('f-sum').value||0,
    payment_freq:document.getElementById('f-freq').value,
    beneficiary:document.getElementById('f-beneficiary').value.trim(),
    coverage, driveFiles,
    notes:document.getElementById('f-notes').value.trim(),
    created_at:editingId?(policies.find(p=>p.id===editingId)?.created_at||new Date().toISOString()):new Date().toISOString(),
    updated_at:new Date().toISOString(),
  };

  if (editingId) { const idx=policies.findIndex(p=>p.id===editingId); if(idx!==-1) policies[idx]=policy; }
  else policies.push(policy);

  saveLocal();
  closeModal('policy-modal');
  renderAll(); checkAlerts();
  saveBtn.disabled=false; saveBtn.innerHTML='💾 บันทึกกรมธรรม์';
  showToast(editingId?'อัพเดทเรียบร้อย ✅':'บันทึกเรียบร้อย ✅', 'success');

  // Sync to Sheets
  if (accessToken && cfg.sheetId) syncToSheet(true);
}

function editPolicy(id) {
  const p=policies.find(p=>p.id===id); if(!p) return;
  editingId=id; pendingFiles=[];
  document.getElementById('modal-title').textContent='✏️ แก้ไขกรมธรรม์';
  clearForm(); populateMemberDropdowns();
  selectType(p.type);
  document.getElementById('f-member').value=p.member;
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
  if (p.coverage) p.coverage.forEach(v=>{ const cb=document.querySelector(`.coverage-grid input[value="${v}"]`); if(cb) cb.checked=true; });
  updateUploadArea();
  closeModal('detail-modal');
  openModal('policy-modal');
}

function deletePolicy(id) {
  if (!confirm('ต้องการลบกรมธรรม์นี้ใช่ไหม?')) return;
  policies=policies.filter(p=>p.id!==id);
  saveLocal(); renderAll(); checkAlerts(); closeModal('detail-modal');
  showToast('ลบกรมธรรม์เรียบร้อย','warn');
  if (accessToken&&cfg.sheetId) syncToSheet(true);
}

function showDetail(id) {
  const p=policies.find(p=>p.id===id); if(!p) return;
  const mem=getMember(p.member), c=TYPE_CFG[p.type]||TYPE_CFG.other;
  const st=getStatus(p), d=daysLeft(p.end_date);
  const stTxt={active:'✅ คุ้มครองอยู่',expiring:'⚠️ ใกล้หมดอายุ',expired:'❌ หมดอายุ'};
  const freqTxt={yearly:'รายปี',halfyearly:'ราย 6 เดือน',quarterly:'รายไตรมาส',monthly:'รายเดือน'};
  const covTags=(p.coverage||[]).map(cv=>`<div class="coverage-tag">${COV_LBL[cv]||cv}</div>`).join('');

  // Drive files
  const filesHTML=(p.driveFiles||[]).length
    ? (p.driveFiles||[]).map(f=>`
      <div class="attached-file-row">
        <div class="attached-file-icon">${f.name?.endsWith('.pdf')?'📄':'🖼️'}</div>
        <div class="attached-file-info">
          <div class="attached-file-name">${f.name}</div>
          <div class="attached-file-meta">Google Drive</div>
        </div>
        <a href="${f.webViewLink||'#'}" target="_blank" class="btn btn-outline btn-sm">เปิด</a>
      </div>`).join('')
    : '<div style="font-size:12px;color:var(--gray-400);padding:8px 0">ไม่มีไฟล์แนบ</div>';

  document.getElementById('detail-content').innerHTML=`
  <div class="detail-header">
    <div class="detail-avatar" style="background:${mem.color}">${getInitials(mem.name)}</div>
    <div><div style="font-size:16px;font-weight:700">${mem.name} <span class="badge badge-${p.type}" style="margin-left:6px">${c.icon} ${c.label}</span></div>
    <div style="font-size:13px;color:var(--gray-500)">${p.company||'-'}${p.plan_name?' · '+p.plan_name:''}</div></div>
  </div>
  <div class="detail-grid">
    <div class="detail-item"><div class="detail-key">เลขกรมธรรม์</div><div class="detail-val" style="font-family:monospace">${p.policy_no||'-'}</div></div>
    <div class="detail-item"><div class="detail-key">สถานะ</div><div class="detail-val">${stTxt[st]}${st==='expiring'?' ('+d+' วัน)':''}</div></div>
    <div class="detail-item"><div class="detail-key">วันเริ่มคุ้มครอง</div><div class="detail-val">${thaiDate(p.start_date)}</div></div>
    <div class="detail-item"><div class="detail-key">วันหมดอายุ</div><div class="detail-val">${thaiDate(p.end_date)}</div></div>
    <div class="detail-item"><div class="detail-key">เบี้ยประกัน/ปี</div><div class="detail-val">${fmtMoney(p.premium)}</div></div>
    <div class="detail-item"><div class="detail-key">ทุนประกัน</div><div class="detail-val">${fmtMoney(p.sum_insured)}</div></div>
    <div class="detail-item"><div class="detail-key">ความถี่ชำระ</div><div class="detail-val">${freqTxt[p.payment_freq]||'-'}</div></div>
    <div class="detail-item"><div class="detail-key">ผู้รับผลประโยชน์</div><div class="detail-val">${p.beneficiary||'-'}</div></div>
  </div>
  ${covTags?`<div style="margin-top:12px"><div class="detail-key" style="margin-bottom:6px">ความคุ้มครอง</div><div class="coverage-tags">${covTags}</div></div>`:''}
  <div style="margin-top:16px">
    <div class="detail-key" style="margin-bottom:8px">📎 ไฟล์แนบ (Google Drive)</div>
    <div class="attached-files">${filesHTML}</div>
  </div>
  ${p.notes?`<div style="margin-top:12px;padding:10px 12px;background:var(--gray-50);border-radius:8px;font-size:13px"><strong>หมายเหตุ:</strong> ${p.notes}</div>`:''}
  <div style="margin-top:12px;font-size:11px;color:var(--gray-400);text-align:right">อัพเดท: ${new Date(p.updated_at||Date.now()).toLocaleString('th-TH')}</div>
  `;
  document.getElementById('detail-edit-btn').onclick=()=>editPolicy(id);
  document.getElementById('detail-delete-btn').onclick=()=>deletePolicy(id);
  openModal('detail-modal');
}

// ═══════════════════════════════════════════════════════════
//  MEMBERS
// ═══════════════════════════════════════════════════════════
function openMemberModal() {
  document.getElementById('m-name').value='';
  document.getElementById('m-role').value='ตัวเอง';
  document.getElementById('m-dob').value='';
  document.getElementById('m-color').value=PALETTE[members.length%PALETTE.length];
  openModal('member-modal');
}
function saveMember() {
  const name=document.getElementById('m-name').value.trim();
  if (!name) { showToast('กรุณากรอกชื่อสมาชิก','error'); return; }
  members.push({ id:uid(), name, role:document.getElementById('m-role').value,
    dob:document.getElementById('m-dob').value, color:document.getElementById('m-color').value });
  saveLocal(); populateMemberDropdowns(); renderMembers(); renderDashboard();
  closeModal('member-modal'); showToast(`เพิ่ม "${name}" เรียบร้อย`,'success');
}
function deleteMember(id) {
  if (!confirm('ลบสมาชิกนี้?')) return;
  members=members.filter(m=>m.id!==id);
  saveLocal(); populateMemberDropdowns(); renderMembers(); renderDashboard();
  showToast('ลบสมาชิกเรียบร้อย','warn');
}
function renderMembers() {
  const el=document.getElementById('members-grid'); if(!el) return;
  if (!members.length) { el.innerHTML='<div class="empty-state"><div class="empty-icon">👨‍👩‍👧‍👦</div><div class="empty-title">ยังไม่มีสมาชิก</div></div>'; return; }
  el.innerHTML=members.map(m=>{
    const mp=policies.filter(p=>p.member===m.id);
    const age=m.dob?Math.floor((Date.now()-new Date(m.dob))/31557600000):null;
    const tpBadges=[...new Set(mp.map(p=>p.type))].map(t=>{ const c=TYPE_CFG[t]||TYPE_CFG.other; return `<div class="mini-badge" style="background:${c.bg};color:${c.color}">${c.icon} ${c.label}</div>`; }).join('');
    const driveLink=m.driveFolderId?`<a href="https://drive.google.com/drive/folders/${m.driveFolderId}" target="_blank" class="btn btn-ghost btn-sm" style="font-size:11px">📁 Drive</a>`:'';
    return `<div class="member-full-card">
      <div class="member-full-top">
        <div class="member-full-avatar" style="background:${m.color}">${getInitials(m.name)}</div>
        <div><div class="member-full-name">${m.name}</div><div class="member-full-role">${m.role||''}${age?' · '+age+' ปี':''}</div></div>
      </div>
      <div style="display:flex;flex-wrap:wrap;gap:4px;margin-bottom:10px">${tpBadges||'<span style="font-size:11px;color:var(--gray-400)">ยังไม่มีกรมธรรม์</span>'}</div>
      <div style="font-size:12px;color:var(--gray-600);margin-bottom:10px">กรมธรรม์ทั้งหมด: <strong>${mp.length}</strong> รายการ</div>
      <div style="display:flex;gap:6px;flex-wrap:wrap">
        ${driveLink}
        <button class="btn btn-danger btn-sm" onclick="deleteMember('${m.id}')">🗑️ ลบ</button>
      </div>
    </div>`;
  }).join('');
}

// ═══════════════════════════════════════════════════════════
//  GOOGLE SHEETS SYNC
// ═══════════════════════════════════════════════════════════
function saveSheetConfig() {
  cfg.sheetId=document.getElementById('sheet-id').value.trim();
  cfg.sheetName=document.getElementById('sheet-name').value.trim()||'Policies';
  cfg.syncInterval=parseInt(document.getElementById('sync-interval').value)||0;
  saveLocal(); setupAutoSync();
  showToast('บันทึกการตั้งค่า Sheet เรียบร้อย','success');
}

function setupAutoSync() {
  if (syncTimer) clearInterval(syncTimer);
  if (accessToken&&cfg.sheetId&&cfg.syncInterval>0)
    syncTimer=setInterval(()=>syncToSheet(true), cfg.syncInterval*60000);
}

async function syncToSheet(silent=false) {
  if (!accessToken) { if(!silent) showToast('กรุณา Login ด้วย Google ก่อน','warn'); return; }
  if (!cfg.sheetId) { if(!silent) showToast('กรุณาตั้งค่า Spreadsheet ID ก่อน','warn'); return; }
  if (!silent) showSyncIndicator(true);

  const HEADERS=['id','สมาชิก','ประเภท','บริษัทประกัน','เลขกรมธรรม์','ชื่อแผน',
    'วันเริ่ม','วันหมดอายุ','เบี้ย/ปี','ทุนประกัน','ความคุ้มครอง',
    'ผู้รับผลประโยชน์','ไฟล์ใน Drive','หมายเหตุ','อัพเดทล่าสุด'];

  const rows=[HEADERS, ...policies.map(p=>[
    p.id, getMember(p.member).name, (TYPE_CFG[p.type]||TYPE_CFG.other).label,
    p.company||'', p.policy_no||'', p.plan_name||'',
    p.start_date||'', p.end_date||'', p.premium||'', p.sum_insured||'',
    (p.coverage||[]).map(c=>COV_LBL[c]||c).join(', '),
    p.beneficiary||'',
    (p.driveFiles||[]).map(f=>f.webViewLink||f.name).join(', '),
    p.notes||'', p.updated_at||'',
  ])];

  try {
    // Clear sheet first
    await gapi.client.sheets.spreadsheets.values.clear({
      spreadsheetId:cfg.sheetId, range:`${cfg.sheetName}!A:Z`,
    });
    // Write data
    await gapi.client.sheets.spreadsheets.values.update({
      spreadsheetId:cfg.sheetId,
      range:`${cfg.sheetName}!A1`,
      valueInputOption:'RAW',
      resource:{ values:rows },
    });
    if (!silent) { showSyncIndicator(false); showToast('Sync ขึ้น Google Sheets สำเร็จ ✅','success'); }
    else showSyncIndicator(false);
  } catch(e) {
    showSyncIndicator(false);
    const msg=e.result?.error?.message||'error';
    if (!silent) showToast('Sync ไม่สำเร็จ: '+msg,'error');
    else console.warn('Auto-sync failed:',msg);
  }
}

async function importFromSheet() {
  if (!accessToken) { showToast('กรุณา Login ด้วย Google ก่อน','warn'); return; }
  if (!cfg.sheetId) { showToast('กรุณาตั้งค่า Spreadsheet ID ก่อน','warn'); return; }
  showToast('กำลัง Import จาก Sheet...','warn'); showSyncIndicator(true);
  try {
    const r=await gapi.client.sheets.spreadsheets.values.get({
      spreadsheetId:cfg.sheetId, range:`${cfg.sheetName}!A:Z`,
    });
    showSyncIndicator(false);
    const [hdrs,...rows]=r.result.values||[];
    if (!hdrs) { showToast('ไม่พบข้อมูลใน Sheet','warn'); return; }
    showToast(`Import สำเร็จ ${rows.length} รายการ ✅`,'success');
  } catch(e) { showSyncIndicator(false); showToast('Import ไม่สำเร็จ: '+(e.result?.error?.message||''),'error'); }
}

// ═══════════════════════════════════════════════════════════
//  SETTINGS — CLIENT ID
// ═══════════════════════════════════════════════════════════
function saveClientId() {
  const id=document.getElementById('client-id-input').value.trim();
  if (!id) { showToast('กรุณากรอก Client ID','error'); return; }
  cfg.clientId=id; saveLocal();
  showToast('บันทึก Client ID เรียบร้อย — กรุณา Refresh หน้าเว็บแล้ว Login ใหม่','success');
  setTimeout(()=>location.reload(),2000);
}

// ═══════════════════════════════════════════════════════════
//  EXPORT CSV
// ═══════════════════════════════════════════════════════════
function exportCSV() {
  const H=['สมาชิก','ประเภท','บริษัท','เลขกรมธรรม์','ชื่อแผน','วันเริ่ม','วันหมด','เบี้ย/ปี','ทุน','ความคุ้มครอง','ผู้รับผลประโยชน์','ไฟล์ Drive','หมายเหตุ'];
  const rows=policies.map(p=>[
    getMember(p.member).name,(TYPE_CFG[p.type]||TYPE_CFG.other).label,
    p.company,p.policy_no,p.plan_name,p.start_date,p.end_date,p.premium,p.sum_insured,
    (p.coverage||[]).map(c=>COV_LBL[c]||c).join('; '),
    p.beneficiary,(p.driveFiles||[]).map(f=>f.webViewLink||f.name).join('; '),p.notes,
  ]);
  const csv=[H,...rows].map(r=>r.map(c=>'"'+String(c||'').replace(/"/g,'""')+'"').join(',')).join('\n');
  const a=document.createElement('a');
  a.href=URL.createObjectURL(new Blob(['\uFEFF'+csv],{type:'text/csv;charset=utf-8;'}));
  a.download=`family_insurance_${new Date().toISOString().slice(0,10)}.csv`; a.click();
  showToast('Export CSV เรียบร้อย','success');
}

function clearAllData() {
  if (!confirm('ลบข้อมูลทั้งหมด?')) return;
  if (!confirm('ยืนยันอีกครั้ง — ลบทั้งหมด?')) return;
  policies=[]; members=[{id:uid(),name:'ฉัน (ตัวเอง)',role:'ตัวเอง',color:'#1a73e8',dob:''}];
  saveLocal(); populateMemberDropdowns(); renderAll();
  showToast('ล้างข้อมูลเรียบร้อย','warn');
}

// ═══════════════════════════════════════════════════════════
//  UI HELPERS
// ═══════════════════════════════════════════════════════════
function showSyncIndicator(show) {
  document.getElementById('sync-indicator').style.display=show?'flex':'none';
}
function openModal(id)  { document.getElementById(id).classList.add('open'); }
function closeModal(id) { document.getElementById(id).classList.remove('open'); }
document.querySelectorAll('.modal-overlay').forEach(o=>o.addEventListener('click',e=>{ if(e.target===o) o.classList.remove('open'); }));

function showToast(msg, type='') {
  const c=document.getElementById('toast-container');
  const t=document.createElement('div');
  t.className='toast'+(type?' toast-'+type:'');
  t.innerHTML=(type==='success'?'✅ ':type==='error'?'❌ ':type==='warn'?'⚠️ ':'ℹ️ ')+msg;
  c.appendChild(t);
  setTimeout(()=>{ t.style.cssText='opacity:0;transform:translateX(100%);transition:all .3s'; setTimeout(()=>t.remove(),300); },3000);
}

// ═══════════════════════════════════════════════════════════
//  BOOT
// ═══════════════════════════════════════════════════════════
window.gapiLoadCallback = () => { if(typeof gapi!=='undefined') gapi.load('client', initGapiClient); };
window.gisLoadCallback  = () => { if(typeof google!=='undefined'&&google.accounts) initTokenClient(); };

init();

// Demo data on first visit
setTimeout(()=>{ if(!policies.length) loadDemo(); }, 400);

function loadDemo() {
  const me=members[0];
  const sp={id:uid(),name:'สมหญิง รักครอบครัว',role:'คู่สมรส',color:'#e91e63',dob:'1990-05-15'};
  const ch={id:uid(),name:'น้องน้ำตาล',role:'ลูก',color:'#ff9800',dob:'2015-09-20'};
  members.push(sp,ch);
  const add=(n)=>{ const d=new Date(); d.setDate(d.getDate()+n); return d.toISOString().slice(0,10); };
  policies=[
    {id:uid(),member:me.id,type:'health',company:'เมืองไทยประกันชีวิต',policy_no:'MTL-2024-001',plan_name:'Health Plus Gold',start_date:add(-180),end_date:add(185),premium:25000,sum_insured:3000000,coverage:['ipd','opd','dental'],beneficiary:'ภรรยา',driveFiles:[],notes:'',created_at:new Date().toISOString(),updated_at:new Date().toISOString()},
    {id:uid(),member:me.id,type:'life',company:'AIA',policy_no:'AIA-LIFE-2022',plan_name:'Life Protect 20/20',start_date:add(-730),end_date:add(2555),premium:48000,sum_insured:5000000,coverage:['death','disability','saving'],beneficiary:'ภรรยาและลูก',driveFiles:[],notes:'',created_at:new Date().toISOString(),updated_at:new Date().toISOString()},
    {id:uid(),member:me.id,type:'accident',company:'Allianz Ayudhya',policy_no:'AA-ACC-2024',plan_name:'PA Master',start_date:add(-60),end_date:add(25),premium:3500,sum_insured:500000,coverage:['accident_med','death'],beneficiary:'ภรรยา',driveFiles:[],notes:'',created_at:new Date().toISOString(),updated_at:new Date().toISOString()},
    {id:uid(),member:sp.id,type:'health',company:'Cigna',policy_no:'CIGNA-2024',plan_name:'Smart Health',start_date:add(-90),end_date:add(55),premium:20000,sum_insured:2000000,coverage:['ipd','opd','maternity'],beneficiary:'สามี',driveFiles:[],notes:'',created_at:new Date().toISOString(),updated_at:new Date().toISOString()},
    {id:uid(),member:ch.id,type:'health',company:'เมืองไทยประกันชีวิต',policy_no:'MTL-CHILD-001',plan_name:'Child Health Star',start_date:add(-30),end_date:add(335),premium:12000,sum_insured:1000000,coverage:['ipd','opd'],beneficiary:'พ่อแม่',driveFiles:[],notes:'',created_at:new Date().toISOString(),updated_at:new Date().toISOString()},
  ];
  saveLocal(); populateMemberDropdowns(); renderAll(); checkAlerts();
  showToast('โหลดข้อมูลตัวอย่างเรียบร้อย 🎉','success');
}
</script>
</body>
</html>
