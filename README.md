<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>usado.com - Artículos usados</title>
<style>
  * { box-sizing: border-box; margin: 0; padding: 0; }
  :root {
    --azul: #1e4fa3; --azul-claro: #2f6fd6; --marron: #6b4226; --marron-claro: #a5693a;
    --rojo: #d62828; --rojo-oscuro: #a81c1c; --crema: #fbf5ec; --texto: #2b1d14; --gris: #7a6a5e;
  }
  body { font-family: system-ui, -apple-system, Segoe UI, Roboto, sans-serif; background: var(--crema); color: var(--texto); }
  input, select, textarea, button { font: inherit; }
  /* Menú superior */
  header { background: linear-gradient(90deg, var(--azul) 0%, var(--marron) 60%, var(--rojo) 100%); color: #fff; position: sticky; top: 0; z-index: 10; box-shadow: 0 3px 10px rgba(0,0,0,.25); }
  .bar { max-width: 1200px; margin: auto; padding: 12px 16px; display: flex; gap: 14px; align-items: center; flex-wrap: wrap; }
  .logo { font-weight: 900; font-size: 1.7rem; letter-spacing: -1px; margin-right: auto; text-decoration: none; color: #fff; }
  .logo span { color: #ffd166; }
  .search { flex: 1; min-width: 200px; max-width: 420px; padding: 10px 16px; border: 2px solid rgba(255,255,255,.4); border-radius: 30px; background: rgba(255,255,255,.15); color: #fff; outline: none; }
  .search::placeholder { color: rgba(255,255,255,.8); }
  .search:focus { background: rgba(255,255,255,.25); border-color: #ffd166; }
  .btn { background: var(--rojo); color: #fff; border: none; padding: 10px 20px; border-radius: 30px; cursor: pointer; font-weight: 700; box-shadow: 0 2px 6px rgba(0,0,0,.25); transition: transform .1s, background .2s; }
  .btn:hover { background: var(--rojo-oscuro); transform: translateY(-1px); }
  .btn.sec { background: var(--azul); }
  .btn.sec:hover { background: var(--azul-claro); }
  .btn.marron { background: var(--marron); }
  .btn.marron:hover { background: var(--marron-claro); }
  .btn.danger { background: var(--rojo); }
  /* Layout */
  .layout { max-width: 1200px; margin: 22px auto; padding: 0 16px; display: grid; grid-template-columns: 240px 1fr; gap: 22px; }
  aside { background: #fff; border-radius: 14px; padding: 18px; height: fit-content; box-shadow: 0 2px 8px rgba(107,66,38,.15); border-top: 5px solid var(--azul); }
  aside h3 { font-size: 1rem; margin-bottom: 10px; color: var(--marron); text-transform: uppercase; letter-spacing: .5px; }
  aside label { display: block; font-size: .88rem; margin-bottom: 6px; color: var(--gris); font-weight: 600; }
  aside select, aside input { width: 100%; padding: 8px; border: 1px solid #e0cdb8; border-radius: 8px; margin-bottom: 12px; background: #fffdf9; }
  .cats { display: flex; flex-direction: column; gap: 5px; margin-bottom: 18px; }
  .cat { text-align: left; background: #f6ece0; border: none; padding: 9px 12px; border-radius: 8px; cursor: pointer; color: var(--marron); font-weight: 600; transition: all .15s; }
  .cat:hover { background: #e6f0ff; color: var(--azul); }
  .cat.active { background: var(--rojo); color: #fff; }
  .cat:nth-child(3n+2):not(.active):hover { background: #ffe5e5; color: var(--rojo); }
  .intro { background: linear-gradient(135deg, var(--azul), var(--marron)); color: #fff; border-radius: 14px; padding: 18px 22px; margin-bottom: 18px; display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 10px; }
  .intro h2 { font-size: 1.3rem; }
  .intro p { opacity: .9; font-size: .92rem; }
  .grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(210px, 1fr)); gap: 18px; }
  .card { background: #fff; border-radius: 14px; overflow: hidden; box-shadow: 0 2px 6px rgba(107,66,38,.15); cursor: pointer; transition: transform .15s, box-shadow .15s; border-bottom: 4px solid var(--marron-claro); }
  .card:nth-child(3n+1) { border-bottom-color: var(--azul); }
  .card:nth-child(3n+3) { border-bottom-color: var(--rojo); }
  .card:hover { transform: translateY(-4px); box-shadow: 0 8px 18px rgba(107,66,38,.25); }
  .card img, .noimg { width: 100%; height: 180px; object-fit: cover; background: linear-gradient(135deg, #e6f0ff, #f6ece0); display: flex; align-items: center; justify-content: center; color: var(--gris); }
  .card .info { padding: 12px 14px; }
  .price { font-size: 1.2rem; font-weight: 800; color: var(--rojo); }
  .title { white-space: nowrap; overflow: hidden; text-overflow: ellipsis; margin: 4px 0; font-weight: 600; }
  .meta { font-size: .8rem; color: var(--gris); }
  .tag { display: inline-block; font-size: .72rem; background: #e6f0ff; color: var(--azul); padding: 2px 8px; border-radius: 10px; margin-top: 6px; font-weight: 600; }
  .empty { grid-column: 1/-1; text-align: center; color: var(--gris); padding: 40px; background: #fff; border-radius: 14px; }
  /* Modales */
  .modal-bg { position: fixed; inset: 0; background: rgba(43,29,20,.6); display: none; align-items: center; justify-content: center; padding: 16px; z-index: 50; }
  .modal-bg.open { display: flex; }
  .modal { background: #fff; border-radius: 16px; width: 100%; max-width: 620px; max-height: 92vh; overflow-y: auto; padding: 22px; position: relative; border-top: 6px solid var(--rojo); }
  .close { position: absolute; right: 12px; top: 12px; background: var(--marron); color: #fff; border: none; border-radius: 50%; width: 32px; height: 32px; cursor: pointer; }
  .close:hover { background: var(--rojo); }
  .modal h2 { margin-bottom: 10px; padding-right: 30px; color: var(--azul); }
  .detail-img { width: 100%; max-height: 360px; object-fit: contain; background: #2b1d14; border-radius: 10px; margin-bottom: 14px; }
  .desc { white-space: pre-wrap; margin: 12px 0; line-height: 1.5; }
  .seller { background: #f6ece0; border-left: 4px solid var(--azul); padding: 10px 12px; border-radius: 8px; margin: 12px 0; font-size: .95rem; }
  form .row { margin-bottom: 12px; display: flex; flex-direction: column; gap: 4px; }
  form label { font-weight: 700; font-size: .88rem; color: var(--marron); }
  form input, form select, form textarea { padding: 9px; border: 1px solid #e0cdb8; border-radius: 8px; background: #fffdf9; }
  form input:focus, form select:focus, form textarea:focus { outline: 2px solid var(--azul-claro); border-color: transparent; }
  form textarea { min-height: 90px; resize: vertical; }
  .two { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
  .actions { display: flex; gap: 8px; justify-content: flex-end; margin-top: 8px; flex-wrap: wrap; }
  .actions a.btn { text-decoration: none; display: inline-block; }
  .preview { width: 100%; height: 160px; object-fit: cover; border-radius: 8px; display: none; margin-top: 6px; }
  .toast { position: fixed; bottom: 20px; left: 50%; transform: translateX(-50%); background: var(--marron); color: #fff; padding: 12px 22px; border-radius: 30px; display: none; z-index: 99; box-shadow: 0 4px 12px rgba(0,0,0,.3); }
  footer { text-align: center; color: var(--gris); padding: 24px; font-size: .85rem; }
  @media (max-width: 760px) { .layout { grid-template-columns: 1fr; } .two { grid-template-columns: 1fr; } }
</style>
</head>
<body>
<header>
  <div class="bar">
    <a class="logo" href="#">usado<span>.com</span></a>
    <input class="search" id="search" placeholder="Buscar artículos...">
    <button class="btn" id="btnNew">+ Publicar</button>
  </div>
</header>
<div class="layout">
  <aside>
    <h3>Categorías</h3>
    <div class="cats" id="cats"></div>
    <h3>Filtros</h3>
    <label>Estado</label>
    <select id="fCondition">
      <option value="">Cualquiera</option>
      <option>Como nuevo</option>
      <option>Buen estado</option>
      <option>Estado aceptable</option>
      <option>Para repuestos</option>
    </select>
    <label>Precio mínimo</label>
    <input type="number" id="fMin" min="0" placeholder="0">
    <label>Precio máximo</label>
    <input type="number" id="fMax" min="0" placeholder="Sin límite">
    <label>Ordenar por</label>
    <select id="fSort">
      <option value="new">Más recientes</option>
      <option value="asc">Precio: menor a mayor</option>
      <option value="desc">Precio: mayor a menor</option>
    </select>
    <button class="btn marron" style="width:100%" id="btnClear">Limpiar filtros</button>
  </aside>
  <main>
    <div class="intro">
      <div>
        <h2>¡Encuentra tesoros de segunda mano!</h2>
        <p>Compra, vende y dale una nueva vida a lo que ya no usas.</p>
      </div>
      <button class="btn sec" onclick="openForm()">Vender ahora</button>
    </div>
    <div class="grid" id="grid"></div>
  </main>
</div>
<footer>usado.com · Compra y venta de artículos usados</footer>
<!-- Modal: publicar -->
<div class="modal-bg" id="modalForm">
  <div class="modal">
    <button class="close" data-close>✕</button>
    <h2 id="formTitle">Publicar artículo</h2>
    <form id="form">
      <input type="hidden" id="editId">
      <div class="row"><label>Título *</label><input id="fTitle" required maxlength="80" placeholder="Ej: Bicicleta de montaña"></div>
      <div class="two">
        <div class="row"><label>Precio ($)*</label><input type="number" id="fPrice" min="0" step="0.01" required></div>
        <div class="row"><label>Categoría *</label>
          <select id="fCat" required>
            <option value="">Selecciona...</option>
          </select>
        </div>
      </div>
      <div class="two">
        <div class="row"><label>Estado *</label>
          <select id="fCond" required>
            <option value="">Selecciona...</option>
            <option>Como nuevo</option>
            <option>Buen estado</option>
            <option>Estado aceptable</option>
            <option>Para repuestos</option>
          </select>
        </div>
        <div class="row"><label>Ubicación</label><input id="fLoc" placeholder="Ej: Madrid"></div>
      </div>
      <div class="row"><label>Descripción</label><textarea id="fDesc" maxlength="1000" placeholder="Describe el artículo..."></textarea></div>
      <div class="row"><label>Tu nombre *</label><input id="fSeller" required maxlength="40"></div>
      <div class="row"><label>Contacto (teléfono o email) *</label><input id="fContact" required maxlength="60"></div>
      <div class="row"><label>Foto (opcional)</label>
        <input type="file" id="fImg" accept="image/*">
        <img id="preview" class="preview" alt="Vista previa">
      </div>
      <div class="actions">
        <button type="button" class="btn marron" data-close>Cancelar</button>
        <button type="submit" class="btn">Publicar</button>
      </div>
    </form>
  </div>
</div>
<!-- Modal: detalle -->
<div class="modal-bg" id="modalDetail">
  <div class="modal" id="detailBox">
    <button class="close" data-close>✕</button>
  </div>
</div>
<div class="toast" id="toast"></div>
<script>
const CATEGORIES = ["Vehículos","Electrónica","Hogar y jardín","Ropa","Deportes","Muebles","Juguetes","Libros","Otros"];
const KEY = "usado_items_v1";
let items = JSON.parse(localStorage.getItem(KEY) || "null") || seed();
let state = { search: "", cat: "" };
function seed() {
  const s = [
    { id: uid(), title: "Bicicleta de montaña", price: 180, category: "Deportes", condition: "Buen estado", location: "Madrid", description: "Cuadro de aluminio, 21 velocidades, frenos de disco recién revisados.", seller: "Ana", contact: "ana@ejemplo.com", image: "", date: Date.now() - 86400000 },
    { id: uid(), title: "Sofá de 3 plazas", price: 120, category: "Muebles", condition: "Estado aceptable", location: "Barcelona", description: "Color gris, algunas marcas de uso. Retirada en persona.", seller: "Luis", contact: "600 123 456", image: "", date: Date.now() - 3600000 },
    { id: uid(), title: "iPhone 12 64GB", price: 350, category: "Electrónica", condition: "Como nuevo", location: "Valencia", description: "Sin rayones, con funda y cargador original. Batería al 88%.", seller: "Marta", contact: "marta@ejemplo.com", image: "", date: Date.now() - 7200000 }
  ];
  localStorage.setItem(KEY, JSON.stringify(s));
  return s;
}
function uid() { return Math.random().toString(36).slice(2, 10) + Date.now().toString(36); }
function save() { localStorage.setItem(KEY, JSON.stringify(items)); }
function esc(s) { return String(s ?? "").replace(/[&<>"']/g, c => ({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"}[c])); }
function money(n) { return Number(n).toLocaleString("es-AR", { style: "currency", currency: "ARS" }); }
function toast(msg) { const t = document.getElementById("toast"); t.textContent = msg; t.style.display = "block"; clearTimeout(t._h); t._h = setTimeout(() => t.style.display = "none", 2200); }
function timeAgo(ts) {
  const m = Math.floor((Date.now() - ts) / 60000);
  if (m < 1) return "ahora mismo";
  if (m < 60) return `hace ${m} min`;
  const h = Math.floor(m / 60);
  if (h < 24) return `hace ${h} h`;
  return `hace ${Math.floor(h / 24)} d`;
}
// Categorías
function renderCats() {
  const box = document.getElementById("cats");
  const all = ["", ...CATEGORIES];
  box.innerHTML = all.map(c => `<button class="cat ${state.cat === c ? "active" : ""}" data-cat="${esc(c)}">${c || "Todas"}</button>`).join("");
  box.querySelectorAll(".cat").forEach(b => b.onclick = () => { state.cat = b.dataset.cat; renderCats(); render(); });
  document.getElementById("fCat").innerHTML = `<option value="">Selecciona...</option>` + CATEGORIES.map(c => `<option>${c}</option>`).join("");
}
// Listado con filtros
function filtered() {
  const q = state.search.toLowerCase().trim();
  const cond = document.getElementById("fCondition").value;
  const min = parseFloat(document.getElementById("fMin").value);
  const max = parseFloat(document.getElementById("fMax").value);
  const sort = document.getElementById("fSort").value;
  let list = items.filter(i =>
    (!q || i.title.toLowerCase().includes(q) || (i.description || "").toLowerCase().includes(q)) &&
    (!state.cat || i.category === state.cat) &&
    (!cond || i.condition === cond) &&
    (isNaN(min) || i.price >= min) &&
    (isNaN(max) || i.price <= max)
  );
  if (sort === "asc") list.sort((a, b) => a.price - b.price);
  else if (sort === "desc") list.sort((a, b) => b.price - a.price);
  else list.sort((a, b) => b.date - a.date);
  return list;
}
function render() {
  const list = filtered();
  const grid = document.getElementById("grid");
  if (!list.length) { grid.innerHTML = `<div class="empty">No hay artículos que coincidan con tu búsqueda.</div>`; return; }
  grid.innerHTML = list.map(i => `
    <div class="card" data-id="${i.id}">
      ${i.image ? `<img src="${i.image}" alt="${esc(i.title)}">` : `<div class="noimg">Sin foto</div>`}
      <div class="info">
        <div class="price">${money(i.price)}</div>
        <div class="title">${esc(i.title)}</div>
        <div class="meta">${esc(i.location || "Sin ubicación")} · ${timeAgo(i.date)}</div>
        <span class="tag">${esc(i.condition)}</span>
      </div>
    </div>`).join("");
  grid.querySelectorAll(".card").forEach(c => c.onclick = () => openDetail(c.dataset.id));
}
// Detalle
function openDetail(id) {
  const i = items.find(x => x.id === id);
  if (!i) return;
  document.getElementById("detailBox").innerHTML = `
    <button class="close" data-close>✕</button>
    ${i.image ? `<img class="detail-img" src="${i.image}" alt="${esc(i.title)}">` : ""}
    <div class="price">${money(i.price)}</div>
    <h2>${esc(i.title)}</h2>
    <div class="meta">${esc(i.category)} · ${esc(i.condition)} · ${esc(i.location || "Sin ubicación")} · ${timeAgo(i.date)}</div>
    <div class="desc">${esc(i.description || "Sin descripción.")}</div>
    <div class="seller"><b>Vendedor:</b> ${esc(i.seller)}<br><b>Contacto:</b> ${esc(i.contact)}</div>
    <div class="actions">
      <button class="btn danger" id="btnDel">Eliminar</button>
      <button class="btn sec" id="btnEdit">Editar</button>
      <a class="btn" href="mailto:${esc(i.contact)}">Contactar</a>
    </div>`;
  wireClose(document.getElementById("detailBox"));
  document.getElementById("btnDel").onclick = () => {
    if (confirm("¿Eliminar esta publicación?")) {
      items = items.filter(x => x.id !== id); save(); closeModals(); render(); toast("Publicación eliminada");
    }
  };
  document.getElementById("btnEdit").onclick = () => { closeModals(); openForm(i); };
  open("modalDetail");
}
// Formulario
let pendingImage = "";
function openForm(item = null) {
  const f = document.getElementById("form");
  f.reset();
  pendingImage = item ? item.image : "";
  document.getElementById("formTitle").textContent = item ? "Editar publicación" : "Publicar artículo";
  document.getElementById("editId").value = item ? item.id : "";
  if (item) {
    fTitle.value = item.title; fPrice.value = item.price; fCat.value = item.category;
    fCond.value = item.condition; fLoc.value = item.location || ""; fDesc.value = item.description || "";
    fSeller.value = item.seller; fContact.value = item.contact;
  }
  const pv = document.getElementById("preview");
  pv.src = pendingImage; pv.style.display = pendingImage ? "block" : "none";
  open("modalForm");
}
document.getElementById("fImg").onchange = e => {
  const file = e.target.files[0];
  if (!file) return;
  if (file.size > 2 * 1024 * 1024) { toast("La imagen debe pesar menos de 2 MB"); e.target.value = ""; return; }
  const reader = new FileReader();
  reader.onload = ev => {
    pendingImage = ev.target.result;
    const pv = document.getElementById("preview");
    pv.src = pendingImage; pv.style.display = "block";
  };
  reader.readAsDataURL(file);
};
document.getElementById("form").onsubmit = e => {
  e.preventDefault();
  const id = document.getElementById("editId").value;
  const data = {
    title: fTitle.value.trim(), price: parseFloat(fPrice.value), category: fCat.value,
    condition: fCond.value, location: fLoc.value.trim(), description: fDesc.value.trim(),
    seller: fSeller.value.trim(), contact: fContact.value.trim(), image: pendingImage
  };
  if (id) {
    const idx = items.findIndex(x => x.id === id);
    items[idx] = { ...items[idx], ...data };
    toast("Publicación actualizada");
  } else {
    items.unshift({ id: uid(), date: Date.now(), ...data });
    toast("¡Artículo publicado!");
  }
  save(); closeModals(); render();
};
// Modales
function open(id) { document.getElementById(id).classList.add("open"); }
function closeModals() { document.querySelectorAll(".modal-bg").forEach(m => m.classList.remove("open")); }
function wireClose(root) { root.querySelectorAll("[data-close]").forEach(b => b.onclick = closeModals); }
document.querySelectorAll(".modal-bg").forEach(bg => bg.addEventListener("click", e => { if (e.target === bg) closeModals(); }));
document.querySelectorAll("#modalForm [data-close]").forEach(b => b.onclick = closeModals);
document.getElementById("btnNew").onclick = () => openForm();
// Búsqueda y filtros
document.getElementById("search").oninput = e => { state.search = e.target.value; render(); };
["fCondition","fMin","fMax","fSort"].forEach(id => document.getElementById(id).addEventListener("input", render));
document.getElementById("btnClear").onclick = () => {
  ["fCondition","fMin","fMax"].forEach(id => document.getElementById(id).value = "");
  document.getElementById("fSort").value = "new";
  document.getElementById("search").value = ""; state.search = ""; state.cat = "";
  renderCats(); render();
};
renderCats();
render();
</script>
</body>
</html>
