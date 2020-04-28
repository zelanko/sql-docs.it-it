---
title: Riferimenti ad altri assembly nelle soluzioni di scripting | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- SSIS Script task, .NET Framework
- Script task [Integration Services], adding references
- referencing custom assemblies
- SSIS Script task, VisualBasic namespace
- assemblies [Integration Services]
- VisualBasic namespace
- Script task [Integration Services], VisualBasic namespace
- Microsoft.VisualBasic namespace
- Script task [Integration Services], .NET Framework
- .NET Framework [Integration Services]
- referencing Web services
ms.assetid: 9b655bcd-19f6-43d8-9f89-1b4d299c6380
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7981bc5ca49ccba465340790789e4a22ce355b51
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "78176160"
---
# <a name="referencing-other-assemblies-in-scripting-solutions"></a>Riferimenti ad altri assembly nelle soluzioni di scripting
  La libreria di classi [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] fornisce allo sviluppatore di script un potente set di strumenti per l'implementazione di funzionalità personalizzate nei pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. L'attività Script e il componente script possono anche utilizzare assembly gestiti personalizzati.

> [!NOTE]
>  Per consentire ai pacchetti di usare gli oggetti e i metodi di un servizio Web, usare il comando **Aggiungi riferimento Web** disponibile in [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA). Nelle versioni precedenti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è necessario generare una classe proxy per utilizzare un servizio Web.

## <a name="using-a-managed-assembly"></a>Utilizzo di un assembly gestito
 Affinché [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] trovi un assembly gestito in fase di progettazione, è necessario effettuare i passaggi seguenti:

1.  Archiviare l'assembly gestito in qualsiasi cartella del computer.

    > [!NOTE]
    >  Nelle versioni precedenti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è possibile aggiungere solo un riferimento a un assembly gestito archiviato nella cartella %windir%\Microsoft.NET\Framework\vx.x.xxxxx o nella cartella %Programmi%\Microsoft SQL Server\100\SDK\Assemblies.

2.  Aggiungere un riferimento all'assembly gestito.

     Per aggiungere il riferimento, nella scheda **Sfoglia** della finestra di dialogo **Aggiungi riferimento** in VSTA individuare e aggiungere l'assembly gestito.

 Affinché [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] trovi l'assembly gestito in fase di esecuzione, è necessario effettuare i passaggi seguenti:

1.  Firmare l'assembly gestito con un nome sicuro.

2.  Installare l'assembly nella Global Assembly Cache nel computer in cui viene eseguito il pacchetto.

     Per altre informazioni, vedere [Compilazione, distribuzione e debug di oggetti personalizzati](../extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md).

## <a name="using-the-microsoft-net-framework-class-library"></a>Utilizzo della libreria di classi Microsoft .NET Framework
 L'attività Script e il componente script possono trarre vantaggio da tutti gli altri oggetti e funzionalità esposti dalla libreria di classi [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Ad esempio, tramite [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] è possibile recuperare informazioni sull'ambiente e interagire con il computer in cui viene eseguito il pacchetto.

 In questo elenco vengono descritte alcune delle classi [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] utilizzate più di frequente:

-   `System.Data`Contiene l'architettura ADO.NET.

-   `System.IO`Fornisce un'interfaccia per la file system e i flussi.

-   `System.Windows.Forms`Consente la creazione di form.

-   `System.Text.RegularExpressions`Fornisce classi per l'utilizzo di espressioni regolari.

-   `System.Environment`Restituisce informazioni sul computer locale, l'utente corrente e le impostazioni del computer e dell'utente.

-   `System.Net`Fornisce le comunicazioni di rete.

-   `System.DirectoryServices`Espone Active Directory.

-   `System.Drawing`Fornisce librerie di manipolazione delle immagini estese.

-   `System.Threading`Consente la programmazione multithreading.

 Per ulteriori informazioni su [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], consultare MSDN Library.

![Integration Services icona (piccola)](../media/dts-16.gif "Icona di Integration Services (piccola)")  **rimane aggiornata con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visitare la pagina relativa a Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.

## <a name="see-also"></a>Vedere anche
 [Estensione di pacchetti tramite scripting](extending-packages-with-scripting.md)


