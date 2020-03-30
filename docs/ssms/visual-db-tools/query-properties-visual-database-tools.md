---
title: Proprietà delle query
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:69636
- vdt.ppg.querydesigner.query
ms.assetid: 07495669-6ed5-4004-904e-aae1230be5e4
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: 0be86ddee956542e2637547acc989cf35407f2dd
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "75255332"
---
# <a name="query-properties-visual-database-tools"></a>Proprietà delle query (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Queste proprietà vengono visualizzate nella finestra Proprietà quando in Progettazione query e Progettazione viste è aperta una query. Se non specificato diversamente, tali proprietà possono essere modificate nella finestra Proprietà.  
  
> [!NOTE]  
> Le proprietà in questo argomento sono ordinate per categoria anziché alfabeticamente.  
  
## <a name="options"></a>Opzioni  
**Categoria Identità**  
Viene espansa per visualizzare la proprietà **Nome** .  
  
**Nome**  
Visualizza il nome della query corrente. Non è possibile modificarlo in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
**Nome database**  
Visualizza il nome dell'origine dati della tabella selezionata  
  
**Nome server**  
Visualizza il nome del server dell'origine dati.  
  
**Categoria Progettazione query**  
Viene espansa per visualizzare le proprietà rimanenti.  
  
**Tabella di destinazione**  
Specifica il nome della tabella in cui si stanno inserendo dati. Questo elenco viene visualizzato se si sta creando una query INSERT o MAKE TABLE. Per una query di inserimento, selezionare un nome di tabella nell'elenco.  
  
Per una query di creazione tabella (MAKE TABLE), specificare il nome della nuova tabella. Per creare una tabella di destinazione in un'altra origine dati, specificare un nome di tabella completo che comprenda il nome dell'origine dati di destinazione, il proprietario (se necessario) e il nome della tabella.  
  
> [!NOTE]  
> Progettazione query non consente di verificare se il nome è già in uso o se l'utente dispone dell'autorizzazione necessaria per creare la tabella.  
  
**Valori DISTINCT**  
Consente di specificare che nella query verranno esclusi i duplicati dal set di risultati. Questa opzione risulta utile quando si utilizzano solo alcune colonne della tabella o delle tabelle e tali colonne potrebbero contenere valori duplicati. L'opzione è utile inoltre quando dal processo di unione di due o più tabelle vengono generate righe duplicate nel set di risultati. Selezionare questa opzione equivale a inserire la parola DISTINCT nell'istruzione del riquadro SQL.  
  
**Estensione GROUP BY**  
Specifica che sono disponibili opzioni aggiuntive per le query basate su query di aggregazione (si applica solo a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]).  
  
**Tutte le colonne**  
Specifica che tutte le colonne di tutte le tabelle nella query corrente saranno presenti nel set di risultati. Selezionare questa opzione equivale a specificare un asterisco (*) al posto dei singoli nomi di colonne dopo la parola chiave SELECT nell'istruzione SQL.  
  
**Elenco parametri query**  
Visualizza i parametri della query. Per modificarli, fare clic sulla proprietà e quindi sui puntini di sospensione **(...)** a destra della proprietà. (si applica solo a OLE DB generico).  
  
**Commento SQL**  
Visualizza una descrizione delle istruzioni SQL. Per visualizzare la descrizione completa o modificarla, fare clic su di essa, quindi sui puntini di sospensione **(...)** a destra della proprietà. Nei commenti è possibile specificare ad esempio chi utilizza la query e quando (si applica solo a database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 o versione successiva).  
  
**Categoria Specifica Top**  
Viene espansa per visualizzare le proprietà relative alle proprietà **In alto**, **Percentuale**, **Espressione**e **Con valori equivalenti** .  
  
**(In alto)**  
Specifica che la query includerà una clausola TOP che restituisce soltanto le prime *n* righe o solo il primo *n* percento delle righe del set di risultati. Per impostazione predefinita, la query restituisce le prime 10 righe del set di risultati.  
  
Utilizzare questa casella per cambiare il numero di righe restituite o specificare una percentuale diversa (si applica solo a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o versione successiva).  
  
**Espressione**  
Specifica il numero o la percentuale delle righe che verranno restituite dalla query. Se si imposta **Percentuale** su Sì, il numero indicherà la percentuale delle righe che verranno restituite dalla query, mentre se si imposta **Percentuale** su No, il valore rappresenterà il numero di righe da restituire (si applica solo a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 o versione successiva).  
  
**Percentuale**  
Specifica che la query restituirà soltanto il primo *n* percento delle righe del set di risultati (si applica solo a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 o versione successiva).  
  
**Con valori equivalenti**  
Specifica che la vista includerà una clausola WITH TIES. WITH TIES è utile se nella vista sono incluse anche una clausola ORDER BY e una clausola TOP basata sulla percentuale. Se questa opzione è impostata e la percentuale limite specificata cade all'interno di un set di righe con valori identici nella clausola ORDER BY, la vista verrà estesa oltre tale percentuale fino a includere tutte queste righe (si applica solo a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 o versione successiva).  
  
## <a name="see-also"></a>Vedere anche  
[Esecuzione di query con parametri &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-parameters-visual-database-tools.md)  
[Procedure per la progettazione di query e viste &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
