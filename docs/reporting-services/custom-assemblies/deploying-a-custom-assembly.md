---
title: Distribuzione di un assembly personalizzato | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-assemblies
ms.topic: reference
helpviewer_keywords:
- deploying custom assemblies [Reporting Services]
- custom assemblies [Reporting Services], deploying
- custom assemblies [Reporting Services], updating
- updating custom assemblies
ms.assetid: c6674cd8-0de7-4a5a-9e7c-12ffa49f6fd2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: bc0b052bd2d932a54a1a857c7aebfe770395c556
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63194936"
---
# <a name="deploying-a-custom-assembly"></a>Distribuzione di un assembly personalizzato
  Per distribuire un assembly personalizzato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], inserire l'assembly nelle cartelle dell'applicazione sia di Progettazione report che del server di report. Per impostazione predefinita, agli assembly personalizzati viene concessa l'autorizzazione **Execution** in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Per concedere agli assembly personalizzati altri privilegi oltre all'autorizzazione Execution, è necessario modificare il file di configurazione rssrvpolicy.config per il server di report e il file di configurazione rspreviewpolicy.config per la finestra di anteprima di Progettazione report. In alternativa, è possibile installare l'assembly personalizzato nella Global Assembly Cache (GAC).  
  
> [!NOTE]  
>  In Progettazione report sono disponibili due modalità di anteprima, vale a dire la scheda Anteprima e la finestra popup di anteprima visualizzata quando il progetto report viene avviato in modalità **DebugLocal**. Nella scheda Anteprima vengono eseguite tutte le espressioni del report usando il set di autorizzazioni **FullTrust** e non vengono applicate le impostazioni dei criteri di sicurezza. La finestra di anteprima popup consente di simulare le funzionalità del server di report e pertanto dispone di un file di configurazione dei criteri che l'utente o un amministratore deve modificare per utilizzare gli assembly personalizzati in Progettazione report. In questa anteprima popup l'assembly personalizzato viene inoltre bloccato. Per modificare o aggiornare il codice dell'assembly personalizzato è pertanto necessario chiudere la finestra di anteprima.  
  
###### <a name="to-deploy-a-custom-assembly-in-reporting-services"></a>Per distribuire un assembly personalizzato in Reporting Services  
  
1.  Copiare l'assembly personalizzato dal percorso di compilazione alla cartella bin del server di report o alla cartella di Progettazione report. Il percorso predefinito della cartella bin del server di report è %Programmi%\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer\bin. Il percorso predefinito di Progettazione report è %Programmi%\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies.  
  
     L'inserimento dell'assembly personalizzato nella cartella bin del server di report consente di pubblicare report che fanno riferimento all'assembly personalizzato, mentre l'inserimento di quest'ultimo nella cartella Progettazione report consente di eseguire i report che fanno riferimento all'assembly personalizzato in Progettazione report ed eseguirne il debug.  
  
     Se è necessario concedere al codice dell'assembly personalizzato autorizzazioni in aggiunta a quelle di esecuzione predefinite, effettuare le operazioni seguenti:  
  
2.  Aprire il file di configurazione appropriato. Il percorso predefinito del file rssrvpolicy.config è %Programmi%Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer. Il percorso predefinito del file rspreviewpolicy.config è %Programmi%\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies.  
  
3.  Aggiungere un gruppo di codice per l'assembly personalizzato. Per altre informazioni vedere [Sviluppo sicuro &#40;Reporting Services&#41;](../../reporting-services/extensions/secure-development/secure-development-reporting-services.md).  
  
## <a name="updating-custom-assemblies"></a>Aggiornamento di assembly personalizzati  
 A un certo punto, potrebbe essere necessario aggiornare una versione di un assembly personalizzato al quale fanno attualmente riferimento diversi report pubblicati. Se tale assembly è già presente nella directory bin del server di report o in Progettazione report e il numero di versione dell'assembly viene incrementato o modificato in altro modo, i report attualmente pubblicati non funzioneranno più correttamente. È necessario aggiornare la versione dell'assembly a cui viene fatto riferimento nell'elemento **CodeModules** della definizione del report e ripubblicare i report. Se si sa che un assembly personalizzato verrà aggiornato di frequente e i report attualmente pubblicati devono fare riferimento al nuovo assembly, è possibile prendere in considerazione l'utilizzo dello stesso numero di versione per tutti gli aggiornamenti di un assembly specifico.  
  
 Se non è necessario che i report attualmente pubblicati facciano riferimento alla nuova versione dell'assembly, è possibile distribuire l'assembly personalizzato nella Global Assembly Cache. La Global Assembly Cache è in grado di gestire più versioni dello stesso assembly, in modo che i report correnti possano fare riferimento alla versione precedente dell'assembly e i nuovi report pubblicati possano fare riferimento all'assembly aggiornato. Un'altra possibilità consiste nell'impostare il reindirizzamento dell'associazione del server di report in modo da forzare un reindirizzamento di tutte le richieste per il vecchio assembly al nuovo assembly. In questo caso, sarebbe necessario modificare il file Web.config e il file ReportService.exe.config del server di report. Il codice può essere simile al seguente:  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="myAssembly"  
                              publicKeyToken="32ab4ba45e0a69a1"  
                              culture="neutral" />  
            <bindingRedirect oldVersion="1.0.0.0"  
                             newVersion="2.0.0.0"/>  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo di assembly personalizzati con i report](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)   
 [Uso di assembly e della Global Assembly Cache](https://go.microsoft.com/fwlink/?LinkId=63912)  
  
  
