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
  --p:#1a73e8;--pk:#1557b0;--pl:#e8f0fe;
  --g:#34a853;--gl:#e6f4ea;
  --w:#fbbc04;--wl:#fef9e7;
  --e:#ea4335;--el:#fce8e6;
  --pu:#9c27b0;--pul:#f3e5f5;
  --o:#ff6d00;--ol:#fff3e0;
  --n50:#f8f9fa;--n100:#f1f3f4;--n200:#e8eaed;--n300:#dadce0;
  --n400:#bdc1c6;--n500:#9aa0a6;--n600:#80868b;--n700:#5f6368;
  --n800:#3c4043;--n900:#202124;--W:#fff;
  --s0:0 1px 3px rgba(0,0,0,.08);--s1:0 4px 12px rgba(0,0,0,.08);
  --r:12px;--rs:8px;
}
*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html,body{height:100%;overflow-x:hidden}
body{font-family:-apple-system,BlinkMacSystemFont,'Segoe UI','Noto Sans Thai',sans-serif;
  background:var(--n50);color:var(--n900);font-size:14px;line-height:1.5;-webkit-font-smoothing:antialiased}

/* ── LOADING ── */
#ld{position:fixed;inset:0;background:#fff;z-index:9999;
  display:flex;flex-direction:column;align-items:center;justify-content:center;gap:14px;
  transition:opacity .3s ease}
#ld.gone{opacity:0;pointer-events:none}
#ld .ico{font-size:52px;animation:bob .9s ease-in-out infinite alternate}
@keyframes bob{to{transform:translateY(-8px)}}
#ld .bar{width:180px;height:4px;background:var(--n200);border-radius:2px;overflow:hidden}
#ld .fill{height:100%;background:var(--p);border-radius:2px;transition:width .2s;width:0}
#ld .sub{font-size:13px;color:var(--n500)}

/* ── SIDEBAR ── */
.side{position:fixed;left:0;top:0;bottom:0;width:256px;background:var(--W);
  border-right:1px solid var(--n200);display:flex;flex-direction:column;
  z-index:300;box-shadow:var(--s1);transition:transform .28s cubic-bezier(.4,0,.2,1)}
.side-brand{display:flex;align-items:center;gap:10px;
  padding:calc(env(safe-area-inset-top)+14px) 18px 14px;border-bottom:1px solid var(--n100)}
.side-ico{width:36px;height:36px;border-radius:10px;flex-shrink:0;
  background:linear-gradient(135deg,var(--p),#4285f4);display:flex;align-items:center;justify-content:center;font-size:18px}
.side-nm{font-size:14px;font-weight:700}
.side-sub{font-size:11px;color:var(--n500)}
.side-nav{flex:1;padding:10px 0;overflow-y:auto}
.nl{font-size:10px;font-weight:700;color:var(--n400);text-transform:uppercase;letter-spacing:.8px;padding:6px 18px 5px;margin-top:4px}
.nr{display:flex;align-items:center;gap:9px;padding:10px 18px;cursor:pointer;
  border-radius:0 22px 22px 0;margin:1px 8px 1px 0;color:var(--n700);font-size:13px;font-weight:500;transition:background .15s}
.nr:active,.nr:hover{background:var(--n100)}
.nr.on{background:var(--pl);color:var(--p)}
.ni{font-size:16px;width:20px;text-align:center;flex-shrink:0}
.nb{margin-left:auto;background:var(--e);color:#fff;border-radius:10px;font-size:11px;font-weight:600;padding:1px 6px}
.side-foot{padding:10px;border-top:1px solid var(--n100)}
.ov{display:none;position:fixed;inset:0;background:rgba(0,0,0,.45);z-index:299;backdrop-filter:blur(2px)}
.ov.on{display:block}

/* ── MAIN ── */
.main{min-height:100vh;display:flex;flex-direction:column}
.tbar{background:var(--W);border-bottom:1px solid var(--n200);padding:0 14px;
  padding-top:env(safe-area-inset-top);height:calc(52px + env(safe-area-inset-top));
  display:flex;align-items:flex-end;padding-bottom:8px;gap:8px;
  position:sticky;top:0;z-index:50;box-shadow:var(--s0)}
.tmenu{width:40px;height:36px;border:none;background:transparent;cursor:pointer;
  font-size:22px;display:flex;align-items:center;justify-content:center;border-radius:8px;flex-shrink:0}
.ttl{font-size:16px;font-weight:700;flex:1}

/* ── SYNC BAR ── */
.sbar{display:flex;align-items:center;gap:8px;padding:7px 14px;font-size:12px;
  border-bottom:1px solid var(--n200);background:var(--W);cursor:pointer;flex-shrink:0}
.sbar:active{background:var(--n50)}
.sd{width:8px;height:8px;border-radius:50%;flex-shrink:0}
.sd-ok{background:var(--g)}.sd-busy{background:var(--w);animation:sp 1s infinite}
.sd-off{background:var(--n400)}.sd-err{background:var(--e)}
@keyframes sp{0%,100%{opacity:1}50%{opacity:.15}}
.stxt{flex:1;color:var(--n600)}
.sbtn{background:none;border:none;color:var(--p);font-size:12px;font-weight:700;
  cursor:pointer;padding:4px 10px;border-radius:6px;font-family:inherit;white-space:nowrap}

/* ── PAGES ── */
.page{display:none;padding:12px 14px calc(88px + env(safe-area-inset-bottom)) 14px}
.page.active{display:block}

/* ── BUTTONS ── */
.btn{display:inline-flex;align-items:center;justify-content:center;gap:6px;
  padding:10px 18px;border-radius:10px;border:none;font-size:13px;font-weight:600;
  cursor:pointer;white-space:nowrap;min-height:44px;font-family:inherit;-webkit-appearance:none;transition:opacity .15s}
.btn:active{opacity:.72}
.bp{background:var(--p);color:#fff}.bp:disabled{background:var(--n300);cursor:not-allowed}
.bo{background:transparent;color:var(--p);border:1.5px solid var(--p)}
.bg{background:transparent;color:var(--n700);border:1.5px solid var(--n200)}
.bd{background:var(--e);color:#fff}
.bs{padding:8px 14px;font-size:12px;min-height:38px;border-radius:8px}
.bx{padding:5px 10px;font-size:11px;min-height:30px;border-radius:6px}

/* ── STATS ── */
.sg{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:14px}
.sc{background:var(--W);border-radius:var(--r);padding:14px;box-shadow:var(--s0);border:1px solid var(--n100);display:flex;align-items:center;gap:10px}
.si{width:38px;height:38px;border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:18px;flex-shrink:0}
.sv{font-size:22px;font-weight:700;line-height:1}.sl{font-size:11px;color:var(--n500);margin-top:2px}

/* ── MEMBER SECTIONS ── */
.msec{background:var(--W);border-radius:var(--r);box-shadow:var(--s0);border:1px solid var(--n100);margin-bottom:12px;overflow:hidden}
.mhd{display:flex;align-items:center;gap:10px;padding:13px 16px;cursor:pointer;background:var(--n50);border-bottom:1px solid var(--n100);transition:background .15s;-webkit-user-select:none}
.mhd:active{background:var(--n100)}
.mav{width:38px;height:38px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:15px;font-weight:700;color:#fff;flex-shrink:0}
.mhi{flex:1;min-width:0}
.mhnm{font-size:14px;font-weight:700}
.mhrl{font-size:11px;color:var(--n500);margin-top:1px}
.mhcnt{font-size:12px;font-weight:600;color:var(--p);background:var(--pl);padding:3px 10px;border-radius:100px;flex-shrink:0}
.mchev{font-size:11px;color:var(--n400);flex-shrink:0;transition:transform .2s}
.mhd.open .mchev{transform:rotate(180deg)}
.mbd{display:none;padding:10px 12px 8px}
.mbd.open{display:block}
.irow{display:flex;align-items:center;gap:10px;padding:10px 12px;border-radius:var(--rs);border:1px solid var(--n100);margin-bottom:8px;cursor:pointer;background:var(--n50);transition:background .15s}
.irow:active{background:var(--n100)}
.iti{width:34px;height:34px;border-radius:8px;display:flex;align-items:center;justify-content:center;font-size:16px;flex-shrink:0}
.iinf{flex:1;min-width:0}
.ico2{font-size:13px;font-weight:600;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.ipl{font-size:11px;color:var(--n500)}
.irt{text-align:right;flex-shrink:0}
.idt{font-size:11px;font-weight:600;padding:3px 8px;border-radius:6px;white-space:nowrap}
.ic{background:var(--el);color:var(--e)}.iw2{background:var(--wl);color:#b06000}
.iok{background:var(--gl);color:var(--g)}.iend{background:var(--n100);color:var(--n600)}
.ipr{font-size:11px;color:var(--n500);margin-top:2px}
.iadd{display:flex;align-items:center;justify-content:center;gap:6px;width:100%;
  padding:8px;border:1.5px dashed var(--n300);border-radius:var(--rs);background:transparent;
  color:var(--n500);font-size:12px;cursor:pointer;font-family:inherit;margin-top:2px;min-height:36px}
.iadd:active{background:var(--n100)}

/* ── DONUT ── */
.dwrap{position:relative;width:100px;height:100px;flex-shrink:0}
.dc{position:absolute;inset:0;display:flex;flex-direction:column;align-items:center;justify-content:center}
.dn{font-size:20px;font-weight:700;line-height:1}.dl{font-size:9px;color:var(--n500)}
svg.donut{transform:rotate(-90deg)}
.drow{display:flex;align-items:center;gap:12px}
.dleg{display:flex;flex-direction:column;gap:5px;flex:1}
.dli{display:flex;align-items:center;gap:5px;font-size:11px;color:var(--n700)}
.dld{width:8px;height:8px;border-radius:50%;flex-shrink:0}

/* ── EXPIRY ── */
.elst{display:flex;flex-direction:column;gap:8px}
.erow{display:flex;align-items:center;gap:10px;padding:10px 12px;border-radius:var(--rs);background:var(--n50);border:1px solid var(--n100);cursor:pointer}
.eav{width:30px;height:30px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:700;color:#fff;flex-shrink:0}
.einf{flex:1;min-width:0}
.enm{font-size:12px;font-weight:600;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.etp{font-size:10px;color:var(--n500)}
.ed{font-size:11px;font-weight:700;padding:3px 7px;border-radius:6px;text-align:center;flex-shrink:0}

/* ── POLICY CARDS ── */
.plst{display:flex;flex-direction:column;gap:10px}
.pcd{background:var(--W);border-radius:var(--r);padding:14px;box-shadow:var(--s0);border:1px solid var(--n100)}
.ptop{display:flex;align-items:flex-start;gap:10px;margin-bottom:8px}
.pav{width:34px;height:34px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:13px;font-weight:700;color:#fff;flex-shrink:0}
.pinf{flex:1;min-width:0}
.pnm{font-size:13px;font-weight:700}.pco{font-size:12px;color:var(--n500);overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.pbot{display:flex;align-items:center;gap:8px;flex-wrap:wrap;font-size:11px;color:var(--n600)}
.pact{display:flex;gap:6px;margin-top:10px;padding-top:10px;border-top:1px solid var(--n100)}

/* ── FILTER ── */
.fscr{display:flex;gap:8px;overflow-x:auto;padding-bottom:4px;margin-bottom:12px;-webkit-overflow-scrolling:touch;scrollbar-width:none}
.fscr::-webkit-scrollbar{display:none}
.fc{display:inline-flex;align-items:center;gap:4px;padding:7px 14px;border-radius:100px;border:1.5px solid var(--n200);background:var(--W);font-size:12px;font-weight:500;color:var(--n700);cursor:pointer;white-space:nowrap;flex-shrink:0;min-height:36px}
.fc.on{background:var(--pl);border-color:var(--p);color:var(--p)}
.srch{display:flex;align-items:center;gap:8px;background:var(--W);border:1.5px solid var(--n200);border-radius:10px;padding:10px 14px;margin-bottom:12px}
.srch:focus-within{border-color:var(--p)}
.srch input{border:none;outline:none;font-size:16px;background:transparent;width:100%;color:var(--n900);font-family:inherit}

/* ── BADGE ── */
.badge{display:inline-flex;align-items:center;gap:3px;padding:3px 8px;border-radius:100px;font-size:11px;font-weight:600}
.bh{background:var(--gl);color:var(--g)}.ba{background:var(--wl);color:#c77a00}
.bl{background:var(--pul);color:var(--pu)}.bc{background:var(--ol);color:var(--o)}.bo2{background:var(--n100);color:var(--n700)}
.sdt{width:7px;height:7px;border-radius:50%;display:inline-block;margin-right:3px}
.sact{background:var(--g)}.sexp{background:var(--w)}.sxd{background:var(--e)}
.fchip{display:inline-flex;align-items:center;gap:4px;padding:3px 8px;background:var(--pl);color:var(--p);border-radius:6px;font-size:11px;font-weight:500;text-decoration:none}

/* ── UPLOAD ── */
.upz{border:2px dashed var(--n300);border-radius:var(--rs);padding:20px;text-align:center;cursor:pointer;background:var(--n50);display:flex;flex-direction:column;align-items:center;gap:6px}
.upz input{display:none}
.flst{display:flex;flex-direction:column;gap:6px;margin-top:8px}
.fitm{display:flex;align-items:center;gap:8px;padding:8px 10px;background:var(--W);border:1px solid var(--n200);border-radius:var(--rs)}
.fnm{flex:1;font-size:12px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}

/* ── MODAL ── */
.mov{display:none;position:fixed;inset:0;background:rgba(0,0,0,.5);z-index:500;align-items:flex-end;justify-content:center;backdrop-filter:blur(3px)}
.mov.on{display:flex;animation:mfi .15s}
@keyframes mfi{from{opacity:0}}
.modal{background:var(--W);border-radius:20px 20px 0 0;width:100%;max-height:93vh;overflow-y:auto;
  animation:msu .25s cubic-bezier(.4,0,.2,1);padding-bottom:env(safe-area-inset-bottom);-webkit-overflow-scrolling:touch}
@keyframes msu{from{transform:translateY(100%)}}
.mhdl{width:36px;height:4px;background:var(--n300);border-radius:2px;margin:10px auto 0}
.mhd2{display:flex;align-items:center;justify-content:space-between;padding:14px 18px 12px;border-bottom:1px solid var(--n100);position:sticky;top:0;background:var(--W);z-index:1}
.mtl{font-size:16px;font-weight:700}
.mcl{width:34px;height:34px;border-radius:50%;border:none;background:var(--n100);cursor:pointer;font-size:16px;display:flex;align-items:center;justify-content:center;color:var(--n600)}
.mbdy{padding:16px 18px}
.mft{display:flex;gap:8px;padding:12px 18px;padding-bottom:calc(12px + env(safe-area-inset-bottom));border-top:1px solid var(--n100);position:sticky;bottom:0;background:var(--W)}
.mft .btn{flex:1}

/* ── FORM ── */
.fg{display:flex;flex-direction:column;gap:6px;margin-bottom:14px}
.fl{font-size:12px;font-weight:600;color:var(--n700)}
.fl .r{color:var(--e);margin-left:2px}
.fi{background:var(--W);border:1.5px solid var(--n200);border-radius:var(--rs);padding:12px 14px;font-size:16px;color:var(--n900);outline:none;width:100%;font-family:inherit;-webkit-appearance:none;transition:border-color .2s}
.fi:focus{border-color:var(--p)}
textarea.fi{resize:vertical;min-height:72px}
select.fi{background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='8' viewBox='0 0 12 8'%3E%3Cpath d='M1 1l5 5 5-5' stroke='%239aa0a6' stroke-width='1.5' fill='none' stroke-linecap='round'/%3E%3C/svg%3E");background-repeat:no-repeat;background-position:right 14px center;padding-right:36px}
.fr{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.fdv{border:none;border-top:1px solid var(--n100);margin:4px 0 14px}
.fsc{font-size:11px;font-weight:700;color:var(--n500);text-transform:uppercase;letter-spacing:.5px;margin-bottom:10px}
.tsel{display:grid;grid-template-columns:repeat(5,1fr);gap:6px}
.tc{display:flex;flex-direction:column;align-items:center;gap:3px;padding:10px 4px;border-radius:10px;cursor:pointer;border:1.5px solid var(--n200);background:var(--W);font-size:10px;font-weight:600;color:var(--n600);min-height:58px;justify-content:center}
.tci{font-size:20px}
.t-h{border-color:var(--g);background:var(--gl);color:var(--g)}
.t-a{border-color:var(--w);background:var(--wl);color:#c77a00}
.t-l{border-color:var(--pu);background:var(--pul);color:var(--pu)}
.t-c{border-color:var(--o);background:var(--ol);color:var(--o)}
.t-o{border-color:var(--p);background:var(--pl);color:var(--p)}
.cgrd{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.ci{display:flex;align-items:center;gap:8px;padding:8px 10px;border:1.5px solid var(--n200);border-radius:8px;cursor:pointer;font-size:12px;color:var(--n700)}
.ci input{width:16px;height:16px;accent-color:var(--p);flex-shrink:0;cursor:pointer}
.ci:has(input:checked){border-color:var(--p);background:var(--pl);color:var(--p)}

/* ── DETAIL ── */
.dth{background:var(--n50);border-radius:var(--rs);padding:14px;margin-bottom:14px;display:flex;align-items:center;gap:12px}
.dtav{width:46px;height:46px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:19px;font-weight:700;color:#fff;flex-shrink:0}
.dtr{display:flex;flex-direction:column;gap:8px}
.dt2{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.drw{padding:10px 12px;background:var(--n50);border-radius:8px}
.dk{font-size:10px;font-weight:600;color:var(--n500);text-transform:uppercase;margin-bottom:3px}
.dv{font-size:13px;font-weight:600;color:var(--n900)}
.ctg{display:flex;flex-wrap:wrap;gap:5px;margin-top:6px}
.ct{background:var(--pl);color:var(--p);font-size:11px;padding:3px 7px;border-radius:5px;font-weight:500}

/* ── MEMBER PAGE ── */
.mlst{display:flex;flex-direction:column;gap:10px}
.mitm{background:var(--W);border-radius:var(--r);padding:14px;box-shadow:var(--s0);border:1px solid var(--n100);display:flex;align-items:center;gap:12px}
.mav2{width:44px;height:44px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:17px;font-weight:700;color:#fff;flex-shrink:0}
.mi{flex:1;min-width:0}
.mi-n{font-size:14px;font-weight:700}.mi-m{font-size:11px;color:var(--n500);margin-top:2px}
.mi-t{display:flex;gap:4px;flex-wrap:wrap;margin-top:6px}
.mb{padding:2px 6px;border-radius:4px;font-size:10px;font-weight:600}

/* ── SETTINGS ── */
.cfg{background:var(--W);border-radius:var(--r);padding:16px;box-shadow:var(--s0);border:1px solid var(--n100);margin-bottom:12px}
.cfg-t{font-size:14px;font-weight:700;margin-bottom:4px}
.cfg-d{font-size:12px;color:var(--n500);margin-bottom:14px;line-height:1.7}
.sr{display:flex;align-items:center;gap:8px;padding:10px 12px;background:var(--n50);border-radius:8px;border:1px solid var(--n200);font-size:12px;margin-bottom:10px}
.sd2{width:8px;height:8px;border-radius:50%;flex-shrink:0}
.sd2-ok{background:var(--g);animation:sp 2s infinite}.sd2-off{background:var(--n400)}
.dcard{background:linear-gradient(135deg,#1a73e8,#4285f4);color:#fff;border-radius:var(--r);padding:14px 16px;display:flex;align-items:center;gap:12px;margin-bottom:12px;text-decoration:none}
.alrt{display:flex;align-items:flex-start;gap:10px;padding:12px 14px;border-radius:var(--rs);margin-bottom:12px;border:1px solid;font-size:13px;line-height:1.5}
.a-d{background:var(--el);border-color:#f5c6c3;color:#c62828}
.a-w{background:var(--wl);border-color:#f5e0a0;color:#b06000}
.auth-card{background:linear-gradient(135deg,#1a73e8,#4285f4);border-radius:var(--r);padding:16px;margin-bottom:14px;color:#fff}
.auth-card h3{font-size:14px;font-weight:700;margin-bottom:4px}
.auth-card p{font-size:12px;opacity:.88;margin-bottom:12px;line-height:1.6}
.acb{background:#fff;color:var(--p);border:none;padding:10px 20px;border-radius:8px;font-size:13px;font-weight:700;cursor:pointer;display:inline-flex;align-items:center;gap:6px;min-height:44px;font-family:inherit}
.asign{background:var(--gl);border:1px solid var(--g);border-radius:var(--r);padding:10px 14px;margin-bottom:14px;display:flex;align-items:center;gap:10px}

/* ── BNAV ── */
.bnav{position:fixed;bottom:0;left:0;right:0;z-index:200;background:var(--W);border-top:1px solid var(--n200);
  padding:6px 0 calc(6px + env(safe-area-inset-bottom));display:grid;grid-template-columns:repeat(5,1fr)}
.bni{display:flex;flex-direction:column;align-items:center;gap:2px;padding:5px 4px;cursor:pointer;
  border:none;background:none;color:var(--n500);font-size:10px;font-weight:500;
  min-height:48px;justify-content:center;font-family:inherit;position:relative}
.bni.on{color:var(--p)}
.bni-i{font-size:22px;line-height:1}
.bni-b{position:absolute;top:3px;right:calc(50% - 22px);background:var(--e);color:#fff;border-radius:10px;font-size:9px;font-weight:700;padding:1px 5px}

/* ── TOAST ── */
.tw{position:fixed;bottom:calc(76px + env(safe-area-inset-bottom));left:12px;right:12px;z-index:999;display:flex;flex-direction:column;gap:6px;pointer-events:none}
.toast{background:var(--n900);color:#fff;padding:12px 14px;border-radius:10px;font-size:13px;display:flex;align-items:center;gap:8px;box-shadow:0 8px 24px rgba(0,0,0,.1);animation:ti .25s;pointer-events:all}
@keyframes ti{from{transform:translateY(8px);opacity:0}}
.t-ok{background:var(--g)}.t-er{background:var(--e)}.t-wn{background:#b06000}
.spin{width:16px;height:16px;border:2px solid rgba(255,255,255,.3);border-top-color:#fff;border-radius:50%;animation:rot .6s linear infinite;flex-shrink:0}
@keyframes rot{to{transform:rotate(360deg)}}
.empty{text-align:center;padding:48px 20px}
.ei{font-size:44px;margin-bottom:12px;opacity:.4}
.et{font-size:15px;font-weight:600;color:var(--n700);margin-bottom:6px}
.ed2{font-size:12px;color:var(--n500);max-width:260px;margin:0 auto 16px}

@media(min-width:768px){
  .sg{grid-template-columns:repeat(4,1fr);gap:14px}
  .fr{grid-template-columns:1fr 1fr}.cgrd{grid-template-columns:repeat(3,1fr)}
  .dt2{grid-template-columns:1fr 1fr}.mlst{display:grid;grid-template-columns:repeat(2,1fr)}
  .modal{border-radius:12px;max-width:620px;margin:auto;animation:mdi .2s}
  @keyframes mdi{from{transform:scale(.95);opacity:0}}
  .mhdl{display:none}.mov{align-items:center}
  .mft{flex-direction:row}.mft .btn{flex:none}
}
@media(min-width:1024px){
  .bnav{display:none!important}.tmenu{display:none!important}
  .side{transform:none!important}.main{margin-left:256px}
  .tbar{height:60px;padding:0 28px}
  .page{padding:24px 28px 32px}
  .tw{left:auto;right:24px;bottom:24px;width:320px}
}
@media(max-width:1023px){
  .side{transform:translateX(-100%)}
  .side.open{transform:translateX(0)}
}
</style>
</head>
<body>

<!-- LOADING — จะถูกซ่อนใน 500ms เสมอ ไม่ว่าจะเกิดอะไร -->
<div id="ld">
  <div class="ico">🛡️</div>
  <div style="font-size:20px;font-weight:700;color:#202124">Family Insurance</div>
  <div class="sub" id="ld-sub">กำลังเริ่มต้น...</div>
  <div class="bar"><div class="fill" id="ld-fill"></div></div>
</div>

<div class="ov" id="ov" onclick="closeSB()"></div>

<!-- SIDEBAR -->
<aside class="side" id="side">
  <div class="side-brand">
    <div class="side-ico">🛡️</div>
    <div><div class="side-nm">Insurance Manager</div><div class="side-sub">Family Policy Tracker</div></div>
  </div>
  <nav class="side-nav">
    <div class="nl">ภาพรวม</div>
    <div class="nr on" onclick="go('dashboard')"><span class="ni">📊</span>Dashboard</div>
    <div class="nr" onclick="go('policies')"><span class="ni">📋</span>กรมธรรม์<span class="nb" id="nb-s" style="display:none">0</span></div>
    <div class="nl" style="margin-top:6px">ประเภท</div>
    <div class="nr" onclick="go('policies');setF2('health')"><span class="ni">❤️‍🩹</span>สุขภาพ</div>
    <div class="nr" onclick="go('policies');setF2('accident')"><span class="ni">⚡</span>อุบัติเหตุ</div>
    <div class="nr" onclick="go('policies');setF2('life')"><span class="ni">🌿</span>ชีวิต</div>
    <div class="nr" onclick="go('policies');setF2('ci')"><span class="ni">🏥</span>โรคร้ายแรง</div>
    <div class="nl" style="margin-top:6px">จัดการ</div>
    <div class="nr" onclick="go('members')"><span class="ni">👨‍👩‍👧‍👦</span>สมาชิก</div>
    <div class="nr" onclick="go('settings')"><span class="ni">⚙️</span>ตั้งค่า</div>
  </nav>
  <div class="side-foot"><div id="sb-auth"></div></div>
</aside>

<!-- MAIN -->
<div class="main">
  <div class="tbar">
    <button class="tmenu" onclick="openSB()">☰</button>
    <div class="ttl" id="pg-t">📊 Dashboard</div>
    <button class="btn bp bs" onclick="openAdd()">＋ เพิ่ม</button>
  </div>

  <div class="sbar" onclick="syncBarClick()">
    <div class="sd sd-off" id="sb-dot"></div>
    <div class="stxt" id="sb-txt">ยังไม่ได้ Login Google</div>
    <button class="sbtn" id="sb-btn" onclick="event.stopPropagation();syncBarClick()">Login</button>
  </div>

  <!-- DASHBOARD -->
  <div class="page active" id="page-dashboard">
    <div id="al-area"></div>
    <div id="da-area"></div>
    <div class="sg">
      <div class="sc"><div class="si" style="background:#e8f0fe">📋</div><div><div class="sv" id="s-tot">0</div><div class="sl">กรมธรรม์</div></div></div>
      <div class="sc"><div class="si" style="background:#e6f4ea">✅</div><div><div class="sv" id="s-act" style="color:var(--g)">0</div><div class="sl">คุ้มครองอยู่</div></div></div>
      <div class="sc"><div class="si" style="background:#fef9e7">⚠️</div><div><div class="sv" id="s-exp" style="color:#c77a00">0</div><div class="sl">ใกล้หมด</div></div></div>
      <div class="sc"><div class="si" style="background:#fce8e6">💰</div><div><div class="sv" id="s-pr" style="color:var(--p);font-size:17px">-</div><div class="sl">เบี้ยรวม/ปี ฿</div></div></div>
    </div>
    <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:10px">
      <span style="font-size:14px;font-weight:700">👨‍👩‍👧‍👦 ประกันของแต่ละคน</span>
      <span style="font-size:11px;color:var(--n500)">แตะเพื่อ expand</span>
    </div>
    <div id="mem-area"></div>
    <div style="background:var(--W);border-radius:var(--r);padding:16px;box-shadow:var(--s0);border:1px solid var(--n100);margin-bottom:12px">
      <div style="font-size:14px;font-weight:600;margin-bottom:12px">สัดส่วนประเภทประกัน</div>
      <div class="drow">
        <div class="dwrap">
          <svg class="donut" id="dsvg" width="100" height="100" viewBox="0 0 100 100">
            <circle cx="50" cy="50" r="38" fill="none" stroke="#e8eaed" stroke-width="12"/>
          </svg>
          <div class="dc"><div class="dn" id="d-n">0</div><div class="dl">รายการ</div></div>
        </div>
        <div class="dleg" id="d-leg"><span style="color:var(--n400);font-size:12px">ยังไม่มีข้อมูล</span></div>
      </div>
    </div>
    <div style="background:var(--W);border-radius:var(--r);padding:16px;box-shadow:var(--s0);border:1px solid var(--n100)">
      <div style="font-size:14px;font-weight:600;margin-bottom:12px">🔔 ใกล้หมดอายุ (90 วัน)</div>
      <div class="elst" id="exp-lst"></div>
    </div>
  </div>

  <!-- POLICIES -->
  <div class="page" id="page-policies">
    <div class="srch"><span>🔍</span><input type="search" id="q" placeholder="ค้นหา..." oninput="renderP()" autocorrect="off" autocapitalize="off"></div>
    <div class="fscr">
      <div class="fc on" data-f="all" onclick="setF(this,'all')">ทั้งหมด</div>
      <div class="fc" data-f="health" onclick="setF(this,'health')">❤️‍🩹 สุขภาพ</div>
      <div class="fc" data-f="accident" onclick="setF(this,'accident')">⚡ อุบัติเหตุ</div>
      <div class="fc" data-f="life" onclick="setF(this,'life')">🌿 ชีวิต</div>
      <div class="fc" data-f="ci" onclick="setF(this,'ci')">🏥 CI</div>
      <div class="fc" data-f="expiring" onclick="setF(this,'expiring')">⚠️ ใกล้หมด</div>
    </div>
    <div class="plst" id="p-lst"></div>
    <div id="p-empty" class="empty" style="display:none">
      <div class="ei">🛡️</div><div class="et">ยังไม่มีกรมธรรม์</div>
      <div class="ed2">กดปุ่ม ＋ เพิ่ม เพื่อเริ่มบันทึก</div>
      <button class="btn bp" onclick="openAdd()">＋ เพิ่มกรมธรรม์แรก</button>
    </div>
  </div>

  <!-- MEMBERS -->
  <div class="page" id="page-members">
    <div style="display:flex;justify-content:flex-end;margin-bottom:12px">
      <button class="btn bp bs" onclick="openMemMod()">＋ เพิ่มสมาชิก</button>
    </div>
    <div class="mlst" id="m-lst"></div>
  </div>

  <!-- SETTINGS -->
  <div class="page" id="page-settings">
    <div class="cfg"><div class="cfg-t">🔐 Google Account</div><div id="set-auth"></div></div>
    <div class="cfg">
      <div class="cfg-t">⚙️ OAuth Client ID</div>
      <div class="cfg-d">สร้างจาก Google Cloud Console → Credentials → OAuth 2.0 Client ID (Web App)<br>
        Authorized origins: <code id="c-org" style="background:var(--n100);padding:2px 5px;border-radius:4px;font-size:11px;word-break:break-all"></code></div>
      <div class="fg"><div class="fl">Client ID</div>
        <input type="text" class="fi" id="cid-in" placeholder="xxx.apps.googleusercontent.com" autocorrect="off" autocapitalize="none"></div>
      <button class="btn bp" onclick="saveCID()" style="width:100%">💾 บันทึก Client ID</button>
    </div>
    <div class="cfg" style="border:2px solid var(--p)">
      <div class="cfg-t" style="color:var(--p)">📊 Google Sheets — แหล่งข้อมูลหลัก</div>
      <div class="cfg-d">ข้อมูลเดียวกันทุกเครื่อง — iPhone, iPad, PC ดึงจาก Sheet โดยตรง<br>
        ID จาก URL: <code style="font-size:11px;background:var(--n100);padding:2px 4px;border-radius:3px;word-break:break-all">docs.google.com/spreadsheets/d/<b style="color:var(--p)">[ID]</b>/edit</code></div>
      <div class="fg"><div class="fl">Spreadsheet ID <span class="r">*</span></div>
        <input type="text" class="fi" id="sid-in" placeholder="1BxiMVs0XRA5..." autocorrect="off" autocapitalize="none"></div>
      <div class="fr">
        <div class="fg"><div class="fl">Sheet กรมธรรม์</div><input type="text" class="fi" id="sn-in" value="Policies" autocorrect="off"></div>
        <div class="fg"><div class="fl">Sheet สมาชิก</div><input type="text" class="fi" id="msn-in" value="Members" autocorrect="off"></div>
      </div>
      <div class="sr" id="sh-row"><div class="sd2 sd2-off" id="sh-dot"></div><span id="sh-txt">ยังไม่ได้เชื่อมต่อ</span></div>
      <div style="display:flex;gap:8px;flex-wrap:wrap">
        <button class="btn bp bs" onclick="saveSCfg()">💾 บันทึก</button>
        <button class="btn bo bs" onclick="pull()">📥 โหลดจาก Sheet</button>
        <button class="btn bg bs" onclick="push()">📤 บันทึกขึ้น Sheet</button>
      </div>
    </div>
    <div class="cfg">
      <div class="cfg-t">📁 Google Drive</div>
      <div class="cfg-d">Folder ID เก็บใน Sheet "Config" — ทุกเครื่องใช้ Folder เดียวกัน</div>
      <div id="drv-area"></div>
      <div class="fg"><div class="fl">Root Folder ID (ปล่อยว่าง = สร้างอัตโนมัติ)</div>
        <input type="text" class="fi" id="dfid-in" placeholder="ปล่อยว่าง" autocorrect="off" autocapitalize="none"></div>
      <button class="btn bo bs" onclick="initDrive()" style="width:100%">📁 สร้าง / เชื่อม Folder</button>
    </div>
    <div class="cfg" style="border-color:var(--el)">
      <div class="cfg-t" style="color:var(--e)">🗑️ จัดการข้อมูล</div>
      <div style="display:flex;gap:8px;flex-wrap:wrap;margin-top:8px">
        <button class="btn bg bs" onclick="doExp()">📥 Export CSV</button>
        <button class="btn bd bs" onclick="clearLoc()">🗑️ ล้างข้อมูลในเครื่อง</button>
      </div>
    </div>
  </div>
</div>

<!-- BOTTOM NAV -->
<nav class="bnav">
  <button class="bni on" data-p="dashboard" onclick="go('dashboard')"><span class="bni-i">📊</span>หน้าหลัก</button>
  <button class="bni" data-p="policies" onclick="go('policies')"><span class="bni-i">📋</span>กรมธรรม์<span class="bni-b" id="nb-b" style="display:none">0</span></button>
  <button class="bni" onclick="openAdd()" style="color:var(--p)">
    <span class="bni-i" style="background:var(--p);color:#fff;border-radius:50%;width:38px;height:38px;display:flex;align-items:center;justify-content:center;font-size:20px">＋</span>เพิ่ม
  </button>
  <button class="bni" data-p="members" onclick="go('members')"><span class="bni-i">👨‍👩‍👧‍👦</span>สมาชิก</button>
  <button class="bni" data-p="settings" onclick="go('settings')"><span class="bni-i">⚙️</span>ตั้งค่า</button>
</nav>

<!-- POLICY MODAL -->
<div class="mov" id="pm"><div class="modal">
  <div class="mhdl"></div>
  <div class="mhd2"><div class="mtl" id="pm-t">➕ เพิ่มกรมธรรม์</div><button class="mcl" onclick="closeMod('pm')">✕</button></div>
  <div class="mbdy">
    <div class="fg"><div class="fl">ประเภทประกัน <span class="r">*</span></div>
      <div class="tsel">
        <div class="tc" onclick="selT('health')" data-t="health"><div class="tci">❤️‍🩹</div>สุขภาพ</div>
        <div class="tc" onclick="selT('accident')" data-t="accident"><div class="tci">⚡</div>อุบัติเหตุ</div>
        <div class="tc" onclick="selT('life')" data-t="life"><div class="tci">🌿</div>ชีวิต</div>
        <div class="tc" onclick="selT('ci')" data-t="ci"><div class="tci">🏥</div>CI</div>
        <div class="tc" onclick="selT('other')" data-t="other"><div class="tci">📌</div>อื่นๆ</div>
      </div>
      <input type="hidden" id="f-tp">
    </div>
    <div class="fg"><div class="fl">สมาชิก <span class="r">*</span></div><select class="fi" id="f-mem"></select></div>
    <div class="fr">
      <div class="fg"><div class="fl">บริษัทประกัน <span class="r">*</span></div><input type="text" class="fi" id="f-co" placeholder="AIA, เมืองไทย..."></div>
      <div class="fg"><div class="fl">เลขกรมธรรม์</div><input type="text" class="fi" id="f-pno" placeholder="TH-001" autocorrect="off"></div>
    </div>
    <div class="fg"><div class="fl">ชื่อแผน</div><input type="text" class="fi" id="f-pl" placeholder="Health Plus Gold"></div>
    <hr class="fdv"><div class="fsc">📅 ระยะเวลาคุ้มครอง</div>
    <div class="fr">
      <div class="fg"><div class="fl">วันเริ่ม <span class="r">*</span></div><input type="date" class="fi" id="f-s"></div>
      <div class="fg"><div class="fl">วันหมด <span class="r">*</span></div><input type="date" class="fi" id="f-e"></div>
    </div>
    <hr class="fdv"><div class="fsc">💰 การเงิน</div>
    <div class="fr">
      <div class="fg"><div class="fl">เบี้ย/ปี (฿)</div><input type="number" class="fi" id="f-pr" placeholder="0" inputmode="numeric"></div>
      <div class="fg"><div class="fl">ทุนประกัน (฿)</div><input type="number" class="fi" id="f-su" placeholder="0" inputmode="numeric"></div>
    </div>
    <div class="fr">
      <div class="fg"><div class="fl">ผู้รับผลประโยชน์</div><input type="text" class="fi" id="f-bn" placeholder="ภรรยา, ลูก"></div>
      <div class="fg"><div class="fl">ความถี่ชำระ</div>
        <select class="fi" id="f-fq"><option value="yearly">รายปี</option><option value="halfyearly">ราย 6 เดือน</option><option value="quarterly">รายไตรมาส</option><option value="monthly">รายเดือน</option></select>
      </div>
    </div>
    <hr class="fdv"><div class="fsc">🩺 ความคุ้มครอง</div>
    <div class="cgrd">
      <label class="ci"><input type="checkbox" value="ipd"> 🏥 IPD</label>
      <label class="ci"><input type="checkbox" value="opd"> 🩺 OPD</label>
      <label class="ci"><input type="checkbox" value="dental"> 🦷 ทันตกรรม</label>
      <label class="ci"><input type="checkbox" value="vision"> 👁️ สายตา</label>
      <label class="ci"><input type="checkbox" value="maternity"> 🤰 คลอดบุตร</label>
      <label class="ci"><input type="checkbox" value="critical"> 🔴 โรคร้ายแรง</label>
      <label class="ci"><input type="checkbox" value="accident_med"> ⚡ อุบัติเหตุ</label>
      <label class="ci"><input type="checkbox" value="death"> 💐 เสียชีวิต</label>
      <label class="ci"><input type="checkbox" value="disability"> ♿ ทุพพลภาพ</label>
      <label class="ci"><input type="checkbox" value="saving"> 💰 สะสมทรัพย์</label>
      <label class="ci"><input type="checkbox" value="retirement"> 👴 บำนาญ</label>
      <label class="ci"><input type="checkbox" value="other_cov"> 📌 อื่นๆ</label>
    </div>
    <hr class="fdv"><div class="fsc">📎 ไฟล์แนบ → Google Drive</div>
    <div id="up-warn" class="alrt" style="display:none;border-color:#b3cef5;background:var(--pl);color:var(--pk)">🔐 Login Google ก่อนอัพโหลดไฟล์</div>
    <div id="up-wrap">
      <div class="upz" onclick="document.getElementById('fi').click()" ondragover="event.preventDefault()" ondrop="onDrop(event)">
        <input type="file" id="fi" multiple accept=".pdf,.jpg,.jpeg,.png" onchange="onPick(event)">
        <div style="font-size:28px">📎</div>
        <div style="font-size:13px;color:var(--n600)">แตะเลือกไฟล์</div>
        <div style="font-size:11px;color:var(--n400)">PDF, JPG, PNG · สูงสุด 20MB</div>
      </div>
      <div class="flst" id="f-lst"></div>
    </div>
    <div class="fg" style="margin-top:14px"><div class="fl">หมายเหตุ</div><textarea class="fi" id="f-nt" placeholder="เงื่อนไขพิเศษ..."></textarea></div>
  </div>
  <div class="mft"><button class="btn bg" onclick="closeMod('pm')">ยกเลิก</button><button class="btn bp" id="sv-btn" onclick="saveP()">💾 บันทึก</button></div>
</div></div>

<!-- DETAIL MODAL -->
<div class="mov" id="dm"><div class="modal">
  <div class="mhdl"></div>
  <div class="mhd2"><div class="mtl">📋 รายละเอียด</div><button class="mcl" onclick="closeMod('dm')">✕</button></div>
  <div class="mbdy" id="dm-b"></div>
  <div class="mft"><button class="btn bg" onclick="closeMod('dm')">ปิด</button><button class="btn bo" id="dm-ed">✏️ แก้ไข</button><button class="btn bd" id="dm-dl">🗑️ ลบ</button></div>
</div></div>

<!-- MEMBER MODAL -->
<div class="mov" id="mm"><div class="modal" style="max-width:440px">
  <div class="mhdl"></div>
  <div class="mhd2"><div class="mtl">👤 เพิ่มสมาชิก</div><button class="mcl" onclick="closeMod('mm')">✕</button></div>
  <div class="mbdy">
    <div class="fg"><div class="fl">ชื่อ-นามสกุล <span class="r">*</span></div><input type="text" class="fi" id="m-nm" placeholder="สมชาย ใจดี"></div>
    <div class="fr">
      <div class="fg"><div class="fl">ความสัมพันธ์</div>
        <select class="fi" id="m-rl"><option>ตัวเอง</option><option>คู่สมรส</option><option>ลูก</option><option>พ่อ</option><option>แม่</option><option>พ่อตา/แม่ยาย</option><option>อื่นๆ</option></select>
      </div>
      <div class="fg"><div class="fl">วันเกิด</div><input type="date" class="fi" id="m-db"></div>
    </div>
    <div class="fg"><div class="fl">สีประจำตัว</div><input type="color" class="fi" id="m-cl" value="#1a73e8" style="height:48px;cursor:pointer;padding:4px 8px"></div>
  </div>
  <div class="mft"><button class="btn bg" onclick="closeMod('mm')">ยกเลิก</button><button class="btn bp" onclick="saveM()">💾 เพิ่มสมาชิก</button></div>
</div></div>

<div class="tw" id="tw"></div>

<script src="https://accounts.google.com/gsi/client" async></script>
<script src="https://apis.google.com/js/api.js" async onload="onGapi()"></script>
<script>
// ════════════════════════
//  CONSTANTS
// ════════════════════════
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

// ════════════════════════
//  STATE
// ════════════════════════
let P=[],M=[],editId=null,selType='',filt='all';
let pf=[],syncTmr=null;
let tok=null,usr=null,gisOk=false;
let cfg={cid:'',sid:'',sn:'Policies',msn:'Members',si:15};
let driveId='';

// ════════════════════════
//  LOADING — ซ่อนแน่นอนใน 500ms
// ════════════════════════
(function(){
  // ซ่อน loading ใน 500ms เสมอ ไม่ว่าจะเกิดอะไร
  setTimeout(hideLd, 500);
})();

function setLd(pct,txt){
  try{
    document.getElementById('ld-fill').style.width=pct+'%';
    if(txt) document.getElementById('ld-sub').textContent=txt;
  }catch(e){}
}
function hideLd(){
  try{
    const el=document.getElementById('ld');
    if(!el||el.style.display==='none') return;
    el.classList.add('gone');
    setTimeout(()=>{ el.style.display='none'; },350);
  }catch(e){}
}

// ════════════════════════
//  BOOT
// ════════════════════════
function boot(){
  try{
    setLd(20,'อ่านการตั้งค่า...');
    loadCfg();

    // ตั้งค่า UI fields
    const co=document.getElementById('c-org'); if(co) co.textContent=location.origin;
    const ci=document.getElementById('cid-in'); if(ci&&cfg.cid) ci.value=cfg.cid;
    const si=document.getElementById('sid-in'); if(si&&cfg.sid) si.value=cfg.sid;
    const sn=document.getElementById('sn-in');  if(sn) sn.value=cfg.sn||'Policies';
    const mn=document.getElementById('msn-in'); if(mn) mn.value=cfg.msn||'Members';

    setLd(45,'โหลดข้อมูล...');
    loadCache();

    if(!M.length){
      M=[{id:uid(),name:'ฉัน (ตัวเอง)',role:'ตัวเอง',color:'#1a73e8',dob:'',driveFolder:''}];
    }

    setLd(75,'เตรียมหน้าจอ...');
    populateMSel();
    renderAll();
    checkAlerts();
    updateAuthUI();
    updateSyncBar();

    setLd(100,'');

    // restore session แบบ background — ไม่ block loading hide
    const saved=sessionStorage.getItem('gt');
    if(saved){
      tok=saved;
      restoreSession();
    }

  }catch(e){
    console.error('boot error:',e);
  }
  // loading จะถูกซ่อนโดย setTimeout 500ms ด้านบนแน่นอน
}

// ════════════════════════
//  SESSION RESTORE (background)
// ════════════════════════
async function restoreSession(){
  try{
    const r=await fetch('https://www.googleapis.com/oauth2/v3/tokeninfo?access_token='+tok);
    if(!r.ok) throw new Error('invalid');
    await fetchUsr();
    if(cfg.sid){
      updateSyncBar('กำลังโหลดจาก Google Sheets...');
      await pull(false);
      toast('โหลดข้อมูลจาก Google Sheets ✅','success');
    }
  }catch(e){
    tok=null; sessionStorage.removeItem('gt');
    updateAuthUI(); updateSyncBar();
  }
}

// ════════════════════════
//  LOCAL CACHE
// ════════════════════════
function loadCache(){
  try{
    P=JSON.parse(localStorage.getItem('ip')||'[]');
    M=JSON.parse(localStorage.getItem('im')||'[]');
    driveId=localStorage.getItem('idf')||'';
    if(driveId){ const el=document.getElementById('dfid-in'); if(el) el.value=driveId; }
  }catch(e){P=[];M=[];}
}
function saveCache(){
  localStorage.setItem('ip',JSON.stringify(P));
  localStorage.setItem('im',JSON.stringify(M));
  localStorage.setItem('idf',driveId);
}
function loadCfg(){
  try{cfg=Object.assign({cid:'',sid:'',sn:'Policies',msn:'Members',si:15},JSON.parse(localStorage.getItem('ic')||'{}'));}
  catch(e){}
}
function saveCfg(){ localStorage.setItem('ic',JSON.stringify(cfg)); }
function uid(){ return Date.now().toString(36)+Math.random().toString(36).substr(2,5); }

// ════════════════════════
//  GOOGLE AUTH
// ════════════════════════
function onGapi(){
  try{ gapi.load('client',()=>{ try{gapi.client.init({});}catch(e){} }); }catch(e){}
}
function tryGIS(){
  if(!cfg.cid){gisOk=true;return;}
  if(typeof google==='undefined'||!google.accounts){setTimeout(tryGIS,500);return;}
  try{
    window._tc=google.accounts.oauth2.initTokenClient({
      client_id:cfg.cid, scope:SCOPE,
      callback:onTok,
      error_callback:(e)=>toast('Login ผิดพลาด: '+(e.type||e),'error'),
    });
    gisOk=true;
  }catch(e){console.warn('GIS:',e);gisOk=true;}
}
async function onTok(r){
  if(r.error){toast('Login ไม่สำเร็จ: '+r.error,'error');return;}
  tok=r.access_token;
  sessionStorage.setItem('gt',tok);
  await fetchUsr();
  if(cfg.sid){
    updateSyncBar('กำลังดึงข้อมูลจาก Sheet...');
    await pull(false);
    toast('โหลดข้อมูลจาก Google Sheets สำเร็จ ✅','success');
  } else {
    toast('Login สำเร็จ! กรุณาตั้งค่า Sheet ID → ⚙️ ตั้งค่า','warn');
  }
  setupAutoSync();
}
async function fetchUsr(){
  try{
    const r=await fetch('https://www.googleapis.com/oauth2/v3/userinfo',{headers:{Authorization:'Bearer '+tok}});
    if(!r.ok){ tok=null; sessionStorage.removeItem('gt'); updateAuthUI(); updateSyncBar(); return; }
    usr=await r.json();
    updateAuthUI(); updateSyncBar();
  }catch(e){console.warn('fetchUsr:',e);}
}
function signIn(){
  if(!cfg.cid){toast('กรุณาตั้งค่า Client ID ก่อน','warn');go('settings');return;}
  if(!gisOk||!window._tc){tryGIS();setTimeout(signIn,800);return;}
  try{ window._tc.requestAccessToken({prompt:tok?'':'consent'}); }
  catch(e){ toast('เปิด Login ไม่ได้ — ลองอีกครั้ง','error'); }
}
function signOut(){
  if(tok&&typeof google!=='undefined') try{google.accounts.oauth2.revoke(tok,()=>{});}catch(e){}
  tok=null; usr=null; sessionStorage.removeItem('gt');
  if(syncTmr){clearInterval(syncTmr);syncTmr=null;}
  updateAuthUI(); updateSyncBar();
  toast('ออกจากระบบแล้ว','warn');
}

// ════════════════════════
//  SYNC BAR
// ════════════════════════
function updateSyncBar(busyMsg){
  const dot=document.getElementById('sb-dot');
  const txt=document.getElementById('sb-txt');
  const btn=document.getElementById('sb-btn');
  if(!dot) return;
  dot.className='sd';
  if(busyMsg){ dot.classList.add('sd-busy'); txt.textContent=busyMsg; btn.textContent='...'; }
  else if(!tok){ dot.classList.add('sd-off'); txt.textContent='ยังไม่ได้ Login Google'; btn.textContent='Login'; }
  else if(!cfg.sid){ dot.classList.add('sd-off'); txt.textContent='Login แล้ว — ยังไม่ได้ตั้งค่า Sheet ID'; btn.textContent='ตั้งค่า'; }
  else{ dot.classList.add('sd-ok'); txt.textContent=`✅ Google Sheets: ${cfg.sn} · ${P.length} กรมธรรม์ · ${M.length} สมาชิก`; btn.textContent='Sync'; }
}
function syncBarClick(){
  if(!tok) signIn();
  else if(!cfg.sid) go('settings');
  else pull();
}
function setupAutoSync(){
  if(syncTmr) clearInterval(syncTmr);
  if(tok&&cfg.sid&&cfg.si>0)
    syncTmr=setInterval(()=>pull(false), cfg.si*60000);
}

// ════════════════════════
//  GOOGLE SHEETS — fetch REST
// ════════════════════════
async function gsh(method,path,body=null){
  if(!tok) throw new Error('NOT_SIGNED_IN');
  const url=`https://sheets.googleapis.com/v4/spreadsheets/${cfg.sid}${path}`;
  const o={method,headers:{Authorization:'Bearer '+tok,'Content-Type':'application/json'}};
  if(body) o.body=JSON.stringify(body);
  const r=await fetch(url,o);
  if(r.status===401){
    tok=null; sessionStorage.removeItem('gt'); usr=null;
    updateAuthUI(); updateSyncBar();
    throw new Error('TOKEN_EXPIRED');
  }
  if(!r.ok){
    const e=await r.json().catch(()=>({}));
    throw new Error(e.error?.message||`HTTP ${r.status}`);
  }
  return r.json();
}

// ── PULL: Google Sheets → App (แหล่งข้อมูลหลัก)
async function pull(showMsg=true){
  if(!tok){ if(showMsg) toast('กรุณา Login ก่อน','warn'); return; }
  if(!cfg.sid){ if(showMsg) toast('กรุณาตั้งค่า Sheet ID → ⚙️ ตั้งค่า','warn'); go('settings'); return; }
  updateSyncBar('กำลังดึงข้อมูลจาก Google Sheets...');
  try{
    // 1. Config sheet → drive folder ID (แชร์ทุกเครื่อง)
    try{
      const cd=await gsh('GET',`/values/${enc('Config')}?majorDimension=ROWS`);
      if(cd.values&&cd.values.length>1){
        const [h,...rows]=cd.values;
        const xi=k=>h.indexOf(k);
        rows.forEach(r=>{
          const key=r[xi('key')]||r[0]||'';
          if(key==='drive_folder_id') driveId=r[xi('value')]||r[1]||'';
        });
        const df=document.getElementById('dfid-in'); if(df) df.value=driveId;
      }
    }catch(e){ /* Config ยังไม่มี */ }

    // 2. Policies sheet
    const pd=await gsh('GET',`/values/${enc(cfg.sn)}?majorDimension=ROWS`);
    if(pd.values&&pd.values.length>1){
      const [h,...rows]=pd.values;
      const xi=k=>h.indexOf(k);
      P=rows
        .filter(r=>{ const id=r[xi('id')]||r[0]||''; return id.trim()!==''; })
        .map(r=>({
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
    } else { P=[]; }

    // 3. Members sheet (รวม driveFolder ของแต่ละคน)
    try{
      const md=await gsh('GET',`/values/${enc(cfg.msn||'Members')}?majorDimension=ROWS`);
      if(md.values&&md.values.length>1){
        const [h,...rows]=md.values;
        const xi=k=>h.indexOf(k);
        const loaded=rows
          .filter(r=>r[xi('name')]||r[1])
          .map(r=>({
            id:r[xi('id')]||uid(),
            name:r[xi('name')]||'',
            role:r[xi('role')]||'',
            dob:r[xi('dob')]||'',
            color:r[xi('color')]||'#1a73e8',
            driveFolder:r[xi('drive_folder_id')]||'',
          }));
        if(loaded.length) M=loaded;
      }
    }catch(e){ /* Members ยังไม่มี */ }

    if(!M.length) M=[{id:uid(),name:'ฉัน (ตัวเอง)',role:'ตัวเอง',color:'#1a73e8',dob:'',driveFolder:''}];

    saveCache();
    populateMSel();
    renderAll();
    checkAlerts();
    updateSyncBar();
    if(driveId) renderDriveCard(null);
    if(showMsg) toast(`โหลดจาก Sheets ✅  ${P.length} กรมธรรม์, ${M.length} สมาชิก`,'success');

  }catch(e){
    updateSyncBar();
    if(e.message==='TOKEN_EXPIRED') toast('Session หมดอายุ — Login ใหม่','warn');
    else if(e.message==='NOT_SIGNED_IN'){ if(showMsg) toast('กรุณา Login ก่อน','warn'); }
    else { if(showMsg) toast('โหลดไม่สำเร็จ: '+e.message,'error'); console.error('pull:',e); }
  }
}

// ── PUSH: App → Google Sheets
async function push(showMsg=true){
  if(!tok){ if(showMsg) toast('กรุณา Login ก่อน','warn'); return; }
  if(!cfg.sid){ if(showMsg) toast('กรุณาตั้งค่า Sheet ID','warn'); return; }
  updateSyncBar('กำลังบันทึกขึ้น Google Sheets...');
  const PH=['id','member_id','member_name','type','company','policy_no','plan_name',
    'start_date','end_date','premium','sum_insured','payment_freq','beneficiary',
    'coverage','drive_files','notes','created_at','updated_at'];
  const pR=[PH,...P.map(p=>[
    p.id,p.member,getMem(p.member).name,p.type,p.company||'',p.policy_no||'',p.plan_name||'',
    p.start_date||'',p.end_date||'',p.premium||0,p.sum_insured||0,p.payment_freq||'yearly',p.beneficiary||'',
    (p.coverage||[]).join(','),JSON.stringify(p.driveFiles||[]),p.notes||'',p.created_at||'',p.updated_at||new Date().toISOString(),
  ])];
  const MH=['id','name','role','dob','color','drive_folder_id'];
  const mR=[MH,...M.map(m=>[m.id,m.name,m.role||'',m.dob||'',m.color||'#1a73e8',m.driveFolder||''])];
  const cR=[['key','value'],['drive_folder_id',driveId||'']];
  try{
    await gsh('POST',`/values/${enc(cfg.sn+'!A:Z')}:clear`);
    await gsh('PUT',`/values/${enc(cfg.sn+'!A1')}?valueInputOption=RAW`,{values:pR});
    try{ await gsh('POST',`/values/${enc((cfg.msn||'Members')+'!A:Z')}:clear`); await gsh('PUT',`/values/${enc((cfg.msn||'Members')+'!A1')}?valueInputOption=RAW`,{values:mR}); }catch(e){}
    try{ await gsh('POST',`/values/${enc('Config!A:Z')}:clear`); await gsh('PUT',`/values/${enc('Config!A1')}?valueInputOption=RAW`,{values:cR}); }catch(e){}
    updateSyncBar();
    if(showMsg) toast('บันทึกขึ้น Sheet ✅','success');
    else updateSyncBar();
  }catch(e){
    updateSyncBar();
    if(e.message==='TOKEN_EXPIRED') toast('Session หมดอายุ — Login ใหม่','warn');
    else if(showMsg) toast('บันทึกไม่สำเร็จ: '+e.message,'error');
  }
}
function enc(s){return encodeURIComponent(s);}

// ════════════════════════
//  GOOGLE DRIVE — fetch REST
// ════════════════════════
async function gdr(m,url,b=null,f=false){
  if(!tok) throw new Error('NOT_SIGNED_IN');
  const o={method:m,headers:{Authorization:'Bearer '+tok}};
  if(b&&!f){o.headers['Content-Type']='application/json';o.body=JSON.stringify(b);}
  if(b&&f) o.body=b;
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
      driveId=inp; await saveDriveToSheet(inp); saveCache();
      toast(`เชื่อมต่อ "${d.name}" สำเร็จ ✅`,'success'); renderDriveCard(d);
    }catch(e){toast('ไม่พบ Folder: '+e.message,'error');}
    return;
  }
  toast('กำลังสร้าง Folder...','warn');
  try{
    const d=await gdr('POST','https://www.googleapis.com/drive/v3/files?fields=id,name,webViewLink',
      {name:'Family Insurance',mimeType:'application/vnd.google-apps.folder'});
    driveId=d.id; document.getElementById('dfid-in').value=d.id;
    await saveDriveToSheet(d.id); saveCache();
    toast('สร้าง Folder เรียบร้อย ✅','success'); renderDriveCard(d);
  }catch(e){toast('สร้างไม่สำเร็จ: '+e.message,'error');}
}
async function saveDriveToSheet(fid){
  if(!cfg.sid) return;
  try{
    await gsh('POST',`/values/${enc('Config!A:Z')}:clear`);
    await gsh('PUT',`/values/${enc('Config!A1')}?valueInputOption=RAW`,{values:[['key','value'],['drive_folder_id',fid]]});
  }catch(e){console.warn('saveDriveToSheet:',e.message);}
}
function renderDriveCard(f){
  const el=document.getElementById('drv-area'); if(!el||!driveId) return;
  el.innerHTML=`<a href="${f?.webViewLink||'https://drive.google.com/drive/folders/'+driveId}" target="_blank" class="dcard">
    <span style="font-size:26px">📁</span>
    <div><div style="font-weight:700">${f?.name||'Family Insurance'}</div>
    <div style="font-size:11px;opacity:.8">ใช้ร่วมกันทุกเครื่อง — คลิกเปิดใน Drive</div></div>
  </a>`;
}
async function getMemFolder(mid){
  const mi=M.findIndex(m=>m.id===mid);
  if(mi!==-1&&M[mi].driveFolder) return M[mi].driveFolder;
  const mem=getMem(mid);
  const d=await gdr('POST','https://www.googleapis.com/drive/v3/files?fields=id',
    {name:mem.name,mimeType:'application/vnd.google-apps.folder',parents:[driveId]});
  if(mi!==-1) M[mi].driveFolder=d.id;
  saveCache(); push(false);
  return d.id;
}
async function upFile(f,pid,i){
  pf[i].status='uploading'; renderFList();
  const meta={name:f.name,parents:[pid]};
  const form=new FormData();
  form.append('metadata',new Blob([JSON.stringify(meta)],{type:'application/json'}));
  form.append('file',f);
  try{
    const d=await gdr('POST','https://www.googleapis.com/upload/drive/v3/files?uploadType=multipart&fields=id,name,webViewLink',form,true);
    pf[i].status='done'; pf[i].wvl=d.webViewLink; renderFList();
    return{id:d.id,name:d.name,webViewLink:d.webViewLink};
  }catch(e){pf[i].status='error'; renderFList(); return null;}
}

// ════════════════════════
//  AUTH UI
// ════════════════════════
function updateAuthUI(){
  const isIn=!!usr;
  const authHtml=isIn
    ?`<div style="display:flex;align-items:center;gap:8px;padding:10px 12px;border-radius:8px;background:var(--gl);border:1px solid var(--g)">
        ${usr.picture?`<img src="${usr.picture}" style="width:24px;height:24px;border-radius:50%">`:'✅'}
        <div style="flex:1;overflow:hidden">
          <div style="font-size:12px;font-weight:600;overflow:hidden;text-overflow:ellipsis;white-space:nowrap">${usr.name}</div>
          <div style="font-size:10px;color:var(--n500);overflow:hidden;text-overflow:ellipsis;white-space:nowrap">${usr.email}</div>
        </div>
        <button onclick="signOut()" style="background:none;border:none;cursor:pointer;font-size:14px;color:var(--n500);padding:2px">✕</button>
      </div>`
    :`<button class="btn bp" onclick="signIn()" style="width:100%;font-size:12px;min-height:40px">🔐 Login Google</button>`;

  const el1=document.getElementById('sb-auth'); if(el1) el1.innerHTML=authHtml;

  const da=document.getElementById('da-area');
  if(da) da.innerHTML=isIn
    ?`<div class="asign">
        ${usr.picture?`<img src="${usr.picture}" style="width:28px;height:28px;border-radius:50%">`:''}
        <div style="flex:1">
          <div style="font-size:13px;font-weight:600;color:var(--g)">${usr.name}</div>
          <div style="font-size:11px;color:var(--n500)">${cfg.sid?'ข้อมูลจาก Google Sheets โดยตรง':'ยังไม่ได้ตั้งค่า Sheet ID'}</div>
        </div>
        <button onclick="pull()" style="background:none;border:1.5px solid var(--g);color:var(--g);padding:6px 10px;border-radius:8px;cursor:pointer;font-size:11px;font-weight:600;font-family:inherit">🔄 Sync</button>
      </div>`
    :`<div class="auth-card">
        <h3>🔐 Login Google เพื่อ Sync ข้อมูลทุกเครื่อง</h3>
        <p>iPhone, iPad, PC จะเห็นข้อมูลเดียวกัน — ดึงจาก Google Sheets โดยตรง</p>
        <button class="acb" onclick="signIn()">🔐 เข้าสู่ระบบ Google</button>
      </div>`;

  const sa=document.getElementById('set-auth');
  if(sa) sa.innerHTML=isIn
    ?`<div style="display:flex;align-items:center;gap:10px;padding:4px 0 12px">
        ${usr.picture?`<img src="${usr.picture}" style="width:40px;height:40px;border-radius:50%">`:''}
        <div><div style="font-weight:700">${usr.name}</div><div style="font-size:12px;color:var(--n500)">${usr.email}</div></div>
        <button onclick="signOut()" class="btn bg bs" style="margin-left:auto">ออก</button>
      </div>`
    :`<div style="padding:4px 0 12px">
        <div style="font-size:13px;color:var(--n600);margin-bottom:10px">ยังไม่ได้ Login — ข้อมูลจะเก็บแค่ในเครื่องนี้</div>
        <button class="btn bp" onclick="signIn()" style="width:100%">🔐 Login ด้วย Google</button>
      </div>`;

  const sd=document.getElementById('sh-dot'),st=document.getElementById('sh-txt');
  if(sd&&st){
    if(isIn&&cfg.sid){sd.className='sd2 sd2-ok';st.textContent=`เชื่อมต่อแล้ว: ${cfg.sn} · ดึงข้อมูลจาก Sheets โดยตรง`;}
    else if(isIn){sd.className='sd2';sd.style.background='var(--w)';st.textContent='Login แล้ว — กรุณาตั้งค่า Sheet ID';}
    else{sd.className='sd2 sd2-off';st.textContent='ยังไม่ได้ Login';}
  }
  const uw=document.getElementById('up-warn'),uwp=document.getElementById('up-wrap');
  if(uw&&uwp){uw.style.display=isIn?'none':'flex';uwp.style.display=isIn?'block':'none';}
  if(isIn&&driveId) renderDriveCard(null);
}

// ════════════════════════
//  NAVIGATION
// ════════════════════════
function go(pg){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.getElementById('page-'+pg).classList.add('active');
  document.querySelectorAll('.nr,.bni[data-p]').forEach(n=>n.classList.remove('on'));
  document.querySelectorAll(`[data-p="${pg}"]`).forEach(n=>n.classList.add('on'));
  const T={dashboard:'📊 Dashboard',policies:'📋 กรมธรรม์',members:'👨‍👩‍👧‍👦 สมาชิก',settings:'⚙️ ตั้งค่า'};
  document.getElementById('pg-t').textContent=T[pg]||pg;
  if(pg==='policies') renderP();
  if(pg==='members')  renderMems();
  if(pg==='dashboard'){renderDash();updateAuthUI();}
  if(pg==='settings'){updateAuthUI();if(driveId)renderDriveCard(null);}
  closeSB(); window.scrollTo({top:0,behavior:'smooth'});
}
function openSB(){ document.getElementById('side').classList.add('open'); document.getElementById('ov').classList.add('on'); }
function closeSB(){ document.getElementById('side').classList.remove('open'); document.getElementById('ov').classList.remove('on'); }

// ════════════════════════
//  UTILS
// ════════════════════════
function dl(d){ if(!d) return Infinity; const n=new Date(); n.setHours(0,0,0,0); return Math.ceil((new Date(d)-n)/864e5); }
function thd(s){
  if(!s) return '-'; const d=new Date(s);
  const Mn=['ม.ค.','ก.พ.','มี.ค.','เม.ย.','พ.ค.','มิ.ย.','ก.ค.','ส.ค.','ก.ย.','ต.ค.','พ.ย.','ธ.ค.'];
  return`${d.getDate()} ${Mn[d.getMonth()]} ${d.getFullYear()+543}`;
}
function fm(n){ return n?Number(n).toLocaleString('th-TH')+' ฿':'-'; }
function pst(p){ const d=dl(p.end_date); return d<0?'expired':d<=90?'expiring':'active'; }
function getMem(id){ return M.find(m=>m.id===id)||{name:id||'?',color:'#9aa0a6',driveFolder:''}; }
function ini(n){ return(n||'?').split(' ').map(w=>w[0]).join('').substr(0,2).toUpperCase(); }
function populateMSel(){
  const s=document.getElementById('f-mem'); if(!s) return;
  const pv=s.value;
  s.innerHTML='<option value="">-- เลือกสมาชิก --</option>';
  M.forEach(m=>{ const o=document.createElement('option'); o.value=m.id; o.textContent=m.name+(m.role?` (${m.role})`:''); s.appendChild(o); });
  if(pv) s.value=pv;
}

// ════════════════════════
//  RENDER ALL
// ════════════════════════
function renderAll(){ renderDash(); renderP(); renderMems(); updBadge(); }
function updBadge(){
  const n=P.filter(p=>{ const d=dl(p.end_date); return d>=0&&d<=90; }).length;
  ['nb-s','nb-b'].forEach(id=>{ const b=document.getElementById(id); if(!b) return; b.style.display=n?'inline':'none'; b.textContent=n; });
}

// ── DASHBOARD ──
function renderDash(){
  document.getElementById('s-tot').textContent=P.length;
  document.getElementById('s-act').textContent=P.filter(p=>pst(p)==='active').length;
  document.getElementById('s-exp').textContent=P.filter(p=>pst(p)==='expiring').length;
  const pr=P.reduce((a,p)=>a+Number(p.premium||0),0);
  document.getElementById('s-pr').textContent=pr?pr.toLocaleString('th-TH'):'-';
  renderMemIns(); renderDonut(); renderExpiry();
}

// ── Member Insurance Sections ──
function renderMemIns(){
  const area=document.getElementById('mem-area'); if(!area) return;
  if(!M.length){
    area.innerHTML=`<div class="auth-card" style="text-align:center">
      <h3>👨‍👩‍👧‍👦 เพิ่มสมาชิกครอบครัวก่อน</h3>
      <p>แล้วเพิ่มกรมธรรม์ให้แต่ละคน</p>
      <button class="acb" onclick="openMemMod()">＋ เพิ่มสมาชิก</button>
    </div>`;
    return;
  }
  area.innerHTML=M.map(m=>{
    const mp=P.filter(p=>p.member===m.id).sort((a,b)=>new Date(a.end_date||0)-new Date(b.end_date||0));
    const exCnt=mp.filter(p=>pst(p)==='expiring').length;
    const endCnt=mp.filter(p=>pst(p)==='expired').length;
    const warn2=exCnt?`<span style="font-size:10px;background:var(--wl);color:#b06000;padding:2px 6px;border-radius:4px;font-weight:600;margin-left:6px">⚠️ ${exCnt}</span>`:
      endCnt?`<span style="font-size:10px;background:var(--el);color:var(--e);padding:2px 6px;border-radius:4px;font-weight:600;margin-left:6px">❌ ${endCnt}</span>`:'';
    const age=m.dob?Math.floor((Date.now()-new Date(m.dob))/315576e5):null;
    const rows=mp.map(p=>{
      const c=TC[p.type]||TC.other; const s=pst(p); const d=dl(p.end_date);
      let cls='iok',dt=thd(p.end_date);
      if(s==='expired'){cls='iend';dt='หมดอายุแล้ว';}
      else if(d<=30){cls='ic';dt=`🔴 อีก ${d} วัน`;}
      else if(d<=90){cls='iw2';dt=`⚠️ อีก ${d} วัน`;}
      return`<div class="irow" onclick="showD('${p.id}')">
        <div class="iti" style="background:${c.b}">${c.i}</div>
        <div class="iinf">
          <div class="ico2">${p.company||'-'}${p.plan_name?' · '+p.plan_name:''}</div>
          <div class="ipl">${c.l}${p.policy_no?' · '+p.policy_no:''}</div>
        </div>
        <div class="irt">
          <div class="idt ${cls}">${dt}</div>
          ${p.premium?`<div class="ipr">${fm(p.premium)}/ปี</div>`:''}
        </div>
      </div>`;
    }).join('');
    const autoOpen=exCnt>0||endCnt>0||mp.length>0;
    return`<div class="msec">
      <div class="mhd${autoOpen?' open':''}" onclick="togMem('mb-${m.id}',this)">
        <div class="mav" style="background:${m.color}">${ini(m.name)}</div>
        <div class="mhi">
          <div class="mhnm">${m.name}${warn2}</div>
          <div class="mhrl">${m.role||''}${age?' · '+age+' ปี':''}</div>
        </div>
        <div class="mhcnt">${mp.length} กรมธรรม์</div>
        <div class="mchev">▼</div>
      </div>
      <div class="mbd${autoOpen?' open':''}" id="mb-${m.id}">
        ${mp.length?rows:'<div style="text-align:center;padding:10px;font-size:12px;color:var(--n400)">ยังไม่มีกรมธรรม์</div>'}
        <button class="iadd" onclick="openAddForMem('${m.id}')">＋ เพิ่มกรมธรรม์ให้ ${m.name.split(' ')[0]}</button>
      </div>
    </div>`;
  }).join('');
}

function togMem(bid,hd){ const b=document.getElementById(bid); if(!b) return; b.classList.toggle('open'); hd.classList.toggle('open'); }
function openAddForMem(mid){ openAdd(); setTimeout(()=>{ const s=document.getElementById('f-mem'); if(s) s.value=mid; },150); }

function renderDonut(){
  const svg=document.getElementById('dsvg');
  document.getElementById('d-n').textContent=P.length;
  svg.querySelectorAll('.ds').forEach(e=>e.remove());
  const lg=document.getElementById('d-leg');
  if(!P.length){lg.innerHTML='<span style="color:var(--n400);font-size:12px">ยังไม่มีข้อมูล</span>';return;}
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
  const el=document.getElementById('exp-lst');
  const ex=P.filter(p=>{const d=dl(p.end_date);return d>=0&&d<=90;}).sort((a,b)=>dl(a.end_date)-dl(b.end_date)).slice(0,6);
  if(!ex.length){el.innerHTML='<div style="text-align:center;padding:14px;color:var(--n400);font-size:12px">ไม่มีกรมธรรม์ที่ใกล้หมดอายุ 🎉</div>';return;}
  el.innerHTML=ex.map(p=>{
    const m=getMem(p.member),c=TC[p.type]||TC.other,d=dl(p.end_date);
    const cls=d<=30?'ic':d<=60?'iw2':'iok';
    return`<div class="erow" onclick="showD('${p.id}')">
      <div class="eav" style="background:${m.color}">${ini(m.name)}</div>
      <div class="einf"><div class="enm">${m.name} — ${p.company||'?'}</div><div class="etp">${c.i} ${c.l}</div></div>
      <div class="ed ${cls}">${d}ว.<br><span style="font-size:9px;font-weight:400">${thd(p.end_date)}</span></div>
    </div>`;
  }).join('');
}

function checkAlerts(){
  const ar=document.getElementById('al-area'); if(!ar) return;
  const cr=P.filter(p=>{const d=dl(p.end_date);return d>=0&&d<=30;});
  const wa=P.filter(p=>{const d=dl(p.end_date);return d>30&&d<=60;});
  ar.innerHTML=(cr.length?`<div class="alrt a-d">🚨 <div><b>ด่วน!</b> ${cr.length} กรมธรรม์หมดอายุใน 30 วัน</div></div>`:'')
    +(wa.length?`<div class="alrt a-w">⚠️ ${wa.length} กรมธรรม์หมดอายุใน 31–60 วัน</div>`:'');
}

// ── POLICIES ──
function setF(el,f){ filt=f; document.querySelectorAll('.fc').forEach(c=>c.classList.remove('on')); el.classList.add('on'); renderP(); }
function setF2(t){ filt=t; document.querySelectorAll('.fc').forEach(c=>c.classList.toggle('on',c.dataset.f===t)); renderP(); }
function getFiltered(){
  const q=(document.getElementById('q')?.value||'').toLowerCase();
  return P.filter(p=>{
    const m=getMem(p.member);
    if(q&&![p.company,p.policy_no,p.plan_name,m.name].join(' ').toLowerCase().includes(q)) return false;
    if(filt==='all') return true;
    if(filt==='expiring') return pst(p)==='expiring';
    if(filt==='expired')  return pst(p)==='expired';
    return p.type===filt;
  }).sort((a,b)=>new Date(a.end_date||0)-new Date(b.end_date||0));
}
function renderP(){
  const pl=document.getElementById('p-lst'),ep=document.getElementById('p-empty');
  const rows=getFiltered();
  if(!rows.length){pl.innerHTML='';ep.style.display='block';return;}
  ep.style.display='none';
  pl.innerHTML=rows.map(p=>{
    const m=getMem(p.member),c=TC[p.type]||TC.other,s=pst(p),d=dl(p.end_date);
    const sm={active:['sact','คุ้มครองอยู่'],expiring:['sexp','ใกล้หมดอายุ'],expired:['sxd','หมดอายุ']};
    const [dc,sl]=sm[s];
    const bcls={health:'bh',accident:'ba',life:'bl',ci:'bc',other:'bo2'}[p.type]||'bo2';
    const fr=(p.driveFiles||[]).length?`<div style="display:flex;gap:4px;flex-wrap:wrap;margin-top:6px">${(p.driveFiles||[]).map(f=>`<a class="fchip" href="${f.webViewLink||'#'}" target="_blank">📎 ${f.name}</a>`).join('')}</div>`:'';
    return`<div class="pcd">
      <div class="ptop">
        <div class="pav" style="background:${m.color}">${ini(m.name)}</div>
        <div class="pinf"><div class="pnm">${m.name}</div><div class="pco">${p.company||'-'}${p.plan_name?' · '+p.plan_name:''}</div></div>
        <span class="badge ${bcls}">${c.i} ${c.l}</span>
      </div>
      <div class="pbot">
        <span class="sdt ${dc}"></span><span>${sl}</span>
        <span>หมด: ${thd(p.end_date)}${s==='expiring'?` <b style="color:var(--w)">(${d}ว.)</b>`:''}</span>
        ${p.premium?`<span style="color:var(--p);font-weight:600">${fm(p.premium)}/ปี</span>`:''}
      </div>${fr}
      <div class="pact">
        <button class="btn bg bs" onclick="showD('${p.id}')" style="flex:1">👁️ ดู</button>
        <button class="btn bo bs" onclick="editP('${p.id}')">✏️</button>
        <button class="btn bd bs" onclick="delP('${p.id}')">🗑️</button>
      </div>
    </div>`;
  }).join('');
}

// ── POLICY CRUD ──
function openAdd(){
  editId=null; pf=[];
  document.getElementById('pm-t').textContent='➕ เพิ่มกรมธรรม์';
  clearF(); populateMSel(); updUp(); openMod('pm');
}
function clearF(){
  selType=''; document.querySelectorAll('.tc').forEach(c=>c.className='tc');
  ['f-tp','f-co','f-pno','f-pl','f-s','f-e','f-pr','f-su','f-bn','f-nt'].forEach(id=>{ const el=document.getElementById(id); if(el) el.value=''; });
  document.getElementById('f-mem').value=''; document.getElementById('f-fq').value='yearly';
  document.querySelectorAll('.cgrd input').forEach(cb=>cb.checked=false);
  pf=[]; renderFList();
}
function updUp(){
  const w=document.getElementById('up-warn'),u=document.getElementById('up-wrap');
  if(w&&u){w.style.display=tok?'none':'flex';u.style.display=tok?'block':'none';}
}
function selT(t){
  selType=t; document.getElementById('f-tp').value=t;
  document.querySelectorAll('.tc').forEach(c=>{ c.className='tc'; if(c.dataset.t===t) c.classList.add('t-'+t[0]); });
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
  const btn=document.getElementById('sv-btn');
  btn.disabled=true; btn.innerHTML='<div class="spin"></div> กำลังบันทึก...';
  let dfs=editId?(P.find(p=>p.id===editId)?.driveFiles||[]):[];
  if(tok&&pf.length&&driveId){
    try{
      const fid=await getMemFolder(mem);
      for(let i=0;i<pf.length;i++){ if(pf[i].status==='pending'){const r=await upFile(pf[i].file,fid,i);if(r)dfs.push(r);} }
    }catch(e){toast('อัพโหลดบางไฟล์ไม่สำเร็จ','warn');}
  }
  const cov=[...document.querySelectorAll('.cgrd input:checked')].map(cb=>cb.value);
  const pol={
    id:editId||uid(),member:mem,type:ty,company:co,
    policy_no:document.getElementById('f-pno').value.trim(),
    plan_name:document.getElementById('f-pl').value.trim(),
    start_date:s,end_date:e,
    premium:document.getElementById('f-pr').value||0,
    sum_insured:document.getElementById('f-su').value||0,
    payment_freq:document.getElementById('f-fq').value,
    beneficiary:document.getElementById('f-bn').value.trim(),
    coverage:cov,driveFiles:dfs,
    notes:document.getElementById('f-nt').value.trim(),
    created_at:editId?(P.find(p=>p.id===editId)?.created_at||new Date().toISOString()):new Date().toISOString(),
    updated_at:new Date().toISOString(),
  };
  if(editId){const i=P.findIndex(p=>p.id===editId);if(i!==-1)P[i]=pol;}
  else P.push(pol);
  saveCache(); closeMod('pm'); renderAll(); checkAlerts();
  btn.disabled=false; btn.innerHTML='💾 บันทึก';
  toast(editId?'อัพเดทเรียบร้อย ✅':'บันทึกเรียบร้อย ✅','success');
  if(tok&&cfg.sid) push(false);
}
function editP(id){
  const p=P.find(p=>p.id===id); if(!p) return;
  editId=id; pf=[];
  document.getElementById('pm-t').textContent='✏️ แก้ไขกรมธรรม์';
  clearF(); populateMSel(); selT(p.type);
  document.getElementById('f-mem').value=p.member;
  document.getElementById('f-co').value=p.company||'';
  document.getElementById('f-pno').value=p.policy_no||'';
  document.getElementById('f-pl').value=p.plan_name||'';
  document.getElementById('f-s').value=p.start_date||'';
  document.getElementById('f-e').value=p.end_date||'';
  document.getElementById('f-pr').value=p.premium||'';
  document.getElementById('f-su').value=p.sum_insured||'';
  document.getElementById('f-fq').value=p.payment_freq||'yearly';
  document.getElementById('f-bn').value=p.beneficiary||'';
  document.getElementById('f-nt').value=p.notes||'';
  if(p.coverage) p.coverage.forEach(v=>{ const cb=document.querySelector(`.cgrd input[value="${v}"]`); if(cb) cb.checked=true; });
  updUp(); closeMod('dm'); openMod('pm');
}
function delP(id){
  if(!confirm('ต้องการลบกรมธรรม์นี้?')) return;
  P=P.filter(p=>p.id!==id);
  saveCache(); renderAll(); checkAlerts(); closeMod('dm');
  toast('ลบเรียบร้อย','warn');
  if(tok&&cfg.sid) push(false);
}
function showD(id){
  const p=P.find(p=>p.id===id); if(!p) return;
  const m=getMem(p.member),c=TC[p.type]||TC.other,s=pst(p),d=dl(p.end_date);
  const stxt={active:'✅ คุ้มครองอยู่',expiring:'⚠️ ใกล้หมดอายุ',expired:'❌ หมดอายุ'};
  const ftxt={yearly:'รายปี',halfyearly:'ราย 6 เดือน',quarterly:'รายไตรมาส',monthly:'รายเดือน'};
  const ct=(p.coverage||[]).map(cv=>`<div class="ct">${CL[cv]||cv}</div>`).join('');
  const fh=(p.driveFiles||[]).map(f=>`<div style="display:flex;align-items:center;gap:8px;padding:8px 10px;background:var(--W);border:1px solid var(--n200);border-radius:8px;margin-bottom:6px">
    <span style="font-size:18px">${f.name?.endsWith('.pdf')?'📄':'🖼️'}</span>
    <div style="flex:1;min-width:0"><div style="font-size:12px;font-weight:600;overflow:hidden;text-overflow:ellipsis;white-space:nowrap">${f.name}</div>
    <div style="font-size:11px;color:var(--n500)">Google Drive</div></div>
    <a href="${f.webViewLink||'#'}" target="_blank" class="btn bo bx">เปิด</a>
  </div>`).join('');
  const bcls={health:'bh',accident:'ba',life:'bl',ci:'bc',other:'bo2'}[p.type]||'bo2';
  document.getElementById('dm-b').innerHTML=`
  <div class="dth">
    <div class="dtav" style="background:${m.color}">${ini(m.name)}</div>
    <div>
      <div style="font-size:15px;font-weight:700">${m.name}</div>
      <div style="margin-top:4px"><span class="badge ${bcls}">${c.i} ${c.l}</span> <span style="font-size:12px;color:var(--n500)">${p.company||''}</span></div>
    </div>
  </div>
  <div class="dtr">
    <div class="dt2">
      <div class="drw"><div class="dk">เลขกรมธรรม์</div><div class="dv" style="font-family:monospace;font-size:12px">${p.policy_no||'-'}</div></div>
      <div class="drw"><div class="dk">สถานะ</div><div class="dv" style="font-size:12px">${stxt[s]}${s==='expiring'?` (${d}ว.)`:''}</div></div>
    </div>
    <div class="dt2">
      <div class="drw"><div class="dk">วันเริ่ม</div><div class="dv">${thd(p.start_date)}</div></div>
      <div class="drw"><div class="dk">วันหมด</div><div class="dv">${thd(p.end_date)}</div></div>
    </div>
    <div class="dt2">
      <div class="drw"><div class="dk">เบี้ย/ปี</div><div class="dv">${fm(p.premium)}</div></div>
      <div class="drw"><div class="dk">ทุนประกัน</div><div class="dv">${fm(p.sum_insured)}</div></div>
    </div>
    <div class="dt2">
      <div class="drw"><div class="dk">ความถี่ชำระ</div><div class="dv">${ftxt[p.payment_freq]||'-'}</div></div>
      <div class="drw"><div class="dk">ผู้รับผลประโยชน์</div><div class="dv">${p.beneficiary||'-'}</div></div>
    </div>
    ${p.plan_name?`<div class="drw"><div class="dk">ชื่อแผน</div><div class="dv">${p.plan_name}</div></div>`:''}
    ${ct?`<div style="padding:10px 12px;background:var(--n50);border-radius:8px"><div class="dk" style="margin-bottom:6px">ความคุ้มครอง</div><div class="ctg">${ct}</div></div>`:''}
    ${fh?`<div><div class="dk" style="margin-bottom:6px">📎 ไฟล์แนบ</div>${fh}</div>`:''}
    ${p.notes?`<div class="drw"><div class="dk">หมายเหตุ</div><div class="dv" style="font-size:12px;font-weight:400">${p.notes}</div></div>`:''}
  </div>`;
  document.getElementById('dm-ed').onclick=()=>editP(id);
  document.getElementById('dm-dl').onclick=()=>delP(id);
  openMod('dm');
}

// ── MEMBERS ──
function openMemMod(){
  document.getElementById('m-nm').value='';
  document.getElementById('m-rl').value='ตัวเอง';
  document.getElementById('m-db').value='';
  document.getElementById('m-cl').value=PAL[M.length%PAL.length];
  openMod('mm');
}
function saveM(){
  const nm=document.getElementById('m-nm').value.trim();
  if(!nm){toast('กรุณากรอกชื่อ','error');return;}
  M.push({id:uid(),name:nm,role:document.getElementById('m-rl').value,
    dob:document.getElementById('m-db').value,color:document.getElementById('m-cl').value,driveFolder:''});
  saveCache(); populateMSel(); renderMems(); renderDash();
  closeMod('mm'); toast(`เพิ่ม "${nm}" เรียบร้อย`,'success');
  if(tok&&cfg.sid) push(false);
}
function delMem(id){
  if(!confirm('ลบสมาชิกนี้?')) return;
  M=M.filter(m=>m.id!==id);
  saveCache(); populateMSel(); renderMems(); renderDash();
  toast('ลบเรียบร้อย','warn');
  if(tok&&cfg.sid) push(false);
}
function renderMems(){
  const el=document.getElementById('m-lst'); if(!el) return;
  if(!M.length){el.innerHTML='<div class="empty"><div class="ei">👨‍👩‍👧‍👦</div><div class="et">ยังไม่มีสมาชิก</div></div>';return;}
  el.innerHTML=M.map(m=>{
    const mp=P.filter(p=>p.member===m.id);
    const age=m.dob?Math.floor((Date.now()-new Date(m.dob))/315576e5):null;
    const tb=[...new Set(mp.map(p=>p.type))].map(t=>{const c=TC[t]||TC.other;return`<div class="mb" style="background:${c.b};color:${c.c}">${c.i} ${c.l}</div>`;}).join('');
    const drv=m.driveFolder?`<a href="https://drive.google.com/drive/folders/${m.driveFolder}" target="_blank" class="btn bg bx">📁</a>`:'';
    return`<div class="mitm">
      <div class="mav2" style="background:${m.color}">${ini(m.name)}</div>
      <div class="mi">
        <div class="mi-n">${m.name}</div>
        <div class="mi-m">${m.role||''}${age?' · '+age+' ปี':''} · ${mp.length} กรมธรรม์</div>
        <div class="mi-t">${tb||'<span style="font-size:11px;color:var(--n400)">ยังไม่มีกรมธรรม์</span>'}</div>
      </div>
      <div style="display:flex;flex-direction:column;gap:5px">${drv}<button class="btn bd bx" onclick="delMem('${m.id}')">🗑️</button></div>
    </div>`;
  }).join('');
}

// ── SETTINGS ──
function saveCID(){
  const id=document.getElementById('cid-in').value.trim();
  if(!id){toast('กรุณากรอก Client ID','error');return;}
  cfg.cid=id; saveCfg(); toast('บันทึกแล้ว กำลัง Refresh...','success');
  setTimeout(()=>location.reload(),1500);
}
function saveSCfg(){
  cfg.sid=document.getElementById('sid-in').value.trim();
  cfg.sn=document.getElementById('sn-in').value.trim()||'Policies';
  cfg.msn=document.getElementById('msn-in').value.trim()||'Members';
  saveCfg(); updateSyncBar(); updateAuthUI();
  toast('บันทึกการตั้งค่า Sheet เรียบร้อย','success');
  if(tok&&cfg.sid) pull();
}
function doExp(){
  const H=['สมาชิก','ประเภท','บริษัท','เลขกรมธรรม์','ชื่อแผน','วันเริ่ม','วันหมด','เบี้ย','ทุน','ความคุ้มครอง','ผู้รับ','หมายเหตุ'];
  const rows=P.map(p=>[getMem(p.member).name,(TC[p.type]||TC.other).l,p.company,p.policy_no,p.plan_name,p.start_date,p.end_date,p.premium,p.sum_insured,(p.coverage||[]).map(c=>CL[c]||c).join('; '),p.beneficiary,p.notes]);
  const csv=[H,...rows].map(r=>r.map(c=>'"'+String(c||'').replace(/"/g,'""')+'"').join(',')).join('\n');
  const a=document.createElement('a');
  a.href=URL.createObjectURL(new Blob(['\uFEFF'+csv],{type:'text/csv;charset=utf-8;'}));
  a.download=`insurance_${new Date().toISOString().slice(0,10)}.csv`; a.click();
  toast('Export CSV เรียบร้อย','success');
}
function clearLoc(){
  if(!confirm('ล้างข้อมูลในเครื่องนี้?')) return;
  P=[]; M=[{id:uid(),name:'ฉัน (ตัวเอง)',role:'ตัวเอง',color:'#1a73e8',dob:'',driveFolder:''}];
  saveCache(); populateMSel(); renderAll(); toast('ล้างข้อมูลเรียบร้อย','warn');
}

// ── FILES ──
function onPick(e){ addF([...e.target.files]); e.target.value=''; }
function onDrop(e){ e.preventDefault(); addF([...e.dataTransfer.files]); }
function addF(files){
  files.forEach(f=>{
    if(f.size>20*1024*1024){toast(`"${f.name}" ใหญ่เกิน 20MB`,'error');return;}
    if(!pf.find(x=>x.file.name===f.name&&x.file.size===f.size)) pf.push({file:f,status:'pending'});
  }); renderFList();
}
function remF(i){ pf.splice(i,1); renderFList(); }
function renderFList(){
  const el=document.getElementById('f-lst'); if(!el) return;
  el.innerHTML=pf.map((p,i)=>{
    const ic=p.file.name.endsWith('.pdf')?'📄':'🖼️';
    const sz=(p.file.size/1024).toFixed(0)+' KB';
    const st=p.status==='done'?'✅':p.status==='uploading'?'⏳':p.status==='error'?'❌':'📌';
    return`<div class="fitm"><span style="font-size:16px">${ic}</span><div class="fnm">${p.file.name}</div>
      <span style="font-size:11px;color:var(--n500);flex-shrink:0">${sz}</span><span>${st}</span>
      ${p.status==='pending'?`<button onclick="remF(${i})" style="background:none;border:none;cursor:pointer;color:var(--n400);font-size:16px;padding:2px">✕</button>`:''}</div>`;
  }).join('');
}

// ── MODAL ──
function openMod(id){ document.getElementById(id).classList.add('on'); }
function closeMod(id){ document.getElementById(id).classList.remove('on'); }
document.querySelectorAll('.mov').forEach(o=>o.addEventListener('click',e=>{ if(e.target===o) o.classList.remove('on'); }));
document.querySelectorAll('.modal').forEach(modal=>{
  let sy=0;
  modal.addEventListener('touchstart',e=>{ sy=e.touches[0].clientY; },{passive:true});
  modal.addEventListener('touchend',e=>{ if(e.changedTouches[0].clientY-sy>80&&modal.scrollTop===0) modal.closest('.mov').classList.remove('on'); },{passive:true});
});

// ── TOAST ──
function toast(msg,type=''){
  const c=document.getElementById('tw');
  const t=document.createElement('div');
  t.className='toast'+(type?(' t-'+({success:'ok',error:'er',warn:'wn'}[type]||type)):'');
  t.innerHTML=(type==='success'?'✅ ':type==='error'?'❌ ':type==='warn'?'⚠️ ':'ℹ️ ')+msg;
  c.appendChild(t);
  setTimeout(()=>{ t.style.cssText='opacity:0;transform:translateY(6px);transition:all .3s'; setTimeout(()=>t.remove(),300); },3200);
}

// ════════════════════════
//  START
//  boot() ถูกเรียกทันที
//  loading ซ่อนใน 500ms เสมอ (IIFE ด้านบน)
// ════════════════════════
boot();
tryGIS();
</script>
</body>
</html>
