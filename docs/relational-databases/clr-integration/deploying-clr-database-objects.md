---
title: Distribuzione di oggetti di database CLR | Microsoft Docs
description: Utilizzando Microsoft Visual Studio, è possibile sviluppare oggetti di database CLR per SQL Server, distribuirli in un server di prova e distribuirli ai server di produzione.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- deployment script [CLR integration]
- common language runtime [SQL Server], deploying
- deploying assemblies [CLR integration]
- deploying [CLR integration]
ms.assetid: 00752573-3367-41a7-af98-7b7a29e8e2f2
author: rothja
ms.author: jroth
ms.openlocfilehash: 26253e3a19b31dce94249a09dcf7cee71fbffeeb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81488210"
---
# <a name="deploying-clr-database-objects"></a>Distribuzione di oggetti di database CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La distribuzione rappresenta il processo tramite il quale si mette a disposizione un'applicazione o un modulo pronto per l'utilizzo perché venga installato ed eseguito in altri computer. L'uso di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio consente di sviluppare oggetti di database CLR (Common Language Runtime) e di distribuirli a un server di prova. In alternativa, è possibile compilare gli oggetti di database gestiti con i file di ridistribuzione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework. Una volta compilati, gli assembly contenenti gli oggetti di database CLR possono essere distribuiti a un server di prova utilizzando Visual Studio o le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)]. Notare che Visual Studio .NET 2003 non può essere utilizzato per la programmazione o la distribuzione dell'integrazione CLR. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene fornito con .NET Framework preinstallato e non è possibile utilizzare assembly di .NET Framework 2.0 in Visual Studio .NET 2003.  
  
 Dopo aver testato e verificato i metodi CLR sul server di prova, sarà possibile distribuirli a server di produzione utilizzando uno script di distribuzione che può essere generato manualmente o tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (vedere la procedura riportata più avanti in questo argomento).  
  
 La caratteristica di integrazione con CLR è disattivata per impostazione predefinita in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e deve essere abilitata per utilizzare gli assembly CLR. Per altre informazioni, vedere [Enabling CLR Integration](../../relational-databases/clr-integration/clr-integration-enabling.md).  
  
## <a name="deploying-the-assembly-to-the-test-server"></a>Distribuzione dell'assembly a un server di prova  
 Visual Studio consente di sviluppare aggregazioni definite dall'utente, tipi definiti dall'utente, trigger, procedure e funzioni CLR, nonché di distribuirli a un server di prova. Questi oggetti di database gestiti possono essere compilati anche con i compilatori della riga di comando, ad esempio csc.exe e vbc.exe, inclusi nei file di ridistribuzione di .NET Framework. Per sviluppare oggetti di database gestiti per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è necessario l'ambiente di sviluppo integrato (IDE, Integrated Development Environment) di Visual Studio.  
  
 Verificare che tutti gli avvisi e gli errori del compilatore siano risolti. Gli assembly contenenti le routine CLR possono essere quindi registrati in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando Visual Studio o le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
> [!NOTE]  
>  È necessario abilitare il protocollo di rete TCP/IP nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per utilizzare [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio per lo sviluppo e il debug remoti. Per ulteriori informazioni sull'abilitazione del protocollo TCP/IP nel server, vedere [configure client Protocols](../../database-engine/configure-windows/configure-client-protocols.md).  
  
#### <a name="to-deploy-the-assembly-using-visual-studio"></a>Per distribuire l'assembly utilizzando Visual Studio  
  
1.  Compilare il progetto selezionando **Compila** \<nome progetto> dal menu **Compila** .  
  
2.  Risolvere tutti gli avvisi e gli errori di compilazione prima di distribuire l'assembly al server di prova.  
  
3.  Scegliere **Distribuisci** dal menu **Compila** . L'assembly verrà quindi registrato nel database e nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] specificati quando il progetto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è stato creato per la prima volta in Visual Studio.  

#### <a name="to-deploy-the-assembly-using-transact-sql"></a>Per distribuire l'assembly utilizzando Transact-SQL  
  
1.  Compilare l'assembly dal file di origine utilizzando i compilatori della riga di comando inclusi in .NET Framework.  
  
2.  Per i file di origine di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#:  
  
3.  `csc /target:library C:\helloworld.cs`  
  
4.  Per i file di origine di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic:  
  
 `vbc /target:library C:\helloworld.vb`  
  
 Questi comandi avviano il compilatore Visual C# o Visual Basic usando l'opzione **/target** per specificare la compilazione di una dll della libreria.  
  
1.  Risolvere tutti gli avvisi e gli errori di compilazione prima di distribuire l'assembly al server di prova.  
  
2.  Aprire [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] sul server di prova. Creare una nuova query, connessa a un database di prova appropriato (ad esempio AdventureWorks).  
  
3.  Creare l'assembly nel server aggiungendo alla query l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente.  
  
 `CREATE ASSEMBLY HelloWorld from 'c:\helloworld.dll' WITH PERMISSION_SET = SAFE;`  
  
1.  La procedura, la funzione, l'aggregazione, il tipo definito dall'utente o il trigger deve essere quindi creato nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se l'assembly **HelloWorld** contiene un metodo denominato **HelloWorld** nella classe **Procedures** , è possibile aggiungere [!INCLUDE[tsql](../../includes/tsql-md.md)] alla query quanto segue per creare una routine denominata **Hello** in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 `CREATE PROCEDURE hello`  
  
 `AS`  
  
 `EXTERNAL NAME HelloWorld.Procedures.HelloWorld`  
  
 Per ulteriori informazioni sulla creazione di diversi tipi di oggetti di database gestiti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]in, [vedere funzioni CLR definite](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)dall'utente, [aggregazioni CLR definite](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)dall'utente, [tipi CLR definiti dall'](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)utente, [stored procedure CLR](https://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)e [trigger CLR](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c).  
  
## <a name="deploying-the-assembly-to-production-servers"></a>Distribuzione dell'assembly a server di produzione  
 Dopo aver testato e verificato gli oggetti di database CLR sul server di prova, sarà possibile distribuirli a server di produzione. Per ulteriori informazioni sul debug di oggetti di database gestiti, vedere [debug di oggetti di database CLR](../../relational-databases/clr-integration/debugging-clr-database-objects.md).  
  
 La distribuzione degli oggetti di database gestiti è simile a quella degli oggetti di database normali, quali tabelle, routine [!INCLUDE[tsql](../../includes/tsql-md.md)] e così via. Gli assembly che contengono gli oggetti di database CLR possono essere distribuiti agli altri server utilizzando uno script di distribuzione. Lo script di distribuzione può essere compilato utilizzando la funzionalità "Genera script" di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Tale script può essere anche compilato manualmente o utilizzando "Genera script" e modificato manualmente. Una volta compilato, può essere eseguito in altre istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per distribuire gli oggetti di database gestiti.  
  
#### <a name="to-generate-a-deployment-script-using-generate-scripts"></a>Per generare uno script di distribuzione utilizzando la funzione Genera script  
  
1.  Aprire [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui è stato registrato l'oggetto di database o l'assembly gestito da distribuire.  
  
2.  Nella **Esplora oggetti**espandere il nome del ** \<server>** e gli alberi dei **database** . Fare clic con il pulsante destro del mouse sul database in cui è registrato l'oggetto di database gestito, selezionare **attività**, quindi selezionare **Genera script**. Verrà avviata la Generazione guidata script.  
  
3.  Selezionare il database nella casella di riepilogo e fare clic su **Avanti**.  
  
4.  Nel riquadro **Scegli opzioni script** fare clic su **Avanti**oppure modificare le opzioni e quindi fare clic su **Avanti**.  
  
5.  Nel riquadro **Selezione tipi di oggetti** scegliere il tipo di oggetto di database da distribuire. Fare clic su **Avanti**.  
  
6.  Per ogni tipo di oggetto selezionato nel riquadro **Selezione tipi di oggetti** , viene visualizzato un riquadro ** \<Scegli tipo>** . In questo riquadro è possibile scegliere tra tutte le istanze del tipo di oggetto di database registrato nel database specificato. Selezionare uno o più oggetti, quindi fare clic su **Avanti**.  
  
7.  Il riquadro **Opzioni di output** viene visualizzato quando tutti i tipi di oggetto di database desiderati sono stati selezionati. Selezionare **script nel file** e specificare un percorso di file per lo script. Selezionare **Avanti**. Verificare le selezioni e fare clic su **fine**. Lo script di distribuzione verrà salvato nel percorso di file specificato.  
  
## <a name="post-deployment-scripts"></a>Script post-distribuzione  
 È possibile eseguire uno script post-distribuzione.  
  
 Per aggiungere uno script post-distribuzione, inserire un file denominato postdeployscript.sql nella directory del progetto di Visual Studio. Ad esempio, fare clic con il pulsante destro del mouse sul progetto in **Esplora soluzioni** e scegliere **Aggiungi elemento esistente**. Aggiungere il file alla radice del progetto, anziché alla cartella Test Scripts.  
  
 Fare clic su Distribuisci. In questo modo lo script verrà eseguito in Visual Studio dopo la distribuzione del progetto.  
  
## <a name="see-also"></a>Vedere anche  
 [Concetti relativi alla programmazione dell'integrazione con CLR &#40;Common Language Runtime&#41;](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
