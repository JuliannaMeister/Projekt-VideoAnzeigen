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
