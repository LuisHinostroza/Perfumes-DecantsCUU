<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0" />
<meta name="apple-mobile-web-app-capable" content="yes" />
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
<meta name="theme-color" content="#1a1208" />
<title>Signature Decants CUU</title>
<link rel="manifest" href="data:application/json,{&quot;name&quot;:&quot;Signature Decants CUU&quot;,&quot;short_name&quot;:&quot;Decants&quot;,&quot;display&quot;:&quot;standalone&quot;,&quot;background_color&quot;:&quot;#faf7f4&quot;,&quot;theme_color&quot;:&quot;#1a1208&quot;}" />
<link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet" />
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
  body { font-family: 'DM Serif Display', Georgia, serif; background: #faf7f4; color: #1a1208; min-height: 100vh; }
  .sans { font-family: 'DM Sans', sans-serif; }

  /* Header */
  header { background: #1a1208; color: #f5e6c8; padding: 16px 20px; display: flex; justify-content: space-between; align-items: center; position: sticky; top: 0; z-index: 50; }
  .header-title { font-size: 20px; letter-spacing: .5px; }
  .header-sub { font-family: 'DM Sans', sans-serif; font-size: 11px; opacity: .55; margin-top: 2px; }
  .header-stat { text-align: right; }
  .header-stat-label { font-family: 'DM Sans', sans-serif; font-size: 10px; opacity: .5; }
  .header-stat-value { font-size: 18px; }

  /* Tabs */
  nav { background: #2d1f0e; display: flex; overflow-x: auto; }
  nav button { flex: 1; min-width: 80px; padding: 12px 6px; border: none; cursor: pointer; font-family: 'DM Sans', sans-serif; font-size: 12px; font-weight: 500; background: transparent; color: #c4a97d; border-bottom: 3px solid transparent; transition: all .2s; white-space: nowrap; }
  nav button.active { background: #f5e6c8; color: #1a1208; border-bottom: 3px solid #c9843a; }

  /* Main */
  main { padding: 16px; max-width: 680px; margin: 0 auto; padding-bottom: 40px; }

  /* Card */
  .card { background: #fff; border-radius: 12px; box-shadow: 0 1px 8px rgba(26,18,8,.07); }

  /* Buttons */
  .btn { background: #1a1208; color: #f5e6c8; border: none; border-radius: 8px; padding: 9px 16px; font-family: 'DM Sans', sans-serif; font-size: 13px; font-weight: 500; cursor: pointer; transition: opacity .15s; }
  .btn:hover { opacity: .85; }
  .btn.sec { background: transparent; color: #7a6a55; border: 1px solid #c4a97d; }
  .btn.danger { background: #fdf0ef; color: #c0392b; border: none; }
  .btn-sm { background: #f5f0ea; border: none; border-radius: 6px; padding: 4px 9px; cursor: pointer; font-size: 14px; }
  .btn-sm.danger { background: #fdf0ef; }

  /* Form */
  .field { margin-bottom: 12px; }
  .field label { display: block; font-family: 'DM Sans', sans-serif; font-size: 12px; font-weight: 500; color: #7a6a55; margin-bottom: 4px; }
  .field input, .field select { width: 100%; border: 1px solid #ddd4c4; border-radius: 7px; padding: 8px 10px; font-family: 'DM Sans', sans-serif; font-size: 14px; background: #faf7f4; color: #1a1208; }
  .field input:focus, .field select:focus { outline: none; border-color: #c9843a; }

  /* Section title */
  .stitle { font-family: 'DM Sans', sans-serif; font-size: 11px; font-weight: 600; text-transform: uppercase; letter-spacing: 2px; color: #c9843a; margin-bottom: 10px; }

  /* Stat grid */
  .stat-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-bottom: 20px; }
  .stat-card { background: #fff; border-radius: 12px; padding: 14px 16px; box-shadow: 0 1px 8px rgba(26,18,8,.07); }
  .stat-card .slabel { font-family: 'DM Sans', sans-serif; font-size: 10px; color: #9a8a75; text-transform: uppercase; letter-spacing: 1px; margin-bottom: 4px; }
  .stat-card .svalue { font-size: 16px; }
  .stat-card.big .svalue { font-size: 20px; font-weight: 700; }

  /* Empty state */
  .empty { text-align: center; font-family: 'DM Sans', sans-serif; color: #b0a090; padding: 32px 16px; font-size: 14px; }

  /* Spinner */
  .spinner { display: flex; justify-content: center; align-items: center; padding: 40px; }
  .spinner::after { content: ''; width: 28px; height: 28px; border: 3px solid #ddd4c4; border-top-color: #c9843a; border-radius: 50%; animation: spin .7s linear infinite; }
  @keyframes spin { to { transform: rotate(360deg); } }

  /* Toast */
  #toast { position: fixed; bottom: 24px; left: 50%; transform: translateX(-50%) translateY(80px); background: #1a1208; color: #f5e6c8; padding: 10px 20px; border-radius: 20px; font-family: 'DM Sans', sans-serif; font-size: 13px; transition: transform .3s; z-index: 200; white-space: nowrap; }
  #toast.show { transform: translateX(-50%) translateY(0); }

  /* Modal */
  .modal-bg { position: fixed; inset: 0; background: rgba(0,0,0,.45); display: flex; align-items: flex-end; justify-content: center; z-index: 100; }
  .modal { background: #faf7f4; border-radius: 16px 16px 0 0; padding: 20px; width: 100%; max-width: 500px; max-height: 88vh; overflow-y: auto; }
  .modal-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 16px; }
  .modal-header .title { font-size: 17px; font-weight: 600; }
  .modal-header .close { background: none; border: none; font-size: 22px; cursor: pointer; color: #7a6a55; }

  /* Sync badge */
  .sync { font-family: 'DM Sans', sans-serif; font-size: 10px; padding: 3px 8px; border-radius: 10px; }
  .sync.online { background: #e8f5e9; color: #27ae60; }
  .sync.offline { background: #fdf0ef; color: #c0392b; }

  /* Row item */
  .item { padding: 12px 14px; margin-bottom: 8px; }
  .item-title { font-weight: 500; font-size: 15px; }
  .item-sub { font-family: 'DM Sans', sans-serif; font-size: 12px; color: #7a6a55; margin-top: 2px; }
  .item-note { font-family: 'DM Sans', sans-serif; font-size: 12px; font-style: italic; color: #a09080; }
  .item-actions { display: flex; gap: 6px; }
  .stock-badge { font-family: 'DM Sans', sans-serif; font-weight: 700; font-size: 18px; }
  .stock-ok { color: #27ae60; } .stock-warn { color: #e67e22; } .stock-low { color: #c0392b; }

  /* Marca tag */
  .marca-tag { font-family: 'DM Sans', sans-serif; font-size: 11px; font-weight: 600; text-transform: uppercase; letter-spacing: 2px; color: #c9843a; margin-bottom: 8px; margin-top: 4px; }

  .row-flex { display: flex; justify-content: space-between; align-items: center; }
  .divider { border: none; border-top: 1px solid #efe8dc; margin: 4px 0; }
</style>
</head>
<body>

<header>
  <div>
    <div class="header-title">🌸 Signature Decants CUU</div>
    <div class="header-sub">Gestión de negocio · MXN</div>
  </div>
  <div class="header-stat">
    <div class="header-stat-label">Ganancia total</div>
    <div class="header-stat-value" id="hdr-ganancia" style="color:#b8e09a">$0.00</div>
  </div>
</header>

<nav>
  <button class="active" onclick="setTab(0)">📦 Stock</button>
  <button onclick="setTab(1)">🛒 Compras</button>
  <button onclick="setTab(2)">💸 Ventas</button>
  <button onclick="setTab(3)">📊 Finanzas</button>
</nav>

<main id="main-content"><div class="spinner"></div></main>

<div id="toast"></div>

<!-- Firebase -->
<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-app.js";
import {
  getFirestore, collection, doc, onSnapshot,
  addDoc, updateDoc, deleteDoc, query, orderBy, serverTimestamp
} from "https://www.gstatic.com/firebasejs/10.12.0/firebase-firestore.js";

const firebaseConfig = {
  apiKey: "AIzaSyAqKZxaBBt2x5N0ssI_IBtDFA-MqTvrfC8",
  authDomain: "signaturedecantscuu.firebaseapp.com",
  projectId: "signaturedecantscuu",
  storageBucket: "signaturedecantscuu.firebasestorage.app",
  messagingSenderId: "1096751110969",
  appId: "1:1096751110969:web:d77674190ec87fa88fa6e8"
};

const app = initializeApp(firebaseConfig);
const db = getFirestore(app);

// ─── STATE ────────────────────────────────────────────
let state = { productos: [], compras: [], ventas: [] };
let currentTab = 0;
const CANALES = ["Efectivo", "Transferencia", "Bizum", "Instagram", "Otra"];

// ─── UTILS ────────────────────────────────────────────
const fmt = n => new Intl.NumberFormat("es-MX", { style: "currency", currency: "MXN" }).format(n || 0);
const today = () => new Date().toISOString().split("T")[0];
const toast = (msg) => {
  const el = document.getElementById("toast");
  el.textContent = msg; el.classList.add("show");
  setTimeout(() => el.classList.remove("show"), 2200);
};
const esc = s => String(s || "").replace(/</g, "&lt;").replace(/>/g, "&gt;");

// ─── FIRESTORE LISTENERS ───────────────────────────────
onSnapshot(query(collection(db, "productos"), orderBy("marca")), snap => {
  state.productos = snap.docs.map(d => ({ id: d.id, ...d.data() }));
  render(); updateHeader();
});
onSnapshot(query(collection(db, "compras"), orderBy("ts", "desc")), snap => {
  state.compras = snap.docs.map(d => ({ id: d.id, ...d.data() }));
  render(); updateHeader();
});
onSnapshot(query(collection(db, "ventas"), orderBy("ts", "desc")), snap => {
  state.ventas = snap.docs.map(d => ({ id: d.id, ...d.data() }));
  render(); updateHeader();
});

// ─── HEADER ───────────────────────────────────────────
function updateHeader() {
  const ganancia = state.ventas.reduce((s, v) => s + (v.total - v.costoTotal), 0);
  const el = document.getElementById("hdr-ganancia");
  if (el) { el.textContent = fmt(ganancia); el.style.color = ganancia >= 0 ? "#b8e09a" : "#e09a9a"; }
}

// ─── TAB ROUTER ───────────────────────────────────────
window.setTab = (i) => {
  currentTab = i;
  document.querySelectorAll("nav button").forEach((b, idx) => b.classList.toggle("active", idx === i));
  render();
};
function render() {
  const el = document.getElementById("main-content");
  if (currentTab === 0) el.innerHTML = renderStock();
  else if (currentTab === 1) el.innerHTML = renderCompras();
  else if (currentTab === 2) el.innerHTML = renderVentas();
  else el.innerHTML = renderFinanzas();
}

// ─── STOCK TAB ────────────────────────────────────────
function renderStock() {
  const marcas = [...new Set(state.productos.map(p => p.marca))].sort();
  let html = `
    <div class="row-flex" style="margin-bottom:16px">
      <h2 style="font-size:20px">Inventario</h2>
      <button class="btn" onclick="openModal('nuevo-producto')">+ Añadir</button>
    </div>`;
  if (state.productos.length === 0) return html + `<div class="empty">Sin productos. Añade el primero.</div>`;
  for (const marca of marcas) {
    html += `<div class="marca-tag">${esc(marca)}</div>`;
    for (const p of state.productos.filter(x => x.marca === marca)) {
      const sc = p.stock <= 2 ? "stock-low" : p.stock <= 5 ? "stock-warn" : "stock-ok";
      html += `<div class="card item row-flex" style="margin-bottom:8px">
        <div>
          <div class="item-title">${esc(p.nombre)} ${p.ml ? `<span style="font-size:12px;color:#9a8a75">${p.ml}ml</span>` : ""}</div>
          <div class="item-sub">Costo: ${fmt(p.costo)} · Venta: ${fmt(p.precio)} · Margen: ${fmt(p.precio - p.costo)}</div>
        </div>
        <div style="display:flex;align-items:center;gap:10px">
          <span class="stock-badge ${sc}">${p.stock}</span>
          <div class="item-actions">
            <button class="btn-sm" onclick="openModal('editar-producto','${p.id}')">✏️</button>
            <button class="btn-sm danger" onclick="delProducto('${p.id}','${esc(p.nombre)}')">🗑️</button>
          </div>
        </div>
      </div>`;
    }
  }
  html += modalNuevoProducto() + modalEditarProducto();
  return html;
}

function modalNuevoProducto() {
  return `<div id="modal-nuevo-producto" class="modal-bg" style="display:none">
    <div class="modal">
      <div class="modal-header"><span class="title">Nuevo producto</span><button class="close" onclick="closeModal('nuevo-producto')">✕</button></div>
      <div class="field"><label>Marca</label><input id="np-marca" placeholder="Chanel"></div>
      <div class="field"><label>Nombre</label><input id="np-nombre" placeholder="No. 5 Mini"></div>
      <div class="field"><label>ml</label><input id="np-ml" type="number" placeholder="5"></div>
      <div class="field"><label>Stock inicial</label><input id="np-stock" type="number" placeholder="10"></div>
      <div class="field"><label>Costo unitario (MXN)</label><input id="np-costo" type="number" placeholder="85"></div>
      <div class="field"><label>Precio de venta (MXN)</label><input id="np-precio" type="number" placeholder="150"></div>
      <div style="display:flex;gap:8px;margin-top:8px">
        <button class="btn" onclick="saveNuevoProducto()">Guardar</button>
        <button class="btn sec" onclick="closeModal('nuevo-producto')">Cancelar</button>
      </div>
    </div>
  </div>`;
}

function modalEditarProducto() {
  return `<div id="modal-editar-producto" class="modal-bg" style="display:none">
    <div class="modal">
      <div class="modal-header"><span class="title">Editar producto</span><button class="close" onclick="closeModal('editar-producto')">✕</button></div>
      <input id="ep-id" type="hidden">
      <div class="field"><label>Marca</label><input id="ep-marca"></div>
      <div class="field"><label>Nombre</label><input id="ep-nombre"></div>
      <div class="field"><label>ml</label><input id="ep-ml" type="number"></div>
      <div class="field"><label>Stock</label><input id="ep-stock" type="number"></div>
      <div class="field"><label>Costo unitario (MXN)</label><input id="ep-costo" type="number"></div>
      <div class="field"><label>Precio de venta (MXN)</label><input id="ep-precio" type="number"></div>
      <div style="display:flex;gap:8px;margin-top:8px">
        <button class="btn" onclick="saveEditarProducto()">Guardar</button>
        <button class="btn sec" onclick="closeModal('editar-producto')">Cancelar</button>
      </div>
    </div>
  </div>`;
}

// ─── COMPRAS TAB ──────────────────────────────────────
function renderCompras() {
  const opts = state.productos.map(p => `<option value="${p.id}">${esc(p.marca)} · ${esc(p.nombre)}</option>`).join("");
  let html = `
    <div class="row-flex" style="margin-bottom:16px">
      <h2 style="font-size:20px">Compras</h2>
      <button class="btn" onclick="openModal('nueva-compra')">+ Registrar</button>
    </div>
    <div id="modal-nueva-compra" class="modal-bg" style="display:none">
      <div class="modal">
        <div class="modal-header"><span class="title">Nueva compra</span><button class="close" onclick="closeModal('nueva-compra')">✕</button></div>
        <div class="field"><label>Producto</label><select id="nc-prod"><option value="">-- Selecciona --</option>${opts}</select></div>
        <div class="field"><label>Cantidad</label><input id="nc-cant" type="number" min="1" placeholder="10"></div>
        <div class="field"><label>Costo total (MXN)</label><input id="nc-costo" type="number" placeholder="850"></div>
        <div class="field"><label>Proveedor</label><input id="nc-prov" placeholder="Nombre o tienda"></div>
        <div class="field"><label>Fecha</label><input id="nc-fecha" type="date" value="${today()}"></div>
        <div class="field"><label>Nota</label><input id="nc-nota" placeholder="Opcional"></div>
        <div style="display:flex;gap:8px;margin-top:8px">
          <button class="btn" onclick="saveCompra()">Guardar</button>
          <button class="btn sec" onclick="closeModal('nueva-compra')">Cancelar</button>
        </div>
      </div>
    </div>`;
  if (state.compras.length === 0) return html + `<div class="empty">Sin compras registradas aún.</div>`;
  for (const c of state.compras) {
    html += `<div class="card item row-flex" style="margin-bottom:8px">
      <div>
        <div class="item-title">${esc(c.marca)} · ${esc(c.producto)}</div>
        <div class="item-sub">${esc(c.proveedor || "Sin proveedor")} · ${esc(c.fecha)}</div>
        ${c.nota ? `<div class="item-note">${esc(c.nota)}</div>` : ""}
      </div>
      <div style="text-align:right">
        <div class="sans" style="font-weight:700">${fmt(c.total)}</div>
        <div class="sans" style="font-size:12px;color:#7a6a55">×${c.cantidad} uds.</div>
      </div>
    </div>`;
  }
  return html;
}

// ─── VENTAS TAB ───────────────────────────────────────
function renderVentas() {
  const opts = state.productos.map(p => `<option value="${p.id}" data-precio="${p.precio}" data-stock="${p.stock}">${esc(p.marca)} · ${esc(p.nombre)} (stock: ${p.stock})</option>`).join("");
  const canalOpts = CANALES.map(c => `<option>${c}</option>`).join("");
  let html = `
    <div class="row-flex" style="margin-bottom:16px">
      <h2 style="font-size:20px">Ventas</h2>
      <button class="btn" onclick="openModal('nueva-venta')">+ Registrar</button>
    </div>
    <div id="modal-nueva-venta" class="modal-bg" style="display:none">
      <div class="modal">
        <div class="modal-header"><span class="title">Nueva venta</span><button class="close" onclick="closeModal('nueva-venta')">✕</button></div>
        <div class="field"><label>Producto</label><select id="nv-prod" onchange="autoFillPrecio()">${'<option value="">-- Selecciona --</option>'}${opts}</select></div>
        <div class="field"><label>Cantidad</label><input id="nv-cant" type="number" min="1" value="1"></div>
        <div class="field"><label>Precio unitario (MXN)</label><input id="nv-precio" type="number" placeholder="150"></div>
        <div class="field"><label>Canal</label><select id="nv-canal">${canalOpts}</select></div>
        <div class="field"><label>Cliente</label><input id="nv-cliente" placeholder="Opcional"></div>
        <div class="field"><label>Fecha</label><input id="nv-fecha" type="date" value="${today()}"></div>
        <div class="field"><label>Nota</label><input id="nv-nota" placeholder="Opcional"></div>
        <div style="display:flex;gap:8px;margin-top:8px">
          <button class="btn" onclick="saveVenta()">Guardar</button>
          <button class="btn sec" onclick="closeModal('nueva-venta')">Cancelar</button>
        </div>
      </div>
    </div>`;
  if (state.ventas.length === 0) return html + `<div class="empty">Sin ventas registradas aún.</div>`;
  for (const v of state.ventas) {
    const gan = v.total - v.costoTotal;
    html += `<div class="card item row-flex" style="margin-bottom:8px">
      <div>
        <div class="item-title">${esc(v.marca)} · ${esc(v.producto)}</div>
        <div class="item-sub">${esc(v.canal)}${v.cliente ? ` · ${esc(v.cliente)}` : ""} · ${esc(v.fecha)}</div>
        ${v.nota ? `<div class="item-note">${esc(v.nota)}</div>` : ""}
      </div>
      <div style="text-align:right">
        <div class="sans" style="font-weight:700;color:#27ae60">${fmt(v.total)}</div>
        <div class="sans" style="font-size:12px;color:#7a6a55">×${v.cantidad} · gan: ${fmt(gan)}</div>
      </div>
    </div>`;
  }
  return html;
}

// ─── FINANZAS TAB ─────────────────────────────────────
function renderFinanzas() {
  const totalVentas = state.ventas.reduce((s, v) => s + v.total, 0);
  const costoVentas = state.ventas.reduce((s, v) => s + v.costoTotal, 0);
  const ganancia = totalVentas - costoVentas;
  const totalCompras = state.compras.reduce((s, c) => s + c.total, 0);
  const inversionStock = state.productos.reduce((s, p) => s + p.stock * p.costo, 0);
  const valorStock = state.productos.reduce((s, p) => s + p.stock * p.precio, 0);

  // por canal
  const porCanal = {};
  state.ventas.forEach(v => { porCanal[v.canal] = (porCanal[v.canal] || 0) + v.total; });
  // por marca
  const porMarca = {};
  state.ventas.forEach(v => {
    if (!porMarca[v.marca]) porMarca[v.marca] = { ventas: 0, ganancia: 0 };
    porMarca[v.marca].ventas += v.total;
    porMarca[v.marca].ganancia += (v.total - v.costoTotal);
  });

  let html = `<h2 style="font-size:20px;margin-bottom:16px">Resumen financiero</h2>
  <div class="stat-grid">
    <div class="stat-card"><div class="slabel">Ventas brutas</div><div class="svalue" style="color:#27ae60">${fmt(totalVentas)}</div></div>
    <div class="stat-card"><div class="slabel">Costo de ventas</div><div class="svalue" style="color:#e67e22">${fmt(costoVentas)}</div></div>
    <div class="stat-card big"><div class="slabel">Ganancia neta</div><div class="svalue" style="color:${ganancia >= 0 ? "#27ae60" : "#c0392b"}">${fmt(ganancia)}</div></div>
    <div class="stat-card"><div class="slabel">Total compras</div><div class="svalue" style="color:#e67e22">${fmt(totalCompras)}</div></div>
    <div class="stat-card"><div class="slabel">Inversión en stock</div><div class="svalue" style="color:#3498db">${fmt(inversionStock)}</div></div>
    <div class="stat-card"><div class="slabel">Valor stock (precio venta)</div><div class="svalue" style="color:#9b59b6">${fmt(valorStock)}</div></div>
  </div>`;

  if (Object.keys(porCanal).length > 0) {
    html += `<div class="card" style="padding:16px;margin-bottom:16px"><div class="stitle">Ventas por canal</div>`;
    Object.entries(porCanal).sort((a,b) => b[1]-a[1]).forEach(([c, t]) => {
      html += `<div class="row-flex sans" style="font-size:14px;padding:6px 0;border-bottom:1px solid #efe8dc"><span>${esc(c)}</span><span style="font-weight:600">${fmt(t)}</span></div>`;
    });
    html += `</div>`;
  }

  if (Object.keys(porMarca).length > 0) {
    html += `<div class="card" style="padding:16px"><div class="stitle">Rendimiento por marca</div>`;
    Object.entries(porMarca).sort((a,b) => b[1].ganancia - a[1].ganancia).forEach(([m, d]) => {
      html += `<div class="row-flex sans" style="font-size:13px;padding:6px 0;border-bottom:1px solid #efe8dc">
        <span style="font-weight:500">${esc(m)}</span>
        <span>Ventas: ${fmt(d.ventas)} · <span style="color:#27ae60;font-weight:600">Gan: ${fmt(d.ganancia)}</span></span>
      </div>`;
    });
    html += `</div>`;
  }

  if (state.ventas.length === 0) html += `<div class="empty">Registra ventas para ver estadísticas.</div>`;
  return html;
}

// ─── MODAL HELPERS ────────────────────────────────────
window.openModal = (name, id) => {
  if (name === "editar-producto" && id) {
    const p = state.productos.find(x => x.id === id);
    if (!p) return;
    document.getElementById("ep-id").value = p.id;
    document.getElementById("ep-marca").value = p.marca;
    document.getElementById("ep-nombre").value = p.nombre;
    document.getElementById("ep-ml").value = p.ml || "";
    document.getElementById("ep-stock").value = p.stock;
    document.getElementById("ep-costo").value = p.costo;
    document.getElementById("ep-precio").value = p.precio;
  }
  const el = document.getElementById(`modal-${name}`);
  if (el) el.style.display = "flex";
};
window.closeModal = (name) => {
  const el = document.getElementById(`modal-${name}`);
  if (el) el.style.display = "none";
};
window.autoFillPrecio = () => {
  const sel = document.getElementById("nv-prod");
  const opt = sel.options[sel.selectedIndex];
  if (opt && opt.dataset.precio) document.getElementById("nv-precio").value = opt.dataset.precio;
};

// ─── CRUD ─────────────────────────────────────────────
window.saveNuevoProducto = async () => {
  const marca = document.getElementById("np-marca").value.trim();
  const nombre = document.getElementById("np-nombre").value.trim();
  const costo = parseFloat(document.getElementById("np-costo").value) || 0;
  const precio = parseFloat(document.getElementById("np-precio").value) || 0;
  if (!marca || !nombre || !precio) { toast("⚠️ Completa marca, nombre y precio"); return; }
  await addDoc(collection(db, "productos"), {
    marca, nombre,
    ml: parseFloat(document.getElementById("np-ml").value) || 0,
    stock: parseInt(document.getElementById("np-stock").value) || 0,
    costo, precio, ts: serverTimestamp()
  });
  closeModal("nuevo-producto");
  toast("✅ Producto añadido");
};

window.saveEditarProducto = async () => {
  const id = document.getElementById("ep-id").value;
  await updateDoc(doc(db, "productos", id), {
    marca: document.getElementById("ep-marca").value.trim(),
    nombre: document.getElementById("ep-nombre").value.trim(),
    ml: parseFloat(document.getElementById("ep-ml").value) || 0,
    stock: parseInt(document.getElementById("ep-stock").value) || 0,
    costo: parseFloat(document.getElementById("ep-costo").value) || 0,
    precio: parseFloat(document.getElementById("ep-precio").value) || 0,
  });
  closeModal("editar-producto");
  toast("✅ Producto actualizado");
};

window.delProducto = async (id, nombre) => {
  if (!confirm(`¿Eliminar "${nombre}"?`)) return;
  await deleteDoc(doc(db, "productos", id));
  toast("🗑️ Producto eliminado");
};

window.saveCompra = async () => {
  const prodId = document.getElementById("nc-prod").value;
  const cant = parseInt(document.getElementById("nc-cant").value) || 0;
  if (!prodId || !cant) { toast("⚠️ Selecciona producto y cantidad"); return; }
  const prod = state.productos.find(p => p.id === prodId);
  const total = parseFloat(document.getElementById("nc-costo").value) || (prod?.costo * cant) || 0;
  await addDoc(collection(db, "compras"), {
    productoId: prodId, producto: prod?.nombre, marca: prod?.marca,
    cantidad: cant, total,
    proveedor: document.getElementById("nc-prov").value.trim(),
    fecha: document.getElementById("nc-fecha").value,
    nota: document.getElementById("nc-nota").value.trim(),
    ts: serverTimestamp()
  });
  await updateDoc(doc(db, "productos", prodId), { stock: (prod?.stock || 0) + cant });
  closeModal("nueva-compra");
  toast("✅ Compra registrada");
};

window.saveVenta = async () => {
  const prodId = document.getElementById("nv-prod").value;
  const cant = parseInt(document.getElementById("nv-cant").value) || 1;
  if (!prodId) { toast("⚠️ Selecciona un producto"); return; }
  const prod = state.productos.find(p => p.id === prodId);
  if (!prod) return;
  if (prod.stock < cant) { toast(`⚠️ Stock insuficiente (${prod.stock} disponibles)`); return; }
  const precio = parseFloat(document.getElementById("nv-precio").value) || prod.precio;
  await addDoc(collection(db, "ventas"), {
    productoId: prodId, producto: prod.nombre, marca: prod.marca,
    cantidad: cant, precio, total: precio * cant, costoTotal: prod.costo * cant,
    canal: document.getElementById("nv-canal").value,
    cliente: document.getElementById("nv-cliente").value.trim(),
    fecha: document.getElementById("nv-fecha").value,
    nota: document.getElementById("nv-nota").value.trim(),
    ts: serverTimestamp()
  });
  await updateDoc(doc(db, "productos", prodId), { stock: prod.stock - cant });
  closeModal("nueva-venta");
  toast("✅ Venta registrada");
};

</script>
</body>
</html>
