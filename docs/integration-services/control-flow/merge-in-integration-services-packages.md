---
title: MERGE nei pacchetti di Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- MERGE statement [SQL Server]
ms.assetid: 7e44a5c2-e6d6-4fe2-a079-4f95ccdb147b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 124d7c0aec844b1a600f051473835e0be667824f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65805179"
---
# <a name="merge-in-integration-services-packages"></a>MERGE in Integration Services Packages

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Nella versione corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]l'istruzione SQL in un'attività Esegui SQL può contenere un'istruzione MERGE. che consente di eseguire più operazioni INSERT, UPDATE e DELETE in una singola istruzione.  
  
 Per utilizzare l'istruzione MERGE in un pacchetto, effettuare le operazioni seguenti:  
  
-   Creare un'attività Flusso di dati per caricare, trasformare e salvare l'origine dati in una tabella temporanea o di staging.  
  
-   Creare un'attività Esegui SQL contenente l'istruzione MERGE.  
  
-   Connettere l'attività Flusso di dati all'attività Esegui SQL e utilizzare i dati della tabella di staging come input per l'istruzione MERGE.  
  
    > [!NOTE]  
    >  Anche se un'istruzione MERGE richiede in genere una tabella di staging in questo scenario, le prestazioni dell'istruzione MERGE sono solitamente superiori a quelle della ricerca riga per riga eseguita con la trasformazione Ricerca. MERGE risulta utile anche quando, a causa delle dimensioni elevate di una tabella di ricerca, viene verificata la memoria a disposizione della trasformazione Ricerca per la memorizzazione nella cache della relativa tabella di riferimento.  
  
 Per un componente di destinazione di esempio che supporta l'utilizzo dell'istruzione MERGE, vedere l'esempio nella community CodePlex relativo alla [destinazione MERGE](https://go.microsoft.com/fwlink/?LinkId=141215).  
  
## <a name="using-merge"></a>Utilizzo di MERGE  
 In genere, si utilizza l'istruzione MERGE quando si desidera applicare modifiche quali inserimenti, aggiornamenti ed eliminazioni da una tabella a un'altra. Prima di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], per eseguire questo processo erano necessarie una trasformazione Ricerca e più trasformazioni Comando OLE DB. Con la trasformazione Ricerca veniva eseguita una ricerca riga per riga per determinare se ogni riga era nuova o era stata modificata. Con la trasformazione Comando OLE DB venivano quindi eseguite tutte le necessarie operazioni INSERT, UPDATE e DELETE. A partire da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]una singola istruzione MERGE può sostituire sia la trasformazione Ricerca sia le trasformazioni Comando OLE DB corrispondenti.  
  
### <a name="merge-with-incremental-loads"></a>MERGE con caricamenti incrementali  
 La funzionalità Change Data Capture, una novità di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] , rende più affidabile l'esecuzione di caricamenti incrementali in un data warehouse. Come alternativa all'utilizzo di trasformazioni Comando OLE DB con parametri per l'esecuzione di inserimenti e aggiornamenti, è possibile utilizzare l'istruzione MERGE per combinare le due operazioni.  
  
 Per altre informazioni, vedere [Applicazione delle modifiche alla destinazione](../../integration-services/change-data-capture/apply-the-changes-to-the-destination.md).  
  
#### <a name="merge-in-other-scenarios"></a>MERGE in altri scenari  
 Negli scenari seguenti è possibile utilizzare l'istruzione MERGE all'esterno o all'interno di un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , tuttavia, è spesso richiesto per caricare questi dati da più origini eterogenee e quindi per combinare e pulire i dati. Pertanto, valutare la possibilità di utilizzare l'istruzione MERGE in un pacchetto per praticità e facilità di manutenzione.  
  
##### <a name="track-buying-habits"></a>Rilevare le abitudini di acquisto  
 Nella tabella FactBuyingHabits del data warehouse viene rilevata l'ultima data in cui un cliente ha acquistato un determinato prodotto. La tabella è costituita dalle colonne ProductID, CustomerID e PurchaseDate. Ogni settimana, il database transazionale genera una tabella PurchaseRecords che include gli acquisti eseguiti durante tale settimana. L'obiettivo è quello di utilizzare una singola istruzione MERGE per unire le informazioni della tabella PurchaseRecords nella tabella FactBuyingHabits. Per le coppie prodotto-cliente che non esistono, l'istruzione MERGE inserisce nuove righe. Per le coppie prodotto-cliente che esistono, l'istruzione MERGE aggiorna la data di acquisto più recente.  
  
###### <a name="track-price-history"></a>Rilevare la cronologia dei prezzi  
 La tabella DimBook rappresenta l'elenco di libri nell'inventario di un libraio e identifica la cronologia dei prezzi di ogni libro. Questa tabella contiene queste colonne: ISBN, ProductID, Price, Shelf e IsCurrent. Include inoltre un'unica riga per ogni prezzo assegnato al libro. Una di queste righe contiene il prezzo corrente. Per indicare quale riga contiene il prezzo corrente, il valore della colonna IsCurrent per tale riga è impostato su 1.  
  
 Ogni settimana, il database genera una tabella WeeklyChanges che contiene le modifiche di prezzo e i nuovi libri aggiunti durante la settimana. Utilizzando una singola istruzione MERGE, è possibile applicare le modifiche della tabella WeeklyChanges alla tabella DimBook. L'istruzione MERGE inserisce nuove righe per i libri appena aggiunti e imposta la colonna IsCurrent su 0 per le righe di libri esistenti il cui prezzo è stato modificato. Inserisce inoltre nuove righe per i libri il cui prezzo è stato modificato e, per queste nuove righe, imposta il valore della colonna IsCurrent su 1.  
  
### <a name="merge-a-table-with-new-data-against-the-old-table"></a>Unire una tabella contenente nuovi dati con la tabella precedente  
 Il database modella le proprietà di un oggetto usando uno "schema aperto", ovvero una tabella contiene coppie nome-valore per ogni proprietà. La tabella Properties contiene tre colonne: EntityID, PropertyID e Value. È necessario sincronizzare una versione più recente della tabella, denominata NewProperties, con la tabella Properties. A tale scopo, è possibile utilizzare una singola istruzione MERGE per effettuare le operazioni seguenti:  
  
-   Eliminare proprietà dalla tabella Properties se non si trovano nella tabella NewProperties.  
  
-   Aggiornare i valori per le proprietà presenti nella tabella Properties con i nuovi valori della tabella NewProperties.  
  
-   Inserire nuove proprietà per le proprietà presenti nella tabella NewProperties ma che non si trovano nella tabella Properties.  
  
 Questo approccio risulta utile negli scenari simili agli scenari di replica, in cui l'obiettivo è quello di mantenere sincronizzati i dati di due tabelle in due server.  
  
### <a name="track-inventory"></a>Tenere traccia dell'inventario  
 Il database Inventory contiene una tabella ProductsInventory con le colonne ProductID e StockOnHand. In una tabella Shipments con le colonne ProductID, CustomerID e Quantity vengono rilevate le spedizioni di prodotti ai clienti. La tabella ProductInventory deve essere aggiornata ogni giorno in base alle informazioni presenti nella tabella Shipments. Con una singola istruzione MERGE è possibile ridurre l'inventario nella tabella ProductInventory in base alle spedizioni effettuate. Se l'inventario per un prodotto è stato ridotto a 0, con l'istruzione MERGE è possibile eliminare anche la riga di tale prodotto dalla tabella ProductInventory.  
  
  
