# JS API pro Ki-Wi Kiosk

## Objekt `kiwi`

Objekt `window.kiwi` slouží pro komunikaci mezi HTML aplikací a programem Ki-Wi Kiosk. Tento objekt je dostupný pouze v Ki-Wi Kiosk a proto je vhodné pro testy HTML aplikace v běžném prohlížeči testovat přítomnost tohoto objektu a případně si definovat mock funkce.

```
<script type="text/javascript" charset="utf-8">
if (!window.kiwi) {
  window.kiwi = {};

  kiwi.printer = function(sensor) {
    return false;
  }
}
</script>
```

### Funkce `printerStatus(sensor)`

Funkce `printerStatus` slouží pro zjišťování stavu tiskárny. Parametr sensor je string představující název senzoru a funkce vrací boolean s hodnotou daného senzoru, případně `undefined`, pokud takový sensor neexistuje nebo nemohl být jeho stav zjištěn.

Jsou podporovány tyto typy senzorů:
* 'noPaper'
* 'nearPaperEnd'
* 'ticketOut'
* 'noCover'
* 'paperJam'
* 'printerOnline'
* 'isPrinting'

```
<script type="text/javascript" charset="utf-8">
function logNearPaperEnd(value) {
  if (value === undefined) {
    console.log('Nelze zjistit stav');
  else if (value)
    console.log('Brzy dojde papir!');
  else
    console.log('Vse v poradku');
}

var nearPaperEnd = kiwi.printerStatus('nearPaperEnd');
logNearPaperEnd(nearPaperEnd);
</script>
```
