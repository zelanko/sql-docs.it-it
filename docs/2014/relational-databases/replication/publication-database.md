---
title: Database di pubblicazione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.publicationdatabase.f1
ms.assetid: a9fafc9b-9963-4b59-97a0-3472158fa665
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cb31bae59d95b01279a9fa84e02cd22c8017ca14
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63021747"
---
# <a name="publication-database"></a>Database di pubblicazione
  Il database di pubblicazione è il database del server di pubblicazione che funge da origine dei dati e degli oggetti di database da replicare. Tutti i database utilizzati nella replica devono essere abilitati. Il database viene abilitato quando un membro del ruolo predefinito del server **sysadmin** :  
  
-   Crea una pubblicazione nel database tramite la Creazione guidata nuova pubblicazione.  
  
-   Seleziona il database nella finestra di dialogo **Proprietà server di pubblicazione** .  
  
-   Esegue **sp_replicationdboption** e imposta su **True** l'opzione per la **pubblicazione** relativa a snapshot e pubblicazioni transazionali o l'opzione per la **pubblicazione di tipo merge**relativa a pubblicazioni di tipo merge.  
  
## <a name="options"></a>Opzioni  
 **Database**  
 Consente di selezionare il nome del database contenente i dati e gli oggetti di database che si desidera pubblicare.  
  
## <a name="see-also"></a>Vedere anche  
 [Pubblicare dati e oggetti di database](publish/publish-data-and-database-objects.md)   
 [Create a Publication](publish/create-a-publication.md)   
 [Visualizzare e modificare le proprietà del server di pubblicazione e del database di distribuzione](view-and-modify-distributor-and-publisher-properties.md)   
 [sp_replicationdboption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql)  
  
  
