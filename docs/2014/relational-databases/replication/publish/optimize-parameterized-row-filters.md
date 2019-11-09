---
title: Ottimizzare i filtri di riga con parametri | Microsoft Docs
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- precomputed partitions [SQL Server replication]
- filters [SQL Server replication], parameterized
- merge replication precomputed partitions [SQL Server replication], SQL Server Management Studio
- parameterized filters [SQL Server replication], optimizing
ms.assetid: 49349605-ebd0-4757-95be-c0447f30ba13
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 216504cc6145a60e8b7d4996d29f46cb9d08458d
ms.sourcegitcommit: 619917a0f91c8f1d9112ae6ad9cdd7a46a74f717
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/09/2019
ms.locfileid: "73882141"
---
# <a name="optimize-parameterized-row-filters"></a>Ottimizzazione dei filtri di riga con parametri
  In questo argomento si descrive come ottimizzare i filtri di riga con parametri in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Indicazioni](#Recommendations)  
  
-   **Per ottimizzare i filtri di riga con parametri, utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Recommendations"></a> Raccomandazioni  
  
-   Quando si utilizzano filtri con parametri, è possibile controllare in che modo i filtri vengono elaborati dalla replica di tipo merge specificando l'opzione **use partition groups** o **keep partition changes** durante la creazione di una pubblicazione. Queste opzioni consentono di migliorare le prestazioni di sincronizzazione delle pubblicazioni con gli articoli filtrati tramite l'archiviazione di metadati aggiuntivi nel database di pubblicazione. È possibile controllare la modalità di condivisione dei dati tra i Sottoscrittori impostando l'opzione **partition options** durante la creazione di un articolo. Per altre informazioni su tali requisiti, vedere [Filtri di riga con parametri](../merge/parameterized-filters-parameterized-row-filters.md).  
  
     Con i Sottoscrittori [!INCLUDE[ssEW](../../../includes/ssew-md.md)], keep_partition_changes deve essere impostato su true per assicurarsi che le eliminazioni vengano propagate correttamente. Se impostato su false, nel Sottoscrittore potrebbero essere presenti più righe rispetto al previsto.  
  
##  <a name="SSMSProcedure"></a> Con SQL Server Management Studio  
 È possibile utilizzare le impostazioni seguenti per ottimizzare i filtri di riga con parametri:  
  
 **Partition Options**  
 Impostare questa opzione nella pagina **Proprietà** della finestra di dialogo **Proprietà articolo - \<Articolo>** o nella finestra di dialogo **Aggiungi filtro**. Entrambe le finestre di dialogo sono disponibili nella Creazione guidata nuova pubblicazione e nella finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** . La finestra di dialogo **Proprietà articolo - \<Articolo>** consente di specificare altri valori per questa opzione, che non sono disponibili nella finestra di dialogo **Aggiungi filtro**.  
  
 **Pre-calcola partizioni**  
 Per impostazione predefinita, questa opzione viene impostata su **True** se gli articoli nella pubblicazione rispondono a una serie di requisiti. Per altre informazioni su questi requisiti, vedere [Ottimizzare le prestazioni dei filtri con parametri con le partizioni pre-calcolate](../merge/parameterized-filters-optimize-for-precomputed-partitions.md). Modificare questa opzione nella pagina **Opzioni sottoscrizione** della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** .  
  
 **Ottimizza sincronizzazione**  
 Questa opzione deve essere impostata su **True** solo se **Pre-calcola partizioni** viene impostata su **False**. Impostare questa opzione nella pagina **Opzioni sottoscrizione** della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** .  
  
 Per altre informazioni sull'uso della Creazione guidata nuova pubblicazione e sull'accesso alla finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** , vedere [Creare una pubblicazione](create-a-publication.md) e [Visualizzare e modificare le proprietà della pubblicazione](view-and-modify-publication-properties.md).  
  
#### <a name="to-set-partition-options-in-the-add-filter-or-edit-filter-dialog-box"></a>Per impostare le opzioni delle partizioni nella finestra di dialogo Aggiungi filtro o Modifica filtro  
  
1.  Nella pagina **Filtro righe tabella** della Creazione guidata nuova pubblicazione o nella pagina **Filtra righe** della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** fare clic su **Aggiungi** e quindi su **Aggiungi filtro**.  
  
2.  Creare un filtro con parametri. Per altre informazioni, vedere [Define and Modify a Parameterized Row Filter for a Merge Article](define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
3.  Selezionare l'opzione corrispondente alla modalità desiderata di condivisione dei dati tra i Sottoscrittori:  
  
    -   **Una riga di questa tabella verrà inviata a più sottoscrizioni**  
  
    -   **Una riga di questa tabella verrà inviata a una sola sottoscrizione**  
  
     Selezionando **Una riga di questa tabella verrà inviata a una sola sottoscrizione**è possibile ottimizzare le prestazioni della replica di tipo merge archiviando ed elaborando una minore quantità di metadati. È tuttavia necessario garantire che i dati vengano partizionati in modo da non consentire la replica di una riga in più Sottoscrittori. Per altre informazioni, vedere la sezione relativa all'impostazione delle opzioni delle partizioni nell'argomento [Filtri di riga con parametri](../merge/parameterized-filters-parameterized-row-filters.md).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Se è visualizzata la finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** fare clic su **OK** per salvare e chiudere la finestra di dialogo.  
  
#### <a name="to-set-partition-options-in-the-article-properties---article-dialog-box"></a>Per impostare Opzioni partizioni nella finestra di dialogo Proprietà articolo - \<Articolo>  
  
1.  Nella pagina **Articoli** della Creazione guidata nuova pubblicazione o nella finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** selezionare una tabella e quindi fare clic su **Proprietà articolo**.  
  
2.  Fare clic su **Imposta proprietà dell'articolo di tabelle evidenziato** o su **Imposta proprietà di tutti gli articoli di tabelle**.  
  
3.  Nella sezione **Oggetto di destinazione** della scheda **Proprietà** della finestra di dialogo **Proprietà articolo - \<Articolo>** specificare uno dei seguenti valori per **Opzioni partizioni**:  
  
    -   **Sovrapposte**  
  
    -   **Sovrapposte, non ammesse modifiche dei dati fuori partizione**  
  
    -   **Non sovrapposte, sottoscrizione unica**  
  
    -   **Non sovrapposte, condivise dalle sottoscrizioni**  
  
     Per ulteriori informazioni su queste opzioni e sulla loro relazione con le opzioni disponibili nelle finestre di dialogo **Aggiungi filtro** e **Modifica filtro** , vedere la sezione relativa all'impostazione delle opzioni partizioni nell'argomento [i filtri di riga con parametri](../merge/parameterized-filters-parameterized-row-filters.md).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Se è visualizzata la finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** fare clic su **OK** per salvare e chiudere la finestra di dialogo.  
  
#### <a name="to-set-precompute-partitions"></a>Per impostare Pre-calcola partizioni  
  
1.  Nella pagina **Opzioni sottoscrizione** della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** selezionare un valore per l'opzione **Pre-calcola partizioni**. Questa proprietà è in sola lettura se:  
  
    -   La pubblicazione non soddisfa i requisiti delle partizioni pre-calcolate.  
  
    -   Non è ancora stato generato lo snapshot per la pubblicazione. In questo caso, l'opzione visualizza il valore **Imposta automaticamente alla creazione di uno snapshot**.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-set-optimize-synchronization"></a>Per impostare Ottimizza sincronizzazione  
  
1.  Nella pagina **Opzioni sottoscrizione** della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** selezionare il valore **True** per l'opzione **Ottimizza sincronizzazione**.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Con Transact-SQL  
 Per le definizioni delle opzioni di filtro per **\@keep_partition_changes** e **\@use_partition_groups**, vedere [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql).  
  
#### <a name="to-specify-merge-filter-optimizations-when-creating-a-new-publication"></a>Per specificare le ottimizzazioni del filtro di merge durante la creazione di una nuova pubblicazione  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql). Specificare **\@publication** e il valore `true` per uno dei seguenti parametri:  
  
    -   **\@use_partition_groups**:-l'ottimizzazione delle prestazioni più elevata, purché gli articoli siano conformi ai requisiti per le partizioni pre-calcolate. Per altre informazioni, vedere [Ottimizzare le prestazioni dei filtri con parametri con le partizioni pre-calcolate](../merge/parameterized-filters-optimize-for-precomputed-partitions.md).  
  
    -   **\@keep_partition_changes** : utilizzare questa ottimizzazione se non è possibile utilizzare le partizioni pre-calcolate.  
  
2.  Aggiungere un processo snapshot per la pubblicazione. Per altre informazioni, vedere [Creare una pubblicazione](create-a-publication.md).  
  
3.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)specificando i parametri seguenti:  
  
    -   **\@publication** : nome della pubblicazione del passaggio 1.  
  
    -   **\@articolo** -un nome per l'articolo  
  
    -   **\@source_object** : l'oggetto di database da pubblicare.  
  
    -   **\@subset_filterclause** : clausola di filtro con parametri facoltativa utilizzata per filtrare orizzontalmente l'articolo.  
  
    -   **\@partition_options** : opzioni di partizione per l'articolo filtrato.  
  
4.  Ripetere il passaggio 3 per ogni articolo della pubblicazione.  
  
5.  (Facoltativo) Nel database di pubblicazione del server di pubblicazione eseguire [sp_addmergefilter](/sql/relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql) per definire un filtro di join tra due articoli. Per altre informazioni, vedere [Define and Modify a Join Filter Between Merge Articles](define-and-modify-a-join-filter-between-merge-articles.md).  
  
#### <a name="to-view-and-modify-merge-filter-behaviors-for-an-existing-publication"></a>Per visualizzare e modificare i comportamenti del filtro di merge per una pubblicazione esistente  
  
1.  Opzionale Nel database di pubblicazione del server di pubblicazione eseguire [sp_helpmergepublication](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql), specificando **\@pubblicazione**. Si noti il valore di **keep_partition_changes** e **use_partition_groups** nel set di risultati.  
  
2.  (Facoltativo) Nel database di pubblicazione del server di pubblicazione eseguire [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql). Specificare il valore **use_partition_groups** per **\@proprietà** e `true` o `false` per **\@valore**.  
  
3.  (Facoltativo) Nel database di pubblicazione del server di pubblicazione eseguire [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql). Specificare il valore **keep_partition_changes** per **\@proprietà** e `true` o `false` per **\@valore**.  
  
    > [!NOTE]  
    >  Quando si abilita **keep_partition_changes**, è necessario disabilitare prima **use_partition_groups** e specificare il valore **1** per **\@force_reinit_subscription**.  
  
4.  (Facoltativo) Nel database di pubblicazione del server di pubblicazione eseguire [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql). Specificare il valore **partition_options** per **\@proprietà** e il valore appropriato per **\@valore**. Per le definizioni di queste opzioni di filtro, vedere [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) .  
  
5.  (Facoltativo) Avviare l'agente snapshot per rigenerare lo snapshot se necessario. Per informazioni sulle modifiche necessarie per la generazione di un nuovo snapshot, vedere [Modificare le proprietà di pubblicazioni e articoli](change-publication-and-article-properties.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Generare automaticamente un set di filtri di join tra gli articoli di merge &#40;SQL Server Management Studio&#41;](automatically-generate-join-filters-between-merge-articles.md)   
 [Definizione e modifica di un filtro di riga con parametri per un articolo di merge](define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [Parameterized Row Filters](../merge/parameterized-filters-parameterized-row-filters.md)  
  
  
