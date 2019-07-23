---
title: Riquadro Dettagli di Esplora oggetti | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.summary.general.f1
- sql13.swb.summary.report.f1
helpviewer_keywords:
- object search [SQL Server], Object Explorer
- Object Explorer
- object search [SQL Server]
- searching objects [SQL Server]
ms.assetid: b963e3c2-dc9e-4d38-bd28-2e00fe9e0e47
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b51309850e4e36083dbbf5fa228746dac18968ef
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264078"
---
# <a name="object-explorer-details-pane"></a>Riquadro Dettagli di Esplora oggetti
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Dettagli Esplora oggetti è un componente di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] che fornisce una vista tabulare di tutti gli oggetti nel server e offre un'interfaccia utente che consente di gestire tali oggetti. Le funzionalità di Esplora oggetti variano leggermente in base al tipo di server, ma in genere comprendono le funzionalità di sviluppo per i database e di gestione per tutti i tipi di server.  
  
Il riquadro Dettagli Esplora oggetti è visibile in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] per impostazione predefinita. Se Esplora oggetti non è visualizzato, scegliere **Dettagli Esplora oggetti** dal menu **Visualizza** oppure premere **F7**.  
  
> [!NOTE]  
> [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] le date vengono formattate in base alle Opzioni internazionali e della lingua di Microsoft Windows attive al momento dell'avvio di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] . Per applicare altre impostazioni di data, riavviare [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] .  
  
## <a name="object-explorer-details"></a>Visualizza  
Dettagli Esplora oggetti può essere usato per spostarsi tra cartelle e oggetti nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Nei sistemi operativi a 32 bit, Esplora oggetti può visualizzare solo 64.000 oggetti. Per accedere a oggetti aggiuntivi, è necessario selezionare un'icona.  
  
In Dettagli Esplora oggetti è inclusa una barra degli strumenti che contiene le icone descritte nella tabella seguente. Alcune icone sono disponibili solo quando è possibile utilizzarle.  
  
|Icona|Azione|  
|--------|----------|  
|**Indietro**|Passa agli elementi precedenti visualizzati in Dettagli Esplora oggetti. Esegue nuovamente una ricerca se la visualizzazione precedente è il risultato di un'operazione di ricerca.|  
|**Avanti**|Sposta lo stato attivo alla schermata successiva dopo la selezione di un'operazione **Indietro** .|  
|**Su**|Sposta lo stato attivo sulla cartella o l'oggetto padre.|  
|**Sincronizza**|Imposta lo stato attivo di Esplora oggetti sull'oggetto selezionato in Dettagli Esplora oggetti.|  
|**Filter**|Quando disponibile, visualizza un subset di oggetti configurabili.|  
|**Aggiorna**|Aggiorna la visualizzazione del contenuto di Dettagli Esplora oggetti.|  
|**Cerca**|Fornisce un'area nella quale immettere un termine di ricerca per determinati oggetti di database.|  
  
### <a name="column-header-selections"></a>Selezioni di intestazioni di colonna  
Dettagli Esplora oggetti dispone di colonne selezionabili. È possibile fare clic con il pulsante destro del mouse su qualsiasi intestazione di colonna e controllare gli elementi che si desidera visualizzare. Le selezioni risulteranno persistenti per tutti i diversi oggetti sui quali ci si sposta. Le selezioni per ogni utente vengono mantenute quando si esce da [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e lo si riavvia.  
  
> [!CAUTION]  
> La visualizzazione di tutte le colonne di alcuni tipi di oggetto (ad esempio, Databases) può rallentare leggermente il rendering nel caso di grandi set di oggetti.  
  
### <a name="sorting"></a>Ordinamento  
Fare clic su un'intestazione di colonna per ordinare la griglia in base a tale colonna. Fare clic di nuovo sulla stessa intestazione di colonna per invertire l'ordinamento della griglia in base a tale colonna. Le selezioni dell'ordinamento vengono mantenute per ogni utente attraverso oggetti e cartelle e al riavvio di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] .  
  
### <a name="filtering"></a>Filtri  
Certi elenchi di oggetti visualizzati in Dettagli Esplora oggetti possono essere filtrati usando l'icona **Filtro** nella barra degli strumenti Dettagli Esplora oggetti. L'icona diventa disponibile quando è possibile applicare un filtro.  
  
### <a name="details-pane"></a>Riquadro Dettagli  
L'area nell'estremità inferiore di Dettagli Esplora oggetti contiene un pannello nel quale vengono visualizzati determinati dettagli dell'oggetto selezionato. Se si selezionano più oggetti, viene visualizzato solo il conteggio degli oggetti. Quando sono selezionati degli elementi nel pannello, fare clic sull'icona **Copia** per copiare negli Appunti il testo visualizzato.  
  
Il pulsante freccia in giù consente di spostare la selezione sul successivo elemento dell'elenco. Il pulsante freccia in su consente di spostare la selezione sull'elemento precedente dell'elenco. Tenendo premuto il pulsante freccia in giù, è possibile scorrere rapidamente gli elementi. La selezione si arresta una volta raggiunta la fine o l'inizio dell'elenco delle proprietà.  
  
Digitando il primo carattere del nome di una proprietà, la selezione si sposta sulla successiva proprietà che inizia con quel carattere.  
  
Quando le proprietà vengono disposte in più colonne, utilizzare la freccia sinistra e la freccia destra per spostarsi nelle colonne adiacenti.  
  
Per copiare i valori delle proprietà negli Appunti, utilizzare le seguenti combinazioni dei pulsanti della tastiera:  
  
-   Ctrl+C per copiare il valore della proprietà.  
  
-   Ctrl+MAIUSC+C per copiare il nome e il valore della proprietà con un delimitatore di tabulazione.  
  
Utilizzare il menu di scelta rapida nel riquadro delle proprietà Dettagli Esplora oggetti per copiare tutte le proprietà o tutte le proprietà e i nomi negli Appunti.  
  
Per visualizzare per intero il valore di una proprietà quando la larghezza del campo non lo consente, passare con il cursore del mouse sul valore oppure impostare lo stato attivo dell'interfaccia utente sul valore della proprietà per attivare una descrizione comandi con il valore della proprietà completo. Gli screen reader per l'accessibilità riporteranno il valore completo della proprietà quando lo stato attivo dell'utente è sul valore long della proprietà.  
  
Se il numero di proprietà nel riquadro delle proprietà supera lo spazio disponibile nell'area del contenuto, nel riquadro sarà visualizzata una barra di scorrimento sul lato destro. Utilizzare la barra di scorrimento per regolare la visualizzazione dei valori della proprietà nell'area del contenuto.  
  
### <a name="multiple-object-selection"></a>Selezione di più oggetti  
Dettagli Esplora oggetti supporta la selezione di più oggetti. Ad esempio, se in Esplora oggetti si seleziona Tabelle, quindi nella finestra Dettagli Esplora oggetti si tiene premuto il tasto **CTRL** , è possibile selezionare numerose tabelle, farvi clic sopra con il pulsante destro del mouse, quindi selezionare **Elimina** o **Crea script per tabella** per agire immediatamente su tutte le tabelle selezionate. I comandi di copia standard consentiranno di copiare negli Appunti il testo visualizzato.  
  
## <a name="sql-server-object-search"></a>Ricerca di oggetti SQL Server  
Caratteri jolly  
  
-   Sono supportati i caratteri jolly standard. Ad esempio, la ricerca di **dm_os%counters** restituisce sia dm_os_memory_cache_counters che dm_os_performance_counters. Per altre informazioni, vedere [Procedura: Eseguire ricerche di testo con caratteri jolly](../../relational-databases/scripting/search-text-with-wildcards.md).  
  
Ambito di ricerca  
  
-   L'ambito di ogni ricerca è determinato dallo stato attivo corrente nell'albero di Esplora oggetti. Ad esempio, se lo stato attivo in Esplora oggetti è su un database, la ricerca di **dm_os%counters** restituirà dm_os_memory_cache_counters e dm_os_performance_counters in quel database. Se lo stato attivo in Esplora oggetti è sul nodo Database, la ricerca verrà eseguita su tutti i database e verranno restituite più istanze delle viste dinamiche.  
  
Set di grandi dimensioni  
  
-   La ricerche eseguite su set di grandi dimensioni possono richiedere tempi particolarmente lunghi e ridurre le prestazioni del server.  
  
## <a name="see-also"></a>Vedere anche  
[Esplora oggetti](../../ssms/object/object-explorer.md)  
  
