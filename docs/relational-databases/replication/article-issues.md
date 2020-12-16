---
description: Problemi articoli
title: Problemi articoli | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.articleissues.f1
ms.assetid: bde57da2-dd47-412f-9df7-9224968b2448
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 53df3848ffac7b7408d90b48d74a27410cd2a155
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467272"
---
# <a name="article-issues"></a>Problemi articoli
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  Nella pagina **Problemi articoli** sono elencate le condizioni rilevate relative ad articoli e tutte le modifiche che è necessario apportare come risultato di tali condizioni. Nella tabella seguente vengono elencati i possibili problemi e indicate le azioni necessarie per garantire il corretto funzionamento della replica e delle applicazioni esistenti.  
  
|Problema articolo|Dettagli|Azione richiesta|  
|-------------------|-------------|---------------------|  
|Nelle tabelle verranno aggiunte colonne di tipo uniqueidentifier.|La replica richiede una colonna di tipo di dati **uniqueidentifier** per tutti gli articoli in una pubblicazione di tipo merge o in una pubblicazione transazionale che consente sottoscrizioni ad aggiornamenti.|La replica aggiunge automaticamente una colonna di tipo di dati **uniqueidentifier** alle tabelle pubblicate che ne sono prive al momento della generazione del primo snapshot. È necessario accertarsi che le istruzioni INSERT e UPDATE che fanno riferimento a queste tabelle utilizzino elenchi di colonne, nonché assicurarsi che lo spazio su disco sia sufficiente per la colonna aggiuntiva.|  
|Le colonne IDENTITY richiedono l'opzione NOT FOR REPLICATION.|La replica richiede che tutte le colonne IDENTITY utilizzino l'opzione NOT FOR REPLICATION. Se in una colonna IDENTITY tale opzione non è specificata, la replica tramite i comandi INSERT potrebbe non essere eseguita correttamente.|Si applica alle pubblicazioni create in server di pubblicazione che eseguono [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] e versioni precedenti. Per ogni colonna IDENTITY, è necessario specificare la proprietà NOT FOR REPLICATION.|  
|La proprietà IDENTITY non è stata trasferita nei Sottoscrittori.|Questa pubblicazione non consente aggiornamenti nei Sottoscrittori. Quando le colonne IDENTITY vengono trasferite nel Sottoscrittore, la proprietà IDENTITY non viene trasferita. Ad esempio, una colonna definita come INT IDENTITY nel server di pubblicazione viene definita come INT nel Sottoscrittore.|Si applica alle pubblicazioni create in server di pubblicazioni in cui è in esecuzione [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] e versioni precedenti. Non è necessaria alcuna azione.|  
|Le tabelle a cui fanno riferimento le viste sono obbligatorie.|In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è necessario che tutte le tabelle a cui fanno riferimento le viste e le viste indicizzate pubblicate siano disponibili nel Sottoscrittore. Le tabelle a cui si fa riferimento che non vengono pubblicate come articoli nella pubblicazione presente devono essere create manualmente nel Sottoscrittore.|Utilizzare il pulsante **Indietro** per spostarsi sulla pagina **Articoli** . Aggiungere tutti gli oggetti necessari.|  
|Gli oggetti a cui fanno riferimento le stored procedure sono obbligatori.|In[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è necessario che tutti gli oggetti a cui fanno riferimento stored procedure pubblicate, ad esempio tabelle e funzioni definite dall'utente, siano disponibili nel Sottoscrittore. Gli oggetti a cui si fa riferimento che non sono pubblicati come articoli nella pubblicazione presente devono essere creati manualmente nel Sottoscrittore.|Utilizzare il pulsante **Indietro** per spostarsi sulla pagina **Articoli** . Aggiungere tutti gli oggetti necessari.|  
  
## <a name="see-also"></a>Vedere anche  
 [Pubblicare dati e oggetti di database](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Creare una pubblicazione](../../relational-databases/replication/publish/create-a-publication.md)  
  
  
