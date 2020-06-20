---
title: 'Lezione 5: automazione della pulizia e della corrispondenza tramite SSIS | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f068d4db-2d56-41b1-bed2-0cffa3ca411d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 90f967b2446e11a27f5a87803bb71d6e1ec53557
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85039838"
---
# <a name="lesson-5-automating-the-cleansing-and-matching-using-ssis"></a>Lezione 5: Automazione della pulizia e della corrispondenza tramite SSIS
  Nella lezione 1 è stata compilata la Knowledge Base Suppliers e utilizzata per pulire i dati nella lezione 2 e le corrispondenze dei dati della lezione 3 mediante lo strumento **client DQS**. In uno scenario reale, potrebbe essere necessario effettuare il pull dei dati da un'origine non supportata da DQS o si desidera automatizzare il processo di pulizia e di corrispondenza senza dover utilizzare lo strumento **client DQS** . SQL Server Integration Services (SSIS) include componenti che è possibile utilizzare per integrare dati da varie origini eterogenee e un componente di **[trasformazione di pulizia DQS](https://msdn.microsoft.com/library/ee677619.aspx)** per richiamare la funzionalità di pulizia esposta da DQS. Attualmente, DQS non espone la funzionalità di corrispondenza per l'utilizzo di SSIS, ma è possibile utilizzare la **[trasformazione Raggruppamento fuzzy](../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)** per identificare i duplicati nei dati.  
  
 È possibile caricare i dati in MDS usando la **funzionalità di gestione temporanea basata su entità**. Quando si crea un'entità in MDS, vengono create automaticamente le tabelle di staging e le stored procedure corrispondenti. Ad esempio, quando è stata creata l'entità Supplier, la tabella **STG. supplier_Leaf** e il stored procedure **STG. udp_Supplier_Leaf** sono stati creati automaticamente. È possibile utilizzare le stored procedure e le tabelle di staging per creare, aggiornare ed eliminare membri di entità. In questa lezione vengono creati nuovi membri entità per l'entità Supplier. Per caricare i dati nel server MDS, tramite il pacchetto SSIS vengono innanzitutto caricati i dati nella tabella di staging stg.supplier_Leaf e, successivamente, viene attivata la stored procedure associata stg.udp_Supplier_Leaf. Per altri dettagli, vedere [importazione di dati](../master-data-services/overview-importing-data-from-tables-master-data-services.md) .  
  
 In questa lezione vengono effettuate le attività seguenti:  
  
1.  Rimozione di dati fornitore in MDS (se sono già state completate le quattro lezioni precedenti). Tramite il pacchetto SSIS creato durante questa lezione i dati vengono caricati automaticamente in MDS. In precedenza, i dati fornitore puliti e corrispondenti venivano caricati nel server MDS manualmente tramite il client DQS.  
  
2.  Creazione di una vista sottoscrizioni nell'entità Supplier per esporre i dati nell'entità ad altre applicazioni. Tramite questa azione viene creata una vista SQL che verrà verificata utilizzando SQL Server Management Studio. Questa vista non verrà utilizzata in questa versione dell'esercitazione.  
  
3.  Creare ed eseguire un progetto SSIS utilizzando **SQL Server Data Tools**. Il progetto utilizza la trasformazione **pulizia dati** per inviare una richiesta di pulizia al server DQS. DQS non espone ancora la funzionalità di corrispondenza, pertanto si utilizzerà la trasformazione **Raggruppamento fuzzy** per identificare i duplicati.  
  
4.  Verifica dell'effettiva creazione dei dati in MDS tramite Gestione dati master.  
  
5.  Analisi dei risultati del progetto DQS Cleansing creato dal pacchetto SSIS e, facoltativamente, esecuzione della pulizia interattiva per continuare a compilare la Knowledge Base.  
  
## <a name="next-step"></a>passaggio successivo  
 [Attività 1 &#40;&#41; prerequisiti: rimozione dei dati fornitore in MDS](../../2014/tutorials/task-1-prerequisite-removing-supplier-data-in-mds.md)  
  
  
