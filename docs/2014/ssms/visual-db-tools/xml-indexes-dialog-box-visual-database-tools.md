---
title: Finestra di dialogo Indici XML (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.xmlindexes
ms.assetid: eef38310-4498-4ccc-bb77-5bbd1c7cc477
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a0c946e0e195937dd2e722ac3f092a57e40427b8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63228370"
---
# <a name="xml-indexes-dialog-box-visual-database-tools"></a>Finestra di dialogo Indici XML (Visual Database Tools)
  Usare la finestra di dialogo **Indici XML** per creare indici per le colonne con tipo di dati XML, le quali non possono essere indicizzate usando la finestra di dialogo **Indici/chiavi** . Ogni colonna XML può avere più indici XML, ma il primo indice creato (primario) verrà utilizzato come base degli altri (secondari). Eliminando l'indice XML primario, verranno eliminati anche gli indici secondari.  
  
## <a name="options"></a>Opzioni  
 **Indice XML selezionato**  
 Elenca gli indici XML esistenti. Selezionarne uno per visualizzarne le proprietà nella griglia di destra. Se l'elenco è vuoto, per la tabella non sono stati definiti indici.  
  
 **Aggiungere**  
 Consente di creare un nuovo indice XML.  
  
 **Elimina**  
 Elimina l'elemento selezionato nell'elenco **Indice XML selezionato** . Se si elimina l'indice XML primario, un messaggio informerà che verranno eliminati anche gli indici secondari e sarà possibile scegliere di continuare o annullare l'operazione.  
  
 **Categoria Generale**  
 Se viene espansa, visualizza i campi delle proprietà relativi a **Colonne**, **Is Primary**e **Tipo**.  
  
 **Colonne**  
 Indica che l'indice è ordinato in sequenza crescente.  
  
 **Is Primary**  
 Indica se si tratta dell'indice primario. Il primo indice XML creato per la colonna verrà utilizzato come base per gli altri.  
  
 **Nome riferimento primario**  
 Nel caso di un indice secondario, visualizza il nome dell'indice primario. È disponibile solo per gli indici secondari.  
  
 **Tipo secondario**  
 Visualizza il tipo di indice secondario. È disponibile solo per gli indici secondari.  
  
 **Tipo**  
 Indica che si tratta di un indice XML.  
  
 **Categoria Identità**  
 Se viene espansa, visualizza i campi delle proprietà **Nome** e **Descrizione** .  
  
 **Nome**  
 Visualizza il nome dell'indice XML. Quando si crea un nuovo indice, gli viene assegnato un nome predefinito sulla base della tabella presente nella finestra attiva di Progettazione tabelle. È possibile modificare il nome in qualsiasi momento.  
  
 **Descrizione**  
 Consente di descrivere l'indice. Per inserire una descrizione più dettagliata, fare clic su **Descrizione** e sui puntini di sospensione ( **...** ) a destra del campo della proprietà. Viene così visualizzata un'area più grande in cui scrivere il testo.  
  
 **Categoria Progettazione tabelle**  
 Se viene espansa, visualizza le informazioni relative alle proprietà dell'indice XML.  
  
 **Specifica riempimento**  
 Se viene espansa, visualizza le informazioni relative a **Riempimento** e **Riempi indice**.  
  
 **Riempimento**  
 Specifica quale percentuale della pagina dell'indice può essere riempita dal sistema. Quando la pagina è piena, dovrà essere divisa se verranno aggiunti nuovi dati, con un conseguente rallentamento delle prestazioni.  
  
-   Un valore pari a 100 indica che le pagine saranno piene. Tale impostazione richiede la quantità più ridotta di spazio di archiviazione ma è la meno efficiente. È consigliabile utilizzare questa impostazione solo se non verranno apportate modifiche ai dati, ad esempio per una tabella di sola lettura.  
  
-   Un valore inferiore lascia più spazio nelle pagine di dati e quindi riduce la necessità di suddividerle all'aumentare delle dimensioni degli indici, ma richiede uno spazio di archiviazione maggiore. Questa impostazione è consigliabile se si prevede che i dati della tabella saranno soggetti a modifiche.  
  
 **Riempi indice**  
 Offre alle pagine di questo indice la stessa percentuale di spazio vuoto (riempimento) specificata in **Riempimento**.  
  
 **Disabilitato**  
 Specifica se l'indice è disabilitato. Gli indici disabilitati non consentono l'esecuzione di ricerche, né vengono aggiornati quando si aggiungono nuovi elementi alla tabella. Disabilitando un indice è possibile migliorare le prestazioni in caso di operazioni di inserimento e aggiornamento bulk.  
  
 **Blocchi pagine consentiti**  
 Specifica se per l'indice è consentito il blocco a livello delle pagine. L'attivazione o la disattivazione di tale blocco incide sulle prestazioni del database.  
  
 **Ricalcola statistiche**  
 Consente di calcolare nuove statistiche quando viene creato l'indice. Il ricalcolo delle statistiche rallenta la compilazione degli indici, ma in genere consente di migliorare le prestazioni delle query.  
  
 **Blocchi righe consentiti**  
 Specifica se per l'indice è consentito il blocco a livello delle righe. L'attivazione o la disattivazione di tale blocco incide sulle prestazioni del database.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di indici XML](../../relational-databases/xml/create-xml-indexes.md)  
  
  
