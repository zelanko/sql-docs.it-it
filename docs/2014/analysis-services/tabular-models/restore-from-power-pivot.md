---
title: Ripristina da PowerPivot | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql11.asvs.ssmsimbi.RestoreFromPP.f1
ms.assetid: 232ac8ed-77fe-47d8-acd3-59bc2fdfdf48
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f90ea08269e79e57c623af41fc2f0fbc09e2fb42
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66066640"
---
# <a name="restore-from-powerpivot"></a>Ripristina da PowerPivot
  È possibile utilizzare la funzionalità Ripristina da PowerPivot in SQL Server Management Studio per creare un nuovo database modello tabulare in un'istanza di Analysis Services (in esecuzione in modalità tabulare) o eseguire il ripristino in un database esistente da una cartella di lavoro di PowerPivot (con estensione xlsx).  
  
> [!NOTE]  
>  Il modello di progetto Importa da PowerPivot in SQL Server Data Tools offre funzionalità simili. Per altre informazioni, vedere [importare da PowerPivot &#40;modello tabulare di SSAS&#41;](import-from-power-pivot-ssas-tabular.md).  
  
 Quando si utilizza Ripristina da PowerPivot, si tenga in considerazione quanto riportato di seguito:  
  
-   Per poter utilizzare Ripristina da PowerPivot, è necessario aver eseguito l'accesso come membro del ruolo di amministratori del server per l'istanza di Analysis Services.  
  
-   L'account del servizio dell'istanza di Analysis Services deve disporre di autorizzazioni di lettura per il file della cartella di lavoro da cui eseguire il ripristino.  
  
-   Per impostazione predefinita, quando si ripristina un database da PowerPivot, la proprietà Impostazioni di rappresentazione origine dati del database modello tabulare è impostata sul valore predefinito, tramite cui viene specificato l'account del servizio dell'istanza di Analysis Services. Si consiglia di impostare le credenziali di rappresentazione su un account utente di Windows nelle proprietà del database. Per altre informazioni, vedere [Rappresentazione &#40;SSAS tabulare&#41;](impersonation-ssas-tabular.md).  
  
-   I dati nel modello di dati PowerPivot verranno copiati in un nuovo database modello tabulare o in uno esistente nell'istanza di Analysis Services. Se nella cartella di lavoro di PowerPivot sono contenute tabelle collegate, queste verranno ricreate come tabelle senza un'origine dati, simili a tabelle create utilizzando Incolla in nuova tabella.  
  
### <a name="to-restore-from-powerpivot"></a>Per ripristinare da PowerPivot  
  
1.  In SQL Server Management Studio, nell'istanza di Active Directory da ripristinare, fare clic destro **database**, quindi fare clic su **Ripristina da PowerPivot**.  
  
2.  Nel **Ripristina da PowerPivot** nella finestra di dialogo **origine ripristino**, in **file di Backup**, fare clic su **Sfoglia**e quindi selezionare un con estensione ABF o con estensione xslx file per il ripristino.  
  
3.  In **Destinazione ripristino**in **Ripristina database**digitare un nome per un nuovo database o per uno esistente. Se non si specifica un nome, viene utilizzato quello della cartella di lavoro.  
  
4.  In **Percorso di archiviazione**fare clic su **Sfoglia**, quindi selezionare un percorso per l'archiviazione del database.  
  
5.  Nella casella **Opzioni**lasciare **Includi informazioni di sicurezza** selezionato. Quando si esegue il ripristino da una cartella di lavoro di PowerPivot, questa impostazione non è applicabile.  
  
## <a name="see-also"></a>Vedere anche  
 [Database modello tabulare &#40;SSAS tabulare&#41;](tabular-model-databases-ssas-tabular.md)   
 [Importare da PowerPivot &#40;tabulare di SSAS&#41;](import-from-power-pivot-ssas-tabular.md)  
  
  
