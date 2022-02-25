# Projekt-VideoAnzeigen
Projekt VideoAnzeigen
/*Cookie is set and read from the first inputs.

 Data is fetched from a Json file, each containing the title of a film as a key and the URL as a value. The Json file was created manually and unfortunately only contains 2 lines.

 The dome is changed and onClick traders are added to open the DIVs (toggler[i].onclick = function). Originally, we did this with EventListener ( toggler[i].addEventListener("click", function ()).

 Data is fetched from an HTML snippet as HTML. In the snippet, the string is changed in the "memory" (insertPart1 + theURL + insertPart2) and the video is replaced.

 The DOM in the document is changed (container.innerHTML = all). 
 Then event handlers will be attached to the inputs before the movies. However, these do not work as hoped.


 End first project

 We end the first project, because with the previous concept we can only create nested handlers and therefore cannot get to the inner inputs without the parent element disappearing again.

 Second project:
 We see a replacement possibility: we build the dome with all videos at the beginning and set the handlers with j_Query - in parallel. The elements are not visible as before. But for that we have to start completely new and get tangled up and maybe.

 So we would rather do a second sub-project and instead of setting the videos and their URLS manually, read them from the DOM and store them. This would make project 1 a little "bigger" - more data.
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
