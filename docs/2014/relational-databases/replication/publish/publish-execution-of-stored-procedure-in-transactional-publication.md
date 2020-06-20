---
title: Pubblicare l'esecuzione di una stored procedure in una pubblicazione transazionale (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publishing [SQL Server replication], stored procedure execution
- stored procedures [SQL Server replication], publishing
ms.assetid: 1d3a3525-0bc5-466f-b097-5359dc74432d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a226d7c58b3b72caf415d8e873b58ca38d3c749f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060431"
---
# <a name="publish-the-execution-of-a-stored-procedure-in-a-transactional-publication-sql-server-management-studio"></a>Pubblicazione dell'esecuzione di una stored procedure in una pubblicazione transazionale (SQL Server Management Studio)
  Consente di specificare che l'esecuzione di un stored procedure (anziché solo la relativa definizione) deve essere pubblicata nella finestra di dialogo **Proprietà articolo- \<Article> ** . Questa finestra di dialogo è disponibile nella creazione guidata nuova pubblicazione e nella finestra di dialogo **Proprietà pubblicazione- \<Publication> ** . Per altre informazioni sull'uso della creazione guidata e l'accesso alla finestra di dialogo, vedere [Creare una pubblicazione](create-a-publication.md) e [Visualizzare e modificare le proprietà della pubblicazione](view-and-modify-publication-properties.md).  
  
 La definizione della procedura, ovvero l'istruzione CREATE PROCEDURE, viene replicata nel Sottoscrittore durante l'inizializzazione della sottoscrizione. Quando la procedura viene eseguita nel server di pubblicazione, la replica esegue la procedura corrispondente nel Sottoscrittore.  
  
### <a name="to-publish-the-execution-of-a-stored-procedure"></a>Per pubblicare l'esecuzione di una stored procedure  
  
1.  Nella pagina **articoli** della creazione guidata nuova pubblicazione o nella finestra di dialogo **proprietà \<Publication> pubblicazione-** selezionare un stored procedure.  
  
2.  Fare clic su **Proprietà articolo**e quindi su **Imposta proprietà dell'articolo di stored procedure evidenziato**.  
  
3.  Nella finestra di dialogo **proprietà \<Article> articolo-** specificare uno dei valori seguenti per l'opzione **replica** :  
  
    -   **Esecuzione della stored procedure**  
  
    -   **Esecuzione in una transazione serializzata della stored procedure**  
  
         Questa è l'opzione consigliata in quanto replica l'esecuzione della procedura solo se essa viene eseguita all'interno del contesto di una transazione serializzabile. Se viene eseguita in un contesto diverso, le modifiche ai dati delle tabelle pubblicate vengono replicate come una serie di istruzioni DML (Data Manipulation Language).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Se si è nella finestra di dialogo **proprietà \<Publication> pubblicazione-** fare clic su **OK** per salvare e chiudere la finestra di dialogo.  
  
## <a name="see-also"></a>Vedere anche  
 [Pubblicazione dell'esecuzione di stored procedure nella replica transazionale](../transactional/publishing-stored-procedure-execution-in-transactional-replication.md)  
  
  
