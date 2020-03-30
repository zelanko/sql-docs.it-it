---
title: Pubblicare l'esecuzione delle stored procedure (transazionali)
description: Informazioni su come pubblicare l'esecuzione di stored procedure usando SQL Server Management Studio.
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publishing [SQL Server replication], stored procedure execution
- stored procedures [SQL Server replication], publishing
ms.assetid: 1d3a3525-0bc5-466f-b097-5359dc74432d
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: b26656d1610b2e813aaf82ece3564af6fc544b11
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "76287596"
---
# <a name="publish-execution-of-stored-procedure-in-transactional-publication"></a>Pubblicare l'esecuzione delle stored procedure nella replica transazionale
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Specificare che nella finestra di dialogo **Proprietà articolo - \<Articolo>** deve essere pubblicata l'esecuzione di una stored procedure, anziché la sola definizione. Questa finestra di dialogo è disponibile nella Creazione guidata nuova pubblicazione e nella finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** . Per altre informazioni sull'uso della creazione guidata e l'accesso alla finestra di dialogo, vedere [Creare una pubblicazione](../../../relational-databases/replication/publish/create-a-publication.md) e [Visualizzare e modificare le proprietà della pubblicazione](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
 La definizione della procedura, ovvero l'istruzione CREATE PROCEDURE, viene replicata nel Sottoscrittore durante l'inizializzazione della sottoscrizione. Quando la procedura viene eseguita nel server di pubblicazione, la replica esegue la procedura corrispondente nel Sottoscrittore.  
  
### <a name="to-publish-the-execution-of-a-stored-procedure"></a>Per pubblicare l'esecuzione di una stored procedure  
  
1.  Nella pagina **Articoli** della Creazione guidata nuova pubblicazione o nella finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** selezionare una stored procedure.  
  
2.  Fare clic su **Proprietà articolo**e quindi su **Imposta proprietà dell'articolo di stored procedure evidenziato**.  
  
3.  Nella finestra di dialogo **Proprietà articolo - \<Articolo>** specificare uno dei valori seguenti per l'opzione **Replica**:  
  
    -   **Esecuzione della stored procedure**  
  
    -   **Esecuzione in una transazione serializzata della stored procedure**  
  
         Questa è l'opzione consigliata in quanto replica l'esecuzione della procedura solo se essa viene eseguita all'interno del contesto di una transazione serializzabile. Se viene eseguita in un contesto diverso, le modifiche ai dati delle tabelle pubblicate vengono replicate come una serie di istruzioni DML (Data Manipulation Language).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Se è visualizzata la finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** fare clic su **OK** per salvare e chiudere la finestra di dialogo.  
  
## <a name="see-also"></a>Vedere anche  
 [Pubblicazione dell'esecuzione delle stored procedure nella replica transazionale](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)  
  
  
