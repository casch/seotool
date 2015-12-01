<h1>SEO Tool v2 by damianschwyrz.de</h1>
<p>Das Tool bietet im Grunde die gleichen Funktionen, wie die erste Version. Hinzugekommen sind einige neue Funktionen, die Codebasis wurde komplett überarbeitet. Außerdem kommt ein ordentliches Adminpanel zum Einsatz. Ich hab mich da für SB Admin entschieden.</p>
<h2>Voraussetzungen</h2>
<p>Wie auch schon bei der ersten Version: Es ist notwendig einen Cronjob per SSH auszuführen, d.h. ein normaler Webspace reicht in der Regel nicht aus. Ursächlich hierfür ist, dass das auszuführende Programm in Perl geschrieben ist und je nach Anzahl von Keywords bis zu 45 Minuten am Stück aktiv ist. So etwas lässt sich nur schwer mit PHP realisieren, man müsste in den Serverkonfigurationen einiges abändern (Max Exec Time etwa,...).</p>

<strong>Ansonsten:</strong>
<ul>
<li>Server mit SSH-Zugang (d.h. kein Webspace nicht geeignet)</li>
<li>PHP 5.6</li>
<li>MYSQL 5.5</li>
<li>PERL 5.20</li>
<li>Grundlegende Serveradmin-Kenntnisse</li>
<li>Subdomain</li>
</ul>

<h2>Installationsanleitung</h2>
<p>Ich bitte die folgende Anweisung exakt zu lesen und zu befolgen. Der Installationsprozess gestaltet sich hier nicht trifvial, wer das Tool nutzen will, aber nicht in der Lage ist es aufzusetzen, <strong>kann mich beauftragen</strong> einen kleinen Server mit dem Tool aufzusetzen. Hier reichen kleine vServer vollkommen aus.</p>

<h3>Schritt 1: Subdomain einrichten</h3>
<p>Das Tool funktioniert ausschließlich unter einer Subdomain. Legt diese mit einer eurer Domains an - eine TLD allgemein oder IP-Adresse wird ebenfalls funktionieren.</p>
<h3>Schritt 2: Repo klonen oder herunterladen</h3>
<p>Einfach alle Dateien, die man hier im Repo sieht an die entsprechende Stelle klonen bzw. das Paket herunterladen. Meist ist das sowas wie: /var/www/euredomain.de/web/</p>
<h3>Schritt 3: htaccess/nginx anpassen</h3>
<p>Das Tool wurde mit dem SLIM Framework 3 RC2 programmiert und entsprechend gilt die folgende Anleitung: Weiter zu <a href="http://www.slimframework.com/docs/start/web-servers.html" target="_blank">slimframework.com</a></p>
<p><strong>WICHTIG:</strong> Der Dokumentenroot MUSS auf public/ zeigen. Das ist eben das Verzeichnis, das ihr über die Subdomain ansteuert. Alle wichtigen Dateien sind außerhalb dieses Ordners und somit nicht für den Nutzer via Browser erreichbar!</p>
<h3>Schritt 4: Composer initialisieren und Abhängigkeiten installieren</h3>
<p>Per SSH einloggen, in das Verzeichnis mit allen Dateien wechseln und mit "composer install" und anschließend "composer dump-autoload -o" alle Abhängigkeiten installieren lassen. Diese sind in der composer.json vermerkt. Das ist wichtig, ansonsten fehlen eben wichtige Komponenten für das Tool. Allgemeine Hinweise zur Verwendung von composer findet man unter <a href="https://getcomposer.org/" target="_blank">getcomposer.org</a></p>
<h3>Schritt 5: Einstellungen anpassen</h3>
<p>In app/settings.php und install/seotracker.pl müssen die Zugangsdaten für die MySQL-Datenbank samt Datenbankname angepasst werden.</p>
<h3>Schritt 6: Import des SQL-Dumps</h3>
<p>In install/ befindet sich eine sql-Dump, der in die Datenbank importiert werden muss.</p>
<h3>Schritt 7: Cronjob einrichten</h3>
<p>Der Cronjob muss folgendermaßen eingerichtet werden. Jede Stunde muss der Cronjob zur vollen Stunde gestartet werden. In der Regel loggt man sich auf den Server per SSH ein, und startet "crontab -e". Hier trägt etwas in der Form ein:</p>
<p><em>0 * * * * perl /var/www/pfad/zur/datei/web/cron/seotracker.pl</em></p>
<h3>Schritt 8: Im Browser URL/Subdomain aufrufen</h3>
<p>Mit den Standard-Login-Daten kann man sich einloggen und anfangen Projekte anzulegen.</p>

<h3>Tipp: Fakedaten generieren</h3>
<p>Um alles mit Fakedaten zu testen, kann man diese über den Aufruf von http://eure.domain.de/mocker/ schnell und einfach generieren.</p>