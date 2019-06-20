---
title: Finestra di dialogo Indici spaziali (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.spatialindexes
ms.assetid: 4d84239a-68c7-4aa2-8602-2b51dd07260f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 00c5e0017b8d81eaea6960f016e40dbc381e69e8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63049135"
---
# <a name="spatial-indexes-dialog-box-visual-database-tools"></a>Finestra di dialogo Indici spaziali (Visual Database Tools)
  La finestra di dialogo **Indici spaziali** consente di creare indici per le colonne con tipo di dati **geometria** o **geografia** (*colonne spaziali*), che non possono essere indicizzate con la finestra di dialogo **Indici/chiavi** . Ogni colonna spaziale può avere più indici spaziali, ma gli indici devono essere creati uno alla volta.  
  
 Per informazioni sulle restrizioni alla creazione di indici spaziali, vedere [Panoramica degli indici spaziali](../../relational-databases/spatial/spatial-indexes-overview.md).  
  
## <a name="options"></a>Opzioni  
 **Indice spaziale selezionato**  
 Consente di visualizzare un elenco degli indici spaziali esistenti. Selezionare un indice per visualizzare le relative proprietà. Se l'elenco è vuoto, significa che non sono stati definiti indici spaziali per la tabella.  
  
 **Aggiungi**  
 Consente di creare un nuovo indice spaziale.  
  
 **Elimina**  
 Consente di eliminare l'indice spaziale selezionato nell'elenco **Indice spaziale selezionato** .  
  
 **Celle per oggetto**  
 Indica il numero di celle per oggetto di mosaico utilizzabile per un singolo oggetto spaziale nell'indice. È possibile usare qualsiasi numero intero compreso tra 1 e 8192. Il valore predefinito è 16.  
  
 Se un oggetto include più celle rispetto a quanto specificato da *n*, per l'indicizzazione viene usata la quantità di celle necessaria a offrire un mosaico di livello principale completo. In tali casi un oggetto può ricevere un numero di celle maggiore di quello specificato: il numero massimo è il numero di celle generate dalla griglia di livello principale che dipende dalla densità di **Livello 1** .  
  
 **Colonne**  
 Indica il nome e l'ordinamento della colonna.  
  
 **IsSpatialIndex**  
 Indica che è stato selezionato un indice spaziale.  
  
 **Livello 1**  
 Indica la densità della griglia di primo livello (superiore).  
  
 **Livello 2**  
 Indica la densità della griglia di secondo livello.  
  
 **Livello 3**  
 Indica la densità della griglia di terzo livello.  
  
 **Livello 4**  
 Indica la densità della griglia di quarto livello.  
  
 **Schema a mosaico**  
 Indica lo schema a mosaico:  
  
 Opzioni per le colonne di tipo**geometria** :  
  
-   **Griglia geometrica** per una colonna di tipo geometria  
  
-   **Griglia geografica** per una colonna di tipo geografia  
  
 **Tipo**  
 Indica che è stato selezionato un indice spaziale.  
  
 **X-max**  
 Specifica la coordinata x dell'angolo superiore destro del rettangolo di selezione. Questa proprietà è visualizzata in grigio se lo **Schema a mosaico** è **Griglia geografica**.  
  
 **X-min**  
 Specifica la coordinata x dell'angolo inferiore sinistro del rettangolo di selezione. Questa proprietà è visualizzata in grigio se lo **Schema a mosaico** è **Griglia geografica**.  
  
 **Y-max**  
 Specifica la coordinata Y dell'angolo superiore destro del riquadro. Questa proprietà è visualizzata in grigio se lo **Schema a mosaico** è **Griglia geografica**.  
  
 **Y-min**  
 Specifica la coordinata y dell'angolo inferiore sinistro del rettangolo di selezione. Questa proprietà è visualizzata in grigio se lo **Schema a mosaico** è **Griglia geografica**.  
  
 **Identità**  
 Se viene espansa, visualizza i campi delle proprietà **Nome** e **Descrizione** .  
  
 **(Nome)**  
 Visualizza il nome dell'indice spaziale. Quando viene creato un nuovo indice, gli viene assegnato un nome predefinito sulla base della tabella presente nella finestra attiva di Progettazione tabelle. Il nome può essere modificato in qualunque momento.  
  
 **Descrizione**  
 Descrive l'indice. Per inserire una descrizione più dettagliata, fare clic su **Descrizione** e sui puntini di sospensione (**...**) a destra del campo della proprietà. Viene così visualizzata un'area più grande in cui scrivere il testo.  
  
 **Categoria Progettazione tabelle**  
 Se viene espansa, visualizza le informazioni relative alle proprietà dell'indice spaziale.  
  
 **Specifica riempimento**  
 Se viene espansa, visualizza le informazioni relative a **Riempimento** e **Riempi indice**.  
  
 **Riempimento**  
 Specifica quale percentuale della pagina dell'indice può essere riempita dal sistema. Quando una pagina è piena, se vengono aggiunti nuovi dati deve essere divisa, con un conseguente rallentamento delle prestazioni.  
  
-   Un valore pari a 100 indica che le pagine saranno piene. Tale impostazione richiede la quantità più ridotta di spazio di archiviazione ma è la meno efficiente. È consigliabile utilizzare questa impostazione solo se non verranno apportate modifiche ai dati, ad esempio per una tabella di sola lettura.  
  
-   Un valore inferiore lascia più spazio nelle pagine di dati e quindi riduce la necessità di suddividerle all'aumentare delle dimensioni degli indici, ma richiede uno spazio di archiviazione maggiore. Questa impostazione è consigliabile se si prevede che i dati della tabella saranno soggetti a modifiche.  
  
 **Riempi indice**  
 Consente di usare per le pagine dell'indice la stessa percentuale di spazio vuoto (riempimento) specificata in **Fattore di riempimento**.  
  
 **Blocchi pagine consentiti**  
 Consente di specificare se per l'indice è consentito il blocco a livello di pagina. L'attivazione o la disattivazione di tale blocco incide sulle prestazioni del database.  
  
 **Ricalcola statistiche**  
 Consente di specificare se calcolare nuove statistiche quando viene creato l'indice. Il ricalcolo delle statistiche rallenta la compilazione degli indici, ma in genere consente di migliorare le prestazioni delle query.  
  
 **Blocchi righe consentiti**  
 Consente di specificare se per l'indice è consentito il blocco a livello di riga. L'attivazione o la disattivazione di tale blocco incide sulle prestazioni del database.  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica degli indici spaziali](../../relational-databases/spatial/spatial-indexes-overview.md)  
  
  
