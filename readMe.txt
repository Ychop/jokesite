Der Code für die Witze seite wurde in 4 komponenten aufgeteilt:

- Toolbar: Enthält die Suche/ den Button um einen Witz hinzuzufügen und Filter um die Witze Liste zu sortieren
- Liste: Zeigt alle Witze an (Fungiert als Hauptseite)
- Witzerstellen: Ruft eine Seite auf in der Man einen Witz zur Liste hinzufügen kann
- Suche: gibt eine Liste aus die das Gesuchte Wort im Titel des Witzes enthält

Diese Achitektur wurde gewählt, da jede komponente einen Screen auf der webseite repräsentiert.
Als Hilfestellung wurde die Prof-rating app verwendet


Beschreibung des Codes:

in App.vue werden alles komponenten zusammen gefügt. 
mit dem v-show wird geprüft welche seite gerade offen/sichtbar ist bzw. sein sollte.
Über die Suchleiste in der Toolbar kann man einen Witz anhand des titels suchen.
Der + button öffnet eine neue Seite indem man einen Witz erstellen kann und zur liste der Witze hinzufügen kann.
das rote Entfernen Icon bei jeden Listen eintrag ermöglicht es einen einen Bestimmten witz aus der Liste und dem Server zu entfernen.
Bei Sortieren nach kann man einmal nach der Id des Witzes oder nach dessen Bewertung sortieren.

Lokal Starten:

terminal starten.
Wechseln in den Ordner jokesite/src/ReST Server.
node server.js eingeben.
nun in das jokesite verzeichniss wechseln und "npm run serve" eingeben
Die webseite sollte nun unter localhost 8080 und der server under localhost 8081 verfügbar sein.

Heroku Backend-Link:

	https://jokesiteserver.herokuapp.com/jokes
or
	https://jokesiteserver.herokuapp.com

Netify Frontend-Link:

	

