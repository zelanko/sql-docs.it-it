---
title: Variare la visualizzazione di poligoni, linee e punti in base a regole e dati analitici (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.mapembeddedpolygonlayerproperties.general.f1
- sql12.rtp.rptdesigner.maplinelayerproperties.widthrules.f1
- sql12.rtp.rptdesigner.mapembeddedpointlayerproperties.general.f1
- "10538"
- "10537"
- MICROSOFT.REPORTDESIGNER.MAPMARKER.MARKERSTYLE
- sql12.rtp.rptdesigner.mapembeddedlinelayerproperties.general.f1
- "10531"
- "10536"
ms.assetid: 7f1f5584-37b4-4fa2-ae44-8988c5f0c744
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 17739424bd8963e5b84bf430f84027829366c940
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66104623"
---
# <a name="vary-polygon-line-and-point-display-by-rules-and-analytical-data-report-builder-and-ssrs"></a>Variare la visualizzazione di poligoni, linee e punti in base a regole e dati analitici (Generatore report e SSRS)
  Le opzioni di visualizzazione per poligoni, linee e punti su un livello mappa vengono controllate impostando le opzioni del livello, le regole per gli elementi della mappa sul livello o sostituendo le opzioni per specifici elementi incorporati della mappa su un livello.  
  
 L'applicazione delle opzioni di visualizzazione è determinata in un elenco a partire da quelle con priorità più bassa:  
  
1.  Le opzioni impostate su un livello poligono, un livello linea e un livello punto si applicano a tutti gli elementi della mappa su quel livello, indipendentemente dal fatto che gli elementi della mappa siano incorporati nella definizione del report.  
  
2.  Le opzioni impostate per le regole si applicano a tutti gli elementi della mappa su un livello. Tutte le opzioni di visualizzazione dei dati si applicano solo agli elementi della mappa associati ai dati spaziali. Un'opzione di visualizzazione dei dati richiede di specificare un campo dati su cui basare le variazioni di visualizzazione. È necessario aver impostato i campi delle corrispondenze per i dati analitici e quelli spaziali prima di poter applicare le regole di visualizzazione dei dati. Per altre informazioni, vedere [Mappe &#40;Generatore report e SSRS&#41;](maps-report-builder-and-ssrs.md).  
  
3.  Opzioni impostate per gli elementi incorporati della mappa selezionati. Si noti che quando si sostituiscono le opzioni del livello, le modifiche apportate alla definizione del report sono permanenti. È possibile modificare i valori del campo dati, nonché sostituire le opzioni di visualizzazione per personalizzare la modalità di visualizzazione di poligoni, linee e punti specifici su un livello.  
  
 Oltre a controllare la visualizzazione degli elementi della mappa su un livello, è possibile regolare la trasparenza del livello per consentire ai livelli disegnati per primi di essere visibili attraverso i livelli disegnati in un secondo momento. Per altre informazioni sulla modifica delle opzioni che influiscono sulla mappa o sull'intero livello mappa, vedere [Personalizzare i dati e la visualizzazione di una mappa o di un livello mappa &#40;Generatore report e SSRS&#41;](customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Rules"></a> Informazioni sulle regole  
 È possibile impostare quattro tipi di regole che consentono all'elaboratore di report di regolare automaticamente le proprietà di visualizzazione per gli elementi della mappa su un livello. Le regole variano a seconda del tipo di elementi della mappa: poligoni, linee o punti.  
  
-   **Poligoni.** Variare il colore dei poligoni.  
  
    -   **Punti centrali dei poligoni.** Per i marcatori visualizzati al centro di ogni poligono, variare il colore, le dimensioni e il tipo di marcatore.  
  
-   **Linee.** Variare il colore e la lunghezza riga.  
  
-   **Punti.** Per i marcatori visualizzati per ogni punto, variare il colore, le dimensioni e il tipo di marcatore.  
  
##  <a name="Color"></a> Informazioni sulle regole colore  
 Le regole colore si applicano ai colori di riempimento per poligoni, linee e marcatori che rappresentano punti o punti centrali dei poligoni.  
  
 Le regole colore supportano quattro opzioni:  
  
-   Applica stile modello. Il tema scelto nella procedura guidata definisce lo stile del modello per il livello. Il tema imposta lo stile per il carattere e il bordo, nonché la tavolozza.  
  
-   Visualizza dati tramite tavolozza colori. Si specifica una tavolozza in base a un nome. L'elaboratore di report imposta il colore di ogni elemento della mappa in un livello passando da un colore all'altro della tavolozza e applicando successivamente sfumature più chiare di ogni colore della tavolozza.  
  
-   Visualizza dati tramite intervalli colori. Si specificano un colore iniziale, uno intermedio e uno finale. Quindi si specificano le opzioni di distribuzione. L'elaboratore di report utilizza i valori dell'opzione di distribuzione per creare un set di colori che produce una visualizzazione simile a una mappa di calore. Una mappa di calore visualizza il colore in relazione alla temperatura. Ad esempio su una scala da 0 a 100, i valori bassi sono blu per rappresentare il freddo, mentre i valori elevati sono rossi per rappresentare il caldo.  
  
-   Visualizza dati tramite colori personalizzati. Si specifica un set di colori. L'elaboratore di report imposta il colore di ogni elemento della mappa nel livello passando da un valore all'altro specificato.  
  
 La tavolozza predefinita include il bianco. Per evitare il contrasto forte tra il bianco e gli altri colori della tavolozza, specificare un colore iniziale chiaro.  
  
 Per non assegnare alcun colore agli elementi della mappa che non sono associati ai dati, impostare **Nessun colore** per il colore predefinito per gli elementi della mappa sul livello.  
  
### <a name="color-scale"></a>Scala dei colori  
 Per impostazione predefinita, tutti i valori delle regole colore vengono visualizzati nella scala dei colori, oltre che nella prima legenda. La scala dei colori è progettata per visualizzare un intervallo di colori. Scegliere i dati più importanti da visualizzare nella scala dei colori.  
  
 Per rimuovere i valori che non si desidera includere nella scala dei colori, deselezionare l'opzione della scala dei colori per ogni regola colore di ciascun livello.  
  
##  <a name="Width"></a> Informazioni sulle regole lunghezza riga  
 Le regole spessore si applicano alle linee. Le regole spessore supportano due opzioni:  
  
-   Usa lunghezza riga predefinita. Si specifica la lunghezza riga in punti.  
  
-   Visualizza dati mediante lunghezza riga. Si impostano gli spessori minimo e massimo per la linea, si specifica il campo dati da utilizzare per variare lo spessore, quindi si specificano le opzioni di distribuzione da applicare a tali dati.  
  
##  <a name="Size"></a> Informazioni sulle regole dimensioni marcatore  
 Le regole dimensioni si applicano ai marcatori che rappresentano punti o punti centrali dei poligoni. Le regole dimensioni supportano due opzioni:  
  
-   Utilizza le dimensioni di un marcatore predefinito. Si specificano le dimensioni in punti.  
  
-   Visualizza dati tramite dimensioni. Si impostano le dimensioni minime e massime per il marcatore, si specifica il campo dati da utilizzare per variare le dimensioni, quindi si specificano le opzioni di distribuzione da applicare a tali dati.  
  
##  <a name="Marker"></a> Informazioni sulle regole tipo marcatore  
 Le regole tipo marcatore si applicano ai marcatori che rappresentano punti o punti centrali dei poligoni. Le regole di tipo marcatore supportano due opzioni:  
  
-   Usa tipo marcatore predefinito. Si specifica uno dei tipi di marcatori disponibili.  
  
-   Visualizza dati tramite marcatori. Si specifica un set di marcatori e il relativo ordine di utilizzo desiderato. I tipi di marcatori includono `Circle`, `Diamond`, `Pentagon`, `PushPin`, `Rectangle`, `Star`, `Triangle`, `Trapezoid` e `Wedge`.  
  
##  <a name="Distribution"></a> Informazioni sulle opzioni di distribuzione  
 Per creare una distribuzione di valori, è possibile dividere i dati in intervalli. Si specifica il tipo di distribuzione, il numero di intervalli secondari e i valori minimo e massimo dell'intervallo.  
  
 Nell'elenco seguente, si supponga di disporre di tre elementi della mappa e di sei valori analitici correlati che vanno da 1 a 9999 con i valori seguenti: 1, 10, 200, 2000, 4777, 8999.  
  
-   **Intervallo equo.** Crea intervalli che dividono i dati in intervalli uguali. Per l'esempio, i tre intervalli sarebbero 0-2999, 3000-5999, 6000-8999. Intervallo secondario 1: 1, 10, 200, 500. Intervallo secondario 2: 4777. Intervallo secondario 3: 8999. Questo metodo non prende in considerazione la modalità di distribuzione dei dati. Valori molto grandi o molto piccoli possono distorcere i risultati della distribuzione.  
  
-   **Distribuzione equa** . Crea intervalli che dividono i dati in modo che ogni intervallo disponga di un numero uguale di elementi. Per i dati dell'esempio, i tre intervalli sarebbero 0-10, 11-500, 501-8999. Intervallo secondario 1: 1, 10. Intervallo secondario 2: 200, 500. Intervallo secondario 3: 4777, 8999. Questo metodo può distorcere la distribuzione creando divisioni che occupano intervalli molto grandi o molto piccoli.  
  
-   **Ottimale.** Crea intervalli che regolano automaticamente la distribuzione in modo da creare intervalli secondari equilibrati. Il numero di intervalli secondari è determinato dall'algoritmo.  
  
-   **Personalizzato.** Specifica il numero di intervalli per controllare la distribuzione di valori. Per i dati dell'esempio, è possibile specificare 3 intervalli: 1-2, 3-8, 9.  
  
 I valori di distribuzione vengono utilizzati dalle regole per variare i valori di visualizzazione degli elementi della mappa.  
  
##  <a name="Legends"></a> Informazioni sulle legende e sui relativi elementi  
 Gli elementi delle legende vengono creati automaticamente dalle regole specificate per ogni livello. Le opzioni delle regole consentono di controllare il numero di elementi creati e in quale legenda vengono visualizzati. Per impostazione predefinita, tutti gli elementi per tutte le regole vengono aggiunte alla prima legenda. Per spostare gli elementi dalla prima legenda, creare tutte le necessarie legende aggiuntive e, per ogni regola, specificare la legenda da utilizzare per visualizzare gli elementi risultanti dalla regola. Per nascondere gli elementi in base a una regola, specificare un nome vuoto per la legenda.  
  
 Per controllare il punto in cui viene visualizzata una legenda, utilizzare la finestra di dialogo Proprietà legenda per specificare una posizione rispetto al viewport mappa. Per altre informazioni, vedere [Modificare legende della mappa, scala dei colori e regole associate &#40;Generatore report e SSRS&#41;](change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md).  
  
 Le legende si espandono automaticamente per visualizzare il titolo o il testo della legenda. Per formattare il testo degli elementi della legenda, utilizzare le parole chiave della legenda della mappa e i formati personalizzati. Per altre informazioni, vedere [Modificare legende della mappa, scala dei colori e regole associate &#40;Generatore report e SSRS&#41;](change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md).  
  
 Nelle tabelle seguenti vengono mostrati esempi di formati diversi che è possibile utilizzare.  
  
|Parola chiave e formato|Descrizione|Esempio di testo visualizzato nella legenda|  
|------------------------|-----------------|---------------------------------------------------|  
|`#FROMVALUE {C0}`|Visualizza la valuta del valore totale senza posizioni decimali|$400|  
|`#FROMVALUE {C2}`|Visualizza la valuta del valore totale con due posizioni decimali.|$400.55|  
|`#TOVALUE`|Visualizza il valore numerico effettivo del campo dati.|10000|  
|`#FROMVALUE{N0} - #TOVALUE{N0}`|Visualizza i valori numerici effettivi dell'inizio e della fine dell'intervallo.|10 - 790|  
  
## <a name="see-also"></a>Vedere anche  
 [Modificare legende della mappa, scala dei colori e regole associate &#40;Generatore report e SSRS&#41;](change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md)   
 [Mappe &#40;Generatore report e SSRS&#41;](maps-report-builder-and-ssrs.md)   
 [Creazione guidata mappa e Creazione guidata livello mappa &#40;Generatore report e SSRS&#41;](map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)  
  
  
