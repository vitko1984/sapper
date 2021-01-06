<svelte:head>
	<title>About</title>
</svelte:head>

<h1>About this site</h1>

<p>This is the 'about' page. There's not much here.</p>
<div class="body">
  <header class="pageHeader">Header</header>
  <nav class="mainNav">Nav</nav>
  <article class="mainArticle">Article</article>
  <div class="siteAds">Ads</div>
  <footer class="pageFooter">Footer</footer>
</div><br />
<div class="grid">
  <div>1</div>
  <div>2</div>
  <div>3</div>
  <div>4</div>
  <div>5</div>
  <div>6</div>
</div><br />
<div class="outer-grid">
  <div>1</div>
  <div>2</div>
  <div>3</div>
  <div class="inner-grid">
    <div>5</div>
    <div>6</div>
    <div>7</div>
    <div>8</div>
  </div>
</div>

<style>
.body {
  display: grid;
  grid-template-areas: 
  "header header header"
  "article nav ads"
  "footer footer footer"
  ;
  grid-template-rows: 80px 1fr 70px;
  grid-template-columns: 1fr 20% 15%;
  height: 100vh;
  margin: 0;
  gap: 10px;
}
.pageHeader {
  grid-area: header;
}
.pageFooter {
  grid-area: footer;
}
.mainNav {
  grid-area: nav;
}
.mainArticle {
  grid-area: article;
}
.siteAds {
  grid-area: ads;
}
header, footer, nav, article, .siteAds {
  background: gold;
  padding: 20px;
}
@media all and (max-width:575px) {
  .body {
    grid-template-areas: 
    "header"
    "nav"
    "article"
    "ads"
    "footer";
    grid-template-columns: 1fr;
    grid-template-rows: 80px 1fr 70px 1fr 70px;
  }
}
.grid {
  display: grid;
  grid-template-rows: 100px 100px;
  grid-template-columns: 1fr 1fr;
  grid-auto-columns: 200px;
  grid-auto-flow: column;
  gap:10px;
}
.grid>div {
  background: yellowgreen;
  padding: .5em;
  text-align: center;
}
.outer-grid {
  display: grid;
  grid-template-rows: 1fr 1fr;
  grid-template-columns: 1fr 1fr;
  gap: .5em;
}
.outer-grid>div {
  background: limegreen;
  padding: 8px;
  font-size: 4vw;
  color: white;
}
.inner-grid {
  display: grid;
  grid-template-rows: 1fr 1fr;
  grid-template-columns: 1fr 1fr;
  gap:4px;
}
.inner-grid>div {
  background: lightgreen;
  padding: 8px;
}
</style>

