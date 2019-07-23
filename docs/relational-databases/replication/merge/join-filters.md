---
title: Filtri di join | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server replication], join
- publications [SQL Server replication], join filters
- merge replication join filters [SQL Server replication]
- join filters
ms.assetid: dd78fd8f-56e3-4582-9abd-6bc25c91e075
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 712665d24946c2826e4ab6c5e53bb853b07642b4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68033239"
---
# <a name="join-filters"></a>filtri di join
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Un filtro di join consente di filtrare una tabella in base al tipo di filtro applicato a una tabella correlata nella pubblicazione Viene in genere filtrata una tabella padre mediante un filtro con parametri, quindi vengono definiti uno o più filtri di join così come si definisce un join tra tabelle. I filtri di join estendono il filtro con parametri affinché i dati nelle tabelle correlate vengano replicati solo se corrispondenti alla clausola di filtro di join.  
  
 I filtri join seguono in genere le relazioni tra chiavi primarie e chiavi esterne definite per le tabelle alle quali vengono applicati, ma non sono necessariamente limitati a tali relazioni. Il filtro di join può essere basato su qualsiasi logica di confronto tra i dati correlati di due tabelle.  
  
 Si considerino le tabelle seguenti del database di esempio [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)] , correlate tramite relazioni di chiave primaria/chiave esterna:  
  
-   **HumanResources.Employee**  
  
-   **Sales.SalesOrderHeader**  
  
-   **Sales.SalesOrderDetail**  
  
 Queste tabelle potrebbero essere utilizzate in un'applicazione per supportare una forza vendita mobile, ma devono essere filtrate affinché ogni venditore della tabella **HumanResources.Employee** riceva soltanto i dati rilevanti per gli ordini dei propri clienti.  
  
 Il primo passaggio consiste nel definire un filtro con parametri per la tabella padre, costituita in questo caso dalla tabella **HumanResources.Employee** . In questa tabella è inclusa la colonna **LoginID**, contenente l'account di accesso per ogni dipendente nel formato *dominio\account accesso*. Per filtrare questa tabella affinché ogni dipendente riceva soltanto i dati pertinenti, specificare la clausola di filtro con parametri:  
  
```  
LoginID = SUSER_SNAME()  
```  
  
 Questo filtro garantisce che la sottoscrizione di ogni dipendente contenga soltanto i dati della tabella **HumanResources.Employee** rilevanti per tale dipendente. In questo caso, si tratta di una singola riga. Per altre informazioni, vedere [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 Il passaggio successivo consiste nell'estendere questo filtro a ogni tabella correlata, utilizzando una sintassi simile a quella utilizzata per specificare un join tra due tabelle. La prima clausola di filtro di join è:  
  
```  
Employee.EmployeeID = SalesOrderHeader.SalesPersonID  
```  
  
 Ciò garantisce che la sottoscrizione conterrà soltanto i dati degli ordini rilevanti per ogni venditore. La seconda clausola di filtro di join è:  
  
```  
SalesOrderHeader.SalesOrderID = SalesOrderDetail.SalesOrderID  
```  
  
 Ciò garantisce che la sottoscrizione conterrà soltanto i dati di dettaglio correlati ai dati degli ordini per ogni venditore. In questo esempio viene illustrato il join di una singola tabella in ogni fase. È inoltre possibile unire in join più tabelle in ogni fase.  
  
 I filtri di join possono essere aggiunti uno per volta tramite la Creazione guidata nuova pubblicazione e la finestra di dialogo **Proprietà pubblicazione** oppure a livello di programmazione. Possono inoltre essere generati automaticamente tramite la Creazione guidata nuova pubblicazione: specificando un filtro di riga per una tabella verranno applicati filtri di join a tutte le tabelle correlate. Per altre informazioni, vedere [Definire e modificare un filtro di join tra articoli di merge](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md), [Generare automaticamente un set di filtri di join tra gli articoli di merge &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/automatically-generate-join-filters-between-merge-articles.md) e [Definire un articolo](../../../relational-databases/replication/publish/define-an-article.md).  
  
## <a name="optimizing-join-filter-performance"></a>Ottimizzazione delle prestazioni dei filtri di join  
 È possibile ottimizzare le prestazioni dei filtri di join attenendosi alle linee guida seguenti:  
  
-   Limitare il numero massimo di tabelle nella gerarchia dei filtri di join.  
  
     I filtri di join possono includere un numero illimitato di tabelle, ma filtri con un numero elevato di tabelle possono influire significativamente sulle prestazioni durante l'elaborazione di processi di merge. Se si generano filtri di join di cinque o più tabelle, considerare altre soluzioni: non filtrare tabelle piccole, non soggette a modifica o tabelle che fungono principalmente da tabelle di ricerca. Utilizzare i filtri di join solo tra tabelle che devono essere partizionate tra diverse sottoscrizioni.  
  
-   Se appropriato, impostare la proprietà **JoinUniqueKey** su **True** .  
  
     Se la colonna unita in join nella tabella padre è univoca, per il processo di merge sono disponibili speciali procedure di ottimizzazione delle prestazioni. Se la condizione di join è basata su una colonna univoca, impostare la proprietà **JoinUniqueKey** per il filtro di join. Per informazioni sull'impostazione di questa proprietà, vedere le procedure elencate nella sezione precedente.  
  
-   Verificare che le colonne a cui viene fatto riferimento nei filtri di join siano indicizzate.  
  
     Se le colonne a cui viene fatto riferimento nel filtro sono indicizzate, i filtri possono essere elaborati dalla replica in modo più efficiente.  
  
-   Non creare filtri di riga che svolgono la funzione di filtri di join.  
  
     È possibile creare filtri di riga che svolgono la funzione di filtri di join utilizzando una sottoquery in una clausola WHERE, ad esempio:  
  
    ```  
    WHERE Customer.SalesPersonID IN (SELECT EmployeeID FROM Employee WHERE LoginID = SUSER_SNAME())   
    ```  
  
     È consigliabile esprimere tale logica in un filtro di join, anziché in una sottoquery. Se l'applicazione richiede l'utilizzo di una sottoquery in un filtro di riga, verificare che la sottoquery faccia riferimento soltanto a dati di ricerca non soggetti a modifiche.  
  
## <a name="see-also"></a>Vedere anche  
 [Filtrare i dati pubblicati per la replica di tipo merge](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)   
 [Filtri di riga con parametri](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
  
  
