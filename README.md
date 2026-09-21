<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>QAFILA TIMES — Admin Panel</title>
<style>
*{box-sizing:border-box;margin:0;padding:0}
:root{--gold:#c99a3b;--gold2:#f0c76a;--black:#090909;--panel:#111;--line:#292929;--muted:#aaa;--red:#d64545;--green:#28a36a}
body{font-family:Inter,Arial,sans-serif;background:#f3f4f6;color:#161616}
button,input,select,textarea{font:inherit}
button{cursor:pointer;border:0}
#loginPage{min-height:100vh;display:grid;place-items:center;padding:20px;background:radial-gradient(circle at 50% 0,#353535,#090909 62%)}
.login-card{width:min(430px,100%);padding:34px;border-radius:24px;background:#fff;box-shadow:0 30px 100px #0009}
.logo-wrap{text-align:center;margin-bottom:18px}
.logo{width:190px;max-width:100%;height:auto;display:inline-block;object-fit:contain}
.login-card h1{text-align:center;font-size:24px}
.login-card .sub{text-align:center;color:#777;margin:7px 0 24px}
.field{margin-bottom:14px}
.field label{display:block;font-size:13px;font-weight:700;margin-bottom:7px}
input,select,textarea{width:100%;border:1px solid #ddd;border-radius:10px;padding:12px 13px;outline:none;background:#fff}
input:focus,select:focus,textarea:focus{border-color:var(--gold);box-shadow:0 0 0 3px #c99a3b18}
.primary{width:100%;padding:13px;border-radius:10px;background:#111;color:#fff;font-weight:800}
.error{color:var(--red);text-align:center;margin-top:10px;font-size:13px;min-height:18px}
#app{display:none}
.topbar{height:74px;background:#0b0b0b;color:#fff;display:flex;align-items:center;justify-content:space-between;padding:8px 24px;position:sticky;top:0;z-index:20;box-shadow:0 4px 20px #0003}
.brand{display:flex;align-items:center;gap:18px}.brand .logo{width:130px;max-height:58px}.brand span{font-weight:700;color:#ddd}
.logout{background:#b83232;color:#fff;padding:10px 15px;border-radius:9px;font-weight:700}
.container{max-width:1500px;margin:auto;padding:24px}
.title{margin-bottom:18px}.title h2{font-size:28px}.title p{color:#777;margin-top:5px}
.stats{display:grid;grid-template-columns:repeat(4,1fr);gap:14px;margin-bottom:18px}
.stat{background:#fff;border-radius:15px;padding:20px;box-shadow:0 4px 18px #0000000b}.stat small{color:#777}.stat strong{display:block;font-size:28px;margin-top:8px}
.category-dashboard{margin:18px 0;background:#fff;border-radius:15px;padding:18px;box-shadow:0 4px 18px #0000000b}
.category-dashboard h3{margin-bottom:14px;font-size:18px}
.category-grid{display:grid;grid-template-columns:repeat(6,1fr);gap:10px}
.category-card{border:1px solid #eee;border-radius:12px;padding:14px;background:#fafafa;cursor:pointer;transition:.15s}
.category-card:hover{border-color:var(--gold);transform:translateY(-1px)}
.category-card small{display:block;color:#777;font-size:12px;margin-bottom:7px}
.category-card strong{font-size:22px}
.category-card.active{border:2px solid var(--gold);background:#fffaf0}
@media(max-width:1100px){.category-grid{grid-template-columns:repeat(3,1fr)}}
@media(max-width:620px){.category-grid{grid-template-columns:repeat(2,1fr)}}

.toolbar{background:#fff;border-radius:15px;padding:15px;display:flex;flex-wrap:wrap;gap:10px;margin-bottom:15px}
.btn{padding:11px 15px;border-radius:9px;color:#fff;font-weight:700}.btn-dark{background:#111}.btn-blue{background:#1769aa}.btn-green{background:#198754}.btn-red{background:#b83232}.btn-gray{background:#777}
.search{margin-left:auto;min-width:280px;flex:1;max-width:450px}
.table-card{background:#fff;border-radius:15px;overflow:hidden;box-shadow:0 4px 18px #0000000b}
.table-wrap{overflow:auto}
table{width:100%;border-collapse:collapse;min-width:1050px}
th{background:#111;color:#fff;text-align:left;font-size:13px;padding:13px}
td{padding:12px;border-bottom:1px solid #eee;font-size:14px;vertical-align:middle}
.product-thumb{width:58px;height:58px;object-fit:cover;border-radius:8px;background:#eee}
.stock-ok{color:var(--green);font-weight:800}.stock-zero{color:var(--red);font-weight:800}
.offer{color:var(--red);font-weight:800}
.small-btn{padding:7px 9px;border-radius:7px;color:#fff;font-size:12px;font-weight:700}.edit{background:#1769aa}.del{background:#b83232}
.pagination{display:flex;align-items:center;justify-content:center;gap:12px;padding:18px}.page{font-weight:800}
.modal{display:none;position:fixed;inset:0;background:#000b;z-index:50;padding:20px;place-items:center}
.modal-box{width:min(650px,100%);max-height:92vh;overflow:auto;background:#fff;border-radius:20px;padding:24px}
.modal-head{display:flex;align-items:center;justify-content:space-between;margin-bottom:18px}.modal-head h3{font-size:22px}
.close{background:#777;color:#fff;padding:8px 11px;border-radius:8px}
.grid2{display:grid;grid-template-columns:1fr 1fr;gap:12px}
.checks{display:flex;gap:20px;margin:5px 0 15px}.check{display:flex;align-items:center;gap:7px}.check input{width:auto}
.preview{display:none;width:140px;height:140px;object-fit:cover;border-radius:12px;margin:5px 0 12px}
.progress-wrap{display:none;height:12px;background:#ddd;border-radius:99px;overflow:hidden;margin:15px 0}.progress{height:100%;width:0;background:var(--green);transition:.15s}
.import-note{background:#f5f5f5;border-radius:10px;padding:13px;line-height:1.55;font-size:13px;margin-bottom:14px}
.empty{text-align:center;color:#777;padding:45px}
@media(max-width:900px){.stats{grid-template-columns:1fr 1fr}.brand span{display:none}}
@media(max-width:620px){.container{padding:12px}.topbar{padding:8px 12px}.brand .logo{width:105px}.stats{gap:8px}.stat{padding:14px}.stat strong{font-size:22px}.grid2{grid-template-columns:1fr}.search{min-width:100%}.toolbar{flex-direction:column}.toolbar .btn{width:100%}}
</style>
</head>
<body>

<div id="loginPage">
  <div class="login-card">
    <div class="logo-wrap"><img class="logo" id="loginLogo" alt="Qafila Times"></div>
    <h1>QAFILA TIMES</h1>
    <div class="sub">Private Product Management</div>
    <div class="field"><label>Username</label><input id="username" autocomplete="username" placeholder="admin"></div>
    <div class="field"><label>Password</label><input id="password" type="password" autocomplete="current-password" placeholder="••••••••"></div>
    <button class="primary" onclick="login()">LOGIN</button>
    <div id="loginError" class="error"></div>
  </div>
</div>

<div id="app">
  <header class="topbar">
    <div class="brand"><img class="logo" id="headerLogo" alt="Qafila Times"><span>Admin Panel</span></div>
    <button class="logout" onclick="logout()">Logout</button>
  </header>

  <main class="container">
    <div class="title"><h2>Product Dashboard</h2><p>Manage Qafila Times products in one place.</p></div>

    <section class="stats">
      <div class="stat"><small>Total Products</small><strong id="total">0</strong></div>
      <div class="stat"><small>In Stock</small><strong id="inStock">0</strong></div>
      <div class="stat"><small>Out of Stock</small><strong id="outStock">0</strong></div>
      <div class="stat"><small>Offers</small><strong id="offers">0</strong></div>
    </section>

    <section class="category-dashboard">
      <h3>📊 Category-wise Dashboard</h3>
      <div class="category-grid" id="categoryGrid"></div>
    </section>

    <section class="toolbar">
      <button class="btn btn-dark" onclick="openProduct()">＋ Add Product</button>
      <button class="btn btn-blue" onclick="openImport()">📊 Bulk CSV Import</button>
      <button class="btn btn-green" onclick="exportCSV()">⬇ Export CSV</button>
      <button class="btn btn-red" onclick="clearAll()">🗑 Clear All</button>
      <select id="categoryFilter" onchange="searchProducts()" style="max-width:190px">
        <option value="">All Categories</option>
        <option>Watches</option>
        <option>Perfumes</option>
        <option>Rings</option>
        <option>Dresses</option>
        <option>New Arrivals</option>
        <option>Offers</option>
      </select>
      <input class="search" id="search" oninput="searchProducts()" placeholder="🔎 Search code, product or category">
    </section>

    <section class="table-card">
      <div class="table-wrap">
        <table>
          <thead><tr><th>Image</th><th>Code</th><th>Product</th><th>Category</th><th>Price</th><th>Stock</th><th>Status</th><th>Actions</th></tr></thead>
          <tbody id="productTable"></tbody>
        </table>
      </div>
      <div class="pagination">
        <button class="btn btn-gray" onclick="prevPage()">← Previous</button>
        <span class="page" id="pageInfo">Page 1</span>
        <button class="btn btn-gray" onclick="nextPage()">Next →</button>
      </div>
    </section>
  </main>
</div>

<div class="modal" id="productModal">
  <div class="modal-box">
    <div class="modal-head"><h3 id="modalTitle">Add Product</h3><button class="close" onclick="closeProduct()">✕</button></div>
    <input type="hidden" id="editId">
    <div class="grid2">
      <div class="field"><label>Product Code *</label><input id="code" placeholder="WT001"></div>
      <div class="field"><label>Product Name *</label><input id="name" placeholder="Classic Black Watch"></div>
    </div>
    <div class="field"><label>Description</label><textarea id="description" rows="3" placeholder="Product description"></textarea></div>
    <div class="grid2">
      <div class="field"><label>Price *</label><input id="price" type="number" min="0" placeholder="2499"></div>
      <div class="field"><label>Old Price</label><input id="oldPrice" type="number" min="0" placeholder="2999"></div>
    </div>
    <div class="grid2">
      <div class="field"><label>Category</label><select id="category"><option value="">Select Category</option><option>Watches</option><option>Perfumes</option><option>Rings</option><option>Dresses</option><option>New Arrivals</option><option>Offers</option></select></div>
      <div class="field"><label>Stock</label><input id="stock" type="number" min="0" placeholder="20"></div>
    </div>
    <div class="field"><label>Product Image</label><input id="imageFile" type="file" accept="image/*" onchange="previewImage(event)"></div>
    <img id="preview" class="preview" alt="Preview">
    <div class="checks">
      <label class="check"><input type="checkbox" id="isNew"> New Arrival</label>
      <label class="check"><input type="checkbox" id="isOffer"> Offer</label>
    </div>
    <button class="btn btn-green" style="width:100%" onclick="saveProduct()">SAVE PRODUCT</button>
  </div>
</div>

<div class="modal" id="importModal">
  <div class="modal-box">
    <div class="modal-head"><h3>Bulk Product Import</h3><button class="close" onclick="closeImport()">✕</button></div>
    <div class="import-note">
      CSV columns:<br>
      <b>code,name,description,price,old_price,category,stock,image,is_new,is_offer</b><br><br>
      Example:<br>
      <code>WT001,Classic Watch,Premium watch,2499,2999,Watches,20,https://example.com/watch.jpg,true,false</code><br><br>
      The importer processes records in batches and supports 2000+ rows in this browser-based version.
    </div>
    <input id="csvFile" type="file" accept=".csv">
    <div class="progress-wrap" id="progressWrap"><div class="progress" id="progressBar"></div></div>
    <div id="importStatus" style="text-align:center;margin:10px 0;color:#555"></div>
    <button class="btn btn-green" style="width:100%" onclick="startImport()">🚀 IMPORT PRODUCTS</button>
  </div>
</div>

<script>
/* The uploaded QAFILA TIMES logo is embedded directly into this HTML. */
const LOGO_DATA = "data:image/jpeg;base64,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";
document.getElementById("loginLogo").src = LOGO_DATA;
document.getElementById("headerLogo").src = LOGO_DATA;

/* Demo credentials. Change these before real deployment. */
const ADMIN_USER = "admin";
const ADMIN_PASS = "qafila123";

const DB_KEY = "qafilaProducts";
const LOGIN_KEY = "qafilaAdminLoggedIn";
const PAGE_SIZE = 50;

let products = loadProducts();
let filtered = [...products];
let page = 1;

function loadProducts(){
  try { return JSON.parse(localStorage.getItem(DB_KEY)) || []; }
  catch(e){ return []; }
}
function saveDB(){ localStorage.setItem(DB_KEY, JSON.stringify(products)); }

function login(){
  const u=document.getElementById("username").value.trim();
  const p=document.getElementById("password").value;
  if(u===ADMIN_USER && p===ADMIN_PASS){
    localStorage.setItem(LOGIN_KEY,"1");
    showApp();
  }else{
    document.getElementById("loginError").textContent="Invalid username or password.";
  }
}
function logout(){
  localStorage.removeItem(LOGIN_KEY);
  location.reload();
}
function showApp(){
  document.getElementById("loginPage").style.display="none";
  document.getElementById("app").style.display="block";
  render();
}
if(localStorage.getItem(LOGIN_KEY)==="1") showApp();

function esc(v){
  return String(v??"").replace(/[&<>"']/g,m=>({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#039;"}[m]));
}
function render(){
  const q=document.getElementById("search").value.trim().toLowerCase();
  const cat=document.getElementById("categoryFilter").value;
  filtered=products.filter(p=>{
    const matchesText=!q ||
      String(p.code).toLowerCase().includes(q) ||
      String(p.name).toLowerCase().includes(q) ||
      String(p.category).toLowerCase().includes(q);
    const matchesCategory=!cat || String(p.category)===cat;
    return matchesText && matchesCategory;
  });

  const pages=Math.max(1,Math.ceil(filtered.length/PAGE_SIZE));
  if(page>pages) page=pages;
  const start=(page-1)*PAGE_SIZE;
  const list=filtered.slice(start,start+PAGE_SIZE);
  const tbody=document.getElementById("productTable");
  tbody.innerHTML="";

  if(!list.length){
    tbody.innerHTML='<tr><td colspan="8" class="empty">No products found.</td></tr>';
  }else{
    list.forEach(p=>{
      const tr=document.createElement("tr");
      const img=p.image || "";
      tr.innerHTML=`
        <td><img class="product-thumb" src="${esc(img)}" alt="" onerror="this.style.opacity='.15'"></td>
        <td><b>${esc(p.code)}</b></td>
        <td><b>${esc(p.name)}</b>${p.isNew?'<br><small>🆕 New</small>':''}</td>
        <td>${esc(p.category)}</td>
        <td>₹${esc(p.price)}${p.oldPrice?`<br><del style="color:#999">₹${esc(p.oldPrice)}</del>`:""}</td>
        <td class="${Number(p.stock)>0?'stock-ok':'stock-zero'}">${esc(p.stock)}</td>
        <td>${p.isOffer?'<span class="offer">🔥 OFFER</span>':(Number(p.stock)>0?'In Stock':'Out of Stock')}</td>
        <td>
          <button class="small-btn edit" onclick="editProduct('${esc(p.id)}')">Edit</button>
          <button class="small-btn del" onclick="deleteProduct('${esc(p.id)}')">Delete</button>
        </td>`;
      tbody.appendChild(tr);
    });
  }

  document.getElementById("pageInfo").textContent=`Page ${page} / ${pages}`;
  document.getElementById("total").textContent=products.length;
  document.getElementById("inStock").textContent=products.filter(p=>Number(p.stock)>0).length;
  document.getElementById("outStock").textContent=products.filter(p=>Number(p.stock)<=0).length;
  document.getElementById("offers").textContent=products.filter(p=>p.isOffer).length;
  renderCategoryDashboard();
}

function renderCategoryDashboard(){
  const categories=["Watches","Perfumes","Rings","Dresses","New Arrivals","Offers"];
  const grid=document.getElementById("categoryGrid");
  const active=document.getElementById("categoryFilter").value;
  grid.innerHTML=categories.map(cat=>{
    let count=products.filter(p=>String(p.category)===cat).length;
    if(cat==="New Arrivals") count=products.filter(p=>p.isNew || String(p.category)==="New Arrivals").length;
    if(cat==="Offers") count=products.filter(p=>p.isOffer || String(p.category)==="Offers").length;
    return `<div class="category-card ${active===cat?'active':''}" onclick="selectCategory('${cat}')">
      <small>${esc(cat)}</small><strong>${count}</strong>
    </div>`;
  }).join("");
}
function selectCategory(cat){
  const filter=document.getElementById("categoryFilter");
  filter.value=filter.value===cat?"":cat;
  page=1;
  render();
}

function searchProducts(){page=1;render()}
function prevPage(){if(page>1){page--;render()}}
function nextPage(){
  const pages=Math.max(1,Math.ceil(filtered.length/PAGE_SIZE));
  if(page<pages){page++;render()}
}

function resetForm(){
  ["editId","code","name","description","price","oldPrice","category","stock"].forEach(id=>document.getElementById(id).value="");
  document.getElementById("imageFile").value="";
  document.getElementById("isNew").checked=false;
  document.getElementById("isOffer").checked=false;
  document.getElementById("preview").style.display="none";
}
function openProduct(){
  resetForm();
  document.getElementById("modalTitle").textContent="Add Product";
  document.getElementById("productModal").style.display="grid";
}
function closeProduct(){document.getElementById("productModal").style.display="none"}

function editProduct(id){
  const p=products.find(x=>x.id===id); if(!p)return;
  document.getElementById("modalTitle").textContent="Edit Product";
  document.getElementById("editId").value=p.id;
  document.getElementById("code").value=p.code||"";
  document.getElementById("name").value=p.name||"";
  document.getElementById("description").value=p.description||"";
  document.getElementById("price").value=p.price||"";
  document.getElementById("oldPrice").value=p.oldPrice||"";
  document.getElementById("category").value=p.category||"";
  document.getElementById("stock").value=p.stock??0;
  document.getElementById("isNew").checked=!!p.isNew;
  document.getElementById("isOffer").checked=!!p.isOffer;
  document.getElementById("imageFile").value="";
  const prev=document.getElementById("preview");
  if(p.image){prev.src=p.image;prev.style.display="block"}else prev.style.display="none";
  document.getElementById("productModal").style.display="grid";
}

function previewImage(e){
  const file=e.target.files[0]; if(!file)return;
  const reader=new FileReader();
  reader.onload=ev=>{
    const p=document.getElementById("preview");
    p.src=ev.target.result;p.style.display="block";
  };
  reader.readAsDataURL(file);
}

function saveProduct(){
  const code=document.getElementById("code").value.trim();
  const name=document.getElementById("name").value.trim();
  if(!code||!name){alert("Product Code and Product Name are required.");return}

  const editId=document.getElementById("editId").value;
  const file=document.getElementById("imageFile").files[0];

  const finish=(image)=>{
    if(editId){
      const p=products.find(x=>x.id===editId);
      if(!p)return;
      if(products.some(x=>x.id!==editId && x.code.toLowerCase()===code.toLowerCase())){
        alert("Another product already uses this code.");return;
      }
      Object.assign(p,{
        code,name,
        description:document.getElementById("description").value.trim(),
        price:document.getElementById("price").value||0,
        oldPrice:document.getElementById("oldPrice").value||"",
        category:document.getElementById("category").value,
        stock:Number(document.getElementById("stock").value)||0,
        isNew:document.getElementById("isNew").checked,
        isOffer:document.getElementById("isOffer").checked
      });
      if(image!==null) p.image=image;
    }else{
      if(products.some(x=>x.code.toLowerCase()===code.toLowerCase())){
        alert("Product code already exists.");return;
      }
      products.push({
        id:crypto.randomUUID ? crypto.randomUUID() : Date.now()+"-"+Math.random(),
        code,name,
        description:document.getElementById("description").value.trim(),
        price:document.getElementById("price").value||0,
        oldPrice:document.getElementById("oldPrice").value||"",
        category:document.getElementById("category").value,
        stock:Number(document.getElementById("stock").value)||0,
        image:image||"",
        isNew:document.getElementById("isNew").checked,
        isOffer:document.getElementById("isOffer").checked
      });
    }
    saveDB();closeProduct();render();
  };

  if(file){
    const reader=new FileReader();
    reader.onload=e=>finish(e.target.result);
    reader.readAsDataURL(file);
  }else{
    finish(editId ? null : "");
  }
}

function deleteProduct(id){
  const p=products.find(x=>x.id===id);
  if(!p)return;
  if(!confirm(`Delete "${p.name}"?`))return;
  products=products.filter(x=>x.id!==id);
  saveDB();render();
}
function clearAll(){
  if(!products.length)return;
  if(!confirm("Delete ALL products? This cannot be undone."))return;
  products=[];saveDB();page=1;render();
}

function openImport(){
  document.getElementById("csvFile").value="";
  document.getElementById("importStatus").textContent="";
  document.getElementById("progressWrap").style.display="none";
  document.getElementById("progressBar").style.width="0";
  document.getElementById("importModal").style.display="grid";
}
function closeImport(){document.getElementById("importModal").style.display="none"}

function parseCSVLine(line){
  const out=[];let cur="",quoted=false;
  for(let i=0;i<line.length;i++){
    const c=line[i];
    if(c==='"'){
      if(quoted && line[i+1]==='"'){cur+='"';i++}
      else quoted=!quoted;
    }else if(c===","&&!quoted){out.push(cur.trim());cur=""}
    else cur+=c;
  }
  out.push(cur.trim());return out;
}
async function startImport(){
  const file=document.getElementById("csvFile").files[0];
  if(!file){alert("Choose a CSV file first.");return}
  const text=await file.text();
  const lines=text.split(/\r?\n/).filter(x=>x.trim());
  if(lines.length<2){alert("CSV has no product rows.");return}

  const headers=parseCSVLine(lines[0]).map(x=>x.toLowerCase());
  let added=0,updated=0,skipped=0;

  const wrap=document.getElementById("progressWrap");
  const bar=document.getElementById("progressBar");
  const status=document.getElementById("importStatus");
  wrap.style.display="block";

  for(let i=1;i<lines.length;i++){
    const vals=parseCSVLine(lines[i]);
    const row={};
    headers.forEach((h,j)=>row[h]=vals[j]??"");
    if(!row.code||!row.name){skipped++;continue}

    const existing=products.find(p=>p.code.toLowerCase()===row.code.toLowerCase());
    const data={
      code:row.code,name:row.name,description:row.description||"",
      price:row.price||0,oldPrice:row.old_price||"",
      category:row.category||"",stock:Number(row.stock)||0,
      image:row.image||"",isNew:String(row.is_new).toLowerCase()==="true",
      isOffer:String(row.is_offer).toLowerCase()==="true"
    };

    if(existing){Object.assign(existing,data);updated++}
    else{
      products.push({id:(crypto.randomUUID?crypto.randomUUID():Date.now()+"-"+i),...data});
      added++;
    }

    if(i%100===0){
      const pct=Math.round(i/(lines.length-1)*100);
      bar.style.width=pct+"%";
      status.textContent=`Importing ${i} / ${lines.length-1}...`;
      saveDB();
      await new Promise(r=>setTimeout(r,0));
    }
  }
  bar.style.width="100%";saveDB();render();
  status.textContent=`Done — ${added} added, ${updated} updated, ${skipped} skipped.`;
  setTimeout(closeImport,1800);
}

function csvEscape(v){return `"${String(v??"").replace(/"/g,'""')}"`}
function exportCSV(){
  if(!products.length){alert("No products to export.");return}
  const head="code,name,description,price,old_price,category,stock,image,is_new,is_offer\n";
  const body=products.map(p=>[
    p.code,p.name,p.description,p.price,p.oldPrice,p.category,p.stock,p.image,p.isNew,p.isOffer
  ].map(csvEscape).join(",")).join("\n");
  const blob=new Blob([head+body],{type:"text/csv;charset=utf-8"});
  const a=document.createElement("a");
  a.href=URL.createObjectURL(blob);a.download="qafila-products.csv";a.click();
  setTimeout(()=>URL.revokeObjectURL(a.href),500);
}
</script>
</body>
</html>
