---
title: Impostare il metodo di propagazione per le modifiche ai dati negli articoli transazionali | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, propagation methods
- propagating data changes [SQL Server replication]
ms.assetid: 0a291582-f034-42da-a1a3-29535b607b74
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: db74bd7de8fcf3cdba6787fda18c510237d63372
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68941088"
---
# <a name="set-the-propagation-method-for-data-changes-to-transactional-articles"></a>Impostazione del metodo di propagazione per le modifiche ai dati negli articoli transazionali
  In questo argomento viene descritto come impostare il metodo di propagazione per le modifiche ai dati negli articoli transazionali in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 Per impostazione predefinita, la replica transazionale propaga le modifiche ai Sottoscrittori tramite un set di stored procedure per ogni articolo. È possibile sostituire tali procedure con procedure personalizzate. Per altre informazioni, vedere [Specificare la modalità di propagazione delle modifiche per gli articoli transazionali](../transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
-   **Per impostare il metodo di propagazione per la modifica dei dati negli articoli transazionali tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
## <a name="before-you-begin"></a>Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   È consigliabile prestare particolare attenzione quando si modificano i file di snapshot generati dalla replica. È necessario testare e supportare la logica personalizzata nelle stored procedure personalizzate. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] non fornisce supporto per la logica personalizzata.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 Specificare il metodo di propagazione nella scheda **Proprietà** della finestra di dialogo **Proprietà articolo- \<Articolo>**, disponibile nella Creazione guidata nuova pubblicazione e nella finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>**. Per altre informazioni sull'uso della creazione guidata e l'accesso alla finestra di dialogo, vedere [Creare una pubblicazione](create-a-publication.md) e [Visualizzare e modificare le proprietà della pubblicazione](view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-the-propagation-method"></a>Per specificare il metodo di propagazione  
  
1.  Nella pagina **Articoli** della Creazione guidata nuova pubblicazione o nella finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** selezionare una tabella e quindi fare clic su **Proprietà articolo**.  
  
2.  Fare clic su **Imposta proprietà dell'articolo tabella evidenziato**.  
  
3.  Nella scheda **Proprietà** della finestra di dialogo **Proprietà articolo - \<Articolo>**, all'interno della sezione **Recapito istruzione**, specificare il metodo di propagazione per ogni operazione usando i menu **Formato recapito INSERT**, **Formato recapito UPDATE** e **Formato recapito DELETE**.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Se è visualizzata la finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** fare clic su **OK** per salvare e chiudere la finestra di dialogo.  
  
#### <a name="to-generate-and-use-custom-stored-procedures"></a>Per generare e utilizzare stored procedure personalizzate  
  
1.  Nella pagina **Articoli** della Creazione guidata nuova pubblicazione o nella finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** selezionare una tabella e quindi fare clic su **Proprietà articolo**.  
  
2.  Fare clic su **Imposta proprietà dell'articolo tabella evidenziato**.  
  
     Nella scheda **Proprietà** della finestra di dialogo **Proprietà articolo - \<Articolo>**, all'interno della sezione **Recapito istruzione**, selezionare la sintassi CALL dal menu del formato di recapito appropriato (**Formato recapito INSERT**, **Formato recapito UPDATE** o **Formato recapito DELETE**) e digitare il nome della stored procedure da usare in **Stored procedure INSERT**, **Stored procedure DELETE** o **Stored procedure UPDATE**. Per altre informazioni sulla sintassi CALL, vedere la sezione "Sintassi di chiamata per le stored procedure" in [Specificare la modalità di propagazione delle modifiche per gli articoli transazionali](../transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
4.  Se è visualizzata la finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** fare clic su **OK** per salvare e chiudere la finestra di dialogo.  
  
5.  Quando lo snapshot per la pubblicazione viene generato, esso include la procedura specificata nel passaggio precedente. Le procedure utilizzeranno la sintassi CALL specificata, ma includeranno la logica predefinita utilizzata dalla replica.  
  
     Dopo la generazione dello snapshot, passare alla cartella snapshot per la pubblicazione cui appartiene questo articolo e individuare il file con estensione **sch** che presenta lo stesso nome dell'articolo. Aprire il file mediante Blocco note o un altro editor di testo, individuare il comando CREATE PROCEDURE per le stored procedure di inserimento, aggiornamento o eliminazione, quindi modificare la definizione della procedura in modo da fornire qualsiasi logica personalizzata per la propagazione delle modifiche ai dati. Se lo snapshot viene rigenerato, è necessario ricreare la stored procedura personalizzata.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
 La replica transazionale consente di controllare la modalità con cui le modifiche vengono propagate dal server di pubblicazione ai Sottoscrittori. Questo metodo di propagazione può inoltre essere impostato a livello di programmazione quando un articolo viene creato e in seguito modificato tramite le stored procedure di replica.  
  
> [!NOTE]  
>  È possibile specificare un metodo di propagazione diverso per ogni tipo di operazione DML (Data Manipulation Language), ovvero inserimento, aggiornamento o eliminazione, che si verifica in una riga di dati pubblicati.  
  
 Per altre informazioni, vedere [Specificare la modalità di propagazione delle modifiche per gli articoli transazionali](../transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
#### <a name="to-create-an-article-that-uses-transact-sql-commands-to-propagate-data-changes"></a>Per creare un articolo che utilizza comandi Transact-SQL per propagare le modifiche ai dati  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql). Specificare il nome della pubblicazione cui appartiene l'articolo per ** \@la pubblicazione**, il nome dell' ** \@articolo per l'articolo,** l'oggetto di database da pubblicare per ** \@source_object**e il valore **SQL** per almeno uno dei parametri seguenti:  
  
    -   ins_cmd: controlla la replica dei comandi [Insert](/sql/t-sql/statements/insert-transact-sql) . ** \@**  
  
    -   upd_cmd: controlla la replica dei comandi [Update](/sql/t-sql/queries/update-transact-sql) . ** \@**  
  
    -   del_cmd: controlla la replica dei comandi [Delete](/sql/t-sql/statements/delete-transact-sql) . ** \@**  
  
    > [!NOTE]  
    >  Quando si specifica il valore **SQL** per uno dei parametri indicati in precedenza, i comandi di tale tipo verranno replicati nel Sottoscrittore come comandi [!INCLUDE[tsql](../../../includes/tsql-md.md)] appropriati.  
  
     Per altre informazioni, vedere [definire un articolo](define-an-article.md).  
  
#### <a name="to-create-an-article-that-does-not-propagate-data-changes"></a>Per creare un articolo che non propaga le modifiche ai dati  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql). Specificare il nome della pubblicazione cui appartiene l'articolo per ** \@la pubblicazione**, il nome dell' ** \@articolo per l'articolo,** l'oggetto di database da pubblicare per ** \@source_object**e il valore **None** per almeno uno dei parametri seguenti:  
  
    -   ins_cmd: controlla la replica dei comandi [Insert](/sql/t-sql/statements/insert-transact-sql) . ** \@**  
  
    -   upd_cmd: controlla la replica dei comandi [Update](/sql/t-sql/queries/update-transact-sql) . ** \@**  
  
    -   del_cmd: controlla la replica dei comandi [Delete](/sql/t-sql/statements/delete-transact-sql) . ** \@**  
  
    > [!NOTE]  
    >   Quando si specifica il valore **NONE** per uno dei parametri indicati in precedenza, i comandi di tale tipo non verranno replicati nel Sottoscrittore.  
  
     Per altre informazioni, vedere [definire un articolo](define-an-article.md).  
  
#### <a name="to-create-an-article-with-user-modified-custom-stored-procedures"></a>Per creare un articolo con stored procedure personalizzate modificate dall'utente  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql). Specificare il nome della pubblicazione cui appartiene l'articolo per ** \@la pubblicazione**, il nome dell' ** \@articolo per l'oggetto di database**da pubblicare per ** \@source_object**, un valore per la ** \@** maschera di schema_option che contiene il valore **0x02** (Abilita la generazione automatica di stored procedure personalizzate) e almeno uno dei seguenti parametri:  
  
    -   ins_cmd: specificare il valore <strong>Call sp_MSins_*article_name*</strong>, dove **_article_name_** è il valore specificato per ** \@article**. ** \@**  
  
    -   **_article_name_** \@ <strong>*article_name* </strong> ** \@del_cmd** : specificare il valore Call sp_MSdel_ article_name o <strong>XCALL sp_MSdel_*article_name*</strong>, dove article_name è il valore specificato per _ * article * *.  
  
    -   ** \@** _**article_name**_ <strong>*article_name*</strong> <strong>*article_name*</strong> ** \@upd_cmd** : specificare il valore SCALL sp_MSupd_ article_name, chiamare sp_MSupd_ article_name, <strong>XCALL sp_MSupd__article_name*</strong>o <strong>MCALL sp_MSupd_* article_name *</strong>, dove article_name è il valore specificato per article.  
  
    > [!NOTE]  
    >  Per ognuno dei parametri di comando indicati in precedenza, è possibile specificare il nome desiderato per le stored procedure generate dalla replica.  
  
    > [!NOTE]  
    >  Per altre informazioni sulla sintassi CALL, SCALL, XCALL e MCALL, vedere [Specificare la modalità di propagazione delle modifiche per gli articoli transazionali](../transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
     Per altre informazioni, vedere [definire un articolo](define-an-article.md).  
  
2.  Dopo la generazione dello snapshot, passare alla cartella snapshot per la pubblicazione cui appartiene questo articolo e individuare il file con estensione **sch** che presenta lo stesso nome dell'articolo. Aprire il file mediante Notepad.exe, individuare il comando CREATE PROCEDURE per le stored procedure di inserimento, aggiornamento o eliminazione e modificare la definizione della procedura per specificare la logica personalizzata per la propagazione delle modifiche ai dati. Per altre informazioni, vedere [Specificare la modalità di propagazione delle modifiche per gli articoli transazionali](../transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
#### <a name="to-create-an-article-with-custom-scripting-in-the-custom-stored-procedures-to-propagate-data-changes"></a>Per creare un articolo con scripting personalizzato nelle stored procedure personalizzate per propagare le modifiche ai dati  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql). Specificare il nome della pubblicazione cui appartiene l'articolo per ** \@la pubblicazione**, il nome dell' ** \@articolo per l'oggetto di database**da pubblicare per ** \@source_object**, un valore per la ** \@** maschera di schema_option che contiene il valore **0x02** (Abilita la generazione automatica di stored procedure personalizzate) e almeno uno dei seguenti parametri:  
  
    -   ins_cmd: specificare il valore <strong>Call sp_MSins_*article_name*</strong>, dove _**article_name**_ è il valore specificato per ** \@article**. ** \@**  
  
    -   ** \@** _**article_name**_ <strong>*article_name* </strong> ** \@del_cmd** : specificare il valore Call sp_MSdel_ article_name o <strong>XCALL sp_MSdel_*article_name*</strong>, dove article_name è il valore specificato per article.  
  
    -   ** \@** <strong>*article_name*</strong> _**article_name**_ <strong>*article_name*</strong> <strong>*article_name*</strong> ** \@upd_cmd** : specificare il valore SCALL sp_MSupd_ article_name, <strong>Call sp_MSupd_*article_name*</strong>, XCALL sp_MSupd_ article_name, MCALL sp_MSupd_ article_name, dove article_name è il valore specificato per article.  
  
    > [!NOTE]  
    >  Per ognuno dei parametri di comando indicati in precedenza, è possibile specificare il nome desiderato per le stored procedure generate dalla replica.  
  
    > [!NOTE]  
    >  Per altre informazioni sulla sintassi CALL, SCALL, XCALL e MCALL, vedere [Specificare la modalità di propagazione delle modifiche per gli articoli transazionali](../transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
     Per altre informazioni, vedere [definire un articolo](define-an-article.md).  
  
2.  Nel database di pubblicazione del server di pubblicazione utilizzare l'istruzione [ALTER PROCEDURE](/sql/t-sql/statements/alter-procedure-transact-sql) per modificare [sp_scriptpublicationcustomprocs](/sql/relational-databases/system-stored-procedures/sp-scriptpublicationcustomprocs-transact-sql) in modo che restituisca uno script [CREATE PROCEDURE](/sql/t-sql/statements/create-procedure-transact-sql) per le stored procedure personalizzate di inserimento, aggiornamento ed eliminazione. Per altre informazioni, vedere [Specificare la modalità di propagazione delle modifiche per gli articoli transazionali](../transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
#### <a name="to-change-the-method-of-propagating-changes-for-an-existing-article"></a>Per modificare il metodo di propagazione delle modifiche per un articolo esistente  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_changearticle](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql). Specificare ** \@publication**, ** \@article**, il valore **ins_cmd**, **upd_cmd**o **del_cmd** per ** \@Property**e il metodo di propagazione appropriato per ** \@value**.  
  
2.  Ripetere il passaggio 1 per ogni metodo di propagazione da modificare.  
  
## <a name="see-also"></a>Vedere anche  
 [Specificare la modalità di propagazione delle modifiche per gli articoli transazionali](../transactional/transactional-articles-specify-how-changes-are-propagated.md)   
 [Creare una pubblicazione](create-a-publication.md)  
  
  
