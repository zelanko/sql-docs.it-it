---
title: Eseguire operazioni online sugli indici | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index online operations [SQL Server]
- online index operations
- ONLINE option
ms.assetid: 1e43537c-bf67-4db3-9908-3cb45c6fdaa1
author: MikeRayMSFT
ms.author: mikeray
ms.prod_service: table-view-index, sql-database
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ac1c10bfefd80a121e858cc0175f08b6ee68ab6f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909606"
---
# <a name="perform-index-operations-online"></a>Eseguire operazioni online sugli indici
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  In questo argomento si illustra come creare, ricompilare o eliminare gli indici online in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. L'opzione ONLINE consente l'accesso simultaneo degli utenti alla tabella sottostante o ai dati dell'indice cluster e a qualsiasi indice non cluster associato durante l'esecuzione di queste operazioni sugli indici. Durante la ricompilazione di un indice cluster da parte di un utente, ad esempio, tale utente e altri utenti possono continuare ad aggiornare ed eseguire query sui dati sottostanti. Quando si eseguono operazioni DDL (Data Definition Language) offline, ad esempio la compilazione o la ricompilazione di un indice cluster, tali operazioni mantengono blocchi esclusivi sui dati sottostanti e gli indici associati. Questo comportamento impedisce modifiche e query nei dati sottostanti fino al termine dell'operazione sull'indice.  
  
> [!NOTE]  
>  Le operazioni sugli indici online sono disponibili solo in alcune edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere Funzionalità supportate dalle edizioni di SQL Server 2016.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Security](#Security)  
  
-   **Per ricompilare un indice online tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   È consigliabile eseguire operazioni online sugli indici per ambiti aziendali in funzione 24 ore al giorno e sette giorni su sette, in cui l'esigenza di attività simultanee durante le operazioni sugli indici rappresenta un elemento essenziale.  
  
-   L'opzione ONLINE è disponibile nelle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] seguenti.  
  
    -   [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)  
  
    -   [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)  
  
    -   [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md)  
  
    -   [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) (per aggiungere o eliminare vincoli UNIQUE o PRIMARY KEY con l'opzione di indice CLUSTERED)  
  
-   Per altre limitazioni e restrizioni relative alla creazione, alla ricompilazione o all'eliminazione degli indici online, vedere [Linee guida per le operazioni di indice online](../../relational-databases/indexes/guidelines-for-online-index-operations.md).  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È richiesta l'autorizzazione ALTER per la tabella o la vista.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-rebuild-an-index-online"></a>Per ricompilare un indice online  
  
1.  In Esplora oggetti fare clic sul segno più per espandere il database contenente la tabella in cui si desidera ricompilare un indice online.  
  
2.  Espandere la cartella **Tabelle** .  
  
3.  Fare clic sul segno più per espandere la tabella in cui si desidera ricompilare un indice online.  
  
4.  Espandere la cartella **Indici** .  
  
5.  Fare clic con il pulsante destro del mouse sull'indice da ricompilare online e selezionare **Proprietà**.  
  
6.  In **Selezione pagina**selezionare **Opzioni**.  
  
7.  Selezionare **Consenti elaborazione DML online**, quindi selezionare **True** dall'elenco.  
  
8.  Fare clic su **OK**.  
  
9. Fare clic con il pulsante destro del mouse sull'indice da ricompilare online e selezionare **Ricompila**.  
  
10. Nella finestra di dialogo **Ricompila indici** verificare che nella griglia **Indici da ricompilare** sia presente l'indice corretto e fare clic su **OK**.  
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
### <a name="to-create-rebuild-or-drop-an-index-online"></a>Per creare, ricompilare o eliminare un indice online  
  
Nell'esempio seguente viene ricompilato un indice online esistente nel database AdventureWorks.
  
 ```sql  
 ALTER INDEX AK_Employee_NationalIDNumber
   ON HumanResources.Employee  
   REBUILD WITH (ONLINE = ON)
;
```  
  
Nell'esempio seguente viene eliminato un indice cluster online e la tabella risultante (heap) viene spostata nel filegroup `NewGroup` tramite la clausola `MOVE TO` . Vengono eseguite query sulle viste del catalogo `sys.indexes`, `sys.tables`e `sys.filegroups` per verificare la posizione dell'indice e della tabella nei filegroup prima e dopo lo spostamento.  
  
[!code-sql[IndexDDL#DropIndex4](../../relational-databases/indexes/codesnippet/tsql/perform-index-operations_1.sql)]  
  
Per altre informazioni, vedere [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
