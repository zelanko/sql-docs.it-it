---
title: 'Lezione 5: Automatizzazione della pulizia e corrispondenza tramite SSIS | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f068d4db-2d56-41b1-bed2-0cffa3ca411d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: ec6f347cdbc6d14e8f621466a1708b8ee9fe7d36
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65489758"
---
# <a name="lesson-5-automating-the-cleansing-and-matching-using-ssis"></a>Lezione 5: Automazione della pulizia e della corrispondenza tramite SSIS
  Nella lezione 1 è compilata la knowledge base Suppliers e usato per pulire i dati nella lezione 2 e corrispondenza dei dati nella lezione 3 mediante lo strumento **Client DQS**. In uno scenario reale, potrebbe essere necessario eseguire il pull dei dati da un'origine che DQS non supporta o si desidera automatizzare il processo di pulizia e di un processo di corrispondenza senza dover usare il **Client DQS** dello strumento. SQL Server Integration Services (SSIS) include componenti che è possibile utilizzare per integrare dati da diverse origini eterogenee e un **[trasformazione DQS Cleansing](https://msdn.microsoft.com/library/ee677619.aspx)** componente da richiamare operazioni di pulizia funzionalità esposta da DQS. Attualmente, DQS non viene esposta la funzionalità corrispondente per SSIS, ma è possibile usare la **[trasformazione Raggruppamento Fuzzy](../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)** per identificare duplicati nei dati.  
  
 È possibile caricare i dati in MDS utilizzando il **funzionalità di gestione temporanea basata su entità**. Quando si crea un'entità in MDS, vengono create automaticamente le tabelle di staging e le stored procedure corrispondenti. Ad esempio, quando è creata l'entità Supplier, il **stg. supplier_leaf** tabella e il **stg. udp_supplier_leaf** stored procedure create automaticamente. È possibile utilizzare le stored procedure e le tabelle di staging per creare, aggiornare ed eliminare membri di entità. In questa lezione vengono creati nuovi membri entità per l'entità Supplier. Per caricare i dati nel server MDS, tramite il pacchetto SSIS vengono innanzitutto caricati i dati nella tabella di staging stg.supplier_Leaf e, successivamente, viene attivata la stored procedure associata stg.udp_Supplier_Leaf. Visualizzare [importazione di dati](../master-data-services/overview-importing-data-from-tables-master-data-services.md) per altri dettagli.  
  
 In questa lezione vengono effettuate le attività seguenti:  
  
1.  Rimozione di dati fornitore in MDS (se sono già state completate le quattro lezioni precedenti). Tramite il pacchetto SSIS creato durante questa lezione i dati vengono caricati automaticamente in MDS. In precedenza, i dati fornitore puliti e corrispondenti venivano caricati nel server MDS manualmente tramite il client DQS.  
  
2.  Creazione di una vista sottoscrizioni nell'entità Supplier per esporre i dati nell'entità ad altre applicazioni. Tramite questa azione viene creata una vista SQL che verrà verificata utilizzando SQL Server Management Studio. Questa vista non verrà utilizzata in questa versione dell'esercitazione.  
  
3.  Creare ed eseguire un progetto SSIS mediante **SQL Server Data Tools**. Il progetto usa **pulizia dei dati** trasformazione per inviare una richiesta di pulizia al server DQS. DQS non ancora, espone la funzionalità di corrispondenza, quindi si utilizzerà **raggruppamento Fuzzy** trasformazione per identificare i duplicati.  
  
4.  Verifica dell'effettiva creazione dei dati in MDS tramite Gestione dati master.  
  
5.  Analisi dei risultati del progetto DQS Cleansing creato dal pacchetto SSIS e, facoltativamente, esecuzione della pulizia interattiva per continuare a compilare la Knowledge Base.  
  
## <a name="next-step"></a>Passaggio successivo  
 [Attività 1 &#40;prerequisiti&#41;: Rimozione dei dati fornitore in MDS](../../2014/tutorials/task-1-prerequisite-removing-supplier-data-in-mds.md)  
  
  
