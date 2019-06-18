---
title: Aggiunta e rimozione dell'accesso Database file (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases
- adding Access files
- adding and removing Access databases
- browsing Access metadata
- browsing metadata, Access databases
- connecting, Access databases
- databases
- files, adding and removing
- finding Access databases
- finding database files
- locating database files
- metadata
- metadata, browsing
- metadata, refreshing
- refreshing metadata
- removing Access files
- scanning for database files
- searching for database files
ms.assetid: e944c740-4c8a-4bc1-b0ed-be57bc06dced
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 8de9b27a58d277191a4d40da6b34dbcbbd43e497
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62760614"
---
# <a name="adding-and-removing-access-database-files-accesstosql"></a>Aggiunta e rimozione di file di Database di Access (AccessToSQL)
Per eseguire la migrazione di dati Access [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, è necessario aggiungere uno o più database di Access al progetto SSMA. Questi database devono essere Access 97 o versioni successive. Se sono presenti database da una versione precedente di accesso, è necessario convertire i database in una versione più recente. Eseguire questa operazione aprendo e salvando i database di Access 97 o versione successiva prima di aggiungerli a SSMA.  
  
## <a name="what-happens-when-you-add-access-database-files"></a>Cosa accade quando si aggiungono file di Database di Access?  
Quando si aggiunge un database di Access in un progetto SSMA, SSMA legge i metadati del database e quindi aggiunge i metadati del file di progetto. Questi metadati vengono descritti i database e i relativi oggetti. SSMA utilizza i metadati durante la conversione di oggetti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o la sintassi SQL Azure, e quando esegue la migrazione di dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. È possibile esplorare i metadati nel Visualizzatore metadati di accesso e le proprietà di singoli oggetti di database.  
  
> [!NOTE]  
> Un database di Access può essere suddivisa in più file: un database back-end che contiene le tabelle e i database front-end contenenti query, form, i report, le macro, moduli e tasti di scelta rapida. Se si vuole eseguire la migrazione di un database di split a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, aggiungere i database front-end in SSMA.  
  
## <a name="permissions-that-are-required-by-ssma"></a>Autorizzazioni necessarie per SSMA  
Eseguire la migrazione di un database di Access per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, il gruppo di utenti e l'utente amministratore deve disporre delle autorizzazioni Administer. Per informazioni su come eseguire la migrazione di database con gruppi di lavoro protezione, vedere [preparare i database di Access per la migrazione](preparing-access-databases-for-migration-accesstosql.md).  
  
## <a name="selecting-databases-to-add"></a>Selezionare i database da aggiungere  
Se si desidera aggiungere uno o più database a un progetto SSMA e i file vengono salvate in un percorso noto, è possibile aggiungere i file usando la procedura seguente.  
  
**Per aggiungere singoli file di database**  
  
1.  Nel **File** menu, fare clic su **aggiungere database**.  
  
2.  Nel **aperto** dialogo casella, individuare la cartella che contiene i file di database.  
  
3.  Selezionare i file che si desidera aggiungere e quindi fare clic su **aperto**.  
  
## <a name="finding-databases-to-add"></a>Individuazione database per aggiungere  
Se si desidera aggiungere più database di Access da cartelle diverse a un progetto SSMA o si desidera aggiungere un singolo file, ma è necessario trovare il file, è possibile seguire questi passaggi per individuare uno o più file e aggiungerli al progetto.  
  
**Per trovare e aggiungere i database**  
  
1.  Nel **File** menu, fare clic su **trovare database**.  
  
2.  In Creazione guidata database di ricerca, immettere il nome di unità, percorso del file o percorso UNC che si desidera cercare. In alternativa, fare clic su **esplorare** per individuare la cartella di rete o unità.  
  
3.  Fare clic su **Add** per aggiungere il percorso all'elenco.  
  
    Ripetere i due passaggi precedenti per aggiungere più percorsi di ricerca.  
  
4.  Facoltativamente, aggiungere criteri di ricerca per restringere l'elenco di database che vengono restituiti.  
  
    > [!IMPORTANT]  
    > Il **tutto o parte del nome del file** casella di testo non supporta caratteri jolly.  
  
5.  Fare clic su **Scan**.  
  
    Viene visualizzata la pagina di analisi. Vengono visualizzati i database che sono stati trovati e lo stato di avanzamento della ricerca. Per arrestare la ricerca, fare clic su **arrestare**.  
  
6.  Nella pagina Seleziona file, selezionare i database che si desidera aggiungere al progetto.  
  
    È possibile usare la **Seleziona tutto** e **Clear All** pulsanti nella parte superiore dell'elenco per selezionare o deselezionare tutti i database. È possibile tenere premuto il tasto CTRL per selezionare più database o tenere premuto il tasto MAIUSC basso per selezionare un intervallo di database.  
  
7.  Scegliere **Avanti**.  
  
8.  Nella pagina di verifica, fare clic su **fine**.  
  
## <a name="browsing-access-metadata"></a>Esplorazione dei metadati di accesso  
Dopo aver aggiunto un database di Access a un progetto, i metadati del progetto viene visualizzato nel Visualizzatore metadati di accesso. È possibile esplorare la gerarchia dei database e oggetti di database in Esplora risorse.  
  
**Per esplorare i metadati**  
  
1.  Nel Visualizzatore metadati di accesso, espandere **accesso metabase**, quindi espandere **database**.  
  
2.  Espandere il database che si desidera esaminare e quindi espandere **query**.  
  
    Si noti che l'elenco delle query. Se si seleziona una query, un **SQL** scheda e un **proprietà** scheda vengono visualizzate nel riquadro di destra.  
  
3.  Espandere **tabelle** e quindi selezionare una tabella.  
  
    Si noti che vengono visualizzati quattro schede: **Nella tabella**, **Mapping dei tipi**, **delle proprietà**, e **dati**.  
  
4.  Espandere una tabella, quindi **chiavi**e quindi selezionare una chiave.  
  
    Nel riquadro di destra vengono visualizzate le proprietà della chiave.  
  
5.  Espandere **indici**e quindi selezionare un indice.  
  
    Le proprietà di indice verranno visualizzate nel riquadro di destra.  
  
## <a name="refreshing-databases"></a>Aggiornamento dei database  
Se un database di Access viene modificato dopo aver aggiunto il file, è possibile aggiornare i metadati dal database di Access.  
  
**Per aggiornare i metadati di accesso**  
  
-   Nel Visualizzatore metadati di accesso, il database e quindi scegliere **aggiornare dal Database**.  
  
## <a name="removing-databases"></a>Rimozione di database  
È possibile rimuovere un database di Access da un progetto seguendo questa procedura.  
  
**Per rimuovere un database da un progetto**  
  
1.  Nel Visualizzatore metadati di accesso, espandere **accesso metabase**, quindi espandere **database**.  
  
2.  Il database e quindi scegliere **Rimuovi Database**.  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo del processo di migrazione consiste [connettersi a SQL Server](https://msdn.microsoft.com/bb8c4bde-cfc2-4636-92ae-5dd24abe9536).  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione dei database di Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Creazione e gestione di progetti](creating-and-managing-projects-accesstosql.md)  
  
