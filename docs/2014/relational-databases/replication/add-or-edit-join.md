---
title: Aggiungi join o Modifica join | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.addeditjoin.f1
ms.assetid: 3b546560-720f-48b8-9d63-cf159290e9d4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5fb76e62e1816be53c312cc263053f854ad3b796
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62625931"
---
# <a name="add-or-edit-join"></a>Aggiungi join o Modifica join
  Le finestre di dialogo **Aggiungi join** e **Modifica join** consentono di aggiungere e modificare filtri join per le pubblicazioni di tipo merge.  
  
> [!NOTE]  
>  Per modificare un filtro in una pubblicazione esistente, è necessario un nuovo snapshot per la pubblicazione. Se la pubblicazione dispone di sottoscrizioni, queste ultime devono essere reinizializzate. Per altre informazioni sulle modifiche delle proprietà, vedere [Modificare le proprietà di pubblicazioni e articoli](publish/change-publication-and-article-properties.md).  
  
 Un filtro di join consente di filtrare una tabella in base al tipo di filtro applicato a una tabella correlata nella pubblicazione Una tabella padre viene in genere filtrata utilizzando un filtro di riga con parametri. In seguito uno o più filtri join vengono definiti in modo molto simile alla definizione di un join tra tabelle. I filtri join estendono il filtro di riga in modo che i dati delle tabelle correlate vengano replicati solo se soddisfano la clausola di filtro join.  
  
 I filtri join seguono in genere le relazioni tra chiavi primarie e chiavi esterne definite per le tabelle alle quali vengono applicati, ma non sono necessariamente limitati a tali relazioni. Il filtro join può essere basato su qualsiasi logica che confronti i dati correlati in due tabelle di articoli.  
  
> [!IMPORTANT]  
>  I filtri join possono includere un numero illimitato di tabelle, ma i filtri con un numero elevato di tabelle possono influire negativamente sulle prestazioni durante l'elaborazione di processi merge. Se si generano filtri di join di cinque o più tabelle, considerare altre soluzioni: non filtrare tabelle piccole, non soggette a modifica o tabelle che fungono principalmente da tabelle di ricerca. Utilizzare filtri join solo tra tabelle che devono essere partizionate tra Sottoscrittori.  
  
## <a name="options"></a>Opzioni  
 In questa finestra di dialogo la procedura di creazione di un filtro join tra due tabelle è suddivisa in tre fasi. Per la creazione di più di un filtro join è necessario utilizzare più volte la finestra di dialogo.  
  
1.  **Controllare la tabella filtrata e selezionare la tabella unita in join**  
  
    -   Se si aggiunge un nuovo join, verificare che la tabella contenuta nella casella di testo **Tabella filtrata** sia corretta. In caso contrario, fare clic su **Annulla**, selezionare la tabella corretta nella pagina **Filtro righe tabella** e quindi fare clic su **Aggiungi join** per tornare a questa finestra di dialogo. Selezionare quindi una tabella nell'elenco a discesa **Tabella unita in join** .  
  
    -   Se si modifica un join esistente, i nomi delle tabelle saranno già specificati e non potranno essere modificati. Per modificare le tabelle specificate nel join è necessario eliminare il filtro join esistente nella pagina **Filtro righe tabella** e creare un nuovo join tra tabelle diverse.  
  
2.  **Creare l'istruzione per il join**  
  
    -   Se si aggiunge un nuovo join, selezionare l'opzione **Per creare l'istruzione verrà utilizzato il generatore** o l'opzione **L'istruzione per il join verrà scritta manualmente**. Se si inizia a scrivere manualmente il join non è possibile utilizzare il generatore.  
  
         Se si sceglie di utilizzare il generatore, utilizzare le colonne della griglia, ovvero**Congiunzione**, **Colonna tabella filtrata**, **Operatore**e **Colonna tabella unita in join**, per compilare un'istruzione per il join. Ogni colonna della griglia contiene un elenco a discesa che consente di selezionare due colonne e un operatore, ovvero**=**, **<>**, **<=**, **\<**, **>=**, **>**, **like**. I risultati vengono visualizzati nell'area di testo **Anteprima** . Se il join include più di una coppia di colonne, selezionare una congiunzione, ovvero**AND** o **OR**, nella colonna **Congiunzione** e quindi digitare altre due colonne e un altro operatore.  
  
         Se si sceglie di scrivere manualmente l'istruzione per il join, digitarla nell'area di testo **Istruzione per il join** . Utilizzare le caselle di riepilogo **Colonne tabella filtrata** e **Colonne tabella unita in join** per trascinare le colonne selezionate nell'area di testo **Istruzione per il join** .  
  
    -   Se si modifica un join esistente è necessario apportare manualmente le modifiche.  
  
3.  **Specificare le opzioni del join**  
  
    -   Se la colonna che si unisce in join alla tabella filtrata è univoca, selezionare **Chiave univoca**. Se la colonna è univoca, per il processo di merge sono disponibili speciali procedure di ottimizzazione delle prestazioni.  
  
        > [!CAUTION]  
        >  Selezionando questa opzione si indica che la relazione tra la tabella padre e le tabelle figlio in un filtro join è uno-a-uno o uno-a-molti. Selezionare questa opzione solo se la colonna unita in join nella tabella padre contiene un vincolo che garantisce l'unicità. Se l'opzione è impostata in modo errato può impedire la convergenza dei dati.  
  
    -   Solo[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive. Per impostazione predefinita, durante la sincronizzazione la replica di tipo merge elabora le modifiche riga per riga. Per fare in modo che le modifiche correlate vengano elaborate come singola unità, selezionare l'opzione **Record logico**. Questa opzione è disponibile solo se sono soddisfatti i requisiti relativi all'utilizzo dei record logici negli articoli e nelle pubblicazioni. Per altre informazioni vedere la sezione "Considerazioni sull'utilizzo di record logici" in [Raggruppare modifiche alle righe correlate con record logici](merge/group-changes-to-related-rows-with-logical-records.md).  
  
 Dopo aver aggiunto o modificato un filtro, fare clic su **OK** per salvare le modifiche e chiudere la finestra di dialogo. Il filtro specificato viene analizzato ed eseguito sulla tabella nella clausola SELECT. Se nell'istruzione di filtro sono presenti errori di sintassi o di altro tipo, verrà visualizzato un apposito messaggio di notifica e sarà possibile modificare l'istruzione.  
  
## <a name="see-also"></a>Vedere anche  
 [Create a Publication](publish/create-a-publication.md)   
 [Visualizzare e modificare le proprietà della pubblicazione](publish/view-and-modify-publication-properties.md)   
 [Filtrare i dati pubblicati](publish/filter-published-data.md)   
 [Join Filters](merge/join-filters.md)   
 [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md)   
 [Pubblicare dati e oggetti di database](publish/publish-data-and-database-objects.md)  
  
  
