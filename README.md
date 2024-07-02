<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Daten-Tool</title>
</head>
<body>
  <form id="dataForm">
    <label for="dataInput">Daten eingeben:</label>
    <input type="text" id="dataInput" name="dataInput">
    <button type="button" onclick="sendData()">Senden</button>
  </form>
  <div id="response"></div>

  <script>
    // Funktion zum Abrufen von Daten aus der Datenbank
    function fetchData() {
      fetch('https://deine-api-endpoint.com/getData')
        .then(response => response.json())
        .then(data => {
          // Hier kannst du die Daten in deinem Formular oder auf deiner Seite anzeigen
          document.getElementById('dataInput').value = data.value;
        })
        .catch(error => console.error('Fehler beim Abrufen der Daten:', error));
    }

    // Funktion zum Senden von Daten an die Datenbank
    function sendData() {
      const dataInput = document.getElementById('dataInput').value;

      fetch('https://deine-api-endpoint.com/sendData', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({ value: dataInput })
      })
        .then(response => response.json())
        .then(data => {
          document.getElementById('response').innerText = 'Daten erfolgreich gesendet!';
        })
        .catch(error => console.error('Fehler beim Senden der Daten:', error));
    }

    // Abrufen der Daten beim Laden der Seite
    document.addEventListener('DOMContentLoaded', fetchData);
  </script>
</body>
</html>
