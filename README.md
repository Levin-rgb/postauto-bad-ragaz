# postauto-bad-ragaz
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>PostAuto Bad Ragaz – Ortsbus</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      background-color: #f9f9f9;
      color: #333;
    }

    header {
      background-color: #FFCC00;
      padding: 1rem;
      display: flex;
      align-items: center;
      justify-content: space-between;
    }

    header img {
      height: 50px;
    }

    nav a {
      margin-left: 1rem;
      text-decoration: none;
      color: #333;
      font-weight: bold;
    }

    .hero {
      background: url('Ortsbus Bad Ragaz.jpg') center/cover no-repeat;
      height: 300px;
      display: flex;
      align-items: center;
      justify-content: center;
      color: white;
      font-size: 2rem;
      font-weight: bold;
      text-shadow: 1px 1px 4px black;
    }

    main {
      padding: 2rem;
    }

    section {
      margin-bottom: 2rem;
    }

    .fahrplan a {
      display: block;
      margin: 0.5rem 0;
      color: #0066cc;
    }

    footer {
      background: #222;
      color: #fff;
      text-align: center;
      padding: 1rem;
      font-size: 0.9rem;
    }

    #live-abfahrten {
      list-style: none;
      padding-left: 0;
    }

    #live-abfahrten li {
      margin-bottom: 0.5rem;
    }
  </style>
</head>
<body>

  <header>
    <img src="Logo_PostAuto.svg.png" alt="Postauto Logo">
    <nav>
      <a href="#linien">Linien</a>
      <a href="#tarife">Tarife</a>
      <a href="#netzplan">Netzplan</a>
      <a href="#abfahrten">Abfahrten</a>
      <a href="#kontakt">Kontakt</a>
    </nav>
  </header>

  <div class="hero">
    Willkommen beim Ortsbus Bad Ragaz
  </div>

  <main>
    <section id="linien">
      <h2>Linien & Fahrpläne</h2>
      <div class="fahrplan">
        <h3>Linie 456 – Bahnhof – Pizolbahn</h3>
        <a href="fahrplan-456.pdf" target="_blank">Fahrplan 456 (PDF)</a>

        <h3>Linie 451 – Pfäfers – Valens – Vättis – Gigerwald</h3>
        <a href="fahrplan-451.pdf" target="_blank">Fahrplan 451 (PDF)</a>

        <h3>Linie 453 – Schluchtenbus (Altes Bad Pfäfers)</h3>
        <a href="fahrplan-453.pdf" target="_blank">Fahrplan 453 (PDF)</a>

        <h3>Linie 022 – Fläsch – Maienfeld – Jenins – Landquart</h3>
        <a href="fahrplan-022.pdf" target="_blank">Fahrplan 022 (PDF)</a>
      </div>
    </section>

    <section id="tarife">
      <h2>Tarife</h2>
      <p>Gültig in der Ostwind-Zone 382 (Bad Ragaz). Tickets sind an Automaten, via App oder beim Chauffeur erhältlich.</p>
      <ul>
        <li>Einzelticket: 3.30 CHF</li>
        <li>Tageskarte: 6.60 CHF</li>
        <li>Mehrfahrtenkarte: 18.20 CHF</li>
      </ul>
    </section>

    <section id="netzplan">
      <h2>Liniennetzplan</h2>
      <a href="liniennetzplan-badragaz.pdf" target="_blank">Liniennetzplan Bad Ragaz (PDF)</a>
    </section>

    <section id="abfahrten">
      <h2>Live-Abfahrtszeiten – Bad Ragaz</h2>
      <ul id="live-abfahrten">Lade Live-Daten …</ul>
    </section>

    <section id="kontakt">
      <h2>Kontakt</h2>
      <p>PostAuto Region Ostschweiz<br>
         Bahnhof Bad Ragaz<br>
         7310 Bad Ragaz<br>
         Tel: +41 81 300 00 00<br>
         E-Mail: <a href="mailto:info@postauto.ch">info@postauto.ch</a>
      </p>
    </section>
  </main>

  <footer>
    &copy; 2025 Postauto Bad Ragaz – Alle Rechte vorbehalten
  </footer>

  <script>
    fetch("https://transport.opendata.ch/v1/stationboard?station=Bad Ragaz&limit=5")
      .then(response => response.json())
      .then(data => {
        const board = data.stationboard;
        const output = document.getElementById("live-abfahrten");
        output.innerHTML = '';
        board.forEach(item => {
          const line = `${item.category} ${item.number}`;
          const to = item.to;
          const time = new Date(item.stop.departure).toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'});
          output.innerHTML += `<li>${line} → ${to} – ${time}</li>`;
        });
      })
      .catch(() => {
        document.getElementById("live-abfahrten").innerHTML = "<li>Fehler beim Laden der Live-Daten.</li>";
      });
  </script>

</body>
</html>
