<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<meta name="mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-title" content="INSTALATO">
<title>INSTALATO S.I.C.</title>
<!-- no external lib needed -->
<style>
:root{
  --gold:#B8860B;--dark:#2C1F00;--light-gold:#fdf3e3;
  --green:#1e8449;--red:#c0392b;--blue:#185FA5;
  --gray:#f5f5f5;--border:#e8e8e8;--text:#111;--sub:#888;
}
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent;}
body{font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif;background:#e0e0e0;display:flex;justify-content:center;min-height:100vh;}
.app{width:100%;max-width:430px;min-height:100vh;background:#fff;display:flex;flex-direction:column;position:relative;box-shadow:0 0 40px rgba(0,0,0,.15);}

/* LOGIN */
#pg-login{flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;padding:32px 28px;background:#fff;}
.logo-box{width:84px;height:84px;border-radius:22px;background:var(--dark);display:flex;align-items:center;justify-content:center;margin-bottom:22px;box-shadow:0 8px 24px rgba(44,31,0,.3);}
.logo-box svg{width:46px;height:46px;}
.login-title{font-size:26px;font-weight:800;color:var(--dark);letter-spacing:1px;margin-bottom:4px;}
.login-sub{font-size:13px;color:var(--sub);margin-bottom:36px;}
.lfield{width:100%;margin-bottom:14px;}
.lfield label{display:block;font-size:11px;font-weight:700;color:var(--sub);text-transform:uppercase;letter-spacing:.5px;margin-bottom:6px;}
.lfield input{width:100%;padding:14px 16px;font-size:15px;border-radius:12px;border:1.5px solid var(--border);background:var(--gray);color:var(--text);outline:none;transition:border .2s;}
.lfield input:focus{border-color:var(--gold);background:#fff;}
.btn-login{width:100%;padding:15px;background:var(--dark);color:#fff;border:none;border-radius:12px;font-size:15px;font-weight:700;cursor:pointer;margin-top:6px;transition:opacity .2s;}
.btn-login:active{opacity:.85;}
.login-err{color:var(--red);font-size:12px;text-align:center;margin-top:10px;display:none;}

/* SHELL */
#shell{flex:1;display:none;flex-direction:column;height:100vh;overflow:hidden;}
.topbar{background:var(--gold);padding:12px 16px 10px;display:flex;align-items:center;justify-content:space-between;flex-shrink:0;}
.tb-logo{font-size:13px;font-weight:800;color:#fff;letter-spacing:1px;}
.tb-info{font-size:10px;color:rgba(255,255,255,.75);margin-top:1px;}
.tb-cfg{background:rgba(255,255,255,.2);border:none;color:#fff;font-size:11px;padding:5px 10px;border-radius:20px;cursor:pointer;font-weight:600;display:none;}
.nav{display:flex;background:#fff;border-bottom:1px solid var(--border);flex-shrink:0;overflow-x:auto;}
.nav::-webkit-scrollbar{display:none;}
.ntab{flex:1;min-width:54px;padding:9px 3px 7px;text-align:center;font-size:8px;font-weight:700;color:var(--sub);cursor:pointer;border-bottom:2.5px solid transparent;display:flex;flex-direction:column;align-items:center;gap:2px;transition:color .15s;white-space:nowrap;}
.ntab .ni{font-size:17px;}
.ntab.on{color:var(--gold);border-bottom-color:var(--gold);}
#tabs{flex:1;overflow:hidden;position:relative;}
.tab{display:none;position:absolute;inset:0;overflow-y:auto;}
.tab::-webkit-scrollbar{width:0;}
.tab.on{display:block;}

/* FORMS */
.pad{padding:14px 16px;display:flex;flex-direction:column;gap:12px;}
.fl{font-size:10px;font-weight:700;color:var(--sub);text-transform:uppercase;letter-spacing:.5px;margin-bottom:5px;}
.inp,.sel{width:100%;padding:12px 13px;font-size:14px;border-radius:12px;border:1.5px solid var(--border);background:var(--gray);color:var(--text);appearance:none;outline:none;transition:border .2s;}
.inp:focus,.sel:focus{border-color:var(--gold);background:#fff;}
.row2{display:grid;grid-template-columns:1fr 1fr;gap:10px;}
.row3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px;}
.btn-pri{width:100%;padding:14px;background:var(--dark);color:#fff;border:none;border-radius:12px;font-size:14px;font-weight:700;cursor:pointer;}
.btn-sec{width:100%;padding:12px;background:transparent;color:var(--gold);border:2px solid var(--gold);border-radius:12px;font-size:13px;font-weight:700;cursor:pointer;}
.btn-gold{width:100%;padding:14px;background:var(--gold);color:#fff;border:none;border-radius:12px;font-size:14px;font-weight:700;cursor:pointer;}
.info-box{background:var(--light-gold);border-radius:10px;padding:10px 12px;font-size:11px;color:#8B6914;line-height:1.6;border-left:3px solid var(--gold);}
.divider{height:1px;background:var(--border);}

/* HERO */
.hero{padding:14px 16px 16px;color:#fff;}
.hero p{font-size:11px;opacity:.82;margin-bottom:2px;}
.hero h2{font-size:19px;font-weight:700;}

/* CARDS */
.card{background:var(--gray);border-radius:14px;padding:13px;}
.card-title{font-size:13px;font-weight:700;color:var(--text);margin-bottom:10px;}
.stat-grid{display:grid;grid-template-columns:1fr 1fr;gap:8px;}
.stat{background:#fff;border-radius:10px;padding:11px;text-align:center;}
.stat .sv{font-size:18px;font-weight:700;color:var(--gold);}
.stat .sl{font-size:10px;color:var(--sub);margin-top:2px;}
.stat3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px;}

/* META */
.meta-card{background:var(--gray);border-radius:14px;padding:13px;}
.meta-top{display:flex;justify-content:space-between;align-items:baseline;margin-bottom:7px;}
.meta-v{font-size:13px;font-weight:700;color:var(--gold);}
.meta-p{font-size:12px;color:var(--sub);}
.prog{height:7px;background:#ddd;border-radius:4px;overflow:hidden;margin-bottom:7px;}
.prog-f{height:100%;border-radius:4px;background:var(--gold);transition:width .4s;}
.weeks-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:6px;margin-bottom:7px;}
.wk{background:#fff;border-radius:6px;padding:5px 3px;text-align:center;}
.wk.done{background:rgba(184,134,11,.15);}
.wk.cur{border:1px solid var(--gold);}
.wk .wl{font-size:8px;color:var(--sub);}
.wk .wv{font-size:10px;font-weight:700;}
.wk.done .wv{color:var(--gold);}
.meta-msg{font-size:11px;padding:7px 10px;border-radius:8px;}
.msg-ok{background:rgba(30,132,73,.1);color:var(--green);}
.msg-warn{background:rgba(184,134,11,.1);color:#854F0B;}
.msg-bad{background:rgba(192,57,43,.1);color:var(--red);}
.meta-inp-row{display:flex;gap:8px;margin-top:9px;}
.meta-inp-row .inp{flex:1;margin-bottom:0;}
.btn-def{padding:11px 14px;background:var(--gold);color:#fff;border:none;border-radius:10px;font-size:13px;cursor:pointer;white-space:nowrap;font-weight:700;}

/* BONUS */
.bonus-item{display:flex;align-items:center;gap:10px;padding:11px 12px;background:var(--gray);border-radius:12px;cursor:pointer;border:1.5px solid transparent;transition:all .15s;}
.bonus-item.on{border-color:var(--gold);background:rgba(184,134,11,.06);}
.bchk{width:22px;height:22px;border-radius:50%;border:1.5px solid #ddd;display:flex;align-items:center;justify-content:center;flex-shrink:0;font-size:12px;}
.bonus-item.on .bchk{background:var(--gold);border-color:var(--gold);color:#fff;}
.bname{font-size:13px;font-weight:600;flex:1;color:var(--text);}
.bpct{font-size:12px;font-weight:700;color:var(--gold);}

/* TOTAL */
.total-card{background:var(--gray);border-radius:14px;padding:13px 15px;}
.t-row{display:flex;justify-content:space-between;font-size:12px;margin-bottom:5px;}
.tl{color:var(--sub);}
.tv{font-weight:600;color:var(--text);}
.t-div{height:1px;background:var(--border);margin:8px 0;}
.t-final{display:flex;justify-content:space-between;align-items:baseline;}
.tfv{font-size:24px;font-weight:700;color:var(--gold);}

/* EXTRAS */
.extra-line{display:grid;grid-template-columns:1fr 80px 70px 32px;gap:6px;align-items:center;margin-bottom:7px;}
.el-inp{width:100%;padding:10px 9px;font-size:13px;border-radius:10px;border:1.5px solid var(--border);background:var(--gray);color:var(--text);outline:none;}
.el-inp:focus{border-color:var(--gold);}
.btn-rem{width:32px;height:32px;border-radius:50%;border:1px solid var(--border);background:transparent;color:var(--sub);cursor:pointer;font-size:16px;display:flex;align-items:center;justify-content:center;}
.btn-add-line{width:100%;padding:10px;border-radius:12px;border:1.5px dashed var(--border);background:transparent;color:var(--sub);font-size:12px;cursor:pointer;margin-top:4px;}

/* HIST */
.hist-item{background:var(--gray);border-radius:12px;padding:12px;display:flex;gap:10px;margin-bottom:8px;}
.hi-ico{width:34px;height:34px;border-radius:50%;background:rgba(184,134,11,.1);display:flex;align-items:center;justify-content:center;flex-shrink:0;font-size:16px;}
.hi-body{flex:1;}
.hi-t{font-size:13px;font-weight:600;}
.hi-s{font-size:11px;color:var(--sub);margin-top:2px;}
.hi-right{text-align:right;}
.hi-v{font-size:13px;font-weight:700;color:var(--gold);}
.hi-d{font-size:10px;color:var(--sub);margin-top:2px;}
.chip{font-size:9px;padding:2px 7px;border-radius:20px;font-weight:700;display:inline-block;}
.chip-ap{background:rgba(30,132,73,.12);color:var(--green);}
.chip-in{background:rgba(184,134,11,.12);color:#854F0B;}
.chip-rp{background:rgba(192,57,43,.1);color:var(--red);}
.chip-g{background:rgba(184,134,11,.12);color:var(--gold);}
.chip-u{background:rgba(192,57,43,.1);color:var(--red);}
.chip-i{background:rgba(24,95,165,.1);color:var(--blue);}

/* RANK */
.rank-item{display:flex;align-items:center;gap:10px;padding:11px 12px;background:var(--gray);border-radius:12px;margin-bottom:8px;}
.rnum{width:26px;height:26px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:700;color:#fff;flex-shrink:0;}
.rinfo{flex:1;}
.rname{font-size:13px;font-weight:600;}
.rmeta{font-size:10px;color:var(--sub);margin-top:1px;}
.rval .rv{font-size:13px;font-weight:700;color:var(--gold);}
.rval .rs{font-size:10px;color:var(--sub);}

/* CONF */
.status-row{display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px;}
.btn-st{padding:13px 6px;border-radius:12px;border:2px solid;font-size:11px;font-weight:700;cursor:pointer;display:flex;flex-direction:column;align-items:center;gap:4px;transition:all .15s;}
.btn-st .si{font-size:20px;}
.btn-ap{background:#fff;border-color:var(--green);color:var(--green);}
.btn-ap.sel{background:var(--green);color:#fff;}
.btn-in{background:#fff;border-color:#BA7517;color:#854F0B;}
.btn-in.sel{background:#BA7517;color:#fff;}
.btn-rp{background:#fff;border-color:var(--red);color:var(--red);}
.btn-rp.sel{background:var(--red);color:#fff;}
.chk-item{background:var(--gray);border-radius:10px;padding:10px 12px;margin-bottom:6px;}
.chk-name{font-size:12px;font-weight:600;margin-bottom:7px;}
.chk-btns{display:flex;gap:7px;}
.cbtn{flex:1;padding:7px;border-radius:8px;border:1.5px solid var(--border);background:#fff;font-size:11px;font-weight:700;cursor:pointer;transition:all .15s;}
.cbtn.ap{border-color:var(--green);color:var(--green);}
.cbtn.ap.on{background:var(--green);color:#fff;}
.cbtn.rp{border-color:var(--red);color:var(--red);}
.cbtn.rp.on{background:var(--red);color:#fff;}

/* MATERIAIS */
.mat-line{display:grid;grid-template-columns:1fr 90px 32px;gap:7px;align-items:center;margin-bottom:7px;}

/* DESPESAS */
.cat-grid{display:grid;grid-template-columns:1fr 1fr;gap:8px;}
.cat-btn{padding:11px 8px;border-radius:12px;border:1.5px solid var(--border);background:var(--gray);cursor:pointer;display:flex;flex-direction:column;align-items:center;gap:5px;font-size:11px;font-weight:700;color:var(--sub);transition:all .15s;}
.cat-btn .ci{font-size:20px;}
.cat-btn.on{border-color:var(--gold);background:rgba(184,134,11,.08);color:var(--gold);}

/* DASH BARS */
.bar-wrap{display:flex;flex-direction:column;gap:7px;}
.bar-row{display:flex;align-items:center;gap:8px;}
.bar-lbl{font-size:11px;color:var(--sub);width:78px;flex-shrink:0;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.bar-track{flex:1;height:8px;background:#e0e0e0;border-radius:4px;overflow:hidden;}
.bar-fill{height:100%;border-radius:4px;background:var(--gold);}
.bar-val{font-size:11px;font-weight:700;min-width:44px;text-align:right;color:var(--text);}

/* AVISO CARD */
.av-card{background:var(--gray);border-radius:12px;padding:13px;margin-bottom:8px;border-left:3px solid var(--gold);}
.av-card.urg{border-left-color:var(--red);}
.av-card.inf{border-left-color:var(--blue);}
.av-header{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:4px;}
.av-title{font-size:13px;font-weight:700;}
.av-msg{font-size:12px;color:#555;margin:5px 0;line-height:1.5;}
.av-footer{display:flex;justify-content:space-between;align-items:center;}
.av-time{font-size:10px;color:var(--sub);}
.av-btns{display:flex;gap:8px;}
.av-btn{background:transparent;border:none;cursor:pointer;font-size:11px;font-weight:700;}
.av-btn.e{color:var(--gold);}
.av-btn.d{color:var(--red);}

/* FILTERS */
.filter-row{display:flex;gap:8px;margin-bottom:4px;}
.filter-row select{flex:1;padding:9px 10px;font-size:12px;border-radius:10px;border:1px solid var(--border);background:var(--gray);color:var(--text);appearance:none;}

/* CFG MENU */
.sec-lbl{padding:10px 16px 3px;font-size:9px;font-weight:700;color:var(--sub);text-transform:uppercase;letter-spacing:.7px;}
.cfg-item{display:flex;align-items:center;gap:12px;padding:13px 16px;cursor:pointer;border-bottom:1px solid var(--border);}
.cfg-item:active{background:var(--gray);}
.ci-ico{width:38px;height:38px;border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:18px;flex-shrink:0;}
.ci-nm{font-size:13px;font-weight:600;}
.ci-ds{font-size:11px;color:var(--sub);margin-top:1px;}

/* SUB PAGES */
.sub-pg{display:none;position:fixed;inset:0;background:#fff;z-index:50;flex-direction:column;max-width:430px;margin:0 auto;}
.sub-pg.on{display:flex;}
.sub-hdr{background:var(--dark);padding:10px 14px 12px;display:flex;align-items:center;gap:12px;flex-shrink:0;}
.btn-bk{width:34px;height:34px;min-width:34px;border-radius:50%;background:rgba(255,255,255,.2);border:1.5px solid rgba(255,255,255,.35);cursor:pointer;font-size:18px;color:#fff;display:flex;align-items:center;justify-content:center;flex-shrink:0;}
.sub-t{font-size:15px;font-weight:700;color:#fff;}
.sub-s{font-size:10px;color:rgba(255,255,255,.6);margin-top:2px;}
.sub-body{flex:1;overflow-y:auto;}
.sub-body::-webkit-scrollbar{display:none;}

/* TOGGLE */
.tog-row{display:flex;align-items:center;justify-content:space-between;padding:12px 14px;background:var(--gray);border-radius:12px;}
.tog-nm{font-size:13px;font-weight:600;}
.tog-sb{font-size:11px;color:var(--sub);margin-top:1px;}
.tog{width:44px;height:26px;border-radius:13px;background:#ddd;position:relative;cursor:pointer;flex-shrink:0;transition:background .2s;}
.tog.on{background:var(--gold);}
.tok{width:20px;height:20px;background:#fff;border-radius:50%;position:absolute;top:3px;left:3px;transition:left .2s;box-shadow:0 1px 4px rgba(0,0,0,.2);}
.tog.on .tok{left:21px;}

/* USER/OBRA CARDS */
.u-card,.o-card{background:var(--gray);border-radius:14px;padding:12px;margin-bottom:10px;}
.u-av{width:36px;height:36px;border-radius:50%;display:flex;align-items:center;justify-content:center;color:#fff;font-size:12px;font-weight:700;flex-shrink:0;}
.tipo-row{display:flex;gap:6px;margin-bottom:9px;}
.tb{flex:1;padding:7px 3px;border-radius:8px;border:1.5px solid var(--border);background:transparent;font-size:10px;font-weight:700;cursor:pointer;color:var(--sub);text-align:center;transition:all .15s;}
.tb.func{background:var(--blue);border-color:var(--blue);color:#fff;}
.tb.lider{background:var(--gold);border-color:var(--gold);color:#fff;}
.tb.adm{background:var(--dark);border-color:var(--dark);color:#fff;}
.ub{flex:1;padding:7px;border-radius:8px;font-size:11px;font-weight:700;cursor:pointer;border:1px solid;background:transparent;display:flex;align-items:center;justify-content:center;gap:3px;}
.ub.tog2{border-color:var(--border);color:var(--sub);}
.ub.del{border-color:rgba(192,57,43,.3);color:var(--red);}
.ub.edit{border-color:var(--gold);color:var(--gold);}

/* MODAL */
.modal-bg{display:none;position:fixed;inset:0;background:rgba(0,0,0,.5);align-items:flex-end;justify-content:center;z-index:100;}
.modal-bg.show{display:flex;}
.modal-sheet{background:#fff;border-radius:20px 20px 0 0;width:100%;max-width:430px;padding:18px 16px 32px;max-height:88vh;overflow-y:auto;}
.modal-sheet::-webkit-scrollbar{display:none;}
.mhdr{display:flex;justify-content:space-between;align-items:center;margin-bottom:14px;}
.mhdr-t{font-size:15px;font-weight:700;}
.mhdr-x{width:28px;height:28px;border-radius:50%;background:var(--gray);border:none;cursor:pointer;font-size:15px;display:flex;align-items:center;justify-content:center;}
.mf{display:flex;flex-direction:column;gap:11px;}
.macts{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-top:14px;}
.bmc{padding:12px;border-radius:10px;border:1px solid var(--border);background:transparent;color:var(--sub);font-size:13px;font-weight:700;cursor:pointer;}
.bmok{padding:12px;border-radius:10px;background:var(--dark);color:#fff;border:none;font-size:13px;font-weight:700;cursor:pointer;}

/* TOAST */
.toast{display:none;position:fixed;bottom:28px;left:50%;transform:translateX(-50%);background:#222;color:#fff;padding:11px 20px;border-radius:22px;font-size:13px;font-weight:500;z-index:300;white-space:nowrap;box-shadow:0 4px 16px rgba(0,0,0,.25);max-width:90vw;}
.toast.show{display:block;}

/* EMPTY */
.empty{text-align:center;padding:40px 20px;color:var(--sub);}
.empty .ei{font-size:36px;margin-bottom:8px;}
.empty p{font-size:13px;}

/* PROG BAR */
.prog-lbl{display:flex;justify-content:space-between;font-size:10px;color:var(--sub);margin-bottom:3px;}
.prog-track{height:6px;background:#e0e0e0;border-radius:3px;overflow:hidden;}
.prog-track-f{height:100%;border-radius:3px;background:var(--gold);}
</style>
</head>
<body>
<div class="app" id="app">

<!-- ══ LOGIN ══ -->
<div id="pg-login">
  <div class="logo-box">
    <svg viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M6 20L24 6L42 20V44H6V20Z" fill="#B8860B"/>
      <path d="M6 20L24 6L42 20" stroke="#D4A017" stroke-width="2.5" stroke-linejoin="round"/>
      <rect x="18" y="28" width="12" height="16" rx="2" fill="#2C1F00"/>
    </svg>
  </div>
  <div class="login-title">INSTALATO S.I.C.</div>
  <div class="login-sub">Sistema Integrado de Controles</div>
  <div class="lfield"><label>Usuário</label><input type="text" id="l-user" placeholder="Seu apelido" autocomplete="off" autocapitalize="off"></div>
  <div class="lfield"><label>Senha</label><input type="password" id="l-pass" placeholder="Sua senha"></div>
  <div style="display:flex;align-items:center;gap:10px;margin-bottom:6px;margin-top:-4px;">
    <input type="checkbox" id="l-remember" style="width:18px;height:18px;accent-color:var(--gold);cursor:pointer;">
    <label for="l-remember" style="font-size:13px;color:var(--sub);cursor:pointer;user-select:none;">Lembrar usuário e senha</label>
  </div>
  <button class="btn-login" id="btn-login">Entrar</button>
  <div class="login-err" id="login-err">❌ Usuário ou senha incorretos</div>
  <div style="margin-top:28px;font-size:11px;color:var(--sub);text-align:center;">© 2025 INSTALATO S.I.C. · Todos os direitos reservados</div>
</div>

<!-- ══ APP SHELL ══ -->
<div id="shell">
  <div class="topbar">
    <div>
      <div class="tb-logo" id="tb-logo">INSTALATO S.I.C.</div>
      <div class="tb-info" id="tb-info">...</div>
    </div>
    <button class="tb-cfg" id="btn-cfg" onclick="openSub('cfg')">⚙️ Config</button>
  </div>
  <div class="nav" id="nav"></div>
  <div id="tabs"></div>
</div>

<!-- ══ SUB: CONFIGURAÇÕES ══ -->
<div class="sub-pg" id="sub-cfg">
  <div class="sub-hdr">
    <button class="btn-bk" onclick="closeSub('cfg')">←</button>
    <div><div class="sub-t">Configurações</div><div class="sub-s">Acesso Admin</div></div>
  </div>
  <div class="sub-body">
    <div class="sec-lbl">Empresa</div>
    <div class="cfg-item" onclick="openSub('empresa')"><div class="ci-ico" style="background:#f5efe0;">🏢</div><div><div class="ci-nm">Dados da empresa</div><div class="ci-ds">Nome, informações gerais</div></div><span style="color:#ccc;font-size:20px;margin-left:auto;">›</span></div>
    <div class="cfg-item" onclick="openSub('obras')"><div class="ci-ico" style="background:#e8f0fb;">🏗️</div><div><div class="ci-nm">Obras</div><div class="ci-ds">Cadastrar e gerenciar obras</div></div><span style="color:#ccc;font-size:20px;margin-left:auto;">›</span></div>
    <div class="sec-lbl">Equipe</div>
    <div class="cfg-item" onclick="openSub('funcs')"><div class="ci-ico" style="background:#fdf3e3;">👥</div><div><div class="ci-nm">Funcionários</div><div class="ci-ds">Perfis, tipos e acessos</div></div><span style="color:#ccc;font-size:20px;margin-left:auto;">›</span></div>
    <div class="cfg-item" onclick="openSub('novofunc')"><div class="ci-ico" style="background:#eafaf1;">➕</div><div><div class="ci-nm">Cadastrar funcionário</div><div class="ci-ds">Adicionar novo membro</div></div><span style="color:#ccc;font-size:20px;margin-left:auto;">›</span></div>
    <div class="sec-lbl">Conta</div>
    <div class="cfg-item" onclick="logout()" style="border-bottom:none;"><div class="ci-ico" style="background:#fdf0f0;">🚪</div><div><div class="ci-nm" style="color:var(--red);">Sair do sistema</div><div class="ci-ds">Encerrar sessão</div></div></div>
  </div>
</div>

<!-- SUB: EMPRESA -->
<div class="sub-pg" id="sub-empresa">
  <div class="sub-hdr"><button class="btn-bk" onclick="closeSub('empresa')">←</button><div><div class="sub-t">Dados da Empresa</div></div></div>
  <div class="sub-body"><div class="pad">
    <div><div class="fl">Nome</div><input class="inp" id="emp-nome" type="text" placeholder="INSTALATO S.I.C."></div>
    <div><div class="fl">Slogan</div><input class="inp" id="emp-slogan" type="text"></div>
    <div class="row2">
      <div><div class="fl">CNPJ</div><input class="inp" id="emp-cnpj" type="text"></div>
      <div><div class="fl">Telefone</div><input class="inp" id="emp-tel" type="tel"></div>
    </div>
    <div><div class="fl">Cidade / Estado</div><input class="inp" id="emp-cidade" type="text"></div>
    <button class="btn-pri" onclick="salvarEmpresa()">💾 Salvar</button>
  </div></div>
</div>

<!-- SUB: OBRAS -->
<div class="sub-pg" id="sub-obras">
  <div class="sub-hdr"><button class="btn-bk" onclick="closeSub('obras')">←</button><div><div class="sub-t">Obras</div></div></div>
  <div class="sub-body"><div class="pad">
    <button class="btn-sec" onclick="showModal('obra',null)">＋ Nova obra</button>
    <div id="obras-list"></div>
  </div></div>
</div>

<!-- SUB: FUNCIONÁRIOS -->
<div class="sub-pg" id="sub-funcs">
  <div class="sub-hdr"><button class="btn-bk" onclick="closeSub('funcs')">←</button><div><div class="sub-t">Funcionários</div></div></div>
  <div class="sub-body"><div class="pad">
    <input class="inp" type="text" id="busca-f" placeholder="🔍 Buscar..." oninput="renderFuncs()">
    <div id="funcs-list"></div>
  </div></div>
</div>

<!-- SUB: NOVO FUNC -->
<div class="sub-pg" id="sub-novofunc">
  <div class="sub-hdr"><button class="btn-bk" onclick="closeSub('novofunc')">←</button><div><div class="sub-t">Novo Funcionário</div></div></div>
  <div class="sub-body"><div class="pad">
    <div class="row2">
      <div><div class="fl">Nome</div><input class="inp" id="nf-nome" type="text" placeholder="Nome completo"></div>
      <div><div class="fl">Apelido</div><input class="inp" id="nf-apelido" type="text" placeholder="Ex: Luiz"></div>
    </div>
    <div><div class="fl">WhatsApp</div><input class="inp" id="nf-tel" type="tel" placeholder="(47) 99999-9999"></div>
    <div><div class="fl">Tipo de usuário</div>
      <div class="row3">
        <button class="tb func" id="nt-func" onclick="selNT('func')">👷 Func.</button>
        <button class="tb" id="nt-lider" onclick="selNT('lider')">👑 Líder</button>
        <button class="tb" id="nt-admin" onclick="selNT('admin')">🛡 Admin</button>
      </div>
    </div>
    <div><div class="fl">Obra vinculada</div><select class="sel" id="nf-obra"><option value="">Selecione</option></select></div>
    <div class="row2">
      <div><div class="fl">R$/m²</div><input class="inp" id="nf-rate" type="number" placeholder="35"></div>
      <div><div class="fl">Meta R$</div><input class="inp" id="nf-meta" type="number" placeholder="12000"></div>
    </div>
    <div><div class="fl">Senha</div><input class="inp" id="nf-senha" type="password" placeholder="Mínimo 6 caracteres"></div>
    <div class="info-box">ℹ️ O tipo define quais abas o funcionário visualiza.</div>
    <button class="btn-pri" onclick="cadastrarFunc()">✅ Cadastrar funcionário</button>
  </div></div>
</div>

<!-- MODAL OBRA -->
<div class="modal-bg" id="modal-obra">
  <div class="modal-sheet">
    <div class="mhdr"><span class="mhdr-t" id="mo-t">Nova obra</span><button class="mhdr-x" onclick="closeModal('obra')">✕</button></div>
    <div class="mf">
      <div><div class="fl">Nome</div><input class="inp" id="mo-nome" type="text" placeholder="Ex: Fischer Dreams"></div>
      <div><div class="fl">Tipo</div><input class="inp" id="mo-tipo" type="text" placeholder="Ex: Residencial, Alto padrão..."></div>
      <div><div class="fl">Cliente</div><input class="inp" id="mo-cliente" type="text"></div>
      <div><div class="fl">Cidade</div><input class="inp" id="mo-cidade" type="text"></div>
      <div class="row2">
        <div><div class="fl">Andares</div><input class="inp" id="mo-andares" type="number"></div>
        <div><div class="fl">Contrato R$</div><input class="inp" id="mo-contrato" type="number"></div>
      </div>
      <div class="row2">
        <div><div class="fl">Início</div><input class="inp" id="mo-inicio" type="date"></div>
        <div><div class="fl">Entrega</div><input class="inp" id="mo-entrega" type="date"></div>
      </div>
      <div><div class="fl">Status</div>
        <select class="sel" id="mo-status">
          <option value="ativa">Em andamento</option>
          <option value="concluida">Concluída</option>
          <option value="pausada">Pausada</option>
        </select>
      </div>
    </div>
    <div class="macts"><button class="bmc" onclick="closeModal('obra')">Cancelar</button><button class="bmok" onclick="salvarObra()">✓ Salvar</button></div>
  </div>
</div>

<!-- MODAL AVISO -->
<div class="modal-bg" id="modal-aviso">
  <div class="modal-sheet">
    <div class="mhdr"><span class="mhdr-t">Publicar aviso</span><button class="mhdr-x" onclick="closeModal('aviso')">✕</button></div>
    <div class="mf">
      <div><div class="fl">Título</div><input class="inp" id="av-titulo" type="text" placeholder="Título do aviso"></div>
      <div><div class="fl">Mensagem</div><textarea class="inp" id="av-msg" rows="3" style="resize:none;" placeholder="Mensagem para a equipe..."></textarea></div>
      <div><div class="fl">Tipo</div>
        <select class="sel" id="av-tipo">
          <option value="geral">Geral</option>
          <option value="urgente">Urgente</option>
          <option value="informativo">Informativo</option>
        </select>
      </div>
    </div>
    <div class="macts"><button class="bmc" onclick="closeModal('aviso')">Cancelar</button><button class="bmok" onclick="salvarAviso()">📢 Publicar</button></div>
  </div>
</div>

<!-- MODAL EDITAR FUNCIONÁRIO -->
<div class="modal-bg" id="modal-editfunc">
  <div class="modal-sheet">
    <div class="mhdr"><span class="mhdr-t">Editar funcionário</span><button class="mhdr-x" onclick="closeModal('editfunc')">✕</button></div>
    <div class="mf">
      <div class="row2">
        <div><div class="fl">Nome completo</div><input class="inp" id="ef-nome" type="text"></div>
        <div><div class="fl">Apelido</div><input class="inp" id="ef-apelido" type="text"></div>
      </div>
      <div><div class="fl">WhatsApp</div><input class="inp" id="ef-tel" type="tel" placeholder="(47) 99999-9999"></div>
      <div><div class="fl">Obra vinculada</div><select class="sel" id="ef-obra"><option value="">Sem obra</option></select></div>
      <div class="row2">
        <div><div class="fl">R$/m²</div><input class="inp" id="ef-rate" type="number"></div>
        <div><div class="fl">Meta R$</div><input class="inp" id="ef-meta" type="number"></div>
      </div>
      <div><div class="fl">Nova senha <span style="font-size:10px;color:var(--sub);font-weight:400;">(deixe em branco para manter)</span></div><input class="inp" id="ef-senha" type="password" placeholder="Nova senha (opcional)"></div>
    </div>
    <div class="macts">
      <button class="bmc" onclick="closeModal('editfunc')">Cancelar</button>
      <button class="bmok" onclick="salvarEditFunc()">✓ Salvar</button>
    </div>
  </div>
</div>

<div class="toast" id="toast"></div>

<script>
const SURL='https://qfqbbfcqkzzezzmopssv.supabase.co';
const SKEY='eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InFmcWJiZmNxa3p6ZXp6bW9wc3N2Iiwicm9sZSI6ImFub24iLCJpYXQiOjE3Nzg2NDMwMDUsImV4cCI6MjA5NDIxOTAwNX0.EiSpKp_ywz4JTxMC18EK_Dv0MWFNpx9Db5jFVQwSdJA';

const H={'apikey':SKEY,'Authorization':'Bearer '+SKEY,'Content-Type':'application/json','Prefer':'return=representation'};

const db={
  from:function(t){
    return {
      _t:t,_filters:[],_ord:null,
      select:function(){return this;},
      eq:function(k,v){this._filters.push({k,v,op:'eq'});return this;},
      ilike:function(k,v){this._filters.push({k,v,op:'ilike'});return this;},
      order:function(c,o){this._ord={c,asc:(o&&o.ascending)!==false};return this;},
      limit:function(n){this._lim=n;return this;},
      _buildUrl:function(){
        let url=SURL+'/rest/v1/'+this._t+'?select=*';
        this._filters.forEach(f=>{
          if(f.op==='eq')url+='&'+f.k+'=eq.'+encodeURIComponent(f.v);
          if(f.op==='ilike')url+='&'+f.k+'=ilike.'+encodeURIComponent('*'+f.v+'*');
        });
        if(this._ord)url+='&order='+this._ord.c+(this._ord.asc?'.asc':'.desc');
        if(this._lim)url+='&limit='+this._lim;
        return url;
      },
      then:async function(res){
        try{
          const r=await fetch(this._buildUrl(),{headers:H});
          const d=await r.json();
          if(!r.ok)return res({data:null,error:{message:d.message||d.hint||JSON.stringify(d)}});
          return res({data:d,error:null});
        }catch(e){return res({data:null,error:{message:e.message}});}
      },
      insert:function(obj){
        const self=this;
        return {
          select:function(){return this;},
          then:async function(res){
            try{
              const r=await fetch(SURL+'/rest/v1/'+self._t,{method:'POST',headers:H,body:JSON.stringify(obj)});
              const d=await r.json();
              if(!r.ok)return res({data:null,error:{message:d.message||d.hint||JSON.stringify(d)}});
              return res({data:Array.isArray(d)?d:[d],error:null});
            }catch(e){return res({data:null,error:{message:e.message}});}
          }
        };
      },
      update:function(obj){
        const self=this;
        return {
          eq:function(k,v){self._filters.push({k,v,op:'eq'});return this;},
          then:async function(res){
            try{
              let url=SURL+'/rest/v1/'+self._t+'?';
              self._filters.forEach(f=>{if(f.op==='eq')url+=f.k+'=eq.'+encodeURIComponent(f.v)+'&';});
              const r=await fetch(url,{method:'PATCH',headers:H,body:JSON.stringify(obj)});
              if(!r.ok){const d=await r.json();return res({data:null,error:{message:d.message||JSON.stringify(d)}});}
              return res({data:null,error:null});
            }catch(e){return res({data:null,error:{message:e.message}});}
          }
        };
      },
      delete:function(){
        const self=this;
        return {
          eq:function(k,v){self._filters.push({k,v,op:'eq'});return this;},
          then:async function(res){
            try{
              let url=SURL+'/rest/v1/'+self._t+'?';
              self._filters.forEach(f=>{if(f.op==='eq')url+=f.k+'=eq.'+encodeURIComponent(f.v)+'&';});
              const r=await fetch(url,{method:'DELETE',headers:{...H,'Prefer':''}});
              if(!r.ok){const d=await r.json();return res({data:null,error:{message:d.message||JSON.stringify(d)}});}
              return res({data:null,error:null});
            }catch(e){return res({data:null,error:{message:e.message}});}
          }
        };
      }
    };
  }
};

// STATE
let U=null,obras=[],users=[],lancs=[],confs=[],mats=[],desps=[],avs=[],ocorrs=[];

// CITAÇÕES BÍBLICAS
const VERSES=[
  {t:'"Tudo posso naquele que me fortalece."',r:'Filipenses 4:13'},
  {t:'"Seja forte e corajoso! Não se apavore nem desanime, pois o Senhor seu Deus estará com você por onde quer que você andar."',r:'Josué 1:9'},
  {t:'"Porque sou eu que conheço os planos que tenho para vocês, planos de fazê-los prosperar e não de causar dano, planos de dar a vocês esperança e um futuro."',r:'Jeremias 29:11'},
  {t:'"Não canseis de fazer o bem, porque a seu tempo ceifaremos, se não desanimarmos."',r:'Gálatas 6:9'},
  {t:'"Aquele que começou boa obra em vocês a completará até o dia de Cristo Jesus."',r:'Filipenses 1:6'},
  {t:'"Todas as coisas cooperam para o bem daqueles que amam a Deus."',r:'Romanos 8:28'},
  {t:'"Não me envergonho, porque sei em quem tenho crido, e estou convicto de que ele é poderoso."',r:'2 Timóteo 1:12'},
  {t:'"Sê fiel até à morte, e dar-te-ei a coroa da vida."',r:'Apocalipse 2:10'},
  {t:'"Deus nos deu não um espírito de timidez, mas de poder, de amor e de equilíbrio."',r:'2 Timóteo 1:7'},
  {t:'"Com paciência corramos a carreira que nos está proposta, olhando para Jesus."',r:'Hebreus 12:1-2'},
  {t:'"O Senhor é o meu pastor e nada me faltará."',r:'Salmos 23:1'},
  {t:'"Bem-aventurado o homem que persevera na provação, porque depois de aprovado receberá a coroa da vida."',r:'Tiago 1:12'},
  {t:'"Posso enfrentar qualquer situação por meio de Cristo que me fortalece."',r:'Filipenses 4:13'},
  {t:'"Se Deus é por nós, quem será contra nós?"',r:'Romanos 8:31'},
  {t:'"Nenhuma arma forjada contra ti prosperará."',r:'Isaías 54:17'},
  {t:'"Não há nada impossível para quem crê."',r:'Marcos 9:23'},
  {t:'"O Senhor abençoará o trabalho das suas mãos."',r:'Deuteronômio 28:12'},
  {t:'"A alegria do Senhor é a vossa força."',r:'Neemias 8:10'},
  {t:'"Levanta-te, resplandece, porque vem a tua luz, e a glória do Senhor nasce sobre ti!"',r:'Isaías 60:1'},
  {t:'"Não te deixes vencer pelo mal, mas vence o mal com o bem."',r:'Romanos 12:21'},
  {t:'"Buscai primeiro o reino de Deus e a sua justiça, e todas essas coisas vos serão acrescentadas."',r:'Mateus 6:33'},
  {t:'"O trabalho braçal leva à liderança; a preguiça leva à escravidão."',r:'Provérbios 12:24'},
  {t:'"Tudo o que fizerem, façam de todo o coração, como para o Senhor e não para os homens."',r:'Colossenses 3:23'},
  {t:'"Vinde a mim, todos os que estais cansados e oprimidos, e eu vos aliviarei."',r:'Mateus 11:28'},
  {t:'"Confie no Senhor de todo o seu coração e não se apoie em seu próprio entendimento."',r:'Provérbios 3:5'},
  {t:'"Entrega o teu caminho ao Senhor; confia nele, e o mais ele fará."',r:'Salmos 37:4-5'},
  {t:'"Porque seis eu que conheço os planos — planos de prosperar, não de prejudicar, para dar a vocês esperança e um futuro."',r:'Jeremias 29:11'},
  {t:'"O Senhor teu Deus está no meio de ti, poderoso para salvar. Ele se deliciará em ti com alegria."',r:'Sofonias 3:17'},
  {t:'"Não temas, porque eu sou contigo; não te assombres, porque eu sou teu Deus; eu te fortaleço."',r:'Isaías 41:10'},
  {t:'"Aquele que semeia com lágrimas ceifará com alegria."',r:'Salmos 126:5'},
  {t:'"Antes da honra vem a humildade."',r:'Provérbios 15:33'},
  {t:'"Peçam e lhes será dado; busquem e encontrarão; batam e a porta lhes será aberta."',r:'Mateus 7:7'},
  {t:'"A bênção do Senhor enriquece, e não acrescenta tristeza com ela."',r:'Provérbios 10:22'},
  {t:'"Renovai-vos no espírito da vossa mente e revesti-vos do novo homem."',r:'Efésios 4:23-24'},
  {t:'"Deleita-te no Senhor, e ele satisfará os desejos do teu coração."',r:'Salmos 37:4'},
  {t:'"O Senhor fará por vós a guerra; ficai vós quietos."',r:'Êxodo 14:14'},
  {t:'"Lança sobre o Senhor o teu peso, e ele te susterá; não permitirá que o justo seja abalado."',r:'Salmos 55:22'},
  {t:'"Não se turbe o vosso coração; credes em Deus, crede também em mim."',r:'João 14:1'},
  {t:'"O Senhor é o meu escudo e a força da minha salvação, o meu alto refúgio."',r:'Salmos 18:2'},
  {t:'"Porque para Deus nada é impossível."',r:'Lucas 1:37'},
  {t:'"Aquele que habita no esconderijo do Altíssimo ficará à sombra do Todo-Poderoso."',r:'Salmos 91:1'},
  {t:'"Sede fortes e corajosos. Não vos atemorizeis nem vos aterrorizeis diante deles, pois o Senhor teu Deus vai contigo."',r:'Deuteronômio 31:6'},
  {t:'"Não me afastarei desta lei; terei muito sucesso onde quer que eu for."',r:'Josué 1:7'},
  {t:'"O Senhor é a minha luz e a minha salvação; a quem temerei?"',r:'Salmos 27:1'},
  {t:'"Bem-aventurado o homem que acha sabedoria e adquire entendimento."',r:'Provérbios 3:13'},
  {t:'"Deus é o nosso refúgio e força, socorro bem presente na angústia."',r:'Salmos 46:1'},
  {t:'"A paz de Deus, que excede todo o entendimento, guardará os vossos corações e as vossas mentes."',r:'Filipenses 4:7'},
  {t:'"Com paciência correi a corrida que está diante de vós."',r:'Hebreus 12:1'},
  {t:'"O Senhor sustenta todos os que caem e levanta todos os que estão abatidos."',r:'Salmos 145:14'},
  {t:'"Sede sóbrios e vigilantes. O diabo, vosso adversário, anda em derredor como leão que ruge, procurando alguém para devorar. Resistam-no firmes na fé."',r:'1 Pedro 5:8-9'},
  {t:'"Melhor é o fim das coisas do que o seu princípio; melhor é o longânimo do que o altivo."',r:'Eclesiastes 7:8'},
  {t:'"O jovem se cansa e se fatiga, o moço tropeça e cai, mas os que esperam no Senhor renovam as suas forças."',r:'Isaías 40:30-31'},
  {t:'"Mas os que esperam no Senhor renovarão as suas forças; subirão com asas como águias."',r:'Isaías 40:31'},
  {t:'"O Senhor é bom, uma força na hora da angústia."',r:'Naum 1:7'},
  {t:'"Não te afaste esta lei da tua boca; medita nela de dia e de noite e assim farás prosperar o teu caminho."',r:'Josué 1:8'},
  {t:'"Humilhai-vos perante o Senhor, e ele vos exaltará."',r:'Tiago 4:10'},
  {t:'"Não me envergonho do evangelho, porque é o poder de Deus para a salvação de todo aquele que crê."',r:'Romanos 1:16'},
  {t:'"A mão dos diligentes governará, mas a dos preguiçosos será sujeita a tributo."',r:'Provérbios 12:24'},
  {t:'"Tudo posso — mas nem tudo é conveniente. Tudo posso — mas nem tudo edifica."',r:'1 Coríntios 10:23'},
  {t:'"Que o Deus da esperança os encha de toda alegria e paz, para que transbordem de esperança."',r:'Romanos 15:13'},
  {t:'"Porque eu, o Senhor teu Deus, te sustento pela minha destra vitoriosa."',r:'Isaías 41:10'},
  {t:'"Alegrai-vos sempre no Senhor. Outra vez digo: alegrai-vos!"',r:'Filipenses 4:4'},
  {t:'"O coração do homem traça o seu caminho, mas o Senhor lhe dirige os passos."',r:'Provérbios 16:9'},
  {t:'"Não se turbe o vosso coração; tendes fé em Deus."',r:'João 14:1'},
  {t:'"Eu vim para que tenham vida e a tenham em abundância."',r:'João 10:10'},
  {t:'"Guarda o teu coração mais do que tudo o que se guarda, pois dele procedem as fontes da vida."',r:'Provérbios 4:23'},
  {t:'"A fé é a certeza daquilo que esperamos e a prova das coisas que não vemos."',r:'Hebreus 11:1'},
  {t:'"Todas as promessas de Deus são sim em Cristo."',r:'2 Coríntios 1:20'},
  {t:'"O Senhor perfeitamente cumprirá os seus propósitos a meu respeito."',r:'Salmos 138:8'},
  {t:'"Louvarei o Senhor em todo o tempo; o seu louvor estará sempre nos meus lábios."',r:'Salmos 34:1'},
  {t:'"Invoca-me, e eu te responderei e te contarei coisas grandes e ocultas que não sabes."',r:'Jeremias 33:3'},
  {t:'"Persevera no que aprendeste e de que te convenceste, sabendo de quem o aprendeste."',r:'2 Timóteo 3:14'},
  {t:'"O nome do Senhor é uma torre forte; o justo corre para ela e está seguro."',r:'Provérbios 18:10'},
  {t:'"Mas em todas essas coisas somos mais do que vencedores por meio daquele que nos amou."',r:'Romanos 8:37'},
  {t:'"Não vos conformeis com este século, mas transformai-vos pela renovação da vossa mente."',r:'Romanos 12:2'},
  {t:'"O Senhor te abençoe e te proteja. O Senhor faça resplandecer o seu rosto sobre ti."',r:'Números 6:24-25'},
  {t:'"Antes de te formar no ventre materno, eu te conheci; antes de nasceres, eu te separei."',r:'Jeremias 1:5'},
  {t:'"Dai graças em tudo, porque esta é a vontade de Deus em Cristo Jesus para convosco."',r:'1 Tessalonicenses 5:18'},
  {t:'"Quem confia no Senhor será como o monte Sião, que não se abala, que permanece para sempre."',r:'Salmos 125:1'},
  {t:'"Todo aquele que invocar o nome do Senhor será salvo."',r:'Romanos 10:13'},
  {t:'"Mais do que tudo o que você guarda, guarde o seu coração, porque dele vem a vida."',r:'Provérbios 4:23'},
  {t:'"Honra ao Senhor com os teus bens e com as primícias de toda a tua renda; e se encherão os teus celeiros."',r:'Provérbios 3:9-10'},
  {t:'"Sede exemplo dos fiéis na palavra, no procedimento, no amor, na fé, na pureza."',r:'1 Timóteo 4:12'},
  {t:'"A alegria do coração é uma boa medicina."',r:'Provérbios 17:22'},
  {t:'"Bem-aventurados os que têm fome e sede de justiça, porque serão fartos."',r:'Mateus 5:6'},
  {t:'"Não temas, porque eu te resgatei; chamei-te pelo teu nome, tu és meu."',r:'Isaías 43:1'},
  {t:'"O Senhor lutará por vocês; apenas fiquem quietos."',r:'Êxodo 14:14'},
  {t:'"Toda dádiva boa e todo dom perfeito vêm do alto, descendo do Pai das luzes."',r:'Tiago 1:17'},
  {t:'"Busquem a paz com todos e a santidade, sem a qual ninguém verá o Senhor."',r:'Hebreus 12:14'},
  {t:'"Confia ao Senhor as tuas obras, e os teus projetos serão estabelecidos."',r:'Provérbios 16:3'},
  {t:'"Não andeis ansiosos por coisa alguma; em tudo apresentai os vossos pedidos a Deus."',r:'Filipenses 4:6'},
  {t:'"Levanta-te e anda! Não desistas, pois Deus está contigo."',r:'Josué 1:9'},
  {t:'"O Senhor te guardará em toda a tua saída e na tua entrada, desde agora e para sempre."',r:'Salmos 121:8'},
  {t:'"Serei contigo, não te deixarei nem te abandonarei."',r:'Josué 1:5'},
  {t:'"Posso me apressar no caminho dos teus mandamentos, porque tu alargas o meu coração."',r:'Salmos 119:32'},
  {t:'"O trabalho que você realiza hoje é a semente da colheita de amanhã."',r:'Gálatas 6:7'},
  {t:'"Cristo vive em mim. A vida que agora vivo no corpo, vivo-a pela fé no Filho de Deus."',r:'Gálatas 2:20'},
];
// AUTO LOGIN se tiver credenciais salvas
window.addEventListener('load', function(){
  var saved=null;
  try{saved=JSON.parse(localStorage.getItem('instalato_creds')||'null');}catch(e){}
  if(!saved)return;
  fetch(SURL+'/rest/v1/usuarios?select=*&ativo=eq.true',{headers:H})
    .then(function(r){if(!r.ok)throw new Error();return r.json();})
    .then(function(data){
      var user=(data||[]).find(function(u){
        return u.apelido.toLowerCase()===saved.u.toLowerCase()&&u.senha===saved.p;
      });
      if(user){U=user;startApp();}
    })
    .catch(function(){});
});
let editObraId=null,editAvId=null,novoTipo='func',confSt='',catSel='';
let chkState={};

// UTILS
const fmt=v=>'R$\u00a0'+(v||0).toLocaleString('pt-BR',{minimumFractionDigits:2,maximumFractionDigits:2});
const fmtK=v=>'R$\u00a0'+(v||0).toLocaleString('pt-BR',{maximumFractionDigits:0});
const fmtD=d=>{if(!d)return'—';const p=(d.split('T')[0]).split('-');return`${p[2]}/${p[1]}/${p[0]}`;};
const hoje=()=>new Date().toISOString().split('T')[0];
const hora=()=>new Date().toLocaleTimeString('pt-BR',{hour:'2-digit',minute:'2-digit'});

function toast(m,d=2500){const e=document.getElementById('toast');e.textContent=m;e.classList.add('show');setTimeout(()=>e.classList.remove('show'),d);}

// DB
async function dbQ(t,f={}){
  try{
    let url=SURL+'/rest/v1/'+t+'?select=*&order=created_at.desc';
    Object.entries(f).forEach(([k,v])=>{url+='&'+k+'=eq.'+encodeURIComponent(v);});
    const r=await fetch(url,{headers:H});
    if(!r.ok){console.error(t,r.status);return[];}
    return await r.json()||[];
  }catch(e){console.error(t,e.message);return[];}
}
async function dbI(t,o){
  try{
    const r=await fetch(SURL+'/rest/v1/'+t,{method:'POST',headers:H,body:JSON.stringify(o)});
    const d=await r.json();
    if(!r.ok){toast('❌ '+(d.message||d.hint||'Erro ao salvar'));return null;}
    return Array.isArray(d)?d[0]:d;
  }catch(e){toast('❌ '+e.message);return null;}
}
async function dbU(t,id,o){
  try{
    const r=await fetch(SURL+'/rest/v1/'+t+'?id=eq.'+id,{method:'PATCH',headers:H,body:JSON.stringify(o)});
    if(!r.ok){const d=await r.json();toast('❌ '+(d.message||'Erro'));return false;}
    return true;
  }catch(e){toast('❌ '+e.message);return false;}
}
async function dbD(t,id){
  try{
    const r=await fetch(SURL+'/rest/v1/'+t+'?id=eq.'+id,{method:'DELETE',headers:{...H,'Prefer':''}});
    return r.ok;
  }catch(e){return false;}
}

// LOGIN
// Carregar credenciais salvas ao abrir
(function(){
  try{
    const saved=JSON.parse(localStorage.getItem('instalato_creds')||'null');
    if(saved){
      document.getElementById('l-user').value=saved.u||'';
      document.getElementById('l-pass').value=saved.p||'';
      document.getElementById('l-remember').checked=true;
    }
  }catch(e){}
})();

function fazerLogin(){
  const ap=(document.getElementById('l-user').value||'').trim();
  const pw=(document.getElementById('l-pass').value||'').trim();
  const remember=document.getElementById('l-remember').checked;
  const errEl=document.getElementById('login-err');
  const btnEl=document.getElementById('btn-login');
  errEl.style.display='none';
  if(!ap||!pw){errEl.textContent='⚠️ Preencha usuário e senha.';errEl.style.display='block';return;}
  btnEl.textContent='Entrando...';btnEl.disabled=true;
  const url=SURL+'/rest/v1/usuarios?select=*&ativo=eq.true';
  fetch(url,{headers:H})
    .then(function(r){
      if(!r.ok) throw new Error('Erro HTTP '+r.status);
      return r.json();
    })
    .then(function(data){
      btnEl.textContent='Entrar';btnEl.disabled=false;
      const user=(data||[]).find(function(u){
        return u.apelido.toLowerCase()===ap.toLowerCase() && u.senha===pw;
      });
      if(!user){
        errEl.textContent='❌ Usuário ou senha incorretos';
        errEl.style.display='block';
        localStorage.removeItem('instalato_creds');
        return;
      }
      errEl.style.display='none';
      if(remember){
        try{localStorage.setItem('instalato_creds',JSON.stringify({u:ap,p:pw}));}catch(e){}
      } else {
        try{localStorage.removeItem('instalato_creds');}catch(e){}
      }
      U=user;
      startApp();
    })
    .catch(function(e){
      btnEl.textContent='Entrar';btnEl.disabled=false;
      errEl.textContent='❌ Erro de conexão: '+e.message;
      errEl.style.display='block';
    });
}
document.getElementById('btn-login').onclick=fazerLogin;
document.getElementById('l-pass').onkeypress=function(e){if(e.key==='Enter')fazerLogin();};
document.getElementById('l-user').onkeypress=function(e){if(e.key==='Enter')fazerLogin();};

// START APP
async function startApp(){
  document.getElementById('pg-login').style.display='none';
  const s=document.getElementById('shell');
  s.style.display='flex';s.style.flexDirection='column';s.style.height='100vh';
  document.getElementById('tb-info').textContent=`${U.apelido} · ${U.tipo==='admin'?'Admin':U.tipo==='lider'?'Líder':'Funcionário'}`;
  if(U.tipo==='admin')document.getElementById('btn-cfg').style.display='block';
  obras=await dbQ('obras');
  users=await dbQ('usuarios');
  avs=await dbQ('avisos');
  buildNav();
  await loadAll();
  renderAll();
}

function buildNav(){
  const nav=document.getElementById('nav');
  const tc=document.getElementById('tabs');
  nav.innerHTML='';tc.innerHTML='';
  tc.style.cssText='flex:1;overflow:hidden;position:relative;';
  const T=U.tipo;
  const tabs=[];
  if(T==='admin'||T==='lider')tabs.push({id:'lancar',i:'➕',l:'Lançar'});
  tabs.push({id:'meu',i:'📊',l:'Meu Resultado'});
  if(T==='admin'||T==='lider')tabs.push({id:'hist',i:'📋',l:'Histórico'});
  if(T==='admin'||T==='lider')tabs.push({id:'rank',i:'🏆',l:'Ranking'});
  if(T==='admin'||T==='lider')tabs.push({id:'conf',i:'✅',l:'Conferência'});
  if(T==='admin'||T==='lider')tabs.push({id:'mat',i:'📦',l:'Materiais'});
  if(T==='admin'||T==='lider')tabs.push({id:'ocorr',i:'⚠️',l:'Ocorrências'});
  if(T==='admin')tabs.push({id:'dash',i:'📈',l:'Dashboard'});
  if(T==='admin')tabs.push({id:'desp',i:'💸',l:'Despesas'});
  tabs.push({id:'aviso',i:'📢',l:'Avisos'});
  tabs.forEach((t,i)=>{
    const n=document.createElement('div');
    n.className='ntab'+(i===0?' on':'');n.id='n-'+t.id;
    n.innerHTML=`<span class="ni">${t.i}</span>${t.l}`;
    n.onclick=()=>goTab(t.id);nav.appendChild(n);
    const d=document.createElement('div');
    d.className='tab'+(i===0?' on':'');d.id='t-'+t.id;
    d.style.cssText='position:absolute;inset:0;overflow-y:auto;';
    tc.appendChild(d);
  });
}

function goTab(id){
  document.querySelectorAll('.ntab').forEach(n=>n.classList.remove('on'));
  document.querySelectorAll('.tab').forEach(t=>t.classList.remove('on'));
  const n=document.getElementById('n-'+id);
  const t=document.getElementById('t-'+id);
  if(n)n.classList.add('on');
  if(t){t.classList.add('on');t.scrollTop=0;}
  renderTab(id);
}

async function loadAll(){
  lancs=await dbQ('lancamentos');
  confs=await dbQ('conferencias');
  mats=await dbQ('materiais_lanc');
  desps=await dbQ('despesas');
  avs=await dbQ('avisos');
  ocorrs=await dbQ('ocorrencias');
}

function renderAll(){
  const T=U.tipo;
  if(T==='admin'||T==='lider'){renderLancar();renderHist();renderRank();renderConf();renderMat();}
  renderMeu();
  if(T==='admin'||T==='lider')renderOcorr();
  if(T==='admin'){renderDash();renderDesp();}
  renderAvisos();
}
function renderTab(id){
  ({lancar:renderLancar,meu:renderMeu,hist:renderHist,rank:renderRank,
    conf:renderConf,mat:renderMat,ocorr:renderOcorr,dash:renderDash,desp:renderDesp,aviso:renderAvisos}[id]||function(){})();
}

// ══ LANÇAR ══
function renderLancar(){
  const el=document.getElementById('t-lancar');if(!el)return;
  const meus=lancs.filter(l=>l.usuario_id===U.id);
  const total=meus.reduce((s,l)=>s+(l.total||0),0);
  const meta=U.meta_mensal||0;
  const pct=meta>0?Math.min(Math.round((total/meta)*100),100):0;
  let mc='msg-ok',mt='👍 No ritmo certo! Continue assim.';
  if(pct>=100){mc='msg-ok';mt='🏆 Meta batida! Excelente!';}
  else if(pct<50){mc='msg-bad';mt='🔥 Foco total! Ainda tem muito pela frente.';}
  else if(pct<80){mc='msg-warn';mt='⚠️ Abaixo do esperado. Acelere!';}
  const semMeta=meta/4;
  const wks=[1,2,3,4].map(w=>`<div class="wk${w<3?' done':w===3?' cur':''}"><div class="wl">Sem ${w}</div><div class="wv">${fmtK(semMeta).replace('R$\u00a0','R$')}</div></div>`).join('');
  const obraOpts=obras.map(o=>`<option value="${o.id}">${o.nome}</option>`).join('');
  const funcOpts=users.filter(u=>u.ativo).map(u=>`<option value="${u.id}">${u.apelido}</option>`).join('');
  const bv=VERSES[Math.floor(Math.random()*VERSES.length)];
  el.innerHTML=`
  <div class="hero" style="background:var(--gold)"><p>Lançamento do dia</p><h2>O que você fez hoje?</h2></div>
  <div style="margin:12px 16px 0;padding:12px 14px;background:var(--light-gold);border-radius:12px;border-left:3px solid var(--gold);">
    <div style="font-size:9px;font-weight:700;color:var(--gold);text-transform:uppercase;letter-spacing:0.5px;margin-bottom:4px;">✨ Palavra do dia</div>
    <div style="font-size:12px;color:#5a3e00;line-height:1.6;font-style:italic;">${bv.t}</div>
    <div style="font-size:10px;color:var(--gold);margin-top:4px;font-weight:600;">— ${bv.r}</div>
  </div>
  <div class="pad">
    <div class="meta-card">
      <div class="meta-top"><span class="meta-v">${fmtK(total)} / ${fmtK(meta)}</span><span class="meta-p">${pct}%</span></div>
      <div class="prog"><div class="prog-f" style="width:${pct}%"></div></div>
      <div class="weeks-grid">${wks}</div>
      <div class="meta-msg ${mc}">${mt}</div>
      <div class="meta-inp-row">
        <input class="inp" type="number" id="l-meta" placeholder="Definir meta (R$)">
        <button class="btn-def" onclick="definirMeta()">Definir</button>
      </div>
    </div>
    <div>
      <div class="fl">Obra</div>
      <select class="sel" id="l-obra" onchange="obraChanged()">
        <option value="">— Selecione a obra —</option>${obraOpts}
      </select>
      <div id="obra-info" style="display:none;background:rgba(184,134,11,.08);border-radius:10px;padding:8px 12px;font-size:11px;color:#854F0B;margin-top:6px;"></div>
    </div>
    <div class="row2">
      <div><div class="fl">Funcionário</div><select class="sel" id="l-func"><option value="">Selecione</option>${funcOpts}</select></div>
      <div><div class="fl">Apto / Casa</div><input class="inp" type="text" id="l-apto" placeholder="Ex: 101"></div>
    </div>
    <div class="row2">
      <div><div class="fl">Ambiente</div>
        <select class="sel" id="l-amb">
          <option value="">Selecione</option>
          <option>Suíte 1</option><option>Suíte 2</option><option>Banheiro Social</option>
          <option>Lavabo</option><option>Varanda</option><option>Sala</option>
          <option>Cozinha</option><option>Área de Serviço</option>
        </select>
      </div>
      <div><div class="fl">Área (m²)</div><input class="inp" type="number" id="l-area" placeholder="0" oninput="calcTotal()"></div>
    </div>
    <div id="rate-info" class="info-box" style="display:none;"></div>
    <div>
      <div class="fl">Outros — rodapés, soleiras, cortes...</div>
      <div style="display:grid;grid-template-columns:1fr 80px 70px 32px;gap:6px;margin-bottom:4px;">
        <div class="fl" style="margin:0;">Descrição</div><div class="fl" style="margin:0;">Valor R$</div><div class="fl" style="margin:0;">Qtd</div><div></div>
      </div>
      <div id="extras-wrap"></div>
      <button class="btn-add-line" onclick="addExtra()">＋ Adicionar item</button>
    </div>
    <div>
      <div class="fl">Bônus de desempenho <span style="font-weight:400;font-size:9px;color:var(--sub);">+2% por item · máx 10%</span></div>
      <div id="bonus-list"></div>
    </div>
    <div class="total-card">
      <div class="t-row"><span class="tl">Produção base</span><span class="tv" id="tv-base">R$ 0,00</span></div>
      <div class="t-row"><span class="tl">Extras</span><span class="tv" id="tv-ext">R$ 0,00</span></div>
      <div class="t-row"><span class="tl">Bônus <span id="tv-pct" style="background:rgba(30,132,73,.12);color:var(--green);font-size:10px;padding:1px 6px;border-radius:20px;margin-left:4px;">0%</span></span><span class="tv" id="tv-bon" style="color:var(--green);">+ R$ 0,00</span></div>
      <div class="t-div"></div>
      <div class="t-final"><span style="font-size:13px;color:var(--sub);">Total a receber</span><span class="tfv" id="tv-tot">R$ 0,00</span></div>
    </div>
    <button class="btn-gold" onclick="salvarLanc()">✅ Salvar produção</button>
  </div>`;
  renderBonusList();
}

function renderBonusList(){
  const items=[
    {k:'qualidade',n:'Qualidade técnica',d:'Assentamento nivelado e com padrão'},
    {k:'limpeza',n:'Organização e limpeza',d:'Local limpo ao fim do dia'},
    {k:'horario',n:'Horário de entrada/saída',d:'Pontualidade no início e término'},
    {k:'epi',n:'Uso de EPIs',d:'Equipamentos utilizados corretamente'},
    {k:'retrabalho',n:'Sem retrabalho',d:'Nenhuma correção necessária'}
  ];
  const el=document.getElementById('bonus-list');if(!el)return;
  el.innerHTML=items.map(it=>`
    <div class="bonus-item" id="b-${it.k}" onclick="toggleBonus('${it.k}')">
      <div class="bchk" id="bc-${it.k}"></div>
      <div class="bname">${it.n}<br><span style="font-size:10px;color:var(--sub);font-weight:400;">${it.d}</span></div>
      <div class="bpct">+2%</div>
    </div>`).join('');
}

function toggleBonus(k){
  const el=document.getElementById('b-'+k);
  el.classList.toggle('on');
  document.getElementById('bc-'+k).textContent=el.classList.contains('on')?'✓':'';
  calcTotal();
}

function obraChanged(){
  const oId=document.getElementById('l-obra')?.value;
  const o=obras.find(x=>x.id===oId);
  const inf=document.getElementById('obra-info');
  const ri=document.getElementById('rate-info');
  if(o){
    inf.style.display='block';
    inf.textContent=`${o.cliente} · ${o.cidade} · ${o.andares} andares`;
    const rate=getRate(oId);
    ri.style.display='block';
    ri.innerHTML=`ℹ️ Valor do m²: <strong>R$ ${rate.toFixed(2)}</strong> — definido pelo admin`;
  } else {
    inf.style.display='none';ri.style.display='none';
  }
  calcTotal();
}

function getRate(obraId){
  const fId=document.getElementById('l-func')?.value;
  if(fId){const u=users.find(x=>x.id===fId);if((u&&u.rate_m2))return u.rate_m2;}
  return 35;
}

function calcTotal(){
  const area=parseFloat(document.getElementById('l-area')?.value)||0;
  const rate=getRate(document.getElementById('l-obra')?.value);
  const base=area*rate;
  let ext=0;
  document.querySelectorAll('#extras-wrap .extra-line').forEach(l=>{
    const ins=l.querySelectorAll('input');
    ext+=(parseFloat(ins[1]?.value)||0)*(parseFloat(ins[2]?.value)||1);
  });
  const bon=document.querySelectorAll('.bonus-item.on').length;
  const pct=Math.min(bon*2,10);
  const bval=base*(pct/100);
  const tot=base+ext+bval;
  const s=document.getElementById('tv-base');if(s)s.textContent=fmt(base);
  const e=document.getElementById('tv-ext');if(e)e.textContent=fmt(ext);
  const b=document.getElementById('tv-bon');if(b)b.textContent='+ '+fmt(bval);
  const p=document.getElementById('tv-pct');if(p)p.textContent=pct+'%';
  const t=document.getElementById('tv-tot');if(t)t.textContent=fmt(tot);
}

function addExtra(){
  const w=document.getElementById('extras-wrap');if(!w)return;
  const d=document.createElement('div');d.className='extra-line';
  d.innerHTML=`<input class="el-inp" type="text" placeholder="Ex: Rodapé" oninput="calcTotal()">
    <input class="el-inp" type="number" placeholder="0,00" oninput="calcTotal()">
    <input class="el-inp" type="number" placeholder="1" oninput="calcTotal()">
    <button class="btn-rem" onclick="this.parentElement.remove();calcTotal()">✕</button>`;
  w.appendChild(d);
}

async function definirMeta(){
  const v=parseFloat(document.getElementById('l-meta')?.value)||0;
  if(!v)return;
  await dbU('usuarios',U.id,{meta_mensal:v});
  U.meta_mensal=v;users=users.map(u=>u.id===U.id?{...u,meta_mensal:v}:u);
  toast('✅ Meta definida!');renderLancar();
}

async function salvarLanc(){
  const oId=document.getElementById('l-obra')?.value;
  const fId=document.getElementById('l-func')?.value;
  const apto=document.getElementById('l-apto')?.value.trim();
  const amb=document.getElementById('l-amb')?.value;
  const area=parseFloat(document.getElementById('l-area')?.value)||0;
  if(!oId){toast('⚠️ Selecione a obra.');return;}
  if(!fId){toast('⚠️ Selecione o funcionário.');return;}
  if(!apto){toast('⚠️ Informe o apto.');return;}
  if(!amb){toast('⚠️ Selecione o ambiente.');return;}
  if(area<=0){toast('⚠️ Informe a área.');return;}
  const rate=getRate(oId);
  const base=area*rate;
  const extras=[];
  document.querySelectorAll('#extras-wrap .extra-line').forEach(l=>{
    const ins=l.querySelectorAll('input');
    const nm=ins[0]?.value.trim();
    const val=parseFloat(ins[1]?.value)||0;
    const qty=parseFloat(ins[2]?.value)||1;
    if(nm)extras.push({nome:nm,valor:val,qty,total:val*qty});
  });
  const extTotal=extras.reduce((s,e)=>s+e.total,0);
  const bonCnt=document.querySelectorAll('.bonus-item.on').length;
  const pct=Math.min(bonCnt*2,10);
  const bval=base*(pct/100);
  const tot=base+extTotal+bval;
  const r=await dbI('lancamentos',{
    obra_id:oId,usuario_id:fId,lancado_por:U.id,
    apartamento:apto,ambiente:amb,area_m2:area,rate_m2:rate,
    valor_base:base,extras:JSON.stringify(extras),extras_total:extTotal,
    bonus_pct:pct,bonus_valor:bval,total:tot,
    data:hoje(),hora:hora()
  });
  if(r){
    toast('✅ Produção salva! '+fmt(tot));
    lancs=[r,...lancs];
    renderLancar();renderMeu();if(U.tipo==='admin')renderDash();
  }
}

// ══ MEU RESULTADO ══
function renderMeu(){
  const el=document.getElementById('t-meu');if(!el)return;
  const meus=lancs.filter(l=>l.usuario_id===U.id);
  const total=meus.reduce((s,l)=>s+(l.total||0),0);
  const m2=meus.reduce((s,l)=>s+(l.area_m2||0),0);
  const meta=U.meta_mensal||0;
  const pct=meta>0?Math.min(Math.round((total/meta)*100),100):0;
  const bonMedia=meus.length?Math.round(meus.reduce((s,l)=>s+(l.bonus_pct||0),0)/meus.length):0;
  const hist=meus.slice(0,5).map(l=>{
    const o=obras.find(x=>x.id===l.obra_id);
    return`<div class="hist-item">
      <div class="hi-ico">🪵</div>
      <div class="hi-body"><div class="hi-t">${l.ambiente||'—'} · Apto ${l.apartamento||'—'}</div>
        <div class="hi-s">${(o&&o.nome)||'—'} · ${l.area_m2}m²</div></div>
      <div class="hi-right"><div class="hi-v">${fmt(l.total)}</div><div class="hi-d">${fmtD(l.data)}</div></div>
    </div>`;}).join('');
  el.innerHTML=`
  <div class="hero" style="background:var(--gold)"><p>Visualização · somente leitura</p><h2>Meu resultado</h2></div>
  <div class="pad">
    <div class="stat-grid">
      <div class="stat"><div class="sv">${fmtK(total)}</div><div class="sl">Acumulado mês</div></div>
      <div class="stat"><div class="sv">${m2.toFixed(0)} m²</div><div class="sl">Produção total</div></div>
      <div class="stat"><div class="sv">${pct}%</div><div class="sl">Meta do mês</div></div>
      <div class="stat"><div class="sv">${bonMedia}%</div><div class="sl">Bônus médio</div></div>
    </div>
    <div class="card">
      <div class="prog-lbl"><span>Meta mensal</span><span style="color:var(--gold);font-weight:700;">${pct}%</span></div>
      <div class="prog-track"><div class="prog-track-f" style="width:${pct}%"></div></div>
    </div>
    <div><div class="fl">Últimos lançamentos</div>
      ${hist||'<div class="empty"><div class="ei">📋</div><p>Nenhum lançamento ainda.</p></div>'}
    </div>
    <div class="info-box">👁 Apenas visualização — lançamentos realizados pelo líder ou admin.</div>
  </div>`;
}

// ══ HISTÓRICO ══
function renderHist(){
  const el=document.getElementById('t-hist');if(!el)return;
  const total=lancs.reduce((s,l)=>s+(l.total||0),0);
  const rows=lancs.map(l=>{
    const u=users.find(x=>x.id===l.usuario_id);
    const o=obras.find(x=>x.id===l.obra_id);
    return`<div class="hist-item">
      <div class="hi-ico">🪵</div>
      <div class="hi-body">
        <div class="hi-t">${(u&&u.apelido)||'—'} · ${l.ambiente||'—'} · Apto ${l.apartamento||'—'}</div>
        <div class="hi-s">${(o&&o.nome)||'—'} · ${l.area_m2}m² · bônus ${l.bonus_pct}%</div>
      </div>
      <div class="hi-right"><div class="hi-v">${fmt(l.total)}</div><div class="hi-d">${fmtD(l.data)}</div></div>
    </div>`;}).join('');
  el.innerHTML=`
  <div class="hero" style="background:var(--dark)"><p>Todos os registros</p><h2>Histórico Geral</h2></div>
  <div class="pad">
    <div style="display:flex;justify-content:space-between;align-items:center;padding:4px 0;">
      <span style="font-size:11px;color:var(--sub);">${lancs.length} registros</span>
      <span style="font-size:13px;font-weight:700;color:var(--gold);">${fmtK(total)} total</span>
    </div>
    ${rows||'<div class="empty"><div class="ei">📋</div><p>Nenhum lançamento ainda.</p></div>'}
  </div>`;
}

// ══ RANKING ══
function renderRank(){
  const el=document.getElementById('t-rank');if(!el)return;
  const totais={};
  lancs.forEach(l=>{totais[l.usuario_id]=(totais[l.usuario_id]||0)+(l.total||0);});
  const m2totais={};
  lancs.forEach(l=>{m2totais[l.usuario_id]=(m2totais[l.usuario_id]||0)+(l.area_m2||0);});
  const rank=users.filter(u=>u.ativo&&totais[u.id]).sort((a,b)=>(totais[b.id]||0)-(totais[a.id]||0));
  const cores=['#B8860B','#888','#CD7F32'];
  const rows=rank.map((u,i)=>`
    <div class="rank-item" ${i===0?'style="border:1.5px solid rgba(184,134,11,.3);"':''}>
      <div class="rnum" style="background:${cores[i]||'#ddd'};${i>2?'color:#888':''};">${i+1}</div>
      <div class="rinfo"><div class="rname">${u.apelido}</div><div class="rmeta">${(m2totais[u.id]||0).toFixed(1)} m²</div></div>
      <div class="rval"><div class="rv">${fmtK(totais[u.id]||0)}</div></div>
    </div>`).join('');
  el.innerHTML=`
  <div class="hero" style="background:var(--dark)"><p>Classificação geral</p><h2>🏆 Ranking de Produção</h2></div>
  <div class="pad">
    ${rows||'<div class="empty"><div class="ei">🏆</div><p>Nenhum dado ainda.</p></div>'}
  </div>`;
}

// ══ CONFERÊNCIA ══
function renderConf(){
  const el=document.getElementById('t-conf');if(!el)return;
  const obraOpts=obras.map(o=>`<option value="${o.id}">${o.nome}</option>`).join('');
  const funcOpts=users.filter(u=>u.ativo&&u.tipo!=='admin').map(u=>`<option value="${u.id}">${u.apelido}</option>`).join('');
  const checks=['Qualidade técnica','Organização e limpeza','Horário de entrada/saída','Uso de EPIs','Nivelamento e alinhamento','Rejunte e acabamento','Postura profissional'];
  const chkHtml=checks.map((c,i)=>`
    <div class="chk-item">
      <div class="chk-name">${c}</div>
      <div class="chk-btns">
        <button class="cbtn ap" id="ca-${i}" onclick="setChk(${i},'ap')">✓ Aprovado</button>
        <button class="cbtn rp" id="cr-${i}" onclick="setChk(${i},'rp')">✗ Reprovado</button>
      </div>
    </div>`).join('');
  const hist=confs.slice(0,3).map(c=>{
    const p=users.find(x=>x.id===c.profissional_id);
    return`<div class="hist-item">
      <div class="hi-ico">${c.status==='aprovado'?'✅':c.status==='incompleto'?'⚠️':'❌'}</div>
      <div class="hi-body"><div class="hi-t">${(p&&p.apelido)||'—'} · Apto ${c.apartamento||'—'}</div>
        <div class="hi-s">${c.ambiente||'—'} · ${c.status}</div>
        ${c.observacao?`<div class="hi-s" style="font-style:italic;">"${c.observacao}"</div>`:''}
      </div>
      <div class="hi-right"><div class="hi-d">${fmtD(c.data)}</div><div class="hi-d">${c.hora||''}</div></div>
    </div>`;}).join('');
  el.innerHTML=`
  <div class="hero" style="background:var(--dark)"><p>Avaliação de serviço</p><h2>Nova Conferência</h2></div>
  <div class="pad">
    <div>
      <div class="fl">Resultado</div>
      <div class="status-row">
        <button class="btn-st btn-ap" id="st-ap" onclick="selSt('aprovado')"><span class="si">✅</span>Aprovado</button>
        <button class="btn-st btn-in" id="st-in" onclick="selSt('incompleto')"><span class="si">⚠️</span>Incompleto</button>
        <button class="btn-st btn-rp" id="st-rp" onclick="selSt('reprovado')"><span class="si">❌</span>Reprovado</button>
      </div>
    </div>
    <div><div class="fl">Obra</div><select class="sel" id="c-obra"><option value="">Selecione</option>${obraOpts}</select></div>
    <div><div class="fl">Profissional responsável</div><select class="sel" id="c-prof"><option value="">Selecione</option>${funcOpts}</select></div>
    <div class="row2">
      <div><div class="fl">Nº Apto / Casa</div><input class="inp" type="text" id="c-apto" placeholder="701"></div>
      <div><div class="fl">Ambiente</div>
        <select class="sel" id="c-amb"><option value="">Selecione</option>
          <option>Sala</option><option>Cozinha</option><option>Banheiro</option>
          <option>Suíte</option><option>Varanda</option><option>Lavabo</option>
          <option>Área de Serviço</option><option>Escada</option>
        </select>
      </div>
    </div>
    <div><div class="fl">Itens avaliados</div>${chkHtml}</div>
    <div><div class="fl">Observação</div><textarea class="inp" id="c-obs" rows="3" style="resize:none;" placeholder="Descreva o que foi observado..."></textarea></div>
    <button class="btn-gold" onclick="salvarConf()">📋 Salvar e notificar</button>
    ${confs.length?`<div><div class="fl">Últimas conferências</div>${hist}</div>`:''}
  </div>`;
  chkState={};
}

function selSt(s){
  confSt=s;
  ['ap','in','rp'].forEach(k=>document.getElementById('st-'+k)?.classList.remove('sel'));
  const map={aprovado:'ap',incompleto:'in',reprovado:'rp'};
  document.getElementById('st-'+map[s])?.classList.add('sel');
}

function setChk(i,v){
  if(chkState[i]===v){chkState[i]=null;document.getElementById('ca-'+i)?.classList.remove('on');document.getElementById('cr-'+i)?.classList.remove('on');}
  else{chkState[i]=v;document.getElementById('ca-'+i)?.classList.toggle('on',v==='ap');document.getElementById('cr-'+i)?.classList.toggle('on',v==='rp');}
}

async function salvarConf(){
  const oId=document.getElementById('c-obra')?.value;
  const pId=document.getElementById('c-prof')?.value;
  const apto=document.getElementById('c-apto')?.value.trim();
  const amb=document.getElementById('c-amb')?.value;
  const obs=document.getElementById('c-obs')?.value.trim();
  if(!confSt){toast('⚠️ Selecione o resultado.');return;}
  if(!oId){toast('⚠️ Selecione a obra.');return;}
  if(!pId){toast('⚠️ Selecione o profissional.');return;}
  if(!apto||!amb){toast('⚠️ Preencha apto e ambiente.');return;}
  const lancId=document.getElementById('c-lanc-id')?.value||null;
  const r=await dbI('conferencias',{
    obra_id:oId,lider_id:U.id,profissional_id:pId,
    lancamento_id:lancId||null,
    status:confSt,apartamento:apto,ambiente:amb,
    checklist:JSON.stringify(chkState),observacao:obs,
    data:hoje(),hora:hora()
  });
  if(r){
    const emoji={aprovado:'✅',incompleto:'⚠️',reprovado:'❌'};
    toast(emoji[confSt]+' Conferência salva e registrada!');
    confs=[r,...confs];confSt='';chkState={};
    const lancEl=document.getElementById('c-lanc-id');if(lancEl)lancEl.value='';
    renderConf();
  }
}

// ══ MATERIAIS ══
function renderMat(){
  const el=document.getElementById('t-mat');if(!el)return;
  const funcOpts=users.filter(u=>u.ativo).map(u=>`<option value="${u.id}">${u.apelido}</option>`).join('');
  const hist=mats.slice(0,4).map(m=>{
    const u=users.find(x=>x.id===m.colaborador_id);
    const itens=Array.isArray(m.itens)?m.itens:JSON.parse(m.itens||'[]');
    return`<div class="hist-item">
      <div class="hi-ico">📦</div>
      <div class="hi-body"><div class="hi-t">Apto ${m.apartamento||'—'}</div>
        <div class="hi-s">${(u&&u.apelido)||'—'} · ${itens.length} material(is)</div>
        ${itens.slice(0,2).map(i=>`<div class="hi-s">${i.nome}: ${i.qty}</div>`).join('')}
      </div>
      <div class="hi-right"><div class="hi-d">${fmtD(m.data)}</div><div class="hi-d">${m.hora||''}</div></div>
    </div>`;}).join('');
  el.innerHTML=`
  <div class="hero" style="background:var(--dark)"><p>Acesso restrito · Líder e Admin</p><h2>Controle de Materiais</h2></div>
  <div class="pad">
    <div><div class="fl">Obra</div><select class="sel" id="m-obra"><option value="">Selecione a obra</option>${obraOpts}</select></div>
    <div class="row2">
      <div><div class="fl">Nº Apartamento</div><input class="inp" type="text" id="m-apto" placeholder="Ex: 701"></div>
      <div><div class="fl">Colaborador</div><select class="sel" id="m-colab"><option value="">Selecione</option>${funcOpts}</select></div>
    </div>
    <div>
      <div class="fl">Materiais</div>
      <div style="display:grid;grid-template-columns:1fr 90px 32px;gap:7px;margin-bottom:4px;">
        <div class="fl" style="margin:0;">Material</div><div class="fl" style="margin:0;">Quantidade</div><div></div>
      </div>
      <div id="mat-wrap"></div>
      <button class="btn-add-line" onclick="addMatLinha()">＋ Adicionar material</button>
    </div>
    <button class="btn-gold" onclick="salvarMat()">💾 Salvar lançamento</button>
    ${mats.length?`<div><div class="fl">Histórico recente</div>${hist}</div>`:''}
  </div>`;
  addMatLinha();
}

function addMatLinha(){
  const w=document.getElementById('mat-wrap');if(!w)return;
  const d=document.createElement('div');d.className='mat-line';
  d.innerHTML=`<input class="el-inp" type="text" placeholder="Ex: Argamassa AC-III">
    <input class="el-inp" type="text" placeholder="Ex: 4 sacos">
    <button class="btn-rem" onclick="this.parentElement.remove()">✕</button>`;
  w.appendChild(d);
}

async function salvarMat(){
  const apto=document.getElementById('m-apto')?.value.trim();
  const cId=document.getElementById('m-colab')?.value;
  if(!apto){toast('⚠️ Informe o apartamento.');return;}
  if(!cId){toast('⚠️ Selecione o colaborador.');return;}
  const itens=[];
  document.querySelectorAll('#mat-wrap .mat-line').forEach(l=>{
    const ins=l.querySelectorAll('input');
    const nome=ins[0]?.value.trim();const qty=ins[1]?.value.trim();
    if(nome)itens.push({nome,qty:qty||'—'});
  });
  if(!itens.length){toast('⚠️ Adicione pelo menos um material.');return;}
  const oId=document.getElementById('m-obra')?.value||null;
  const r=await dbI('materiais_lanc',{
    obra_id:oId,usuario_id:U.id,colaborador_id:cId,apartamento:apto,
    itens:JSON.stringify(itens),data:hoje(),hora:hora()
  });
  if(r){toast('📦 Materiais registrados!');mats=[r,...mats];renderMat();}
}

// ══ OCORRÊNCIAS ══
function renderOcorr(){
  const el=document.getElementById('t-ocorr');if(!el)return;
  const obraOpts=obras.map(o=>`<option value="${o.id}">${o.nome}</option>`).join('');
  const funcOpts=users.filter(u=>u.ativo).map(u=>`<option value="${u.id}">${u.apelido}</option>`).join('');
  const tipos=[
    {k:'atraso',i:'⏰',l:'Atraso'},
    {k:'qualidade',i:'🔨',l:'Qualidade'},
    {k:'conduta',i:'⚠️',l:'Conduta'},
    {k:'acidente',i:'🚨',l:'Acidente'},
    {k:'material',i:'📦',l:'Material'},
    {k:'outro',i:'📝',l:'Outro'}
  ];
  const tipoGrid=tipos.map(t=>`<div class="cat-btn${ocorrTipo===t.k?' on':''}" onclick="selOcorrTipo('${t.k}')"><span class="ci">${t.i}</span>${t.l}</div>`).join('');
  const hist=ocorrs.slice(0,30).map(o=>{
    const u=users.find(x=>x.id===o.colaborador_id);
    const ob=obras.find(x=>x.id===o.obra_id);
    const tObj=tipos.find(t=>t.k===o.tipo);
    return`<div class="hist-item" style="border-left:3px solid var(--red);">
      <div class="hi-ico">${(tObj&&tObj.i)||'⚠️'}</div>
      <div class="hi-body">
        <div class="hi-t">${(u&&u.apelido)||'—'} · ${(tObj&&tObj.l)||o.tipo||'—'}</div>
        <div class="hi-s">${(ob&&ob.nome)||'—'}</div>
        ${o.observacao?`<div class="hi-s" style="font-style:italic;">"${o.observacao}"</div>`:''}
      </div>
      <div class="hi-right">
        <div class="hi-d">${fmtD(o.data)}</div>
        <div class="hi-d">${o.hora||''}</div>
        ${U.tipo==='admin'?`<button onclick="delOcorr('${o.id}')" style="background:transparent;border:none;cursor:pointer;color:var(--red);font-size:11px;margin-top:3px;">🗑</button>`:''}
      </div>
    </div>`;}).join('');
  el.innerHTML=`
  <div class="hero" style="background:#8B0000;"><p>Acesso restrito · Líder e Admin</p><h2>⚠️ Ocorrências</h2></div>
  <div class="pad">
    <div><div class="fl">Tipo de ocorrência</div><div class="cat-grid" id="ocorr-tipo-grid">${tipoGrid}</div></div>
    <div><div class="fl">Colaborador</div><select class="sel" id="oc-colab"><option value="">Selecione</option>${funcOpts}</select></div>
    <div><div class="fl">Obra</div><select class="sel" id="oc-obra"><option value="">Selecione a obra</option>${obraOpts}</select></div>
    <div><div class="fl">Observação</div><textarea class="inp" id="oc-obs" rows="4" style="resize:none;" placeholder="Descreva a ocorrência detalhadamente..."></textarea></div>
    <button class="btn-pri" style="background:#8B0000;" onclick="salvarOcorr()">⚠️ Registrar ocorrência</button>
    ${ocorrs.length?`
    <div>
      <div class="fl">Filtrar histórico</div>
      <div class="filter-row">
        <select id="of-obra" onchange="renderOcorrFiltro()"><option value="">Todas as obras</option>${obraOpts}</select>
        <select id="of-colab" onchange="renderOcorrFiltro()"><option value="">Todos</option>${funcOpts}</select>
      </div>
      <div id="ocorr-hist-list">${hist}</div>
    </div>`:'<div class="empty"><div class="ei">✅</div><p>Nenhuma ocorrência registrada.</p></div>'}
  </div>\`;
}

let ocorrTipo='';
function selOcorrTipo(t){ocorrTipo=t;renderOcorr();}

function renderOcorrFiltro(){
  const oId=document.getElementById('of-obra')?.value;
  const cId=document.getElementById('of-colab')?.value;
  let lista=ocorrs;
  if(oId)lista=lista.filter(o=>o.obra_id===oId);
  if(cId)lista=lista.filter(o=>o.colaborador_id===cId);
  const tipos=[
    {k:'atraso',i:'⏰',l:'Atraso'},{k:'qualidade',i:'🔨',l:'Qualidade'},
    {k:'conduta',i:'⚠️',l:'Conduta'},{k:'acidente',i:'🚨',l:'Acidente'},
    {k:'material',i:'📦',l:'Material'},{k:'outro',i:'📝',l:'Outro'}
  ];
  const el=document.getElementById('ocorr-hist-list');if(!el)return;
  el.innerHTML=lista.map(o=>{
    const u=users.find(x=>x.id===o.colaborador_id);
    const ob=obras.find(x=>x.id===o.obra_id);
    const tObj=tipos.find(t=>t.k===o.tipo);
    return`<div class="hist-item" style="border-left:3px solid var(--red);">
      <div class="hi-ico">${(tObj&&tObj.i)||'⚠️'}</div>
      <div class="hi-body">
        <div class="hi-t">${(u&&u.apelido)||'—'} · ${(tObj&&tObj.l)||o.tipo||'—'}</div>
        <div class="hi-s">${(ob&&ob.nome)||'—'}</div>
        ${o.observacao?`<div class="hi-s" style="font-style:italic;">"${o.observacao}"</div>`:''}
      </div>
      <div class="hi-right">
        <div class="hi-d">${fmtD(o.data)}</div>
        <div class="hi-d">${o.hora||''}</div>
        ${U.tipo==='admin'?`<button onclick="delOcorr('${o.id}')" style="background:transparent;border:none;cursor:pointer;color:var(--red);font-size:11px;margin-top:3px;">🗑</button>`:''}
      </div>
    </div>`;}).join('')||'<div class="empty"><p>Nenhum resultado.</p></div>';
}

async function salvarOcorr(){
  if(!ocorrTipo){toast('⚠️ Selecione o tipo.');return;}
  const cId=document.getElementById('oc-colab')?.value;
  const oId=document.getElementById('oc-obra')?.value;
  const obs=document.getElementById('oc-obs')?.value.trim();
  if(!cId){toast('⚠️ Selecione o colaborador.');return;}
  if(!obs){toast('⚠️ Descreva a ocorrência.');return;}
  const r=await dbI('ocorrencias',{
    colaborador_id:cId,obra_id:oId||null,tipo:ocorrTipo,
    observacao:obs,registrado_por:U.id,data:hoje(),hora:hora()
  });
  if(r){
    toast('⚠️ Ocorrência registrada!');
    ocorrs=[r,...ocorrs];ocorrTipo='';
    renderOcorr();
  }
}

async function delOcorr(id){
  if(!confirm('Excluir esta ocorrência?'))return;
  await dbD('ocorrencias',id);
  ocorrs=ocorrs.filter(o=>o.id!==id);
  renderOcorr();toast('🗑 Excluída.');
}

// ══ DASHBOARD ══
function renderDash(){
  const el=document.getElementById('t-dash');if(!el)return;
  const totalFat=lancs.reduce((s,l)=>s+(l.total||0),0);
  const totalM2=lancs.reduce((s,l)=>s+(l.area_m2||0),0);
  const totalDesp=desps.reduce((s,d)=>s+(d.valor||0),0);
  const obraFat={};lancs.forEach(l=>{obraFat[l.obra_id]=(obraFat[l.obra_id]||0)+(l.total||0);});
  const maxO=Math.max(1,...Object.values(obraFat));
  const obrasBars=obras.map(o=>`
    <div class="bar-row">
      <div class="bar-lbl">${o.nome}</div>
      <div class="bar-track"><div class="bar-fill" style="width:${Math.round(((obraFat[o.id]||0)/maxO)*100)}%"></div></div>
      <div class="bar-val">${fmtK(obraFat[o.id]||0)}</div>
    </div>`).join('');
  const userFat={};lancs.forEach(l=>{userFat[l.usuario_id]=(userFat[l.usuario_id]||0)+(l.total||0);});
  const maxU=Math.max(1,...Object.values(userFat));
  const userBars=users.filter(u=>userFat[u.id]).sort((a,b)=>(userFat[b.id]||0)-(userFat[a.id]||0)).slice(0,6).map(u=>`
    <div class="bar-row">
      <div class="bar-lbl">${u.apelido}</div>
      <div class="bar-track"><div class="bar-fill" style="width:${Math.round(((userFat[u.id]||0)/maxU)*100)}%"></div></div>
      <div class="bar-val">${fmtK(userFat[u.id]||0)}</div>
    </div>`).join('');
  el.innerHTML=`
  <div class="hero" style="background:var(--dark)"><p>Visão geral executiva</p><h2>Dashboard Admin</h2></div>
  <div class="pad">
    <div class="stat3">
      <div class="stat"><div class="sv">${fmtK(totalFat)}</div><div class="sl">Faturado</div></div>
      <div class="stat"><div class="sv">${totalM2.toFixed(0)}m²</div><div class="sl">Produção</div></div>
      <div class="stat"><div class="sv">${obras.filter(o=>o.status==='ativa').length}</div><div class="sl">Obras ativas</div></div>
    </div>
    <div class="stat-grid">
      <div class="stat"><div class="sv">${fmtK(totalDesp)}</div><div class="sl">Total despesas</div></div>
      <div class="stat"><div class="sv">${lancs.length>0?'R$\u00a0'+(totalFat/lancs.length).toLocaleString('pt-BR',{maximumFractionDigits:0}):'—'}</div><div class="sl">Ticket médio</div></div>
    </div>
    <div class="card"><div class="card-title">💰 Faturamento por obra</div><div class="bar-wrap">${obrasBars||'<p style="font-size:12px;color:var(--sub);">Nenhum dado.</p>'}</div></div>
    <div class="card"><div class="card-title">👷 Produção por funcionário</div><div class="bar-wrap">${userBars||'<p style="font-size:12px;color:var(--sub);">Nenhum dado.</p>'}</div></div>
  </div>`;
}

// ══ DESPESAS ══
function renderDesp(){
  const el=document.getElementById('t-desp');if(!el)return;
  const obraOpts=obras.map(o=>`<option value="${o.id}">${o.nome}</option>`).join('');
  const catItems=[
    {k:'Combustível',i:'⛽'},{k:'Ferramentas',i:'🔧'},{k:'Insumos',i:'📦'},
    {k:'Transporte',i:'🚛'},{k:'Alimentação',i:'🍽️'},{k:'Manutenção',i:'⚙️'},
    {k:'EPIs',i:'🦺'},{k:'Outros',i:'📌'}
  ];
  const catHtml=catItems.map(c=>`<div class="cat-btn${catSel===c.k?' on':''}" onclick="selCat('${c.k}')"><span class="ci">${c.i}</span>${c.k}</div>`).join('');
  const total=desps.reduce((s,d)=>s+(d.valor||0),0);
  const hist=desps.slice(0,5).map(d=>{
    const o=obras.find(x=>x.id===d.obra_id);
    return`<div class="hist-item">
      <div class="hi-ico">${catItems.find(c=>c.k===d.categoria)?.i||'💰'}</div>
      <div class="hi-body"><div class="hi-t">${d.descricao}</div>
        <div class="hi-s">${d.categoria} · ${(o&&o.nome)||'Geral'}</div></div>
      <div class="hi-right"><div class="hi-v">${fmt(d.valor)}</div><div class="hi-d">${fmtD(d.data)}</div></div>
    </div>`;}).join('');
  el.innerHTML=`
  <div class="hero" style="background:var(--dark)"><p>Gestão financeira</p><h2>Controle de Despesas</h2></div>
  <div class="pad">
    <div><div class="fl">Categoria</div><div class="cat-grid" id="cat-grid">${catHtml}</div></div>
    <div><div class="fl">Descrição</div><input class="inp" type="text" id="d-desc" placeholder="Ex: Abastecimento Strada"></div>
    <div class="row2">
      <div><div class="fl">Valor R$</div><input class="inp" type="number" id="d-valor" placeholder="0,00"></div>
      <div><div class="fl">Data</div><input class="inp" type="date" id="d-data" value="${hoje()}"></div>
    </div>
    <div><div class="fl">Obra (opcional)</div><select class="sel" id="d-obra"><option value="">Geral</option>${obraOpts}</select></div>
    <div><div class="fl">Responsável</div><input class="inp" type="text" id="d-resp" placeholder="Ex: Leandro"></div>
    <div><div class="fl">Observação</div><input class="inp" type="text" id="d-obs" placeholder="Opcional"></div>
    <button class="btn-gold" onclick="salvarDesp()">💾 Registrar despesa</button>
    <div style="display:flex;justify-content:space-between;align-items:center;padding:4px 0;">
      <span style="font-size:11px;color:var(--sub);">${desps.length} registros</span>
      <span style="font-size:13px;font-weight:700;color:var(--red);">${fmtK(total)} total</span>
    </div>
    ${hist||'<div class="empty"><div class="ei">💸</div><p>Nenhuma despesa registrada.</p></div>'}
  </div>`;
}

function selCat(c){catSel=c;renderDesp();}

async function salvarDesp(){
  if(!catSel){toast('⚠️ Selecione a categoria.');return;}
  const desc=document.getElementById('d-desc')?.value.trim();
  const valor=parseFloat(document.getElementById('d-valor')?.value)||0;
  const data=document.getElementById('d-data')?.value;
  if(!desc){toast('⚠️ Informe a descrição.');return;}
  if(!valor){toast('⚠️ Informe o valor.');return;}
  const r=await dbI('despesas',{
    obra_id:document.getElementById('d-obra')?.value||null,
    categoria:catSel,descricao:desc,valor,
    responsavel:document.getElementById('d-resp')?.value.trim(),
    observacao:document.getElementById('d-obs')?.value.trim(),
    data:data||hoje()
  });
  if(r){toast('✅ Despesa registrada!');desps=[r,...desps];catSel='';renderDesp();}
}

// ══ AVISOS ══
function renderAvisos(){
  const el=document.getElementById('t-aviso');if(!el)return;
  const chipMap={geral:'chip-g',urgente:'chip-u',informativo:'chip-i'};
  const borderMap={geral:'var(--gold)',urgente:'var(--red)',informativo:'var(--blue)'};
  const cards=avs.map(a=>`
    <div class="av-card" style="border-left-color:${borderMap[a.tipo]||'var(--gold)'};">
      <div class="av-header">
        <div class="av-title">${a.titulo}</div>
        <span class="chip ${chipMap[a.tipo]||'chip-g'}">${a.tipo}</span>
      </div>
      <div class="av-msg">${a.mensagem}</div>
      <div class="av-footer">
        <div class="av-time">${fmtD(a.data)} ${a.hora?'· '+a.hora:''}</div>
        ${U.tipo==='admin'?`<div class="av-btns">
          <button class="av-btn e" onclick="editAviso('${a.id}')">✏️ Editar</button>
          <button class="av-btn d" onclick="delAviso('${a.id}')">🗑 Excluir</button>
        </div>`:''}
      </div>
    </div>`).join('');
  el.innerHTML=`
  <div class="hero" style="background:var(--dark)"><p>Comunicação com a equipe</p><h2>📢 Avisos</h2></div>
  <div class="pad">
    ${U.tipo==='admin'?`<button class="btn-sec" onclick="showModal('aviso',null)">＋ Novo aviso</button>`:''}
    ${cards||'<div class="empty"><div class="ei">📢</div><p>Nenhum aviso publicado.</p></div>'}
  </div>`;
}

async function salvarAviso(){
  const titulo=document.getElementById('av-titulo')?.value.trim();
  const msg=document.getElementById('av-msg')?.value.trim();
  const tipo=document.getElementById('av-tipo')?.value;
  if(!titulo||!msg){toast('⚠️ Preencha título e mensagem.');return;}
  if(editAvId){
    await dbU('avisos',editAvId,{titulo,mensagem:msg,tipo});
    avs=avs.map(a=>a.id===editAvId?{...a,titulo,mensagem:msg,tipo}:a);
    toast('✅ Aviso atualizado!');
  } else {
    const r=await dbI('avisos',{titulo,mensagem:msg,tipo,autor_id:U.id,data:hoje(),hora:hora()});
    if(r){avs=[r,...avs];toast('📢 Aviso publicado!');}
  }
  closeModal('aviso');editAvId=null;renderAvisos();
}

function editAviso(id){
  const a=avs.find(x=>x.id===id);if(!a)return;
  editAvId=id;
  document.getElementById('av-titulo').value=a.titulo;
  document.getElementById('av-msg').value=a.mensagem;
  document.getElementById('av-tipo').value=a.tipo;
  document.getElementById('modal-aviso').classList.add('show');
}

async function delAviso(id){
  if(!confirm('Excluir este aviso?'))return;
  await dbD('avisos',id);avs=avs.filter(a=>a.id!==id);
  toast('🗑 Aviso excluído.');renderAvisos();
}

// ══ CONFIG SUBS ══
function openSub(id){
  document.getElementById('sub-'+id)?.classList.add('on');
  if(id==='obras')renderObrasCfg();
  if(id==='funcs')renderFuncs();
  if(id==='novofunc'){
    const oOpts=obras.map(o=>`<option value="${o.id}">${o.nome}</option>`).join('');
    const sel=document.getElementById('nf-obra');
    if(sel)sel.innerHTML='<option value="">Selecione</option>'+oOpts;
  }
}
function closeSub(id){document.getElementById('sub-'+id)?.classList.remove('on');}

async function salvarEmpresa(){
  const nome=document.getElementById('emp-nome')?.value.trim();
  if(!nome){toast('⚠️ Informe o nome.');return;}
  const empR=await fetch(SURL+'/rest/v1/empresa?select=*&limit=1',{headers:H});
  const empData=empR.ok?await empR.json():[];
  const data=empData;
  if((data&&data.length)){
    await dbU('empresa',data[0].id,{
      nome,slogan:document.getElementById('emp-slogan')?.value,
      cnpj:document.getElementById('emp-cnpj')?.value,
      telefone:document.getElementById('emp-tel')?.value,
      cidade:document.getElementById('emp-cidade')?.value
    });
  }
  document.getElementById('tb-logo').textContent=nome;
  toast('✅ Dados salvos!');
}

// OBRAS CFG
function renderObrasCfg(){
  const el=document.getElementById('obras-list');if(!el)return;
  el.innerHTML=obras.map(o=>`
    <div class="o-card">
      <div style="display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:6px;">
        <div><div style="font-size:14px;font-weight:700;">${o.nome}</div><div style="font-size:11px;color:var(--sub);">${o.cliente||'—'} · ${o.cidade||'—'}</div>
        ${o.tipo?`<span class="chip chip-g" style="margin-top:4px;">📋 ${o.tipo}</span>`:''}
        </div>
        <span class="chip ${o.status==='ativa'?'chip-ap':'chip-g'}">${o.status==='ativa'?'Ativa':'Concluída'}</span>
      </div>
      <div style="display:grid;grid-template-columns:1fr 1fr;gap:6px;margin-bottom:9px;">
        <div style="background:#fff;border-radius:8px;padding:7px 9px;"><div style="font-size:9px;color:var(--sub);">Contrato</div><div style="font-size:12px;font-weight:700;">${fmtK(o.contrato)}</div></div>
        <div style="background:#fff;border-radius:8px;padding:7px 9px;"><div style="font-size:9px;color:var(--sub);">Faturado</div><div style="font-size:12px;font-weight:700;">${fmtK(o.faturado)}</div></div>
      </div>
      <div style="margin-bottom:8px;">
        <div class="prog-lbl"><span>Progresso financeiro</span><span style="color:var(--gold);font-weight:700;">${o.contrato>0?Math.min(Math.round((o.faturado/o.contrato)*100),100):0}%</span></div>
        <div class="prog-track"><div class="prog-track-f" style="width:${o.contrato>0?Math.min(Math.round((o.faturado/o.contrato)*100),100):0}%"></div></div>
      </div>
      <div style="display:flex;gap:7px;">
        <button class="ub edit" onclick="showModal('obra','${o.id}')">✏️ Editar</button>
        <button class="ub del" onclick="delObra('${o.id}')">🗑 Excluir</button>
      </div>
    </div>`).join('')||'<div class="empty"><div class="ei">🏗️</div><p>Nenhuma obra.</p></div>';
}

// FUNCS CFG
function renderFuncs(){
  const el=document.getElementById('funcs-list');if(!el)return;
  const busca=(document.getElementById('busca-f')?.value||'').toLowerCase();
  const lista=users.filter(u=>u.apelido.toLowerCase().includes(busca)||u.nome.toLowerCase().includes(busca));
  el.innerHTML=lista.map(u=>`
    <div class="u-card" style="opacity:${u.ativo?1:.55};">
      <div style="display:flex;align-items:center;gap:10px;margin-bottom:10px;">
        <div class="u-av" style="background:${['#B8860B','#185FA5','#1D9E75','#534AB7','#2C1F00'][users.indexOf(u)%5]};">${u.apelido.slice(0,2).toUpperCase()}</div>
        <div style="flex:1;">
          <div style="font-size:13px;font-weight:700;">${u.apelido} <span class="chip chip-g">${u.tipo==='admin'?'Admin':u.tipo==='lider'?'Líder':'Func.'}</span></div>
          <div style="font-size:11px;color:var(--sub);">${u.nome}${!u.ativo?' · Desativado':''}</div>
          <div style="font-size:11px;color:var(--sub);">${u.telefone||''}</div>
        </div>
      </div>
      <div class="tipo-row">
        <button class="tb${u.tipo==='func'?' func':''}" onclick="setTipoUser('${u.id}','func')">👷 Func.</button>
        <button class="tb${u.tipo==='lider'?' lider':''}" onclick="setTipoUser('${u.id}','lider')">👑 Líder</button>
        <button class="tb${u.tipo==='admin'?' adm':''}" onclick="setTipoUser('${u.id}','admin')">🛡 Admin</button>
      </div>
      <div style="display:flex;gap:7px;">
        <button class="ub edit" onclick="abrirEditFunc('${u.id}')">✏️ Editar</button>
        <button class="ub tog2" onclick="toggleUser('${u.id}')">${u.ativo?'⏸ Desativar':'▶ Ativar'}</button>
        <button class="ub del" onclick="delUser('${u.id}')">🗑 Excluir</button>
      </div>
    </div>`).join('')||'<div class="empty"><p>Nenhum funcionário.</p></div>';
}

async function setTipoUser(id,tipo){
  await dbU('usuarios',id,{tipo});
  users=users.map(u=>u.id===id?{...u,tipo}:u);
  renderFuncs();toast('✅ Tipo atualizado: '+(tipo==='admin'?'Admin':tipo==='lider'?'Líder':'Funcionário'));
}
async function toggleUser(id){
  const u=users.find(x=>x.id===id);if(!u)return;
  await dbU('usuarios',id,{ativo:!u.ativo});
  users=users.map(x=>x.id===id?{...x,ativo:!x.ativo}:x);
  renderFuncs();toast(u.ativo?'⏸ Acesso desativado':'✅ Acesso ativado');
}
async function delUser(id){
  if(!confirm('Excluir este funcionário?'))return;
  await dbD('usuarios',id);users=users.filter(u=>u.id!==id);renderFuncs();toast('🗑 Removido.');
}

function selNT(t){
  novoTipo=t;
  ['func','lider','admin'].forEach(k=>{
    const b=document.getElementById('nt-'+k);if(b)b.className='tb'+(k===t?' '+(k==='func'?'func':k==='lider'?'lider':'adm'):'');
  });
}

async function cadastrarFunc(){
  const nome=document.getElementById('nf-nome')?.value.trim();
  const ap=document.getElementById('nf-apelido')?.value.trim();
  const pw=document.getElementById('nf-senha')?.value;
  if(!nome||!ap){toast('⚠️ Preencha nome e apelido.');return;}
  if(!pw||pw.length<6){toast('⚠️ Senha mínimo 6 caracteres.');return;}
  const r=await dbI('usuarios',{
    nome,apelido:ap,telefone:document.getElementById('nf-tel')?.value,
    tipo:novoTipo,obra_id:document.getElementById('nf-obra')?.value||null,
    rate_m2:parseFloat(document.getElementById('nf-rate')?.value)||35,
    meta_mensal:parseFloat(document.getElementById('nf-meta')?.value)||0,
    senha:pw,ativo:true
  });
  if(r){
    toast('✅ '+ap+' cadastrado como '+(novoTipo==='admin'?'Admin':novoTipo==='lider'?'Líder':'Funcionário')+'!');
    users=[...users,r];
    ['nf-nome','nf-apelido','nf-tel','nf-senha','nf-rate','nf-meta'].forEach(id=>{const e=document.getElementById(id);if(e)e.value='';});
    const sel=document.getElementById('nf-obra');if(sel)sel.value='';
    selNT('func');
  }
}

// MODAL OBRAS
function showModal(type,id){
  editObraId=null;
  if(type==='obra'){
    if(id){
      const o=obras.find(x=>x.id===id);if(!o)return;
      editObraId=id;
      document.getElementById('mo-t').textContent='Editar obra';
      document.getElementById('mo-nome').value=o.nome;
      document.getElementById('mo-tipo').value=o.tipo||'';
      document.getElementById('mo-cliente').value=o.cliente||'';
      document.getElementById('mo-cidade').value=o.cidade||'';
      document.getElementById('mo-andares').value=o.andares||'';
      document.getElementById('mo-contrato').value=o.contrato||'';
      document.getElementById('mo-inicio').value=o.inicio||'';
      document.getElementById('mo-entrega').value=o.entrega||'';
      document.getElementById('mo-status').value=o.status||'ativa';
    } else {
      document.getElementById('mo-t').textContent='Nova obra';
      ['mo-nome','mo-tipo','mo-cliente','mo-cidade','mo-andares','mo-contrato','mo-inicio','mo-entrega'].forEach(id=>{const e=document.getElementById(id);if(e)e.value='';});
      document.getElementById('mo-status').value='ativa';
    }
    document.getElementById('modal-obra').classList.add('show');
  } else if(type==='aviso'){
    editAvId=null;
    ['av-titulo','av-msg'].forEach(id=>{const e=document.getElementById(id);if(e)e.value='';});
    document.getElementById('av-tipo').value='geral';
    document.getElementById('modal-aviso').classList.add('show');
  }
}
function closeModal(t){document.getElementById('modal-'+t)?.classList.remove('show');}

async function salvarObra(){
  const nome=document.getElementById('mo-nome')?.value.trim();
  if(!nome){toast('⚠️ Informe o nome.');return;}
  const obj={
    nome,tipo:document.getElementById('mo-tipo')?.value,
    cliente:document.getElementById('mo-cliente')?.value,
    cidade:document.getElementById('mo-cidade')?.value,
    andares:parseInt(document.getElementById('mo-andares')?.value)||0,
    contrato:parseFloat(document.getElementById('mo-contrato')?.value)||0,
    inicio:document.getElementById('mo-inicio')?.value||null,
    entrega:document.getElementById('mo-entrega')?.value||null,
    status:document.getElementById('mo-status')?.value
  };
  if(editObraId){
    await dbU('obras',editObraId,obj);
    obras=obras.map(o=>o.id===editObraId?Object.assign({},o,obj):o);
    toast('🏗️ Obra atualizada!');
  } else {
    const r=await dbI('obras',obj);
    if(r){obras=[...obras,r];toast('🏗️ Obra cadastrada!');}
  }
  closeModal('obra');renderObrasCfg();renderLancar();
}

async function delObra(id){
  if(!confirm('Excluir esta obra?'))return;
  await dbD('obras',id);obras=obras.filter(o=>o.id!==id);renderObrasCfg();toast('🗑 Obra removida.');
}

function abrirCfg(){openSub('cfg');}
function logout(){if(confirm('Sair do sistema?')){location.reload();}}

let editFuncId=null;
function abrirEditFunc(id){
  const u=users.find(x=>x.id===id);if(!u)return;
  editFuncId=id;
  document.getElementById('ef-nome').value=u.nome||'';
  document.getElementById('ef-apelido').value=u.apelido||'';
  document.getElementById('ef-tel').value=u.telefone||'';
  document.getElementById('ef-rate').value=u.rate_m2||35;
  document.getElementById('ef-meta').value=u.meta_mensal||0;
  document.getElementById('ef-senha').value='';
  const sel=document.getElementById('ef-obra');
  sel.innerHTML='<option value="">Sem obra</option>'+obras.map(o=>`<option value="${o.id}"${u.obra_id===o.id?' selected':''}>${o.nome}</option>`).join('');
  document.getElementById('modal-editfunc').classList.add('show');
}

async function salvarEditFunc(){
  if(!editFuncId)return;
  const nome=document.getElementById('ef-nome').value.trim();
  const apelido=document.getElementById('ef-apelido').value.trim();
  if(!nome||!apelido){toast('⚠️ Preencha nome e apelido.');return;}
  const obj={
    nome,apelido,
    telefone:document.getElementById('ef-tel').value.trim(),
    obra_id:document.getElementById('ef-obra').value||null,
    rate_m2:parseFloat(document.getElementById('ef-rate').value)||35,
    meta_mensal:parseFloat(document.getElementById('ef-meta').value)||0,
  };
  const novaSenha=document.getElementById('ef-senha').value;
  if(novaSenha){
    if(novaSenha.length<6){toast('⚠️ Senha mínimo 6 caracteres.');return;}
    obj.senha=novaSenha;
  }
  const ok=await dbU('usuarios',editFuncId,obj);
  if(ok){
    users=users.map(function(u){return u.id===editFuncId?Object.assign({},u,obj):u;});
    if(editFuncId===U.id){U=Object.assign({},U,obj);}
    toast('✅ Funcionário atualizado!');
    closeModal('editfunc');
    renderFuncs();
  }
}
</script>
</body>
</html>
