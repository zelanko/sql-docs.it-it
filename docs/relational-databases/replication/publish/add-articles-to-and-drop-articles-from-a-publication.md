---
title: Aggiungere ed eliminare articoli di una pubblicazione (SSMS)
description: Descrive in che modo aggiungere ed eliminare articoli in una pubblicazione usando SQL Server Management Studio (SSMS).
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- articles [SQL Server replication], dropping
- deleting articles
- dropping articles
- adding articles
- articles [SQL Server replication], adding
ms.assetid: d5a3e536-62d2-4473-a178-877ba52f7d7f
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 0b0194dec7902311ef48dc889dab6eb6d299df9f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "76286548"
---
# <a name="add-articles-to-and-drop-articles-from-a-publication"></a>Aggiungere ed eliminare articoli in una pubblicazione
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Aggiungere inizialmente articoli a una pubblicazione durante la creazione nell'ambito della Creazione guidata nuova pubblicazione. Per altre informazioni sull'uso di questa procedura guidata, vedere [Creare una pubblicazione](../../../relational-databases/replication/publish/create-a-publication.md).  
  
 Dopo la creazione di una pubblicazione, aggiungere ed eliminare articoli nella pagina **Articoli** della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** . Per ulteriori informazioni sull'accesso a questa finestra di dialogo, vedere [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md). Per altre informazioni sulle considerazioni relative all'aggiunta e l'eliminazione di articoli, vedere [Aggiungere ed eliminare articoli in pubblicazioni esistenti](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
### <a name="to-add-an-article-after-a-publication-is-created"></a>Per aggiungere un articolo dopo la creazione di una pubblicazione  
  
1.  Nella pagina **Articoli** della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** deselezionare la casella di controllo **Mostra solo oggetti selezionati nell'elenco**. Ciò consente di visualizzare gli oggetti non pubblicati nel database di pubblicazione.  
  
2.  Selezionare la casella di controllo accanto a ogni articolo che si desidera aggiungere.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-delete-an-article"></a>Per eliminare un articolo  
  
1.  Nella pagina **Articoli** della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** deselezionare la casella di controllo accanto a ogni articolo che si desidera eliminare.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)   
 [Pubblicare dati e oggetti di database](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
