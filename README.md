# Projekt-VideoAnzeigen
Projekt VideoAnzeigen
/* 
Cookie wird gesetzt und gelesen aus den ersten Inputs

Es werden Daten aus einem Json File geholt, die jeweils den Titel eines Filmes als Key sowie die URL als Value enthalten.Das Json-File wurde manuell erstellt und beinhaltet leider nur 2 Zeilen

Der Dom wird verändert und es werden onClick-Händler eingebaut um die DIVs zu öffnen (toggler[i].onclick = function). Ursprünglich machten wir dies mit EventListener (  toggler[i].addEventListener("click", function ())

Es werden Daten aus einem HTML-Snippet geholt als HTML. In dem Snippet wird im "Speicher" der String verändert (einbauTeil1 + dieURL + einbauTeil2) und das Video ausgetauscht.

Der DOM im Dokument wird verändert (container.innerHTML = alles). 
Dann werden Event-Händler an die Inputs vor den Filmen gehängt werden. Diese funktionieren aber nicht wie gehofft.


Ende erstes Projekt

Wir enden das erste Projekt, da wir mit dem bisherigen Konzept nur nested-Handler erzeugen können und deshallb nicht an die inneren Inputs kommen ohne das das Parent-Element wieder verschwindet.

Zweites Projekt:
Wir sehen eine Ersatz-Möglichkeit: wir bauen den Dom mit allen Videos am Anfang auf und setzen die Handler mit j_Query - parallel. Die Elemente sind nicht sichtbar wie bisher. Aber dazu müssen wir komplett neu anfangen und verheddern und vielleicht.

Deshalb würden wir lieber ein zweites Teilprojekt machen und statt die Videos und deren URLS manuell zu setzen, diese aus dem DOM auszulesen und abzulegen. Damit würde Projekt 1 etwas "Größer" - mehr Daten.
*/
"use strict"

let komplettesCookie = document.cookie
console.log("komplettesCookie", komplettesCookie)


var dieNote = komplettesCookie.split('=')[1] * 1;
console.log("dienote", dieNote)

//var dieseUrl = komplettesCookie.split(';')[1];
//console.log("dieseURL",dieseUrl)
//var komplettesCookie = note.split('=')[1] * 1;

let container, xg
let geholt = arrayHolen("");
function arrayAusHandlerHolen(geholtesArray) {
    geholt = geholtesArray
}
//Verwendung von Ajax und jSON
function arrayHolen(linkName) {
    let arryGeholt = new XMLHttpRequest();
    arryGeholt.onload = function () {
        if (arryGeholt.status != 200) {
            container.textContent = "Oops";
            return;
        }
        arrayAusHandlerHolen(arryGeholt.responseText);
    };
    arryGeholt.open("GET", "Zuordnungen.json");
    arryGeholt.send();
}

let ersteInputs = document.querySelectorAll("input");
if (dieNote > -1) {
    ersteInputs[dieNote].checked = true
}




for (let i = 0; i < ersteInputs.length; i++) {
    //    toggler[i].addEventListener("click", function () {

    ersteInputs[i].addEventListener("click", function () {
        console.log(this.id)
        document.cookie = "Note=" + i;
        console.log("note", document.cookie)

    })
}


let toggler = document.getElementsByClassName("caret");
let i;
for (i = 0; i < toggler.length; i++) {
    //  console.log(toggler[i]);
    //  console.log()
    var newUl = document.createElement("ul");
    //   console.log(newUl)
    newUl.className = "nested"
    var newDiv = document.createElement("div");

    let weiter = toggler[i].append(newUl);

    xg = toggler[i].querySelector("ul").appendChild(newDiv);

    //xg.innerText="123"
}
let austausch
console.log("togglerlänge", toggler.length)
for (i = 0; i < toggler.length; i++) {
    //Arbeiten mit Events

    toggler[i].onclick = function (event) {
        //console.log("ClassName", this)
        //console.log("event", event)

        this.classList.toggle("caret-down");
        this.parentElement.querySelector(".nested").classList.toggle("active");
        /*  if (this.parentElement.querySelector(".nested").className == "nested active") {
             let dieInputs = this.querySelectorAll("input");
             console.log("dieInputs", dieInputs)
             for (let t = 0; t < dieInputs.length; t++) {
                 let ZZ = dieInputs[t].addEventHandler("click", function () {
                     alert(1)
                 })
             }
         } */


        container = this.querySelector("div");

        let dieURL

        let ueberschrift = container.parentElement.parentElement.parentElement.innerText

        let geparstgeholt = JSON.parse(geholt)
        let ueberschriftPur = ueberschrift.split("\n")[0];
        console.log("ueberschrift", ueberschriftPur)
        for (let u = 0; u < geparstgeholt.length; u++) {
            //console.log(geparstgeholt[u])
            let gefunden = geparstgeholt[u];
            dieURL = gefunden[ueberschriftPur];
            //console.log("dieurl", dieURL, u, ueberschriftPur)

            if (dieURL) {
                dieURL = decodeURIComponent(gefunden[ueberschriftPur]);

                dieURL = gefunden[ueberschriftPur];
                console.log("ok", ueberschriftPur, dieURL)
                loadContent(dieURL)
            }
            ;

        };

    }
}

// Funktion soll Snippets über AJAX laden und in Container integrieren
function loadContent(dieURL) {
    console.log("dieurl", dieURL)
    let xhr = new XMLHttpRequest();
    xhr.onload = function () {
        if (xhr.status != 200) {
            container.textContent = "Oops";
            return;
        }

        let einbau = xhr.responseText
        ///Verwendung von Arrays und String und SPLIT
        let einbauTeil1 = einbau.split("|||")[0]
        let einbauTeil2 = einbau.split("|||")[1]

        // Zusammenbau

        let zielTag = container.parentElement.parentElement
        let dasZiel = container.parentElement.parentElement.parentElement.querySelector('.caret')




        let dieURL2 = dieURL.replace("localhost", "www.youtube.com");

        let derText = dasZiel.innerHTML
        let neuerText = "<a href ='" + dieURL2 + "' target = 'new'>" + container.parentElement.parentElement.parentElement.innerText + "</a><ul class=\"nested active\"><div></div></ul>"
        console.log("neuerText", neuerText)
        //"Introduction to Arrays with JavaScript<ul class=\"nested active\"><div></div></ul>"
        //   "<a href ='dieurl'>Introduction to Arrays with JavaScript</a><ul class=\"nested active\"><div></div></ul>"
        // dasZiel.innerText="Thomas"
        console.log("zielTag", zielTag)
        console.log("dertext", derText)
        //console.log("einbau1", einbauTeil1)
        //dasZiel.innerHTML = neuerText

        //let alles = neuerText + einbau
        //console.log("einbau",alles)
       let alles = einbauTeil1 + dieURL2 + einbauTeil2

        console.log("Container", container)
        //Erzeugung und Integration von DOM-Teilbäumen
        console.log("alles", alles)
        container.innerHTML = alles
        //let ueberschrift = container.parentElement.parentElement.parentElement.innerText
        let dieURLXYZ = dieURL2

        let erg = dieURLXYZ //.replace("www.youtube.com","localhost")
        console.log("ERG",erg)
        let unsereNotehier = localStorage.getItem(erg)*1
        

        console.log("unsereNotehier", unsereNotehier, erg)
        container.querySelectorAll("input")[unsereNotehier].checked = true
        console.log("derText", derText)
        let inputs = container.querySelectorAll("input");
        console.log("neueInputs", inputs)
        for (let t = 0; t < inputs.length; t++) {
            inputs[t].onclick = function () {
                this.selected = true
                localStorage.setItem(dieURL, t);

                alert(t)
            }
        }
    };
    xhr.open("GET", "inlineHTML.html");
    xhr.send();

}
