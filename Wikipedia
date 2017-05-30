function onOpen(e) {
    DocumentApp.getUi().createAddonMenu()
        .addItem('Insert', 'insert')
        .addItem('Typewriter', 'typewriter')
        .addToUi();
}

function onInstall(e) {
    onOpen(e);
}

var content, title, text, body;
function typewriter() {
    var str = "Sphinx of black quartz, judge my vow."
    type(str);
}
function insert() {
    wikipedia();
    content = format(content);
    var par1 = body.insertParagraph(0, title);
    par1.setAlignment(DocumentApp.HorizontalAlignment.CENTER);
    text.appendText(content);
}
function wikipedia(){
     body = DocumentApp.getActiveDocument().getBody();
     text = body.editAsText();
    var response = UrlFetchApp.fetch('https://en.wikipedia.org/w/api.php?&format=json&action=query&generator=random&grnnamespace=0&prop=title&grnlimit=1');
    var json = JSON.parse(response);

    for (key in json.query.pages) {
         title = json.query.pages[key].title;
    }
    var url = 'https://en.wikipedia.org/w/api.php?format=json&action=query&prop=extracts&explaintext=&titles=' + title
    var response2 = UrlFetchApp.fetch(url);
    var json2 = JSON.parse(response2);
    for (key in json2.query.pages) {
         content = json2.query.pages[key].extract;
    }
}
function type(string){
      var split = string.split("");
    for (var i = split.length - 1; i >= 0; i--) {
        text.appendText(split[i]);
        DocumentApp.getActiveDocument().saveAndClose();
        body = DocumentApp.getActiveDocument().getBody();
        text = body.editAsText();
    }
}
function format(txt) {
    txt = '\n' + txt;
    txt = txt.replace(/\===(.+?)\===/g, "").replace(/\==(.+?)\==/g, "").replace(/\n+/g, "\n").replace(/\n/g, "\n" + "            ");
    return txt;
}
