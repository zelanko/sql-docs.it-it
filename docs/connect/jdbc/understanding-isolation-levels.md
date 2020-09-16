---
description: Informazioni sui livelli di isolamento
title: Informazioni sui livelli di isolamento | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2c41e23a-da6c-4650-b5fc-b5fe53ba65c3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 758012112df2bce1b0a7624834bfde3c3c4ece10
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488044"
---
# <a name="understanding-isolation-levels"></a>Informazioni sui livelli di isolamento

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Le transazioni specificano un livello di isolamento che definisce il grado di isolamento di una transazione dalle modifiche alle risorse o ai dati apportate da altre transazioni. I livelli di isolamento sono descritti in termini di effetti collaterali consentiti sulla concorrenza, ad esempio letture dirty o fantasma.  
  
I livelli di isolamento delle transazioni controllano gli elementi seguenti:  
  
- Se i blocchi vengono acquisiti alla lettura dei dati e quali tipi di blocchi vengono richiesti.  
  
- La durata dei blocchi di lettura.  
  
- Se un'operazione di lettura che fa riferimento a righe modificate da un'altra transazione:  
  
  - Si blocca fino al rilascio del blocco esclusivo sulla riga.  
  
  - Recupera la versione di cui è stato eseguito il commit della riga esistente al momento dell'avvio dell'istruzione o della transazione.  
  
  - Legge la modifica dei dati di cui non è stato eseguito il commit.  

La scelta di un livello di isolamento delle transazioni non ha effetto sui blocchi acquisiti per proteggere le modifiche dei dati. Una transazione ottiene sempre un blocco esclusivo su qualsiasi dato da essa modificato e mantiene tale blocco fino al suo completamento, indipendentemente dal livello di isolamento impostato per tale transazione. Per le operazioni di lettura, i livelli di isolamento delle transazioni definiscono essenzialmente il livello di protezione dagli effetti delle modifiche apportate da altre transazioni.  
  
Un livello di isolamento minore aumenta le possibilità di accesso ai dati da parte di molti utenti contemporaneamente, ma anche la quantità di effetti di concorrenza, ad esempio letture dirty o perdita di aggiornamenti, che possono verificarsi. Al contrario, un livello di isolamento maggiore riduce i tipi di effetti di concorrenza che si possono verificare, ma richiede più risorse di sistema e aumenta le probabilità che una transazione venga bloccata da un'altra. La scelta del livello di isolamento corretto dipende dal giusto equilibrio tra requisiti relativi all'integrità dei dati per l'applicazione e overhead di ogni livello di isolamento. Il livello di isolamento più elevato, Serializable, garantisce che una transazione recuperi esattamente gli stessi dati a ogni ripetizione di un'operazione di lettura. Tuttavia questo avviene applicando un livello di blocco con probabilità effetti su altri utenti in sistemi multiutente. Il livello di isolamento minimo, Read uncommitted, consente di recuperare i dati modificati ma di cui non è stato eseguito il commit da altre transazioni. In tale livello possono verificarsi tutti gli effetti collaterali della concorrenza, ma l'assenza di blocco in lettura e di controllo delle versioni riduce al minimo l'overhead.  

## <a name="remarks"></a>Osservazioni

 Nella tabella seguente vengono illustrati gli effetti collaterali della concorrenza consentiti dai diversi livelli di isolamento.  
  
| Livello di isolamento  | Lettura dirty | Lettura non ripetibile | Lettura fantasma |
| ---------------- | ---------- | ------------------- | ------- |
| Read Uncommitted | Sì        | Sì                 | Sì     |
| Read Committed   | No         | Sì                 | Sì     |
| Repeatable Read  | No         | No                  | Sì     |
| Snapshot         | No         | No                  | No      |
| Serializable     | No         | No                  | No      |
  
Le transazioni devono essere eseguite almeno a un livello di isolamento Repeatable read, per impedire la perdita di aggiornamenti che può verificarsi quando due transazioni recuperano entrambe la stessa riga e successivamente la aggiornano in base ai valori recuperati in origine. Se le due transazioni aggiornano le righe usando una singola istruzione UPDATE e non basano l'aggiornamento sui valori recuperati in precedenza, non possono verificarsi perdite di aggiornamenti al livello di isolamento predefinito Read committed.  

Per impostare il livello di isolamento per una transazione, è possibile usare il metodo [setTransactionIsolation](../../connect/jdbc/reference/settransactionisolation-method-sqlserverconnection.md) della classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md). Questo metodo accetta un valore **int** come argomento, basato su una delle costanti di connessione, come illustrato di seguito:  

```java
con.setTransactionIsolation(Connection.TRANSACTION_READ_COMMITTED);  
```

Per usare il nuovo livello di isolamento dello snapshot di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile usare una delle costanti `SQLServerConnection`:  

```java
con.setTransactionIsolation(SQLServerConnection.TRANSACTION_SNAPSHOT);  
```

In alternativa, è possibile utilizzare:  

```java
con.setTransactionIsolation(Connection.TRANSACTION_READ_COMMITTED + 4094);  
```

Per altre informazioni sui livelli di isolamento di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere "Livelli di isolamento nel [!INCLUDE[ssDE](../../includes/ssde_md.md)]" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

## <a name="see-also"></a>Vedere anche

[Esecuzione di transazioni con il driver JDBC](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
