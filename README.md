[canteiroflow (1).html](https://github.com/user-attachments/files/29399123/canteiroflow.1.html)
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>CanteiroFlow — Controle de Estoque</title>
<link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><rect width='100' height='100' rx='20' fill='%23E8521A'/><text y='.9em' font-size='80' x='10' fill='white' font-style='italic'>C</text></svg>">
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@latest/dist/tabler-icons.min.css">
<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2/dist/umd/supabase.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/react/18.2.0/umd/react.production.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/react-dom/18.2.0/umd/react-dom.production.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/babel-standalone/7.23.5/babel.min.js"></script>
<style>
*{box-sizing:border-box;margin:0;padding:0}
:root{--brand:#E8521A;--bg:#F7F6F4;--sf:#fff;--bd:#E4E2DE;--bds:#C8C5BF;--tx:#1A1814;--tx2:#6B6560;--tx3:#9B9690;--ok:#1D7A3B;--ok-bg:#EDFAF2;--wn:#92580A;--wn-bg:#FEF6E8;--dg:#B91C1C;--dg-bg:#FEF2F2;--inf:#1D4ED8;--inf-bg:#EFF6FF;--sb:#1C1A17;--smt:#706A62;--r:8px}
body{font-family:system-ui,-apple-system,sans-serif;background:var(--bg);color:var(--tx);min-height:100vh}
input,select,textarea,button{font-family:inherit}button{cursor:pointer}
::-webkit-scrollbar{width:4px;height:4px}::-webkit-scrollbar-thumb{background:var(--bds);border-radius:2px}
@keyframes fi{from{opacity:0;transform:translateY(5px)}to{opacity:1;transform:translateY(0)}}
@keyframes su{from{opacity:0;transform:translateY(10px)}to{opacity:1;transform:translateY(0)}}
.app{display:flex;min-height:100vh}
.sb{width:220px;flex-shrink:0;background:var(--sb);display:flex;flex-direction:column;height:100vh;position:sticky;top:0;overflow:auto}
.sb-logo{padding:16px 14px 13px;border-bottom:.5px solid rgba(255,255,255,.07);display:flex;align-items:center;gap:9px}
.sb-mark{width:28px;height:28px;background:var(--brand);border-radius:6px;display:flex;align-items:center;justify-content:center;font-weight:500;color:#fff;font-size:13px;font-style:italic;flex-shrink:0}
.sb-name{font-weight:500;font-size:14px;color:#EAE8E4}.sb-name span{color:var(--brand)}
.sb-nav{flex:1;padding:7px 6px}
.nb{display:flex;align-items:center;gap:9px;width:100%;padding:8px 10px;border-radius:7px;border:none;background:transparent;color:var(--smt);font-size:13px;font-weight:500;text-align:left;cursor:pointer;margin-bottom:1px;transition:all .1s}
.nb.on{background:rgba(232,82,26,.16);color:var(--brand);font-weight:500}
.nb:hover:not(.on){background:rgba(255,255,255,.06);color:#A89F97}
.nb i{font-size:15px;width:16px;text-align:center;flex-shrink:0}
.nb .cnt{margin-left:auto;background:#B91C1C;color:#fff;border-radius:20px;font-size:10px;font-weight:500;padding:1px 6px}
.sb-foot{padding:11px 13px;border-top:.5px solid rgba(255,255,255,.06)}
.sb-email{font-size:11px;color:var(--smt);overflow:hidden;text-overflow:ellipsis;white-space:nowrap;margin-bottom:2px}
.sb-role{font-size:10px;color:var(--brand);font-weight:500;text-transform:uppercase;letter-spacing:.07em;margin-bottom:8px}
.sb-out{font-size:12px;color:var(--smt);background:none;border:none;cursor:pointer;padding:0}
.main{flex:1;overflow:auto;min-width:0}
.page{padding:28px 32px;max-width:1100px;margin:0 auto;animation:fi .15s ease}
.pw{padding:28px 32px;max-width:1240px;margin:0 auto;animation:fi .15s ease}
.ph1{font-size:20px;font-weight:500;margin-bottom:3px}
.psub{font-size:13px;color:var(--tx2);margin-bottom:20px}
.card{background:var(--sf);border:.5px solid var(--bd);border-radius:10px;overflow:hidden}
.kpi{background:var(--sf);border:.5px solid var(--bd);border-radius:10px;padding:16px 18px}
.kpi.w{box-shadow:0 0 0 1.5px #EF9F27}.kpi.d{box-shadow:0 0 0 1.5px var(--dg)}
.kpi-l{font-size:10px;font-weight:500;color:var(--tx3);text-transform:uppercase;letter-spacing:.07em;margin-bottom:5px}
.kpi-v{font-size:26px;font-weight:500;font-family:monospace;line-height:1}
.kpi-v.w{color:var(--wn)}.kpi-v.d{color:var(--dg)}
.kpi-s{font-size:11px;color:var(--tx3);margin-top:4px}
.g2{display:grid;grid-template-columns:1fr 1fr;gap:12px}
.g3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:10px}
.g4{display:grid;grid-template-columns:repeat(4,1fr);gap:12px;margin-bottom:20px}
.tbl{width:100%;border-collapse:collapse;font-size:13px}
.th{padding:9px 14px;text-align:left;font-size:10px;font-weight:500;color:var(--tx3);text-transform:uppercase;letter-spacing:.07em;border-bottom:.5px solid var(--bd);background:#F7F6F4;white-space:nowrap}
.th.r{text-align:right}
.td{padding:10px 14px;border-bottom:.5px solid var(--bd);font-size:13px}
.td.mono{font-family:monospace;font-size:11px}.td.mt{color:var(--tx2)}.td.b{font-weight:500}.td.r{text-align:right}.td.dg{color:var(--dg);font-weight:500}.td.wn{color:var(--wn);font-weight:500}
.tr:hover .td{background:#FAFAF9}
.bdg{display:inline-flex;align-items:center;font-size:10px;font-weight:500;padding:2px 8px;border-radius:20px;white-space:nowrap;text-transform:uppercase;letter-spacing:.06em}
.bdg.ok{background:var(--ok-bg);color:var(--ok)}.bdg.wn{background:var(--wn-bg);color:var(--wn)}.bdg.dg{background:var(--dg-bg);color:var(--dg)}.bdg.mt{background:#F4F3F1;color:var(--tx3)}.bdg.inf{background:var(--inf-bg);color:var(--inf)}
.inp{width:100%;padding:8px 11px;border:.5px solid var(--bds);border-radius:var(--r);font-size:13px;background:var(--bg);color:var(--tx);outline:none;transition:border .15s}
.inp:focus{border-color:var(--brand);box-shadow:0 0 0 2px rgba(232,82,26,.1)}
.btn{display:inline-flex;align-items:center;justify-content:center;gap:6px;padding:8px 16px;border-radius:var(--r);font-size:13px;font-weight:500;cursor:pointer;border:none;transition:opacity .1s}
.btn.pr{background:var(--brand);color:#fff}.btn.sc{background:transparent;color:var(--tx);border:.5px solid var(--bds)}.btn.dk{background:var(--sb);color:#fff}.btn.sm{padding:5px 11px;font-size:12px}
.btn:disabled{opacity:.5;cursor:not-allowed}.btn:hover:not(:disabled){opacity:.85}.btn.fw{width:100%}
.pill{padding:4px 13px;border-radius:20px;border:.5px solid var(--bd);background:transparent;color:var(--tx2);font-size:12px;font-weight:500;cursor:pointer}
.pill.on{background:var(--sb);color:#fff;border-color:var(--sb)}
.pills{display:flex;gap:6px;flex-wrap:wrap;margin-bottom:14px}
.tabs{display:flex;border-bottom:.5px solid var(--bd);margin-bottom:16px}
.tab{padding:9px 16px;font-size:13px;font-weight:500;border:none;border-bottom:2px solid transparent;margin-bottom:-1px;background:none;color:var(--tx2);cursor:pointer}
.tab.on{border-bottom-color:var(--brand);color:var(--tx)}
.fld{margin-bottom:13px}.lbl{font-size:11px;font-weight:500;color:var(--tx2);text-transform:uppercase;letter-spacing:.07em;display:block;margin-bottom:5px}
.empty{padding:44px 20px;text-align:center;color:var(--tx3)}.empty i{font-size:28px;margin-bottom:10px;display:block}
.spin{padding:40px;text-align:center;color:var(--tx3);font-size:13px}
.chdr{padding:12px 16px;border-bottom:.5px solid var(--bd);display:flex;justify-content:space-between;align-items:center}.chdr-t{font-weight:500;font-size:14px}
.mbg{position:fixed;inset:0;z-index:1000;background:rgba(0,0,0,.5);display:flex;align-items:center;justify-content:center;padding:14px}
.modal{background:var(--sf);border-radius:10px;border:.5px solid var(--bd);width:100%;max-height:92vh;overflow:auto;box-shadow:0 24px 64px rgba(0,0,0,.22)}
.mhdr{padding:16px 22px;border-bottom:.5px solid var(--bd);display:flex;align-items:center;justify-content:space-between;position:sticky;top:0;background:var(--sf);z-index:1}
.mhdr-t{font-weight:500;font-size:15px}.mbdy{padding:22px}
.toast{position:fixed;bottom:20px;right:20px;z-index:9999;padding:12px 18px;border-radius:10px;font-size:13px;font-weight:500;color:#fff;max-width:320px;box-shadow:0 4px 20px rgba(0,0,0,.25);animation:su .2s ease}
.srch{position:relative;margin-bottom:13px}.srch i{position:absolute;left:10px;top:50%;transform:translateY(-50%);color:var(--tx3);font-size:15px;pointer-events:none}.srch .inp{padding-left:32px}
.tcard{background:var(--sf);border:.5px solid var(--bd);border-radius:10px;padding:16px;display:flex;flex-direction:column}
.scrd{background:var(--sf);border:.5px solid var(--bd);border-radius:10px;padding:14px 16px}
.rrow{background:var(--sf);border:.5px solid var(--bd);border-radius:10px;padding:12px 16px;display:flex;align-items:center;gap:12px;flex-wrap:wrap}
.bi{padding:4px 7px;border-radius:6px;border:.5px solid var(--bd);background:none;cursor:pointer;display:inline-flex;align-items:center}.bi.dg{border-color:rgba(185,28,28,.3);color:var(--dg)}
</style>
</head>
<body><div id="root"></div>
<script type="text/babel">
const{useState,useEffect,useCallback}=React;
const SB_URL="https://idcojjyrgdqridhdcekz.supabase.co";
const SB_KEY="eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImlkY29qanlyZ2RxcmlkaGRjZWt6Iiwicm9sZSI6ImFub24iLCJpYXQiOjE3Nzg1MTQwODgsImV4cCI6MjA5NDA5MDA4OH0.b3HPlt-aDvxTet4PZ-16_p4i9CiGEPRSC4iUxhj5Tr0";
let _db=null;const db=()=>{if(!_db)_db=supabase.createClient(SB_URL,SB_KEY);return _db;};
const fmtDate=v=>v?new Date((v.includes?.('T')?v:v+'T00:00:00')).toLocaleDateString('pt-BR'):'—';
const fmtDT=v=>v?new Date(v).toLocaleString('pt-BR'):'—';
const fmtBRL=v=>Number(v||0).toLocaleString('pt-BR',{style:'currency',currency:'BRL',minimumFractionDigits:0});
const daysUntil=d=>{const a=new Date(d+'T00:00:00').getTime(),b=new Date(new Date().toISOString().slice(0,10)+'T00:00:00').getTime();return Math.round((a-b)/86400000);};
const BM={OK:'ok',Baixo:'wn',Crítico:'dg',Inativo:'mt',entrada:'ok',saida:'wn',ajuste:'inf',pendente:'wn',falta_material:'dg',concluida:'ok',disponivel:'ok',em_uso:'wn',manutencao:'dg',baixada:'mt',ativo:'ok',encerrado:'mt',cancelado:'dg',planejada:'inf',em_andamento:'ok',pausada:'wn',low_stock:'wn',zero_stock:'dg'};
const BL={OK:'OK',Baixo:'Baixo',Crítico:'Crítico',Inativo:'Inativo',entrada:'Entrada',saida:'Saída',ajuste:'Ajuste',pendente:'Pendente',falta_material:'Falta material',concluida:'Concluída',disponivel:'Disponível',em_uso:'Em uso',manutencao:'Manutenção',baixada:'Baixada',ativo:'Ativo',encerrado:'Encerrado',cancelado:'Cancelado',planejada:'Planejada',em_andamento:'Em andamento',pausada:'Pausada',low_stock:'Baixo',zero_stock:'Zerado'};
const Bdg=({t,l})=><span className={`bdg ${BM[t]||'mt'}`}>{l||BL[t]||t}</span>;
const Btn=({children,onClick,v='pr',disabled,sm,type='button',fw})=><button type={type} onClick={onClick} disabled={disabled} className={`btn ${v}${sm?' sm':''}${fw?' fw':''}`}>{children}</button>;
const Fld=({label,children,req})=><div className="fld"><label className="lbl">{label}{req&&<span style={{color:'var(--dg)',marginLeft:2}}>*</span>}</label>{children}</div>;
const Inp=({value,onChange,type='text',req,min,placeholder,rows})=>rows?<textarea value={value} onChange={e=>onChange(e.target.value)} rows={rows} placeholder={placeholder||''} className="inp" style={{resize:'vertical'}}/>:<input type={type} value={value} onChange={e=>onChange(e.target.value)} required={req} min={min} placeholder={placeholder||''} className="inp"/>;
const Sel=({value,onChange,children})=><select value={value} onChange={e=>onChange(e.target.value)} className="inp">{children}</select>;
const Empty=({icon,text})=><div className="empty"><i className={`ti ${icon}`} aria-hidden="true"/><p style={{fontSize:13}}>{text}</p></div>;
const Spin=()=><div className="spin">Carregando…</div>;
const Pills=({items,active,onChange})=><div className="pills">{items.map(it=><button key={it.v} onClick={()=>onChange(it.v)} className={`pill${active===it.v?' on':''}`}>{it.l}</button>)}</div>;
const Tabs=({tabs,active,onChange})=><div className="tabs">{tabs.map(t=><button key={t.id} onClick={()=>onChange(t.id)} className={`tab${active===t.id?' on':''}`}>{t.label}</button>)}</div>;
const Kpi=({label,value,sub,w,d})=><div className={`kpi${w?' w':''}${d?' d':''}`}><p className="kpi-l">{label}</p><p className={`kpi-v${w?' w':''}${d?' d':''}`}>{value}</p>{sub&&<p className="kpi-s">{sub}</p>}</div>;
const Toast=({msg,onDone})=>{useEffect(()=>{const t=setTimeout(onDone,3500);return()=>clearTimeout(t);},[]);return<div className="toast" style={{background:msg?.startsWith('❌')?'#991B1B':'#1C1A17'}}>{msg}</div>;};
const Modal=({title,onClose,children,wide})=><div className="mbg" onClick={onClose}><div className="modal" style={{maxWidth:wide?820:500}} onClick={e=>e.stopPropagation()}><div className="mhdr"><span className="mhdr-t">{title}</span><button onClick={onClose} style={{background:'none',border:'none',fontSize:20,color:'var(--tx3)',cursor:'pointer'}}>×</button></div><div className="mbdy">{children}</div></div></div>;
async function checkStockAlert(materialId){
  const{data:mat}=await db().from('materials').select('id,name,sku,unit,quantity,min_stock,active').eq('id',materialId).maybeSingle();
  if(!mat||!mat.active||Number(mat.min_stock)<=0||Number(mat.quantity)>Number(mat.min_stock))return null;
  const since=new Date(Date.now()-86400000).toISOString();
  const{data:recent}=await db().from('stock_alert_log').select('id').eq('material_id',materialId).gte('alerted_at',since).limit(1).maybeSingle();
  if(recent)return null;
  const isCritical=Number(mat.quantity)===0;
  await db().from('stock_alert_log').insert({material_id:materialId,quantity_at_alert:mat.quantity,min_stock_at_alert:mat.min_stock,alert_type:isCritical?'zero_stock':'low_stock'}).catch(()=>{});
  const{data:roles}=await db().from('user_roles').select('user_id').in('role',['admin','almoxarife']);
  const uids=(roles||[]).map(r=>r.user_id);
  if(uids.length){const{data:profiles}=await db().from('profiles').select('id').in('id',uids).eq('approved',true);if((profiles||[]).length){await db().from('notifications').insert(profiles.map(p=>({user_id:p.id,title:isCritical?`⚠️ Zerado: ${mat.name}`:`📦 Baixo: ${mat.name}`,body:`${mat.sku} — ${mat.quantity}/${mat.min_stock} ${mat.unit}`,link:'/materiais'}))).catch(()=>{});}}
  return{isCritical,materialName:mat.name};
}
const AuthPage=({onLogin})=>{
  const[email,setEmail]=useState('');const[pass,setPass]=useState('');const[loading,setLoading]=useState(false);const[err,setErr]=useState('');
  const go=async e=>{e.preventDefault();setLoading(true);setErr('');const{error}=await db().auth.signInWithPassword({email,password:pass});if(error)setErr(error.message);else onLogin();setLoading(false);};
  return<div style={{minHeight:'100vh',display:'grid',placeItems:'center',background:'var(--bg)'}}>
    <div style={{width:360}}>
      <div style={{textAlign:'center',marginBottom:26}}>
        <div style={{display:'inline-flex',alignItems:'center',gap:10,marginBottom:8}}><div style={{width:36,height:36,background:'var(--brand)',borderRadius:8,display:'flex',alignItems:'center',justifyContent:'center',fontWeight:500,color:'#fff',fontSize:16,fontStyle:'italic'}}>C</div><span style={{fontWeight:500,fontSize:20}}>CANTEIRO<span style={{color:'var(--brand)'}}>FLOW</span></span></div>
        <p style={{color:'var(--tx2)',fontSize:13}}>Controle de estoque da obra</p>
      </div>
      <div className="card" style={{padding:24}}>
        <form onSubmit={go}>
          <Fld label="E-mail" req><Inp value={email} onChange={setEmail} type="email" placeholder="seu@email.com"/></Fld>
          <Fld label="Senha" req><Inp value={pass} onChange={setPass} type="password" placeholder="••••••••"/></Fld>
          {err&&<p style={{color:'var(--dg)',fontSize:12,marginBottom:12,padding:'7px 10px',background:'var(--dg-bg)',borderRadius:6}}>{err}</p>}
          <Btn type="submit" disabled={loading} fw>{loading?'Entrando…':'Entrar'}</Btn>
        </form>
      </div>
    </div>
  </div>;
};
const Dashboard=()=>{
  const[mats,setMats]=useState([]);const[movs,setMovs]=useState([]);const[loading,setLoading]=useState(true);
  useEffect(()=>{Promise.all([db().from('materials').select('*').order('name'),db().from('stock_movements').select('*,materials(name,sku,unit)').order('created_at',{ascending:false}).limit(10)]).then(([m,mv])=>{setMats(m.data||[]);setMovs(mv.data||[]);setLoading(false);});},[]);
  const active=mats.filter(m=>m.active!==false);const critical=active.filter(m=>Number(m.quantity)===0);const low=active.filter(m=>Number(m.quantity)>0&&Number(m.min_stock)>0&&Number(m.quantity)<=Number(m.min_stock));
  const today=new Date();today.setHours(0,0,0,0);const movToday=movs.filter(m=>new Date(m.created_at)>=today).length;
  if(loading)return<div className="page"><Spin/></div>;
  return<div className="page">
    <p className="ph1">Dashboard</p><p className="psub">Visão geral do almoxarifado</p>
    <div className="g4"><Kpi label="Total de itens" value={active.length} sub="Catálogo ativo"/><Kpi label="Estoque baixo" value={low.length} sub="Abaixo do mínimo" w={low.length>0}/><Kpi label="Sem estoque" value={critical.length} sub="Itens zerados" d={critical.length>0}/><Kpi label="Movim. hoje" value={movToday} sub="Entradas e saídas"/></div>
    <div className="g2">
      <div className="card"><div className="chdr"><span className="chdr-t">Materiais em alerta</span><span style={{fontSize:12,color:'var(--tx3)'}}>{critical.length+low.length} itens</span></div>
        {critical.length+low.length===0?<Empty icon="ti-circle-check" text="Nenhum material em alerta"/>:<table className="tbl"><thead><tr><th className="th">Material</th><th className="th r">Estoque</th><th className="th">Status</th></tr></thead><tbody>{[...critical,...low].slice(0,7).map(m=>{const d=Number(m.quantity)===0;return<tr key={m.id} className="tr"><td className="td b">{m.name}<span style={{display:'block',fontSize:10,fontFamily:'monospace',color:'var(--tx3)'}}>{m.sku}</span></td><td className={`td mono r ${d?'dg':'wn'}`}>{m.quantity} <span style={{fontWeight:400,fontSize:10,color:'var(--tx3)'}}>{m.unit}</span></td><td className="td"><Bdg t={d?'Crítico':'Baixo'}/></td></tr>;})}</tbody></table>}
      </div>
      <div className="card"><div className="chdr"><span className="chdr-t">Movimentações recentes</span></div>
        <div style={{padding:'8px 14px',maxHeight:320,overflow:'auto'}}>
          {movs.length===0?<Empty icon="ti-arrows-exchange" text="Nenhuma"/>:movs.map(mv=><div key={mv.id} style={{padding:'8px 0',borderBottom:'.5px solid var(--bd)',display:'flex',gap:9}}>
            <div style={{width:6,height:6,borderRadius:'50%',marginTop:5,flexShrink:0,background:mv.type==='entrada'?'var(--ok)':mv.type==='saida'?'var(--brand)':'#818CF8'}}/>
            <div style={{flex:1,minWidth:0}}><p style={{fontSize:11,fontWeight:500,color:mv.type==='entrada'?'var(--ok)':mv.type==='saida'?'var(--brand)':'#4338CA',textTransform:'uppercase',letterSpacing:'.05em'}}>{mv.type}</p><p style={{fontSize:13,fontWeight:500,overflow:'hidden',textOverflow:'ellipsis',whiteSpace:'nowrap'}}>{mv.materials?.name}</p><p style={{fontSize:11,color:'var(--tx3)',fontFamily:'monospace'}}>{mv.quantity} {mv.materials?.unit} · {fmtDT(mv.created_at)}</p></div>
          </div>)}
        </div>
      </div>
    </div>
  </div>;
};
const MatForm=({material,onClose,onSaved})=>{
  const[f,setF]=useState({sku:material?.sku||'',name:material?.name||'',category:material?.category||'',unit:material?.unit||'un',quantity:material?.quantity??0,min_stock:material?.min_stock??0,location:material?.location||''});
  const[saving,setSaving]=useState(false);const s=k=>v=>setF(p=>({...p,[k]:v}));
  const save=async e=>{e.preventDefault();setSaving(true);const p={...f,quantity:Number(f.quantity),min_stock:Number(f.min_stock),category:f.category||null,location:f.location||null};if(material)await db().from('materials').update(p).eq('id',material.id);else await db().from('materials').insert(p);setSaving(false);onSaved(material?'Material atualizado':'Material criado');};
  return<Modal title={material?'Editar material':'Novo material'} onClose={onClose}><form onSubmit={save}>
    <div className="g2"><Fld label="SKU" req><Inp value={f.sku} onChange={s('sku')}/></Fld><Fld label="Unidade" req><Inp value={f.unit} onChange={s('unit')}/></Fld></div>
    <Fld label="Nome" req><Inp value={f.name} onChange={s('name')}/></Fld>
    <div className="g2"><Fld label="Categoria"><Inp value={f.category} onChange={s('category')}/></Fld><Fld label="Localização"><Inp value={f.location} onChange={s('location')}/></Fld></div>
    <div className="g2"><Fld label="Quantidade"><Inp value={String(f.quantity)} onChange={s('quantity')} type="number" min="0"/></Fld><Fld label="Estoque mínimo"><Inp value={String(f.min_stock)} onChange={s('min_stock')} type="number" min="0"/></Fld></div>
    <div style={{display:'flex',gap:10,marginTop:4}}><Btn v="sc" onClick={onClose} fw>Cancelar</Btn><Btn type="submit" disabled={saving} fw>{saving?'Salvando…':'Salvar'}</Btn></div>
  </form></Modal>;
};
const MovForm=({material,onClose,onSaved})=>{
  const[type,setType]=useState('entrada');const[qty,setQty]=useState('');const[reason,setReason]=useState('');const[saving,setSaving]=useState(false);
  const save=async e=>{e.preventDefault();const n=Number(qty);if(!n||n<=0)return;setSaving(true);const{data:{user}}=await db().auth.getUser();await db().from('stock_movements').insert({material_id:material.id,type,quantity:n,reason:reason||null,performed_by:user?.id});let next=Number(material.quantity);if(type==='entrada')next+=n;else if(type==='saida')next=Math.max(0,next-n);else next=n;await db().from('materials').update({quantity:next}).eq('id',material.id);let r=null;if(type==='saida'||(type==='ajuste'&&next<Number(material.quantity)))r=await checkStockAlert(material.id).catch(()=>null);setSaving(false);onSaved(r);};
  return<Modal title={`Movimentar — ${material.name}`} onClose={onClose}><form onSubmit={save}>
    <div style={{marginBottom:13}}><label className="lbl">Tipo</label><div className="g3">{['entrada','saida','ajuste'].map(t=><button key={t} type="button" onClick={()=>setType(t)} style={{padding:'8px 0',borderRadius:8,fontSize:12,fontWeight:500,textTransform:'uppercase',letterSpacing:'.05em',border:type===t?'1.5px solid var(--brand)':'0.5px solid var(--bd)',background:type===t?'rgba(232,82,26,.07)':'transparent',color:type===t?'var(--brand)':'var(--tx2)',cursor:'pointer'}}>{t}</button>)}</div></div>
    <Fld label={type==='ajuste'?'Novo total':'Quantidade'} req><Inp value={qty} onChange={setQty} type="number" min="0"/></Fld>
    <Fld label="Observação"><Inp value={reason} onChange={setReason} placeholder="Opcional…"/></Fld>
    <div style={{fontSize:12,color:'var(--tx2)',marginBottom:14,padding:'9px 11px',background:'var(--bg)',borderRadius:8}}>Atual: <strong style={{fontFamily:'monospace'}}>{material.quantity} {material.unit}</strong>{Number(material.min_stock)>0&&<> · Mín: <strong style={{fontFamily:'monospace'}}>{material.min_stock}</strong></>}</div>
    <div style={{display:'flex',gap:10}}><Btn v="sc" onClick={onClose} fw>Cancelar</Btn><Btn type="submit" disabled={saving||!qty||Number(qty)<=0} fw>{saving?'Registrando…':'Registrar'}</Btn></div>
  </form></Modal>;
};
const Materiais=({roles,showToast})=>{
  const isStaff=roles.includes('admin')||roles.includes('almoxarife');
  const[items,setItems]=useState([]);const[loading,setLoading]=useState(true);const[q,setQ]=useState('');const[fs,setFs]=useState('todos');
  const[editing,setEditing]=useState(null);const[moveItem,setMoveItem]=useState(null);const[creating,setCreating]=useState(false);
  const load=useCallback(async()=>{const{data}=await db().from('materials').select('*').order('name');setItems(data||[]);setLoading(false);},[]);
  useEffect(()=>{load();},[load]);
  const toggleActive=async m=>{await db().from('materials').update({active:!m.active}).eq('id',m.id);showToast(m.active?'Material desativado':'Material reativado');load();};
  const remove=async m=>{if(!confirm(`Excluir "${m.name}"?`))return;await db().from('materials').delete().eq('id',m.id);showToast('Material excluído');load();};
  const filtered=items.filter(m=>{const match=[m.name,m.sku,m.category,m.location].filter(Boolean).join(' ').toLowerCase().includes(q.toLowerCase());if(!match)return false;if(fs==='todos')return true;if(fs==='critico')return Number(m.quantity)===0&&m.active!==false;if(fs==='baixo'){const q2=Number(m.quantity),mn=Number(m.min_stock);return q2>0&&mn>0&&q2<=mn&&m.active!==false;}if(fs==='ok'){const q2=Number(m.quantity),mn=Number(m.min_stock);return(mn===0||q2>mn)&&m.active!==false;}if(fs==='inativo')return m.active===false;return true;});
  const cnt={c:items.filter(m=>Number(m.quantity)===0&&m.active!==false).length,b:items.filter(m=>{const q=Number(m.quantity),mn=Number(m.min_stock);return q>0&&mn>0&&q<=mn&&m.active!==false;}).length};
  return<div className="pw">
    <div style={{display:'flex',justifyContent:'space-between',alignItems:'flex-end',marginBottom:16,flexWrap:'wrap',gap:10}}><div><p className="ph1">Materiais</p><p className="psub" style={{marginBottom:0}}>Catálogo · {items.length} itens</p></div>{isStaff&&<Btn onClick={()=>setCreating(true)}><i className="ti ti-plus" aria-hidden="true"/>Novo material</Btn>}</div>
    <Pills items={[{v:'todos',l:'Todos'},{v:'critico',l:`Crítico${cnt.c>0?` (${cnt.c})`:''}`},{v:'baixo',l:`Baixo${cnt.b>0?` (${cnt.b})`:''}`},{v:'ok',l:'OK'},{v:'inativo',l:'Inativos'}]} active={fs} onChange={setFs}/>
    <div className="srch"><i className="ti ti-search" aria-hidden="true"/><input value={q} onChange={e=>setQ(e.target.value)} placeholder="Buscar por nome, SKU, categoria ou local…" className="inp"/></div>
    <div className="card">{loading?<Spin/>:<table className="tbl">
      <thead><tr><th className="th">SKU</th><th className="th">Material</th><th className="th">Categoria</th><th className="th">Local</th><th className="th r">Estoque</th><th className="th r">Mín</th><th className="th">Status</th>{isStaff&&<th className="th"/>}</tr></thead>
      <tbody>{filtered.length===0&&<tr><td colSpan={8}><Empty icon="ti-package" text="Nenhum resultado."/></td></tr>}
      {filtered.map(m=>{const qty=Number(m.quantity),mn=Number(m.min_stock);const d=qty===0,low=!d&&mn>0&&qty<=mn;const status=m.active===false?'Inativo':d?'Crítico':low?'Baixo':'OK';return<tr key={m.id} className="tr" style={{opacity:m.active===false?.5:1}}>
        <td className="td mono mt">{m.sku}</td><td className="td b">{m.name}</td><td className="td mt">{m.category||'—'}</td><td className="td mono mt">{m.location||'—'}</td>
        <td className={`td mono r${d?' dg':low?' wn':''}`} style={{fontWeight:500}}>{m.quantity} <span style={{fontWeight:400,fontSize:11,color:'var(--tx3)'}}>{m.unit}</span></td>
        <td className="td mono r mt">{mn||'—'}</td><td className="td"><Bdg t={status}/></td>
        {isStaff&&<td className="td"><div style={{display:'flex',gap:3,justifyContent:'flex-end'}}>
          <button onClick={()=>setMoveItem(m)} className="bi" title="Movimentar"><i className="ti ti-arrows-exchange" style={{fontSize:13}} aria-hidden="true"/></button>
          <button onClick={()=>setEditing(m)} className="bi" title="Editar"><i className="ti ti-edit" style={{fontSize:13}} aria-hidden="true"/></button>
          <button onClick={()=>toggleActive(m)} className="bi"><i className={`ti ${m.active?'ti-player-pause':'ti-player-play'}`} style={{fontSize:13}} aria-hidden="true"/></button>
          <button onClick={()=>remove(m)} className="bi dg"><i className="ti ti-trash" style={{fontSize:13}} aria-hidden="true"/></button>
        </div></td>}
      </tr>;})}
      </tbody></table>}
    </div>
    {(creating||editing)&&<MatForm material={editing} onClose={()=>{setCreating(false);setEditing(null);}} onSaved={msg=>{load();showToast(msg);setCreating(false);setEditing(null);}}/>}
    {moveItem&&<MovForm material={moveItem} onClose={()=>setMoveItem(null)} onSaved={async r=>{load();showToast('Movimentação registrada');if(r)showToast(r.isCritical?`⚠️ Zerado: ${r.materialName}`:`📦 Baixo: ${r.materialName}`);setMoveItem(null);}}/>}
  </div>;
};
const Movimentos=()=>{
  const[items,setItems]=useState([]);const[loading,setLoading]=useState(true);const[tipo,setTipo]=useState('todos');
  useEffect(()=>{db().from('stock_movements').select('*,materials(name,sku,unit)').order('created_at',{ascending:false}).limit(150).then(({data})=>{setItems(data||[]);setLoading(false);});},[]);
  const filtered=tipo==='todos'?items:items.filter(m=>m.type===tipo);
  return<div className="page"><p className="ph1">Movimentações</p><p className="psub">Histórico de entradas e saídas</p>
    <Pills items={[{v:'todos',l:'Todos'},{v:'entrada',l:'Entradas'},{v:'saida',l:'Saídas'},{v:'ajuste',l:'Ajustes'}]} active={tipo} onChange={setTipo}/>
    <div className="card">{loading?<Spin/>:<table className="tbl"><thead><tr><th className="th">Tipo</th><th className="th">Material</th><th className="th r">Qtd</th><th className="th">Observação</th><th className="th">Data</th></tr></thead>
      <tbody>{filtered.length===0&&<tr><td colSpan={5}><Empty icon="ti-arrows-exchange" text="Nenhuma movimentação."/></td></tr>}
      {filtered.map(m=><tr key={m.id} className="tr"><td className="td"><Bdg t={m.type}/></td><td className="td"><p style={{fontWeight:500}}>{m.materials?.name}</p><p style={{fontSize:11,fontFamily:'monospace',color:'var(--tx3)'}}>{m.materials?.sku}</p></td><td className="td mono r b">{m.quantity} <span style={{fontWeight:400,fontSize:11,color:'var(--tx3)'}}>{m.materials?.unit}</span></td><td className="td mt">{m.reason||'—'}</td><td className="td mt" style={{whiteSpace:'nowrap',fontSize:12}}>{fmtDT(m.created_at)}</td></tr>)}
      </tbody></table>}
    </div></div>;
};
const SolForm=({onClose,onSaved})=>{
  const[title,setTitle]=useState('');const[dest,setDest]=useState('');const[notes,setNotes]=useState('');const[its,setIts]=useState([{material_id:'',quantity:1}]);const[mats,setMats]=useState([]);const[saving,setSaving]=useState(false);
  useEffect(()=>{db().from('materials').select('id,name,sku,unit,quantity').eq('active',true).order('name').then(({data})=>setMats(data||[]));},[]);
  const save=async e=>{e.preventDefault();const valid=its.filter(it=>it.material_id&&Number(it.quantity)>0);if(!valid.length){alert('Adicione ao menos um material');return;}setSaving(true);const{data:{user}}=await db().auth.getUser();const{data:req}=await db().from('kit_requests').insert({title:title.trim(),notes:notes||null,destination:dest||null,requested_by:user?.id,status:'pendente'}).select('id').single();if(req?.id)await db().from('kit_request_items').insert(valid.map(it=>({request_id:req.id,material_id:it.material_id,quantity:Number(it.quantity)})));setSaving(false);onSaved();};
  return<Modal title="Nova solicitação de kit" onClose={onClose} wide><form onSubmit={save}>
    <Fld label="Título" req><Inp value={title} onChange={setTitle} placeholder="Ex.: Kit elétrico — Pavimento 3"/></Fld>
    <div className="g2"><Fld label="Local de entrega"><Inp value={dest} onChange={setDest}/></Fld><Fld label="Observações"><Inp value={notes} onChange={setNotes}/></Fld></div>
    <div style={{marginBottom:13}}><div style={{display:'flex',justifyContent:'space-between',marginBottom:8}}><label className="lbl">Materiais *</label><button type="button" onClick={()=>setIts(a=>[...a,{material_id:'',quantity:1}])} style={{fontSize:12,color:'var(--brand)',fontWeight:500,background:'none',border:'none',cursor:'pointer'}}>+ Adicionar</button></div>
    {its.map((it,i)=><div key={i} style={{display:'flex',gap:7,alignItems:'center',marginBottom:7}}>
      <select value={it.material_id} onChange={e=>setIts(a=>a.map((x,idx)=>idx===i?{...x,material_id:e.target.value}:x))} className="inp" style={{flex:1}}><option value="">Selecione…</option>{mats.map(m=><option key={m.id} value={m.id}>{m.name} · {m.quantity} {m.unit}</option>)}</select>
      <input type="number" min="0" value={it.quantity} onChange={e=>setIts(a=>a.map((x,idx)=>idx===i?{...x,quantity:e.target.value}:x))} className="inp" style={{width:65}}/>
      <span style={{fontSize:11,color:'var(--tx3)',width:22}}>{mats.find(m=>m.id===it.material_id)?.unit||''}</span>
      <button type="button" onClick={()=>setIts(a=>a.filter((_,idx)=>idx!==i))} style={{padding:'5px 7px',borderRadius:6,border:'.5px solid rgba(185,28,28,.3)',background:'none',color:'var(--dg)',cursor:'pointer',fontSize:13}}>×</button>
    </div>)}</div>
    <div style={{display:'flex',gap:10}}><Btn v="sc" onClick={onClose} fw>Cancelar</Btn><Btn type="submit" disabled={saving} fw>{saving?'Enviando…':'Enviar'}</Btn></div>
  </form></Modal>;
};
const Solicitacoes=({roles,showToast})=>{
  const isStaff=roles.includes('admin')||roles.includes('almoxarife');
  const[items,setItems]=useState([]);const[loading,setLoading]=useState(true);const[filter,setFilter]=useState('todas');const[creating,setCreating]=useState(false);
  const load=useCallback(async()=>{const{data}=await db().from('kit_requests').select('*,kit_request_items(id,quantity,material_id,materials(name,sku,unit))').order('created_at',{ascending:false});setItems(data||[]);setLoading(false);},[]);
  useEffect(()=>{load();},[load]);
  const SM={pendente:{l:'Pendente'},falta_material:{l:'Falta material'},concluida:{l:'Concluída'}};
  const filtered=filter==='todas'?items:items.filter(r=>r.status===filter);
  const updStatus=async(id,status)=>{await db().from('kit_requests').update({status}).eq('id',id);showToast('Status atualizado');load();};
  const remove=async r=>{if(!confirm(`Excluir "${r.title}"?`))return;await db().from('kit_requests').delete().eq('id',r.id);showToast('Removida');load();};
  return<div className="page">
    <div style={{display:'flex',justifyContent:'space-between',alignItems:'flex-end',marginBottom:16}}><div><p className="ph1">Solicitações de kits</p><p className="psub" style={{marginBottom:0}}>Pedidos de montagem</p></div><Btn onClick={()=>setCreating(true)}><i className="ti ti-plus" aria-hidden="true"/>Nova</Btn></div>
    <Pills items={[{v:'todas',l:'Todas'},{v:'pendente',l:'Pendente'},{v:'falta_material',l:'Falta material'},{v:'concluida',l:'Concluída'}]} active={filter} onChange={setFilter}/>
    {loading?<Spin/>:filtered.length===0?<div className="card"><Empty icon="ti-clipboard-list" text="Nenhuma solicitação."/></div>:<div style={{display:'flex',flexDirection:'column',gap:10}}>
      {filtered.map(r=><div key={r.id} className="scrd">
        <div style={{display:'flex',justifyContent:'space-between',alignItems:'flex-start',marginBottom:10,gap:12}}><div><p style={{fontWeight:500,fontSize:14,marginBottom:2}}>{r.title}</p><p style={{fontSize:12,color:'var(--tx2)'}}>{fmtDT(r.created_at)}{r.destination&&<> · 📍 {r.destination}</>}</p></div><Bdg t={r.status}/></div>
        {r.notes&&<p style={{fontSize:13,color:'var(--tx2)',marginBottom:10,fontStyle:'italic'}}>{r.notes}</p>}
        <div style={{border:'.5px solid var(--bd)',borderRadius:8,marginBottom:10,overflow:'hidden'}}>
          {(r.kit_request_items||[]).map((it,i)=><div key={i} style={{display:'flex',justifyContent:'space-between',padding:'7px 12px',borderBottom:i<r.kit_request_items.length-1?'.5px solid var(--bd)':'none',fontSize:13}}><span><span style={{fontFamily:'monospace',fontSize:11,color:'var(--tx3)',marginRight:7}}>{it.materials?.sku}</span>{it.materials?.name}</span><span style={{fontFamily:'monospace',fontWeight:500}}>{it.quantity} <span style={{fontWeight:400,fontSize:11,color:'var(--tx3)'}}>{it.materials?.unit}</span></span></div>)}
          {(r.kit_request_items||[]).length===0&&<div style={{padding:'8px 12px',fontSize:12,color:'var(--tx3)'}}>Sem itens</div>}
        </div>
        {r.picked_up_at&&<div style={{marginBottom:10,padding:'7px 11px',background:'var(--ok-bg)',border:'.5px solid rgba(29,122,59,.2)',borderRadius:7,fontSize:12,color:'var(--ok)'}}>Retirado por <strong>{r.picked_up_by}</strong> em {fmtDT(r.picked_up_at)}</div>}
        {isStaff&&<div style={{display:'flex',justifyContent:'space-between',alignItems:'center',flexWrap:'wrap',gap:6}}><div style={{display:'flex',gap:5,flexWrap:'wrap'}}>{Object.entries(SM).map(([s,{l}])=><button key={s} onClick={()=>updStatus(r.id,s)} style={{padding:'4px 11px',borderRadius:6,border:'.5px solid var(--bd)',background:r.status===s?'var(--sb)':'transparent',color:r.status===s?'#fff':'var(--tx2)',fontSize:11,fontWeight:500,cursor:'pointer'}}>{l}</button>)}</div><button onClick={()=>remove(r)} style={{padding:'4px 9px',borderRadius:6,border:'.5px solid rgba(185,28,28,.3)',background:'none',color:'var(--dg)',fontSize:11,cursor:'pointer'}}>Excluir</button></div>}
      </div>)}
    </div>}
    {creating&&<SolForm onClose={()=>setCreating(false)} onSaved={()=>{load();showToast('Solicitação criada');setCreating(false);}}/>}
  </div>;
};
const ToolForm=({tool,onClose,onSaved})=>{
  const SML={disponivel:'Disponível',em_uso:'Em uso',manutencao:'Manutenção',baixada:'Baixada'};
  const[f,setF]=useState({name:tool?.name||'',code:tool?.code||'',category:tool?.category||'',location:tool?.location||'',status:tool?.status||'disponivel',notes:tool?.notes||''});
  const[saving,setSaving]=useState(false);const s=k=>v=>setF(p=>({...p,[k]:v}));
  const save=async e=>{e.preventDefault();if(!f.name.trim()||!f.code.trim()){alert('Nome e código obrigatórios');return;}setSaving(true);const p={...f,category:f.category||null,location:f.location||null,notes:f.notes||null};if(tool)await db().from('tools').update(p).eq('id',tool.id);else await db().from('tools').insert(p);setSaving(false);onSaved(tool?'Ferramenta atualizada':'Ferramenta cadastrada');};
  return<Modal title={tool?'Editar ferramenta':'Nova ferramenta'} onClose={onClose}><form onSubmit={save}>
    <div className="g2"><Fld label="Nome" req><Inp value={f.name} onChange={s('name')}/></Fld><Fld label="Código" req><Inp value={f.code} onChange={s('code')}/></Fld></div>
    <div className="g2"><Fld label="Categoria"><Inp value={f.category} onChange={s('category')}/></Fld><Fld label="Local"><Inp value={f.location} onChange={s('location')}/></Fld></div>
    <Fld label="Status"><Sel value={f.status} onChange={s('status')}>{Object.entries(SML).map(([v,l])=><option key={v} value={v}>{l}</option>)}</Sel></Fld>
    <Fld label="Observações"><Inp value={f.notes} onChange={s('notes')} rows={2}/></Fld>
    <div style={{display:'flex',gap:10,marginTop:4}}><Btn v="sc" onClick={onClose} fw>Cancelar</Btn><Btn type="submit" disabled={saving} fw>{saving?'Salvando…':'Salvar'}</Btn></div>
  </form></Modal>;
};
const RetiradaForm=({tools,onClose,onSaved})=>{
  const[toolId,setToolId]=useState('');const[by,setBy]=useState('');const[dest,setDest]=useState('');const[expected,setExpected]=useState('');const[saving,setSaving]=useState(false);
  const save=async e=>{e.preventDefault();if(!toolId||!by.trim()){alert('Informe ferramenta e responsável');return;}setSaving(true);const{data:{user}}=await db().auth.getUser();await db().from('tool_checkouts').insert({tool_id:toolId,withdrawn_by:by.trim(),recorded_by:user?.id,destination:dest||null,expected_return_at:expected?new Date(expected).toISOString():null});await db().from('tools').update({status:'em_uso'}).eq('id',toolId);setSaving(false);onSaved();};
  return<Modal title="Nova retirada de ferramenta" onClose={onClose}><form onSubmit={save}>
    <Fld label="Ferramenta" req><Sel value={toolId} onChange={setToolId}><option value="">Selecione…</option>{tools.map(t=><option key={t.id} value={t.id}>{t.name} ({t.code})</option>)}</Sel>{tools.length===0&&<p style={{fontSize:11,color:'var(--wn)',marginTop:3}}>Nenhuma disponível.</p>}</Fld>
    <Fld label="Retirado por" req><Inp value={by} onChange={setBy} placeholder="Nome completo"/></Fld>
    <div className="g2"><Fld label="Destino"><Inp value={dest} onChange={setDest}/></Fld><Fld label="Devolução prevista"><Inp value={expected} onChange={setExpected} type="date"/></Fld></div>
    <div style={{display:'flex',gap:10}}><Btn v="sc" onClick={onClose} fw>Cancelar</Btn><Btn type="submit" disabled={saving} fw>{saving?'Registrando…':'Registrar'}</Btn></div>
  </form></Modal>;
};
const ManutencaoDialog=({tool,canEdit,onClose,showToast})=>{
  const ML={preventiva:'Preventiva',corretiva:'Corretiva',calibracao:'Calibração',outro:'Outro'};
  const[items,setItems]=useState([]);const[loading,setLoading]=useState(true);const[adding,setAdding]=useState(false);
  const[f,setF]=useState({type:'corretiva',description:'',cost:'',performedBy:'',startedAt:new Date().toISOString().slice(0,10),finishedAt:''});
  const s=k=>v=>setF(p=>({...p,[k]:v}));
  const load=useCallback(async()=>{const{data}=await db().from('tool_maintenances').select('*').eq('tool_id',tool.id).order('started_at',{ascending:false});setItems(data||[]);setLoading(false);},[tool.id]);
  useEffect(()=>{load();},[load]);
  const addM=async e=>{e.preventDefault();if(!f.description.trim()){alert('Informe a descrição');return;}const{data:{user}}=await db().auth.getUser();await db().from('tool_maintenances').insert({tool_id:tool.id,type:f.type,description:f.description.trim(),cost:f.cost?Number(f.cost):null,performed_by:f.performedBy||null,started_at:new Date(f.startedAt).toISOString(),finished_at:f.finishedAt?new Date(f.finishedAt).toISOString():null,recorded_by:user?.id||null});showToast('Manutenção registrada');setAdding(false);setF({type:'corretiva',description:'',cost:'',performedBy:'',startedAt:new Date().toISOString().slice(0,10),finishedAt:''});load();};
  const rem=async id=>{if(!confirm('Remover?'))return;await db().from('tool_maintenances').delete().eq('id',id);showToast('Removida');load();};
  return<Modal title={`Manutenção · ${tool.name}`} onClose={onClose}>
    {canEdit&&!adding&&<div style={{marginBottom:12}}><Btn sm onClick={()=>setAdding(true)}><i className="ti ti-plus" aria-hidden="true"/>Nova manutenção</Btn></div>}
    {canEdit&&adding&&<form onSubmit={addM} style={{background:'var(--bg)',border:'.5px solid var(--bd)',borderRadius:8,padding:14,marginBottom:14}}>
      <div className="g2"><Fld label="Tipo"><Sel value={f.type} onChange={s('type')}>{Object.entries(ML).map(([v,l])=><option key={v} value={v}>{l}</option>)}</Sel></Fld><Fld label="Custo (R$)"><Inp value={f.cost} onChange={s('cost')} type="number" min="0"/></Fld></div>
      <div className="g2"><Fld label="Início"><Inp value={f.startedAt} onChange={s('startedAt')} type="date"/></Fld><Fld label="Conclusão"><Inp value={f.finishedAt} onChange={s('finishedAt')} type="date"/></Fld></div>
      <Fld label="Responsável"><Inp value={f.performedBy} onChange={s('performedBy')}/></Fld>
      <Fld label="Descrição" req><Inp value={f.description} onChange={s('description')} rows={2}/></Fld>
      <div style={{display:'flex',gap:8}}><Btn sm v="sc" onClick={()=>setAdding(false)}>Cancelar</Btn><Btn sm type="submit">Salvar</Btn></div>
    </form>}
    {loading?<Spin/>:items.length===0?<p style={{textAlign:'center',color:'var(--tx3)',fontSize:13,padding:24}}>Nenhuma manutenção registrada.</p>:<div style={{display:'flex',flexDirection:'column',gap:9}}>
      {items.map(m=><div key={m.id} style={{border:'.5px solid var(--bd)',borderRadius:8,padding:11}}>
        <div style={{display:'flex',justifyContent:'space-between',marginBottom:5}}><div><span style={{fontSize:9,fontWeight:500,background:'var(--bg)',border:'.5px solid var(--bd)',borderRadius:3,padding:'1px 5px',textTransform:'uppercase'}}>{ML[m.type]||m.type}</span><span style={{fontSize:11,color:'var(--tx3)',marginLeft:7}}>{fmtDate(m.started_at.slice(0,10))}{m.finished_at&&<> → {fmtDate(m.finished_at.slice(0,10))}</>}</span></div>
        {canEdit&&<button onClick={()=>rem(m.id)} style={{padding:'1px 5px',borderRadius:3,border:'.5px solid rgba(185,28,28,.3)',background:'none',fontSize:12,color:'var(--dg)',cursor:'pointer'}}>✕</button>}</div>
        <p style={{fontSize:13,whiteSpace:'pre-line'}}>{m.description}</p>
        {(m.performed_by||m.cost!=null)&&<p style={{fontSize:11,color:'var(--tx3)',marginTop:4}}>{m.performed_by&&`Por: ${m.performed_by}`}{m.performed_by&&m.cost!=null&&' · '}{m.cost!=null&&`R$ ${Number(m.cost).toFixed(2)}`}</p>}
      </div>)}
    </div>}
  </Modal>;
};
const Ferramentas=({roles,showToast})=>{
  const isStaff=roles.includes('admin')||roles.includes('almoxarife');
  const[tab,setTab]=useState('ferramentas');const[tools,setTools]=useState([]);const[checkouts,setCheckouts]=useState([]);const[loading,setLoading]=useState(true);
  const[search,setSearch]=useState('');const[sf,setSf]=useState('todas');const[editTool,setEditTool]=useState(null);const[creating,setCreating]=useState(false);const[newRet,setNewRet]=useState(false);const[maintTool,setMaintTool]=useState(null);
  const loadAll=useCallback(async()=>{const[t,c]=await Promise.all([db().from('tools').select('*').order('name'),db().from('tool_checkouts').select('*').order('checkout_at',{ascending:false})]);setTools(t.data||[]);setCheckouts(c.data||[]);setLoading(false);},[]);
  useEffect(()=>{loadAll();},[loadAll]);
  const SML={disponivel:'Disponível',em_uso:'Em uso',manutencao:'Manutenção',baixada:'Baixada'};
  const filteredTools=tools.filter(t=>{if(sf!=='todas'&&t.status!==sf)return false;if(!search.trim())return true;const s=search.toLowerCase();return t.name.toLowerCase().includes(s)||t.code.toLowerCase().includes(s);});
  const devolver=async id=>{await db().from('tool_checkouts').update({returned_at:new Date().toISOString()}).eq('id',id);showToast('Devolução registrada');loadAll();};
  const remTool=async t=>{if(!confirm(`Excluir "${t.name}"?`))return;await db().from('tools').delete().eq('id',t.id);showToast('Ferramenta removida');loadAll();};
  return<div className="pw">
    <div style={{display:'flex',justifyContent:'space-between',alignItems:'flex-end',marginBottom:18,gap:10,flexWrap:'wrap'}}><div><p className="ph1">Ferramentas</p><p className="psub" style={{marginBottom:0}}>Cadastro, retiradas e manutenção</p></div><div style={{display:'flex',gap:8}}><Btn v="sc" sm onClick={()=>setNewRet(true)}><i className="ti ti-upload" aria-hidden="true"/>Nova retirada</Btn>{isStaff&&<Btn sm onClick={()=>setCreating(true)}><i className="ti ti-plus" aria-hidden="true"/>Nova</Btn>}</div></div>
    <Tabs tabs={[{id:'ferramentas',label:'Ferramentas'},{id:'retiradas',label:'Retiradas'}]} active={tab} onChange={setTab}/>
    {tab==='ferramentas'&&<><div style={{display:'flex',gap:10,marginBottom:14}}><div className="srch" style={{flex:1,marginBottom:0}}><i className="ti ti-search" aria-hidden="true"/><input value={search} onChange={e=>setSearch(e.target.value)} placeholder="Buscar…" className="inp"/></div><select value={sf} onChange={e=>setSf(e.target.value)} className="inp" style={{width:'auto'}}><option value="todas">Todos</option>{Object.entries(SML).map(([v,l])=><option key={v} value={v}>{l}</option>)}</select></div>
    {loading?<Spin/>:filteredTools.length===0?<div className="card"><Empty icon="ti-tool" text="Nenhuma ferramenta."/></div>:<div style={{display:'grid',gridTemplateColumns:'repeat(auto-fill,minmax(220px,1fr))',gap:12}}>
      {filteredTools.map(t=>{const open=checkouts.find(c=>c.tool_id===t.id&&!c.returned_at);return<div key={t.id} className="tcard">
        <div style={{display:'flex',justifyContent:'space-between',gap:7,marginBottom:9}}><div style={{minWidth:0}}><p style={{fontWeight:500,fontSize:13,overflow:'hidden',textOverflow:'ellipsis',whiteSpace:'nowrap'}}>{t.name}</p><p style={{fontSize:11,fontFamily:'monospace',color:'var(--tx3)'}}>{t.code}</p></div><Bdg t={t.status}/></div>
        <div style={{fontSize:12,color:'var(--tx2)',flex:1,marginBottom:10}}>{t.category&&<p>{t.category}</p>}{t.location&&<p>{t.location}</p>}{open&&<p style={{fontWeight:500,color:'var(--wn)',marginTop:3}}>Com: {open.withdrawn_by}</p>}</div>
        <div style={{display:'flex',gap:5,flexWrap:'wrap'}}>
          <button onClick={()=>setMaintTool(t)} style={{padding:'4px 9px',borderRadius:6,border:'.5px solid var(--bd)',background:'none',fontSize:12,cursor:'pointer'}}><i className="ti ti-tool" style={{fontSize:12,marginRight:3}} aria-hidden="true"/>Manutenção</button>
          {isStaff&&<><button onClick={()=>setEditTool(t)} className="bi"><i className="ti ti-edit" style={{fontSize:12}} aria-hidden="true"/></button><button onClick={()=>remTool(t)} className="bi dg"><i className="ti ti-trash" style={{fontSize:12}} aria-hidden="true"/></button></>}
        </div>
      </div>;})}
    </div>}</>}
    {tab==='retiradas'&&<div style={{display:'flex',flexDirection:'column',gap:9}}>
      {checkouts.length===0?<div className="card"><Empty icon="ti-upload" text="Nenhuma retirada."/></div>:checkouts.map(c=>{const tool=tools.find(t=>t.id===c.tool_id);const open=!c.returned_at;return<div key={c.id} className="rrow"><div style={{width:7,height:7,borderRadius:'50%',flexShrink:0,background:open?'var(--wn)':'var(--ok)'}}/>
        <div style={{flex:1,minWidth:160}}><p style={{fontWeight:500,fontSize:13}}>{tool?.name||'—'} <span style={{fontFamily:'monospace',fontSize:11,color:'var(--tx3)'}}>({tool?.code})</span></p><p style={{fontSize:12,color:'var(--tx2)'}}>Retirou: <strong>{c.withdrawn_by}</strong>{c.destination&&<> · {c.destination}</>}</p></div>
        <div style={{fontSize:12,color:'var(--tx2)',textAlign:'right'}}><p>{fmtDT(c.checkout_at)}</p>{c.returned_at?<p style={{color:'var(--ok)'}}>Dev.: {fmtDT(c.returned_at)}</p>:c.expected_return_at?<p>Prev.: {fmtDate(c.expected_return_at.slice(0,10))}</p>:<p style={{color:'var(--wn)'}}>Em aberto</p>}</div>
        {open&&<Btn sm v="sc" onClick={()=>devolver(c.id)}><i className="ti ti-download" aria-hidden="true"/>Devolver</Btn>}
      </div>;})}
    </div>}
    {(creating||editTool)&&<ToolForm tool={editTool} onClose={()=>{setCreating(false);setEditTool(null);}} onSaved={msg=>{loadAll();showToast(msg);setCreating(false);setEditTool(null);}}/>}
    {newRet&&<RetiradaForm tools={tools.filter(t=>t.status==='disponivel')} onClose={()=>setNewRet(false)} onSaved={()=>{loadAll();showToast('Retirada registrada');setNewRet(false);}}/>}
    {maintTool&&<ManutencaoDialog tool={maintTool} canEdit={isStaff} onClose={()=>setMaintTool(null)} showToast={showToast}/>}
  </div>;
};
const LocacaoForm=({contract,projects,onClose,onSaved})=>{
  const today=new Date().toISOString().slice(0,10);
  const[f,setF]=useState({supplier:contract?.supplier||'',contact:contract?.contact||'',delivery_date:contract?.delivery_date||today,expiration_date:contract?.expiration_date||today,notify_days_before:contract?.notify_days_before??7,project_id:contract?.project_id||'',status:contract?.status||'ativo',notes:contract?.notes||''});
  const[formItems,setFI]=useState([{equipment:'',quantity:1,unit:'un',monthly_cost:0,notes:''}]);
  const[saving,setSaving]=useState(false);const s=k=>v=>setF(p=>({...p,[k]:v}));
  const setI=(i,k,v)=>setFI(a=>a.map((it,idx)=>idx===i?{...it,[k]:v}:it));
  useEffect(()=>{if(contract){db().from('rental_contract_items').select('*').eq('contract_id',contract.id).then(({data})=>{if(data&&data.length>0)setFI(data);else setFI([{equipment:contract.equipment,quantity:contract.quantity,unit:contract.unit,monthly_cost:contract.monthly_cost,notes:''}]);});}},[]);
  const total=formItems.reduce((s,i)=>s+Number(i.monthly_cost||0),0);
  const save=async e=>{e.preventDefault();const clean=formItems.filter(i=>i.equipment.trim());if(!f.supplier.trim()||!clean.length){alert('Informe fornecedor e ao menos um equipamento');return;}setSaving(true);const first=clean[0];const payload={...f,equipment:clean.length===1?first.equipment:`${first.equipment} (+${clean.length-1})`,quantity:first.quantity,unit:first.unit,monthly_cost:total,project_id:f.project_id||null,notes:f.notes||null,contact:f.contact||null,notify_days_before:Number(f.notify_days_before)};let cid=contract?.id;if(contract)await db().from('rental_contracts').update(payload).eq('id',contract.id);else{const{data:{user}}=await db().auth.getUser();const{data}=await db().from('rental_contracts').insert({...payload,created_by:user?.id||null}).select('id').single();cid=data?.id;}if(cid){await db().from('rental_contract_items').delete().eq('contract_id',cid);await db().from('rental_contract_items').insert(clean.map(i=>({contract_id:cid,equipment:i.equipment,quantity:Number(i.quantity)||0,unit:i.unit||'un',monthly_cost:Number(i.monthly_cost)||0,notes:i.notes||null})));}setSaving(false);onSaved(contract?'Contrato atualizado':'Contrato cadastrado');};
  return<Modal title={contract?'Editar contrato':'Novo contrato de locação'} onClose={onClose} wide><form onSubmit={save}>
    <div className="g2"><Fld label="Fornecedor" req><Inp value={f.supplier} onChange={s('supplier')}/></Fld><Fld label="Contato"><Inp value={f.contact} onChange={s('contact')} placeholder="Telefone ou e-mail"/></Fld></div>
    <div className="g3"><Fld label="Entrega" req><Inp value={f.delivery_date} onChange={s('delivery_date')} type="date"/></Fld><Fld label="Vencimento" req><Inp value={f.expiration_date} onChange={s('expiration_date')} type="date"/></Fld><Fld label="Avisar X dias antes"><Inp value={String(f.notify_days_before)} onChange={s('notify_days_before')} type="number" min="0"/></Fld></div>
    <div className="g2"><Fld label="Obra vinculada"><Sel value={f.project_id} onChange={s('project_id')}><option value="">Nenhuma</option>{projects.map(p=><option key={p.id} value={p.id}>{p.name}</option>)}</Sel></Fld><Fld label="Status"><Sel value={f.status} onChange={s('status')}><option value="ativo">Ativo</option><option value="encerrado">Encerrado</option><option value="cancelado">Cancelado</option></Sel></Fld></div>
    <Fld label="Observações do contrato"><Inp value={f.notes} onChange={s('notes')} rows={2}/></Fld>
    <div style={{marginBottom:14}}><div style={{display:'flex',justifyContent:'space-between',alignItems:'center',marginBottom:10}}><label className="lbl">Equipamentos do contrato</label><button type="button" onClick={()=>setFI(a=>[...a,{equipment:'',quantity:1,unit:'un',monthly_cost:0,notes:''}])} style={{fontSize:12,color:'var(--brand)',fontWeight:500,background:'none',border:'none',cursor:'pointer'}}>+ Adicionar item</button></div>
    {formItems.map((it,i)=><div key={i} style={{border:'.5px solid var(--bd)',borderRadius:8,padding:12,marginBottom:8}}>
      <div style={{display:'flex',justifyContent:'space-between',marginBottom:8}}><span style={{fontSize:11,color:'var(--tx3)'}}>Item {i+1}</span>{formItems.length>1&&<button type="button" onClick={()=>setFI(a=>a.filter((_,idx)=>idx!==i))} style={{background:'none',border:'none',cursor:'pointer',color:'var(--tx3)',fontSize:16}}>×</button>}</div>
      <Fld label="Equipamento" req><Inp value={it.equipment} onChange={v=>setI(i,'equipment',v)}/></Fld>
      <div className="g3"><Fld label="Qtd"><Inp value={String(it.quantity)} onChange={v=>setI(i,'quantity',v)} type="number" min="0"/></Fld><Fld label="Unidade"><Inp value={it.unit} onChange={v=>setI(i,'unit',v)}/></Fld><Fld label="Custo mensal (R$)"><Inp value={String(it.monthly_cost)} onChange={v=>setI(i,'monthly_cost',v)} type="number" min="0"/></Fld></div>
      <Fld label="Obs."><Inp value={it.notes||''} onChange={v=>setI(i,'notes',v)}/></Fld>
    </div>)}
    <p style={{fontSize:12,color:'var(--tx2)'}}>Total mensal: <strong>{fmtBRL(total)}</strong></p></div>
    <div style={{display:'flex',gap:10}}><Btn v="sc" onClick={onClose} fw>Cancelar</Btn><Btn type="submit" disabled={saving} fw>{saving?'Salvando…':contract?'Salvar':'Cadastrar'}</Btn></div>
  </form></Modal>;
};
const Locacoes=({roles,showToast})=>{
  const canEdit=roles.includes('admin')||roles.includes('almoxarife');
  const[items,setItems]=useState([]);const[projects,setProjects]=useState([]);const[ibc,setIbc]=useState({});const[expanded,setExpanded]=useState({});
  const[loading,setLoading]=useState(true);const[filter,setFilter]=useState('todos');const[open,setOpen]=useState(false);const[editing,setEditing]=useState(null);
  const load=useCallback(async()=>{const[{data:c},{data:p},{data:ci}]=await Promise.all([db().from('rental_contracts').select('*').order('expiration_date',{ascending:true}),db().from('projects').select('id,name').order('name'),db().from('rental_contract_items').select('*')]);setItems(c||[]);setProjects(p||[]);const map={};for(const it of(ci||[])){(map[it.contract_id]=map[it.contract_id]||[]).push(it);}setIbc(map);setLoading(false);},[]);
  useEffect(()=>{load();},[load]);
  const ctotal=(c,list)=>{if(list&&list.length>0)return list.reduce((s,i)=>s+Number(i.monthly_cost||0),0);return Number(c.monthly_cost||0);};
  const filtered=items.filter(c=>{const d=daysUntil(c.expiration_date);if(filter==='ativos')return c.status==='ativo';if(filter==='encerrados')return c.status!=='ativo';if(filter==='vencendo')return c.status==='ativo'&&d>=0&&d<=c.notify_days_before;if(filter==='vencidos')return c.status==='ativo'&&d<0;return true;});
  const ativos=items.filter(i=>i.status==='ativo');const vencendo=ativos.filter(i=>{const d=daysUntil(i.expiration_date);return d>=0&&d<=i.notify_days_before;}).length;const vencidos=ativos.filter(i=>daysUntil(i.expiration_date)<0).length;const custoMensal=ativos.reduce((s,i)=>s+ctotal(i,ibc[i.id]),0);
  const setStatus=async(c,status)=>{await db().from('rental_contracts').update({status}).eq('id',c.id);showToast('Status atualizado');load();};
  const remove=async c=>{if(!confirm('Excluir contrato?'))return;await db().from('rental_contracts').delete().eq('id',c.id);showToast('Contrato excluído');load();};
  return<div className="pw">
    <div style={{display:'flex',justifyContent:'space-between',alignItems:'flex-end',marginBottom:18,gap:10,flexWrap:'wrap'}}><div><p className="ph1">Locações de equipamentos</p><p className="psub" style={{marginBottom:0}}>Controle de contratos com aviso de vencimento</p></div>{canEdit&&<Btn onClick={()=>{setEditing(null);setOpen(true);}}><i className="ti ti-plus" aria-hidden="true"/>Novo contrato</Btn>}</div>
    <div className="g4"><Kpi label="Contratos ativos" value={ativos.length} sub="Em vigor"/><Kpi label="A vencer" value={vencendo} w={vencendo>0} sub="Nos próximos dias"/><Kpi label="Vencidos" value={vencidos} d={vencidos>0} sub="Requer ação"/><Kpi label="Custo mensal" value={fmtBRL(custoMensal)} sub="Contratos ativos"/></div>
    <Pills items={[{v:'todos',l:'Todos'},{v:'ativos',l:'Ativos'},{v:'vencendo',l:'A vencer'},{v:'vencidos',l:'Vencidos'},{v:'encerrados',l:'Encerrados'}]} active={filter} onChange={setFilter}/>
    <div className="card">{loading?<Spin/>:filtered.length===0?<Empty icon="ti-file-text" text="Nenhum contrato encontrado."/>:
      <table className="tbl"><thead><tr><th className="th" style={{width:28}}/><th className="th">Equipamento</th><th className="th">Fornecedor</th><th className="th">Vencimento</th><th className="th">Status</th><th className="th r">Custo/mês</th>{canEdit&&<th className="th"/>}</tr></thead>
      <tbody>{filtered.flatMap(c=>{const d=daysUntil(c.expiration_date);const isA=c.status==='ativo';const alert=isA&&d<=c.notify_days_before;const over=isA&&d<0;const list=ibc[c.id]||[];const isExp=expanded[c.id];const proj=projects.find(p=>p.id===c.project_id);
        return[<tr key={c.id} className="tr"><td className="td" style={{textAlign:'center'}}>{list.length>1&&<button onClick={()=>setExpanded(p=>({...p,[c.id]:!p[c.id]}))} style={{background:'none',border:'none',cursor:'pointer',fontSize:13,color:'var(--tx3)'}}>{isExp?'▾':'▸'}</button>}</td>
          <td className="td"><p style={{fontWeight:500}}>{list.length>1?`${list.length} equipamentos`:list[0]?.equipment||c.equipment}</p>{proj&&<p style={{fontSize:11,color:'var(--tx3)'}}>{proj.name}</p>}</td>
          <td className="td"><p>{c.supplier}</p>{c.contact&&<p style={{fontSize:11,color:'var(--tx2)'}}>{c.contact}</p>}</td>
          <td className="td" style={{whiteSpace:'nowrap'}}>{fmtDate(c.expiration_date)}{alert&&<span style={{marginLeft:5,fontSize:10,fontWeight:500,padding:'1px 6px',borderRadius:20,background:over?'var(--dg-bg)':'var(--wn-bg)',color:over?'var(--dg)':'var(--wn)'}}>{over?`${Math.abs(d)}d venc.`:d===0?'hoje':`${d}d`}</span>}</td>
          <td className="td"><Bdg t={c.status}/></td><td className="td r b">{fmtBRL(ctotal(c,list))}</td>
          {canEdit&&<td className="td"><div style={{display:'flex',gap:3,justifyContent:'flex-end'}}>
            {c.status==='ativo'&&<><button onClick={()=>setStatus(c,'encerrado')} className="bi" title="Encerrar">✓</button><button onClick={()=>setStatus(c,'cancelado')} className="bi" title="Cancelar">✕</button></>}
            <button onClick={()=>{setEditing(c);setOpen(true);}} className="bi"><i className="ti ti-edit" style={{fontSize:12}} aria-hidden="true"/></button>
            <button onClick={()=>remove(c)} className="bi dg"><i className="ti ti-trash" style={{fontSize:12}} aria-hidden="true"/></button>
          </div></td>}
        </tr>,
        isExp&&list.length>0&&<tr key={c.id+'-exp'} style={{background:'#FAFAF9'}}><td/><td colSpan={canEdit?6:5} style={{padding:'8px 14px'}}>
          <p style={{fontSize:9,fontWeight:500,color:'var(--tx3)',textTransform:'uppercase',marginBottom:6}}>Equipamentos do contrato</p>
          <table style={{width:'100%',fontSize:12}}><tbody>{list.map((it,i)=><tr key={i} style={{borderTop:i>0?'.5px solid var(--bd)':'none'}}><td style={{padding:'3px 5px'}}>{it.equipment}</td><td style={{padding:'3px 5px',color:'var(--tx2)'}}>{Number(it.quantity)} {it.unit}</td><td style={{padding:'3px 5px',fontWeight:500}}>{fmtBRL(it.monthly_cost)}</td><td style={{padding:'3px 5px',color:'var(--tx2)'}}>{it.notes||''}</td></tr>)}</tbody></table>
        </td></tr>].filter(Boolean);})}</tbody>
      </table>}
    </div>
    {open&&<LocacaoForm contract={editing} projects={projects} onClose={()=>{setOpen(false);setEditing(null);}} onSaved={msg=>{load();showToast(msg);setOpen(false);setEditing(null);}}/>}
  </div>;
};
const Obras=()=>{
  const[obras,setObras]=useState([]);const[loading,setLoading]=useState(true);
  const SC={planejada:'#4338CA',em_andamento:'var(--ok)',pausada:'var(--wn)',concluida:'var(--tx3)'};const SL={planejada:'Planejada',em_andamento:'Em andamento',pausada:'Pausada',concluida:'Concluída'};
  useEffect(()=>{db().from('projects').select('*').order('name').then(({data})=>{setObras(data||[]);setLoading(false);});},[]);
  return<div className="page"><p className="ph1">Obras</p><p className="psub">Projetos e controle de andamento</p>
    {loading?<Spin/>:obras.length===0?<div className="card"><Empty icon="ti-building" text="Nenhuma obra cadastrada."/></div>:<div style={{display:'grid',gridTemplateColumns:'repeat(auto-fill,minmax(280px,1fr))',gap:14}}>
      {obras.map(o=>{const c=SC[o.status]||'var(--tx3)';return<div key={o.id} className="card" style={{padding:18}}>
        <div style={{display:'flex',justifyContent:'space-between',alignItems:'flex-start',marginBottom:10,gap:10}}><div><p style={{fontWeight:500,fontSize:14,marginBottom:2}}>{o.name}</p>{o.code&&<p style={{fontSize:11,fontFamily:'monospace',color:'var(--tx3)'}}>{o.code}</p>}</div><span style={{fontSize:11,fontWeight:500,color:c,background:c+'18',padding:'2px 8px',borderRadius:20,whiteSpace:'nowrap'}}>{SL[o.status]||o.status}</span></div>
        {o.client&&<p style={{fontSize:12,color:'var(--tx2)',marginBottom:4}}><i className="ti ti-user" style={{fontSize:12,marginRight:4}} aria-hidden="true"/>{o.client}</p>}
        {o.address&&<p style={{fontSize:12,color:'var(--tx2)',marginBottom:4}}><i className="ti ti-map-pin" style={{fontSize:12,marginRight:4}} aria-hidden="true"/>{o.address}</p>}
        <div style={{display:'flex',justifyContent:'space-between',marginTop:12,paddingTop:10,borderTop:'.5px solid var(--bd)'}}><span style={{fontSize:11,color:'var(--tx3)'}}>{fmtDate(o.start_date)} → {fmtDate(o.end_date)}</span><span style={{fontSize:13,fontWeight:500}}>{fmtBRL(o.budget_total)}</span></div>
      </div>;})}
    </div>}
  </div>;
};
const Alertas=({roles,refreshCount})=>{
  const isAdmin=roles.includes('admin');
  const[logs,setLogs]=useState([]);const[lowMats,setLowMats]=useState([]);const[loading,setLoading]=useState(true);const[enabled,setEnabled]=useState(true);
  const load=useCallback(async()=>{setLoading(true);const[lr,mr,sr]=await Promise.all([db().from('stock_alert_log').select('id,alerted_at,quantity_at_alert,min_stock_at_alert,alert_type,materials(name,sku,unit)').order('alerted_at',{ascending:false}).limit(30),db().from('materials').select('id,name,sku,unit,quantity,min_stock').eq('active',true).gt('min_stock',0),isAdmin?db().from('app_settings').select('value').eq('key','stock_alerts_enabled').maybeSingle():Promise.resolve({data:null})]);setLogs(lr.data||[]);setLowMats((mr.data||[]).filter(m=>Number(m.quantity)<=Number(m.min_stock)));if(sr?.data)setEnabled(sr.data.value?.enabled!==false);setLoading(false);},[isAdmin]);
  useEffect(()=>{load();},[load]);
  const toggle=async()=>{const v=!enabled;await db().from('app_settings').upsert({key:'stock_alerts_enabled',value:{enabled:v},updated_at:new Date().toISOString()});setEnabled(v);};
  const scan=async()=>{let n=0;for(const m of lowMats){const r=await checkStockAlert(m.id);if(r)n++;}await load();if(refreshCount)refreshCount();alert(n>0?`${n} alerta(s) enviado(s).`:'Nenhum novo alerta — cooldown de 24h ativo.');};
  if(loading)return<div className="page"><Spin/></div>;
  return<div className="page"><p className="ph1">Alertas de estoque</p><p className="psub">Monitoramento automático de estoque mínimo</p>
    {isAdmin&&<div className="card" style={{padding:16,marginBottom:16}}>
      <div style={{display:'flex',alignItems:'center',justifyContent:'space-between',flexWrap:'wrap',gap:12}}>
        <div style={{display:'flex',alignItems:'center',gap:12}}><i className={`ti ${enabled?'ti-bell':'ti-bell-off'}`} style={{fontSize:20,color:enabled?'var(--ok)':'var(--tx3)'}} aria-hidden="true"/><div><p style={{fontWeight:500,fontSize:14,marginBottom:2}}>Alertas automáticos</p><p style={{fontSize:12,color:'var(--tx2)'}}>Notificação para admins e almoxarifes. Cooldown 24h por material.</p></div></div>
        <div style={{display:'flex',gap:10,alignItems:'center'}}>
          <button onClick={toggle} style={{width:40,height:22,borderRadius:11,border:'none',background:enabled?'var(--ok)':'var(--bds)',cursor:'pointer',position:'relative',flexShrink:0}}><span style={{position:'absolute',top:2,left:enabled?20:2,width:18,height:18,background:'#fff',borderRadius:'50%',boxShadow:'0 1px 3px rgba(0,0,0,.2)',transition:'left .15s'}}/></button>
          <span style={{fontSize:12,fontWeight:500,color:enabled?'var(--ok)':'var(--tx3)'}}>{enabled?'Ativo':'Inativo'}</span>
          <Btn sm v="dk" onClick={scan}><i className="ti ti-player-play" aria-hidden="true"/>Varredura agora</Btn>
        </div>
      </div>
    </div>}
    <div className="card" style={{marginBottom:14}}><div className="chdr"><span className="chdr-t">Materiais abaixo do mínimo agora</span><span style={{fontSize:12,color:'var(--tx3)'}}>{lowMats.length} itens</span></div>
      {lowMats.length===0?<Empty icon="ti-circle-check" text="Todos os materiais acima do mínimo"/>:<table className="tbl"><thead><tr><th className="th">Material</th><th className="th r">Atual</th><th className="th r">Mínimo</th><th className="th">Situação</th></tr></thead><tbody>{lowMats.map(m=>{const d=Number(m.quantity)===0;return<tr key={m.id} className="tr"><td className="td b">{m.name}<span style={{display:'block',fontSize:10,fontFamily:'monospace',color:'var(--tx3)'}}>{m.sku}</span></td><td className={`td mono r${d?' dg':' wn'}`} style={{fontWeight:500}}>{m.quantity} <span style={{fontWeight:400,fontSize:10,color:'var(--tx3)'}}>{m.unit}</span></td><td className="td mono r mt">{m.min_stock} {m.unit}</td><td className="td"><Bdg t={d?'Crítico':'Baixo'}/></td></tr>;})}</tbody></table>}
    </div>
    <div className="card"><div className="chdr"><span className="chdr-t">Histórico de alertas enviados</span><span style={{fontSize:12,color:'var(--tx3)'}}>Últimos 30</span></div>
      {logs.length===0?<Empty icon="ti-clipboard" text="Nenhum alerta enviado ainda"/>:<table className="tbl"><thead><tr><th className="th">Material</th><th className="th r">Qtd / Mín</th><th className="th">Tipo</th><th className="th">Quando</th></tr></thead><tbody>{logs.map(l=><tr key={l.id} className="tr"><td className="td b">{l.materials?.name||'—'}<span style={{display:'block',fontSize:10,fontFamily:'monospace',color:'var(--tx3)'}}>{l.materials?.sku}</span></td><td className={`td mono r ${l.alert_type==='zero_stock'?'dg':'wn'}`} style={{fontWeight:500}}>{l.quantity_at_alert}/{l.min_stock_at_alert} <span style={{fontWeight:400,fontSize:10,color:'var(--tx3)'}}>{l.materials?.unit}</span></td><td className="td"><Bdg t={l.alert_type}/></td><td className="td mt" style={{fontSize:12,whiteSpace:'nowrap'}}>{fmtDT(l.alerted_at)}</td></tr>)}</tbody></table>}
    </div>
  </div>;
};
const Usuarios=()=>{
  const[users,setUsers]=useState([]);const[loading,setLoading]=useState(true);
  useEffect(()=>{db().rpc('admin_list_profiles').then(({data})=>{setUsers(data||[]);setLoading(false);});},[]);
  return<div className="page"><p className="ph1">Usuários</p><p className="psub">Contas cadastradas no sistema</p>
    <div className="card">{loading?<Spin/>:<table className="tbl"><thead><tr><th className="th">Nome</th><th className="th">E-mail</th><th className="th">Status</th><th className="th">Cadastro</th></tr></thead><tbody>{users.length===0&&<tr><td colSpan={4}><Empty icon="ti-users" text="Nenhum usuário."/></td></tr>}{users.map(u=><tr key={u.id} className="tr"><td className="td b">{u.full_name||'—'}</td><td className="td mt">{u.email}</td><td className="td"><Bdg t={u.approved?'OK':'Baixo'}/></td><td className="td mt" style={{fontSize:12}}>{fmtDate(u.created_at)}</td></tr>)}</tbody></table>}</div>
  </div>;
};
const NAV=[{id:'dashboard',l:'Dashboard',i:'ti-layout-dashboard'},{id:'materiais',l:'Materiais',i:'ti-package'},{id:'movimentos',l:'Movimentações',i:'ti-arrows-exchange'},{id:'solicitacoes',l:'Solicitações',i:'ti-clipboard-list'},{id:'ferramentas',l:'Ferramentas',i:'ti-tool'},{id:'locacoes',l:'Locações',i:'ti-file-text'},{id:'obras',l:'Obras',i:'ti-building'},{id:'alertas',l:'Alertas estoque',i:'ti-bell'}];
const Sidebar=({page,setPage,user,roles,onLogout,alertCount})=>{
  const isAdmin=roles.includes('admin');const nav=[...NAV,...(isAdmin?[{id:'usuarios',l:'Usuários',i:'ti-users'}]:[])];
  return<aside className="sb">
    <div className="sb-logo"><div className="sb-mark">C</div><span className="sb-name">CANTEIRO<span>FLOW</span></span></div>
    <nav className="sb-nav">{nav.map(n=><button key={n.id} onClick={()=>setPage(n.id)} className={`nb${page===n.id?' on':''}`}><i className={`ti ${n.i}`} aria-hidden="true"/><span style={{flex:1}}>{n.l}</span>{n.id==='alertas'&&alertCount>0&&<span className="cnt">{alertCount}</span>}</button>)}</nav>
    <div className="sb-foot"><p className="sb-email">{user?.email}</p><p className="sb-role">{roles[0]||'—'}</p><button onClick={onLogout} className="sb-out">Sair →</button></div>
  </aside>;
};
const App=()=>{
  const[session,setSession]=useState(null);const[roles,setRoles]=useState([]);const[page,setPage]=useState('dashboard');const[toast,setToast]=useState(null);const[loading,setLoading]=useState(true);const[alertCount,setAlertCount]=useState(0);
  const showToast=msg=>setToast(msg);
  const refreshCount=useCallback(async()=>{const{count}=await db().from('stock_alert_log').select('id',{count:'exact',head:true}).gte('alerted_at',new Date(Date.now()-86400000).toISOString());setAlertCount(count||0);},[]);
  const loadRoles=useCallback(async uid=>{const{data}=await db().from('user_roles').select('role').eq('user_id',uid);setRoles((data||[]).map(r=>r.role));refreshCount();setLoading(false);},[refreshCount]);
  useEffect(()=>{db().auth.getSession().then(({data:{session:s}})=>{setSession(s);if(s)loadRoles(s.user.id);else setLoading(false);});const{data:{subscription}}=db().auth.onAuthStateChange((_,s)=>{setSession(s);if(s)loadRoles(s.user.id);else{setRoles([]);setLoading(false);}});return()=>subscription.unsubscribe();},[loadRoles]);
  const logout=async()=>{await db().auth.signOut();setPage('dashboard');};
  if(loading)return<div style={{minHeight:'100vh',display:'grid',placeItems:'center',background:'var(--bg)'}}><div style={{textAlign:'center'}}><div style={{display:'inline-flex',alignItems:'center',gap:10,marginBottom:12}}><div style={{width:34,height:34,background:'var(--brand)',borderRadius:8,display:'flex',alignItems:'center',justifyContent:'center',fontWeight:500,color:'#fff',fontSize:15,fontStyle:'italic'}}>C</div><span style={{fontWeight:500,fontSize:20}}>CANTEIRO<span style={{color:'var(--brand)'}}>FLOW</span></span></div><p style={{color:'var(--tx2)',fontSize:13}}>Carregando…</p></div></div>;
  if(!session)return<AuthPage onLogin={()=>{}}/>;
  const pages={dashboard:<Dashboard/>,materiais:<Materiais roles={roles} showToast={showToast}/>,movimentos:<Movimentos/>,solicitacoes:<Solicitacoes roles={roles} showToast={showToast}/>,ferramentas:<Ferramentas roles={roles} showToast={showToast}/>,locacoes:<Locacoes roles={roles} showToast={showToast}/>,obras:<Obras/>,alertas:<Alertas roles={roles} refreshCount={refreshCount}/>,usuarios:roles.includes('admin')?<Usuarios/>:<Dashboard/>};
  return<div className="app">
    <Sidebar page={page} setPage={setPage} user={session.user} roles={roles} onLogout={logout} alertCount={alertCount}/>
    <main className="main">{pages[page]||pages.dashboard}</main>
    {toast&&<Toast msg={toast} onDone={()=>setToast(null)}/>}
  </div>;
};
ReactDOM.render(<App/>,document.getElementById('root'));
</script>
</body>
</html>
