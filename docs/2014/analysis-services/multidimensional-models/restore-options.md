---
title: Opzioni di ripristino | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- databases [Analysis Services], restoring
- restoring databases [Analysis Services]
ms.assetid: 75c73802-f321-4671-afc7-54505d62c013
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a754ac9650c94511e8576a8a05e0b81fb38138a3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66073090"
---
# <a name="restore-options"></a>Opzioni di ripristino
  È possibile eseguire il backup dei database di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in diversi modi e in tutti i casi è necessario disporre delle autorizzazioni di amministratore sia per il computer server che per il database [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Per ripristinare un database [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , è possibile aprire la finestra di dialogo **Ripristina database** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], selezionare le opzioni di configurazione opportune e infine eseguire il ripristino dalla finestra di dialogo. Oppure, è possibile creare uno script utilizzando le impostazioni già specificate nel file; lo script può infine essere salvato per essere eseguito secondo necessità. In questo modo, il ripristino viene completato utilizzando XMLA, come descritto nella sezione seguente.  
  
## <a name="restoring-databases-using-xmla"></a>Ripristino di database tramite XMLA  
 Il comando di ripristino di XMLA consente di automatizzare il processo di ripristino utilizzando un file con estensione abf. Il comando di ripristino prevede un certo numero di proprietà che consentono di specificare definizioni di sicurezza, la posizione di archiviazione delle partizioni remote e lo spostamento di oggetti relazionali OLAP (ROLAP). Per altre informazioni, vedere [Restore Element &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla).  
  
> [!IMPORTANT]  
>  Per ogni file di backup, l'utente che esegue il comando di ripristino deve disporre delle autorizzazioni per leggere dal percorso di backup specificato per ogni file. Per ripristinare un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] non installato nel server, l'utente deve inoltre essere un membro del ruolo del server per l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] specifica. Per sovrascrivere un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , l'utente deve avere uno dei ruoli seguenti: deve essere un membro del ruolo del server per l'istanza [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o un membro di un ruolo del database con autorizzazioni Controllo completo (amministratore) sul database da ripristinare.  
  
> [!NOTE]  
>  Dopo avere ripristinato un database esistente, l'utente che ha effettuato l'operazione potrebbe perdere l'accesso al database ripristinato. Può verificarsi questa perdita di accesso se, al momento dell’esecuzione del backup, l'utente non era un membro del ruolo del server o non era un membro del ruolo del database con autorizzazioni Controllo completo (amministratore).  
  
## <a name="see-also"></a>Vedere anche  
 [Finestra di dialogo Ripristina Database &#40;Analysis Services - Dati multidimensionali&#41;](../restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [Backup e ripristino di database di Analysis Services](backup-and-restore-of-analysis-services-databases.md)   
 [Elemento Restore &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla)   
 [Backup, ripristino e sincronizzazione di database &#40;XMLA&#41;](../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)  
  
  
