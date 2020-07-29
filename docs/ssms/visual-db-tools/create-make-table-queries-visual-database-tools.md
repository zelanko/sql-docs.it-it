---
title: Creare query di creazione tabella
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- queries [SQL Server], types
- table creation [SQL Server], Make Table query
- inserting tables
- Make Table query
- adding tables
ms.assetid: 4493cffa-7b2d-4c24-8ef0-d49329198972
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: dc2c7c425bc9f75304917ec37531a2db7cab57da
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "86010397"
---
# <a name="create-make-table-queries-visual-database-tools"></a>Creazione di query di creazione tabella (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Per copiare delle righe in una nuova tabella è possibile utilizzare una query di creazione tabella, che consente di creare subset di dati da utilizzare o di copiare il contenuto di una tabella da un database a un altro. Una query di creazione tabella è analoga a una query di accodamento, con la differenza che viene creata una nuova tabella in cui copiare le righe.  
  
Durante la creazione di una query di creazione tabella è necessario specificare:  
  
-   Il nome della nuova tabella di database, ossia la tabella di destinazione.  
  
-   Le tabelle da cui copiare le righe, ossia le tabelle di origine. È possibile effettuare la copia da una singola tabella o da tabelle in join.  
  
-   Le colonne della tabella di origine di cui si desidera copiare il contenuto.  
  
-   Il criterio di ordinamento, se si desidera copiare le righe in un particolare ordine.  
  
-   Le condizioni di ricerca per la definizione delle righe da copiare.  
  
-   Le opzioni di raggruppamento, se si desidera copiare solo le informazioni di riepilogo.  
  
L'esempio di query visualizzato di seguito consente di creare una nuova tabella con nome `uk_customers` e di copiarvi le informazioni contenute nella tabella `customers`:  
  
```  
SELECT *   
INTO uk_customers  
FROM customers  
WHERE country = 'UK'  
```  
  
Per utilizzare correttamente una query di creazione tabella è necessario che:  
  
-   il database supporti la sintassi SELECT...INTO;  
  
-   l'autore disponga dei privilegi necessari per creare una tabella nel database di destinazione.  
  
### <a name="to-create-a-make-table-query"></a>Per creare una query di creazione tabella  
  
1.  Aggiungere le tabelle di origine nel riquadro Diagramma.  
  
2.  Scegliere **Modifica tipo** dal menu **Progettazione query**e fare clic su **Creazione tabella**.  
  
3.  Digitare il nome della tabella di destinazione nella finestra di dialogo **Creazione tabella** . In Progettazione query e Progettazione viste non viene eseguito alcun controllo per verificare se il nome è già in uso o se si è autorizzati a creare la tabella.  
  
    Per creare una tabella di destinazione in un altro database è necessario specificare il nome completo di una tabella, compreso il nome del database di destinazione, il proprietario (se necessario) e il nome della tabella.  
  
4.  Specificare le colonne da copiare aggiungendole alla query. Per informazioni dettagliate, vedere [Aggiungere colonne a query](../../ssms/visual-db-tools/add-columns-to-queries-visual-database-tools.md). Verranno copiate solo le colonne aggiunte alla query. Per copiare righe intere, scegliere **&#42; (Tutte le colonne)** .  
  
    Le colonne selezionate verranno aggiunte alla colonna **Colonna** del riquadro Criteri.  
  
5.  Se si desidera copiare le righe in un particolare ordine, specificare il criterio di ordinamento. Per informazioni dettagliate, vedere **Ordinamento e raggruppamento dei risultati delle query**.  
  
6.  Specificare le righe da copiare immettendo le condizioni di ricerca. Per informazioni dettagliate, vedere [Specificare criteri di ricerca](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md).  
  
    Se non si specifica alcuna condizione di ricerca, tutte le righe della tabella di origine verranno copiate nella tabella di destinazione.  
  
    > [!NOTE]  
    > Quando nel riquadro Criteri si aggiunge una colonna da includere nella ricerca, tale colonna verrà aggiunta anche all'elenco delle colonne da copiare. Se si desidera utilizzare una colonna per la ricerca senza copiarla, deselezionare la casella di controllo accanto al nome della colonna nel rettangolo che rappresenta la tabella o l'oggetto con struttura di tabella.  
  
7.  Se si desidera copiare le informazioni di riepilogo, specificare le opzioni di raggruppamento. Per informazioni dettagliate, vedere [Riepilogare i risultati di query](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md).  
  
Quando si esegue una query di creazione tabella, non viene restituito alcun risultato nel [riquadro Risultati](../../ssms/visual-db-tools/results-pane-visual-database-tools.md). Viene invece visualizzato un messaggio che indica il numero di righe copiate.  
  
## <a name="see-also"></a>Vedere anche  
[Procedure per la progettazione di query e viste](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Tipi di query (../../ssms/visual-db-tools/types-of-queries-visual-database-tools.md)  
  
