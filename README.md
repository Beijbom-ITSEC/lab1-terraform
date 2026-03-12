# lab1-terraform
Repo för lab1-terrafrom i devsecops kursen

Vad gör projektet?
Projektet använder github actions och terrafrom för att skapa en ubuntu VM på GCS. Det skapar även en daglig backup av VM:en. Via github actions körs kontroller av terrafrom handligens struktur, säkerhet och konfiguring.
Det finns även ett startup script som VM maskinen gör som innehåller enkla hardnings handlingar som att instalera brandvägg och konfigureringar. Det skapas även en log om handlingar i scriptet ifall av error.

Hur man kör: terraform init, plan, apply
För att terraform ska funka måste man först ha det instalerat och ha .tf filer i directoryt man kör det it. Man börjar med terraform init som ser till att provider plugins finns och startar upp miljön som terrafrom behöver för att fungera. 

terraform plan kör man efteråt och då får man en "rapport" om vilka förendringar som kommer hända, vad som kommer tas bort, vad som kommer skapas och vad som kommer ändras.

terrafrom apply tillämpar sedan dom ändringarna som plan visade och slutför dom så att det blir aktuellt i infrastrukturen.


Screenshot över terraform pipeline:
<img width="1887" height="896" alt="2026-03-11-115318_hyprshot" src="https://github.com/user-attachments/assets/67dc48e5-0d5b-40e1-91c0-edacbb583bb5" />




Screenshot om att VM har skapats på Google Cloud.
<img width="1309" height="48" alt="2026-03-12-085542_hyprshot" src="https://github.com/user-attachments/assets/d23f1fcc-2ccf-4c89-8532-672830eaa3c5" />




Säkerhetsbeslut (varför ufw, fail2ban, etc.):
UFW är en väldigt enkel brandvägg som by default stoppar all inkommande trafik. Den är även väldigt lätt att konfigurera beroende på vad vilken trafik man behöver slappa in eller ut som t.ex ssh. 
fail2ban är också ett enkelt verktyg som skyddar en maskin mot bruteforce attacker. Bra att ha ifall man är uppen på internet och behöver stoppa trafik från samma IP address som försöker ta sig in. Då blir dom automatiskt bannade.
dpkg-reconfigure -plow unattended-upgrades gör så att systemet automatisk uppdaterar sig så att det konstant patchas vid behov. Att mjukvara är uppdaterad är en viktig del av att säkerställa maskiner.
