---
title: Confrontare le differenze tra le tabelle replicate (SP di replica)
description: Usare le stored procedure di replica per confrontare le differenze tra le tabelle replicate nel server di pubblicazione e nel Sottoscrittore.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- tablediff utility
- comparing replicated tables
ms.assetid: cd253a17-0c85-42b4-912c-690169ebe799
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 6130acf6a503f3a803978b7db5a9a23b9918a3c7
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "76286869"
---
# <a name="compare-differences-between-replicated-tables-replication-programming"></a>Confrontare le differenze tra le tabelle replicate (programmazione della replica)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  La convalida degli articoli consente di determinare se i dati pubblicati per gli articoli di tabella nel server di pubblicazione e nel Sottoscrittore non sono identici, fattore che può indicare la mancanza di convergenza. Per altre informazioni, vedere [Convalidare i dati replicati](../../../relational-databases/replication/validate-data-at-the-subscriber.md). La convalida restituisce tuttavia solo un risultato positivo o negativo e non fornisce informazioni sulle differenze specifiche tra le tabelle di origine e di destinazione. L'utilità del prompt dei comandi **tablediff** restituisce informazioni dettagliate sulle differenze tra due tabelle e può anche generare uno script [!INCLUDE[tsql](../../../includes/tsql-md.md)] per ripristinare la convergenza tra una sottoscrizione e i dati nel server di pubblicazione.  
  
> [!NOTE]  
>  L'utilità **tablediff** è supportata solo per i server [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
### <a name="to-compare-replicated-tables-for-differences-using-tablediff"></a>Per confrontare le tabelle replicate al fine di individuare le differenze mediante tablediff  
  
1.  Dal prompt dei comandi in qualsiasi server in una topologia di replica, eseguire l' [tablediff Utility](../../../tools/tablediff-utility.md). Specificare i parametri seguenti:  
  
    -   **-sourceserver** : nome del server i cui dati sono considerati corretti, generalmente il server di pubblicazione.  
  
    -   **-sourcedatabase** : nome del database contenente i dati corretti.  
  
    -   **-sourcetable** : nome della tabella di origine dell'articolo da confrontare.  
  
    -   (Facoltativo) **-sourceschema** : proprietario dello schema della tabella di origine, se diverso dallo schema predefinito.  
  
    -   (Facoltativo) **-sourceuser** e **-sourcepassword** quando si utilizza l'autenticazione di SQL Server per la connessione al server di pubblicazione.  
  
        > [!IMPORTANT]  
        >  Se possibile, usare l'autenticazione di Windows. Se è necessario utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , richiedere agli utenti di immettere le credenziali di sicurezza in fase di esecuzione. Se è necessario archiviare le credenziali in un file script, è fondamentale proteggere il file per evitare accessi non autorizzati.  
  
    -   **-destinationserver** : nome del server nel quale vengono confrontati in dati, generalmente un Sottoscrittore.  
  
    -   **-destinationdatabase** : nome di un database da confrontare.  
  
    -   **-destinationtable** : nome della tabella da confrontare.  
  
    -   (Facoltativo) **-destinationschema** : proprietario dello schema della tabella di destinazione, se diverso dallo schema predefinito.  
  
    -   (Facoltativo) **-destinationuser** e **-destinationpassword** se si utilizza l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per la connessione al Sottoscrittore.  
  
        > [!IMPORTANT]  
        >  Se possibile, usare l'autenticazione di Windows. Se è necessario utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , richiedere agli utenti di immettere le credenziali di sicurezza in fase di esecuzione. Se è necessario archiviare le credenziali in un file script, è fondamentale proteggere il file per evitare accessi non autorizzati.  
  
    -   (Facoltativo) Utilizzare **-c** per eseguire un confronto a livello di colonna.  
  
    -   (Facoltativo) Utilizzare **-q** per eseguire un confronto rapido del solo schema mediante conteggio delle righe.  
  
    -   (Facoltativo) Specificare un nome file e un percorso per **-o** per restituire i risultati in un file.  
  
    -   (Facoltativo) Specificare una tabella nel database di sottoscrizione in cui inserire i risultati per **-et**. Se la tabella esiste già, è necessario eliminarla. A tale scopo, specificare **-dt** .  
  
    -   (Facoltativo) Utilizzare **-f** per generare un file [!INCLUDE[tsql](../../../includes/tsql-md.md)] per correggere i dati nel Sottoscrittore e fare in modo che corrispondano a quelli nel server di pubblicazione. Utilizzare **-df** per specificare il numero di istruzioni [!INCLUDE[tsql](../../../includes/tsql-md.md)] in ciascun file.  
  
    -   (Facoltativo) Utilizzare **-rc** e **-ri** per specificare il numero di tentativi di esecuzione di un'operazione e l'intervallo tra ogni tentativo.  
  
    -   (Facoltativo) Utilizzare **-strict** per imporre il confronto dello schema di tipo strict tra le tabelle di origine e di destinazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Convalidare i dati nel Sottoscrittore](../../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
