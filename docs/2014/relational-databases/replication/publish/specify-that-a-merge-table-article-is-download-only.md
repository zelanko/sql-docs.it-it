---
title: Specificare il tipo solo download per un articolo di tabella di merge | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication [SQL Server replication], download-only articles
- articles [SQL Server replication], download-only
- download-only articles
ms.assetid: 14839cec-6dbf-49c2-aa27-56847b09b4db
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5594c811642225336586c8bce040f7f69724cadb
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52756193"
---
# <a name="specify-that-a-merge-table-article-is-download-only"></a>Impostazione del tipo solo download per un articolo di tabella di merge
  In questo argomento viene descritto come specificare che un articolo di tabella del merge è di solo download in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Gli articoli di solo download sono progettati per le applicazioni i cui dati non vengono aggiornati nei Sottoscrittori. Per altre informazioni, vedere [Ottimizzare le prestazioni della replica di tipo merge con gli articoli di solo download](../merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
-   **Per specificare che un articolo di tabella di merge è di solo download tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Se si specifica che un articolo è di tipo solo download dopo l'inizializzazione delle sottoscrizioni, tutte le sottoscrizioni client a cui è stato inviato l'articolo devono essere reinizializzate. Non è necessario reinizializzare le sottoscrizioni server. Per altre informazioni sugli effetti delle modifiche delle proprietà, vedere [Modifica delle proprietà di pubblicazioni e articoli](change-publication-and-article-properties.md).  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 Specificare che un articolo è di tipo solo download nella pagina **Articoli** della Creazione guidata nuova pubblicazione o nella scheda **Proprietà** della finestra di dialogo **Proprietà articolo - \<Articolo>**. Questa finestra di dialogo è disponibile nella Creazione guidata nuova pubblicazione e nella finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>**. Per altre informazioni sull'uso della creazione guidata e l'accesso alla finestra di dialogo, vedere [Creare una pubblicazione](create-a-publication.md) e [Visualizzare e modificare le proprietà della pubblicazione](view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-that-an-article-is-download-only-on-the-articles-page"></a>Per specificare che un articolo è di tipo solo download nella pagina Articoli  
  
-   Selezionare una tabella nella pagina **Articoli** di Creazione guidata nuova pubblicazione e quindi selezionare la casella di controllo **La tabella evidenziata è di tipo solo download**.  
  
#### <a name="to-specify-that-an-article-is-download-only-on-the-properties-tab-of-the-article-properties---article-dialog-box"></a>Per specificare che un articolo è di tipo solo download nella scheda Proprietà della finestra di dialogo Proprietà articolo - \<Articolo>  
  
1.  Nella pagina **Articoli** della Creazione guidata nuova pubblicazione o nella finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** selezionare una tabella e quindi fare clic su **Proprietà articolo**.  
  
2.  Fare clic su **Imposta proprietà dell'articolo di tabelle evidenziato** o su **Imposta proprietà di tutti gli articoli di tabelle**.  
  
3.  Nella sezione **Oggetto di destinazione** della scheda **Proprietà** della finestra di dialogo **Proprietà articolo - \<Articolo>** specificare uno dei valori seguenti in **Direzione sincronizzazione**:  
  
    -   **Solo download sul Sottoscrittore, non consentire modifiche del Sottoscrittore**  
  
    -   **Solo download sul Sottoscrittore, consenti modifiche del Sottoscrittore**  
  
4.  Se è visualizzata la finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** fare clic su **OK** per salvare e chiudere la finestra di dialogo.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-specify-that-a-new-merge-table-article-is-download-only"></a>Per specificare che un nuovo articolo di tabella di merge è di solo download  
  
1.  Eseguire [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql), specificando il valore **1** o **2** per il parametro **@subscriber_upload_options**. I numeri corrispondono al comportamento seguente:  
  
    -   **0** : nessuna restrizione (valore predefinito). Le modifiche eseguite nel Sottoscrittore vengono caricate nel server di pubblicazione.  
  
    -   **1** : le modifiche sono consentite nel Sottoscrittore, ma non vengono caricate nel server di pubblicazione.  
  
    -   **2** : non è consentito apportare modifiche nel Sottoscrittore.  
  
        > [!NOTE]  
        >  Se la tabella di origine di un articolo è già inclusa in un'altra pubblicazione, il valore di **@subscriber_upload_options** deve coincidere per entrambi gli articoli.  
  
#### <a name="to-modify-an-existing-merge-table-article-to-be-download-only"></a>Per impostare il tipo di un articolo di tabella di merge esistente su solo download  
  
1.  Per determinare se un articolo è di tipo solo download, eseguire [sp_helpmergearticle](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql). Si noti il valore di **upload_options** relativo all'articolo nel set di risultati.  
  
2.  Se il valore restituito al passaggio 1 è **0**, eseguire [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql), specificando il valore **subscriber_upload_options** per **@property**, il valore **1** per **@force_invalidate_snapshot** e **@force_reinit_subscription**e il valore **1** o **2** per **@value**, che corrisponde al comportamento seguente:  
  
    -   **1** : le modifiche sono consentite nel Sottoscrittore, ma non vengono caricate nel server di pubblicazione.  
  
    -   **2** : non è consentito apportare modifiche nel Sottoscrittore.  
  
        > [!NOTE]  
        >  Se la tabella di origine di un articolo è già inclusa in un'altra pubblicazione, il comportamento del solo download deve coincidere per entrambi gli articoli.  
  
## <a name="see-also"></a>Vedere anche  
 [Ottimizzare le prestazioni della replica di tipo merge con gli articoli di solo download](../merge/optimize-merge-replication-performance-with-download-only-articles.md)   
 [Define an Article](define-an-article.md)   
 [Visualizzare e modificare le proprietà degli articoli](view-and-modify-article-properties.md)  
  
  
