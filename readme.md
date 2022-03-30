#Devilseye installieren

git clone https://github.com/rly0nheart/thedevilseye.git

cd thedevilseye

pip install -r requirements.txt

#Suche nach Suchbegriff wie "osint" und speichern in Datei

python3 eye -q osint > done.txt

#Tor installieren

sudo apt install tor

#Download der Seiten mit wget ->  mit -t wird definiert wie oft der Download versucht werden soll

cat done.txt | grep ".onion" | awk '{print "torsocks wget -t 1 "$1}' |bash 2>log

#Zuordnung Onion Seite zu Datei

cat log | grep "Wird in.*index" -B3 | egrep "([a-z0-9]+\.onion\)|index[^ ]+)" -o | tr  ")" ";" | tr -d "\n" | tr "«" "\n"

#Dateien umbenennen, so dass sie nicht auf .1 .2 etc enden sondern auf .html

ls index* | awk -F "." '$3~/[0-9]$/{print "mv " $0" " $1$3"."$2}
