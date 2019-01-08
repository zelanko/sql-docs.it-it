---
title: Il contenuto di FORMAT_STRING (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: da10e8ab533c2fbfec76c89527fca0fd67082a6d
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52535371"
---
# <a name="mdx-cell-properties---formatstring-contents"></a>Proprietà delle celle MDX - Contenuto di FORMAT_STRING
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  La proprietà **FORMAT_STRING** di una cella determina la formattazione della proprietà **VALUE** della cella, creando il valore della proprietà **FORMATTED_VALUE** della cella. La proprietà **FORMAT_STRING** della cella è in grado di gestire valori non elaborati di tipo stringa e numerici, applicando un'espressione di formato a un valore per restituire un valore formattato per la proprietà **FORMATTED_VALUE** . Nelle tabelle seguenti vengono indicati in dettaglio la sintassi e i caratteri di formattazione utilizzati per gestire valori di tipo stringa e numerici.  
  
## <a name="string-values"></a>Valori stringa  
 Un'espressione di formato per le stringhe può includere una sezione oppure due sezioni separate da un punto e virgola (;).  
  
|Uso|Risultato|  
|-----------|------------|  
|Una sezione|Il formato viene applicato a tutti i valori stringa.|  
|Due sezioni|La prima sezione viene applicata ai dati stringa, mentre la seconda sezione viene applicata ai valori Null e alle stringhe di lunghezza zero ("").|  
  
 Nella tabella seguente vengono illustrati i caratteri che è possibile utilizzare nella stringa di formato per le stringhe di caratteri.  
  
|Carattere|Descrizione|  
|---------------|-----------------|  
|@|Rappresenta un segnaposto di carattere al posto del quale viene visualizzato un carattere o uno spazio. Se nella stringa è presente un carattere nella posizione in cui nella stringa di formato è presente il simbolo chiocciola (@), verrà visualizzato il carattere. In caso contrario, in tale posizione della stringa formattata verrà visualizzato uno spazio. I segnaposti vengono sostituiti da destra verso sinistra, a meno che la stringa di formato non includa un punto esclamativo (!).|  
|&|Rappresenta un segnaposto di carattere al posto del quale viene visualizzato un carattere oppure nulla. Se nella stringa è presente un carattere nella posizione in cui è presente il simbolo (&) nella stringa formattata verrà visualizzato il carattere. In caso contrario, nella stringa formattata non verrà visualizzato nulla. I segnaposti vengono sostituiti da destra verso sinistra, a meno che la stringa di formato non includa un punto esclamativo (!).|  
|\<|Impone la visualizzazione di caratteri minuscoli. Tutti i caratteri nella stringa formattata vengono visualizzati in minuscolo.|  
|>|Impone la visualizzazione di caratteri maiuscoli. Tutti i caratteri nella stringa formattata vengono visualizzati in maiuscolo.|  
|!|Impone la sostituzione dei segnaposti da sinistra verso destra. Per impostazione predefinita, i segnaposti vengono sostituiti da destra verso sinistra.|  
  
## <a name="numeric-values"></a>Valori numerici  
 Un'espressione di formato definita dall'utente per i numeri può includere da una a quattro sezioni separate da punti e virgola. Se l'argomento del formato include un formato numerico predefinito, sarà possibile utilizzare una sola sezione.  
  
|Uso|Risultato|  
|-----------|------------|  
|Una sezione|L'espressione di formato viene applicata a tutti i valori.|  
|Due sezioni|La prima sezione viene applicata ai valori positivi e agli zeri, la seconda ai valori negativi.|  
|Tre sezioni|La prima sezione viene applicata ai valori positivi, la seconda ai valori negativi e la terza agli zeri.|  
|Quattro sezioni|La prima sezione viene applicata ai valori positivi, la seconda ai valori negativi, la terza agli zeri e la quarta ai valori Null.|  
  
 Nell'esempio seguente vengono utilizzate due sezioni. La prima definisce il formato per i valori positivi e gli zeri, la seconda definisce il formato per i valori negativi.  
  
```  
"$#,##0;($#,##0)"  
```  
  
 Se si specificano punti e virgola (;) consecutivi, per i valori corrispondenti alla sezione mancante verrà utilizzando il formato per i valori positivi. La stringa di formato seguente, ad esempio, visualizza i valori positivi e negativi utilizzando il formato specificato nella prima sezione e visualizza "Zero" se il valore è zero:  
  
```  
"$#,##0;;\Z\e\r\o"  
```  
  
 Nella tabella seguente sono indicati i caratteri che è possibile utilizzare nella stringa di formato per i formati numerici.  
  
|Carattere|Descrizione|  
|---------------|-----------------|  
|None|Visualizza il numero senza formattazione.|  
|**0**|Rappresenta un segnaposto di cifra al posto del quale viene visualizzata una cifra o uno zero (0).<br /><br /> Se nel numero è presente una cifra nella posizione in cui nella stringa di formato è presente lo zero, nel valore formattato verrà visualizzata la cifra. In caso contrario, in tale posizione del valore formattato verrà visualizzato uno zero.<br /><br /> Se il numero include meno cifre di quanti sono gli zeri nella stringa di formato, su entrambi i lati del separatore decimale, nel valore formattato verranno visualizzati zeri iniziali o finali.<br /><br /> Se, a destra del separatore decimale, il numero include più cifre di quanti sono gli zeri a destra del separatore decimale nell'espressione di formato, il valore formattato verrà arrotondato specificando tante cifre decimali quanti sono gli zeri.<br /><br /> Se, a sinistra del separatore decimale, il numero include più cifre di quanti sono gli zeri a sinistra del separatore decimale nell'espressione di formato, nel valore formattato le cifre aggiuntive verranno visualizzate senza modifiche.|  
|**#**|Rappresenta un segnaposto di cifra al posto del quale viene visualizzata una cifra oppure nulla.<br /><br /> Se nell'espressione è presente una cifra nella posizione in cui nella stringa di formato è presente il simbolo cancelletto (**#**), nel valore formattato verrà visualizzata la cifra. In caso contrario, in tale posizione del valore formattato non verrà visualizzato nulla.<br /><br /> Come segnaposto il simbolo cancelletto (**#**) funziona come lo zero (**0**), con la differenza che, se il valore include un numero di cifre minore o uguale a quello dei caratteri **#** su entrambi i lati del separatore decimale nell'espressione di formato, non verranno visualizzati gli zeri iniziali e finali.|  
|**.**|Rappresenta un segnaposto di decimali che determina il numero di cifre visualizzate a sinistra e a destra del separatore decimale.<br /><br /> Se l'espressione di formato include solo simboli cancelletto (**#**) a sinistra del separatore decimale (**.**), i numeri inferiori a 1 inizieranno con il separatore decimale. Per visualizzare uno zero iniziale con i numeri frazionari, utilizzare zero (0) come primo segnaposto di cifra a sinistra del separatore decimale.<br /><br /> Il carattere effettivo utilizzato come segnaposto di decimali nell'output formattato dipende dal formato numerico riconosciuto dal computer in uso.<br /><br /> Nota: In alcune impostazioni locali come separatore decimale viene utilizzata la virgola.|  
|**%**|Rappresenta un segnaposto di percentuale. L'espressione viene moltiplicata per 100. Il segno di percentuale (**%**) viene inserito nella posizione in cui viene visualizzata la percentuale nella stringa di formato.|  
|**,**|Rappresenta il separatore delle migliaia, che separa le migliaia dalle centinaia all'interno di un numero con quattro o più posizioni a sinistra del separatore decimale.<br /><br /> Se il formato include un separatore delle migliaia racchiuso tra segnaposti di cifra (**0** o **#**), il separatore delle migliaia verrà usato in modo standard.<br /><br /> Se sono presenti due separatori delle migliaia consecutivi oppure un separatore delle migliaia immediatamente a sinistra del separatore decimale, indipendentemente dal fatto che sia specificato un decimale, il numero verrà diviso per 1000 e arrotondato come necessario. È possibile, ad esempio, usare la stringa di formato "**##0**,," per rappresentare 100 milioni come 100. I numeri minori di 1 milione vengono visualizzati come 0. Due separatori delle migliaia adiacenti in una posizione diversa da quella immediatamente a sinistra del separatore decimale vengono considerati elementi che specificano l'utilizzo di un separatore delle migliaia.<br /><br /> Il carattere effettivo utilizzato come separatore delle migliaia nell'output formattato dipende dal formato numerico riconosciuto dal computer in uso.<br /><br /> Nota: In alcune impostazioni locali come separatore delle migliaia viene utilizzato il punto.|  
|**:**|Rappresenta il separatore dell'ora che separa le ore, i minuti e i secondi nei valori di ora formattati.<br /><br /> Nota: In alcune impostazioni locali potrebbero essere utilizzati altri caratteri come separatore dell'ora.<br /><br /> Il carattere effettivo utilizzato come separatore dell'ora nell'output formattato è determinato dalle impostazioni di sistema del computer in uso.|  
|**/**|Rappresenta il separatore della data che separa il giorno, il mese e l'anno nei valori di data formattati.<br /><br /> Il carattere effettivo utilizzato come separatore della data nell'output formattato è determinato dalle impostazioni di sistema del computer in uso.<br /><br /> Nota: In alcune impostazioni locali potrebbero essere utilizzati altri caratteri come separatore della data.|  
|**E- E+ e- e+**|Rappresenta il formato scientifico.<br /><br /> Se l'espressione di formato contiene almeno un segnaposto di cifra (**0** o **#**) a destra di **E-**, **E+**, **e-** o **e+**, il valore formattato verrà visualizzato in formato scientifico e tra il numero e l'esponente verrà inserito il carattere E o e. Il numero di segnaposti di cifra a destra determina il numero di cifre nell'esponente. Usare **E-** o **e-** per inserire un segno di sottrazione accanto agli esponenti negativi. Usare **E+** o **e+** per inserire un segno di sottrazione accanto agli esponenti negativi e un segno di addizione accanto agli esponenti positivi.|  
|**- + $ ( )**|Visualizza un carattere letterale.<br /><br /> Per visualizzare un carattere diverso da quelli elencati, inserire una barra rovesciata (**\\**) prima del carattere o racchiudere il carattere tra virgolette doppie (**" "**).|  
|**\\**|Visualizza il carattere successivo nella stringa di formato.<br /><br /> Per visualizzare un carattere dotato di significato speciale come carattere letterale, inserire una barra rovesciata (**\\**) prima del carattere. La barra rovesciata non viene visualizzata. Utilizzare una barra rovesciata equivale a racchiudere il carattere successivo tra virgolette doppie. Per visualizzare una barra rovesciata, usare due barre rovesciate (**\\\\**). I caratteri che non possono essere visualizzati come caratteri letterali includono i seguenti:<br /><br /> <br /><br /> I caratteri di formattazione della data e ora la formattazione -**una**, **c**, **1!d**, **h**, **m**, **n**, **p**, **q**, **s**, **t**, **w**, **y** , **/**, e **:**<br /><br /> I caratteri di formattazione di numeri -**#**, **0**, **%**, **elettronica**, **elettronica**, **virgole**, e **periodo**<br /><br /> I caratteri di formattazione di stringhe -**@**, **&**, **\<**, **>**, e **!**|  
|**"ABC"**|Visualizza la stringa racchiusa tra virgolette doppie (**" "**).<br /><br /> Per includere una stringa formattata dal codice, racchiudere il testo tra due Chr(**34**). **34**è il codice carattere per la virgoletta doppia.|  
  
### <a name="named-numeric-formats"></a>Formati numerici denominati  
 Nella tabella seguente sono indicati i nomi dei formati numerici predefiniti:  
  
|Nome formato|Descrizione|  
|-----------------|-----------------|  
|`General Number`|Il numero viene visualizzato senza il separatore delle migliaia.|  
|`Currency`|Il numero viene visualizzato con il separatore delle migliaia, quando necessario. Il numero viene visualizzato con cifre a destra del separatore decimale. L'output dipende dalle impostazioni locali del sistema.|  
|`Fixed`|Il numero viene visualizzato con almeno una cifra a sinistra e due a destra del separatore decimale.|  
|`Standard`|In numero viene visualizzato con il separatore delle migliaia e con almeno una cifra a sinistra e due a destra del separatore decimale.|  
|`Percent`|Il numero viene visualizzato moltiplicato per 100 con un segno di percentuale (%) aggiunto a destra. Il numero viene sempre visualizzato con due cifre a destra del separatore decimale.|  
|`Scientific`|Utilizza la notazione scientifica standard.|  
|`Yes/No`|Viene visualizzato No se il numero è 0; in caso contrario, viene visualizzato Sì.|  
|`True/False`|Viene visualizzato Falso se il numero è 0; in caso contrario, viene visualizzato Vero.|  
|`On/Off`|Viene visualizzato Disattivato se il numero è 0; in caso contrario, viene visualizzato Attivato.|  
  
## <a name="date-values"></a>Valori di data  
 Nella tabella seguente sono indicati i caratteri che è possibile utilizzare nella stringa di formato per i formati di data e di ora.  
  
|Carattere|Descrizione|  
|---------------|-----------------|  
|**:**|Rappresenta il separatore dell'ora che separa le ore, i minuti e i secondi nei valori di ora formattati.<br /><br /> Il carattere effettivo utilizzato come separatore dell'ora nell'output formattato è determinato dalle impostazioni di sistema del computer in uso.<br /><br /> Nota: In alcune impostazioni locali potrebbero essere utilizzati altri caratteri come separatore dell'ora.|  
|**/**|Rappresenta il separatore della data che separa il giorno, il mese e l'anno nei valori di data formattati.<br /><br /> Il carattere effettivo utilizzato come separatore della data nell'output formattato è determinato dalle impostazioni di sistema del computer in uso.<br /><br /> Nota: In alcune impostazioni locali potrebbero essere utilizzati altri caratteri per rappresentare il separatore della data.|  
|**C**|Visualizza la data come **ddddd** e l'ora come **ttttt**, in questo ordine.<br /><br /> Se il numero seriale della data non include una parte frazionaria, verranno visualizzate solo le informazioni della data. Se non esiste una parte intera, verranno visualizzate solo le informazioni dell'ora.|  
|**d**|Visualizza il giorno sotto forma di numero senza zero iniziale (1-31).|  
|**gg**|Visualizza il giorno sotto forma di numero con uno zero iniziale (01-31).|  
|**ddd**|Visualizza il giorno nella forma abbreviata (LUN-DOM).|  
|**dddd**|Visualizza il giorno come un nome completo (lunedì-domenica).|  
|**ddddd**|Visualizza la data completa, inclusi il giorno, il mese e l'anno, formattata in base all'impostazione del formato di data breve del sistema in uso.<br /><br /> In Microsoft Windows il formato di data breve predefinito è **g/m/aa**.|  
|**dddddd**|Visualizza un numero seriale di data sotto forma di una data completa, inclusi il giorno, il mese e l'anno, formattata in base all'impostazione del formato di data estesa riconosciuta dal computer in uso.<br /><br /> In Windows il formato di data estesa predefinito è **gg mmmm aaaa**.|  
|**w**|Visualizza il giorno della settimana sotto forma di numero (1 corrisponde al lunedì e 7 alla domenica).|  
|**ww**|Visualizza la settimana dell'anno sotto forma di numero (1-54).|  
|**m**|Visualizza il mese sotto forma di numero senza zero iniziale (1-12).<br /><br /> Se il segnaposto **m** è indicato immediatamente dopo **h** o **hh**, anziché il mese verrà visualizzato il minuto.|  
|**mm**|Visualizza il mese sotto forma di numero con uno zero iniziale (01-12).<br /><br /> Se il segnaposto **m** è indicato immediatamente dopo **h** o **hh**, anziché il mese verrà visualizzato il minuto.|  
|**mmm**|Visualizza il mese nella forma abbreviata (gen-dic).|  
|**mmmm**|Visualizza il mese come nome completo del mese (gennaio-dicembre).|  
|**q**|Visualizza il trimestre dell'anno sotto forma di numero (1-4).|  
|**y**|Visualizza il giorno dell'anno sotto forma di numero (1-366).|  
|**yy**|Visualizza l'anno come numero a due cifre (00-99).|  
|**aaaa**|Visualizza l'anno come numero a quattro cifre (100-9999).|  
|**h**|Visualizza l'ora sotto forma di numero senza zeri iniziali (0-23).|  
|**hh**|Visualizza l'ora sotto forma di numero con zeri iniziali (00-23).|  
|**n**|Visualizza il minuto sotto forma di numero senza zeri iniziali (0-59).|  
|**nn**|Visualizza il minuto sotto forma di numero con zeri iniziali (00-59).|  
|**s**|Visualizza il secondo sotto forma di numero senza zeri iniziali (0-59).|  
|**ss**|Visualizza il secondo sotto forma di numero con zeri iniziali (00-59).|  
|**t t t t t**|Visualizza l'ora completa, inclusi ora, minuti e secondi, formattata utilizzando il separatore dell'ora definito dal formato di ora riconosciuto dal computer in uso.<br /><br /> Se è selezionata l'opzione relativa allo zero iniziale e l'ora è anteriore alle 10.00, verrà visualizzato uno zero iniziale nel ciclo mattutino o pomeridiano . Ad esempio, 09.59.<br /><br /> In Windows il formato di ora predefinito è **h.mm.ss**.|  
|**AM/PM**|Visualizza i caratteri **AM** maiuscoli accanto a tutte le ore da mezzanotte a mezzogiorno e i caratteri **PM** maiuscoli accanto a tutte le ore da mezzogiorno a mezzanotte.<br /><br /> Nota: Utilizza il formato a 12 ore.|  
|**am/pm**|Visualizza i caratteri **am** minuscoli accanto a tutte le ore da mezzanotte a mezzogiorno e i caratteri **pm** minuscoli accanto a tutte le ore da mezzogiorno a mezzanotte.<br /><br /> Nota: Utilizza il formato a 12 ore.|  
|**A/P**|Visualizza il carattere **A** maiuscolo accanto a tutte le ore da mezzanotte a mezzogiorno e il carattere **P** maiuscolo accanto a tutte le ore da mezzogiorno a mezzanotte.<br /><br /> Nota: Utilizza il formato a 12 ore.|  
|**a/p**|Visualizza il carattere **a** minuscolo accanto a tutte le ore da mezzanotte a mezzogiorno e il carattere **p** minuscolo accanto a tutte le ore da mezzogiorno a mezzanotte.<br /><br /> Nota: Utilizza il formato a 12 ore.|  
|**AMPM**|Visualizza la stringa letterale AM in base a quanto specificato dal computer in uso accanto a tutte le ore da mezzanotte e mezzogiorno e la stringa letterale PM in base a quanto specificato dal computer in uso accanto a tutte le ore da mezzogiorno a mezzanotte.<br /><br /> **AMPM** può essere formattato in maiuscolo o in minuscolo, ma la formattazione della stringa effettivamente visualizzata corrisponde alla stringa definita dalle impostazioni di sistema del computer.<br /><br /> In Windows viene usato il formato **AM/PM**per impostazione predefinita.<br /><br /> Nota: Utilizza il formato a 12 ore.|  
  
### <a name="named-date-formats"></a>Formati di data denominati  
 Nella tabella seguente sono indicati i nomi dei formati di data e ora predefiniti:  
  
|Nome formato|Descrizione|  
|-----------------|-----------------|  
|`General Date`|Vengono visualizzate una data e/o un'ora. Per i numeri reali, vengono visualizzate una data e ora, ad esempio, 4/3/93 17:34. Se non vi è parte frazionaria, viene visualizzata solo la data, ad esempio, 4/3/93. Se non vi è parte intera, viene visualizzata solo l'ora, ad esempio, 17:35. Il formato della visualizzazione relativa alla data è determinato dalle impostazioni del sistema.|  
|`Long Date`|Viene visualizzata la data in base al formato di data esteso del sistema.|  
|`Medium Date`|Viene visualizzata una data utilizzando il formato d data medio appropriato alla versione di lingua dell'applicazione host.|  
|`Short Date`|Viene visualizzata la data in base al formato di data breve del sistema.|  
|`Long Time`|Viene visualizzata l'ora in base al formato di data esteso del sistema; in genere comprende ore, minuti e secondi.|  
|`Medium Time`|Viene visualizzata l'ora nel formato a 12 ore utilizzando ore e minuti e l'identificatore AM/PM.|  
|`Short Time`|Viene visualizzata l'ora utilizzando il formato a 24 ore, ad esempio, 17:45.|  
  
## <a name="see-also"></a>Vedere anche  
 [LANGUAGE e FORMAT_STRING in FORMATTED_VALUE](../../../analysis-services/multidimensional-models/mdx/mdx-cell-properties-formatted-value-property.md)   
 [Utilizzo delle proprietà delle celle &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-properties-using-cell-properties.md)   
 [Creazione e utilizzo di valori di proprietà &#40;MDX&#41;](http://msdn.microsoft.com/library/0cafb269-03c8-4183-b6e9-220f071e4ef2)   
 [Nozioni fondamentali sulle query MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
