---
title: Esempi di attività Script | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], examples
- examples [Integration Services]
- SSIS Script task, examples
ms.assetid: b0dd77ee-ee11-4cd9-87aa-61dd67f2fe1c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d47fa22b8207facc5b4bc22a4077b8bd81837ec2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62768477"
---
# <a name="script-task-examples"></a>Esempi di attività Script
  L'attività Script è uno strumento multifunzione che è possibile utilizzare in un pacchetto per rispondere ai requisiti non soddisfatti dalle attività incluse in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. In questo argomento sono riportati esempi di codice dell'attività Script che dimostrano alcune delle funzionalità disponibili.  
  
> [!NOTE]  
>  Se si desidera creare attività da riutilizzare più facilmente con più pacchetti, è possibile utilizzare il codice di questi esempi di attività Script come punto iniziale per attività personalizzate. Per altre informazioni, vedere [Sviluppo di un'attività personalizzata](../extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
## <a name="in-this-section"></a>In questa sezione  
  
### <a name="example-topics"></a>Argomenti di esempio  
 Questa sezione contiene esempi di codice che dimostrano i vari utilizzi delle classi di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] che è possibile incorporare in un'attività Script di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:  
  
 [Rilevamento di un file flat vuoto con l'attività Script](../extending-packages-scripting-task-examples/detecting-an-empty-flat-file-with-the-script-task.md)  
 Viene controllato un file flat per determinare se contiene righe di dati, quindi il risultato viene salvato in una variabile da utilizzare nella diramazione del flusso di controllo.  
  
 [Raccolta di un elenco per il ciclo ForEach con l'attività Script](../extending-packages-scripting-task-examples/gathering-a-list-for-the-foreach-loop-with-the-script-task.md)  
 Viene raccolto un elenco di file che soddisfano criteri specificati dall'utente e viene popolata una variabile per un utilizzo successivo da parte dell'enumeratore Foreach da variabile.  
  
 [Esecuzione di query su Active Directory tramite l'attività Script](../extending-packages-scripting-task-examples/querying-the-active-directory-with-the-script-task.md)  
 Vengono recuperate informazioni utente da Active Directory in base al valore di una variabile [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], tramite le classi dello spazio dei nomi System.DirectoryServices.  
  
 [Monitoraggio dei contatori delle prestazioni con l'attività Script](../extending-packages-scripting-task-examples/monitoring-performance-counters-with-the-script-task.md)  
 Viene creato un contatore delle prestazioni personalizzato che può essere usato per registrare lo stato dell'esecuzione di un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], tramite le classi dello spazio dei nomi System.Diagnostics.  
  
 [Utilizzo di immagini con l'attività Script](../extending-packages-scripting-task-examples/working-with-images-with-the-script-task.md)  
 Vengono compresse immagini in formato JPEG e da esse vengono create immagini anteprima, tramite le classi dello spazio dei nomi System.Drawing.  
  
 [Ricerca di stampanti installate con l'attività Script](../extending-packages-scripting-task-examples/finding-installed-printers-with-the-script-task.md)  
 Vengono individuate le stampanti installate che supportano un formato della carta specifico, tramite le classi dello spazio dei nomi System.Drawing.Printing.  
  
 [Invio di un messaggio di posta HTML con l'attività Script](../extending-packages-scripting-task-examples/sending-an-html-mail-message-with-the-script-task.md)  
 Viene inviato un messaggio di posta in formato HTML anziché di testo normale.  
  
 [Utilizzo di file di Excel con l'attività Script](../extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)  
 Vengono elencati i fogli di lavoro di un file di Excel e viene verificata l'esistenza di un foglio di lavoro specifico.  
  
 [Invio di messaggi a una coda privata remota tramite l'attività Script](../extending-packages-scripting-task-examples/sending-to-a-remote-private-message-queue-with-the-script-task.md)  
 Viene inviato un messaggio a una coda privata remota.  
  
### <a name="other-examples"></a>Altri esempi  
 Anche gli argomenti riportati di seguito contengono esempi di codice da utilizzare con l'attività Script:  
  
 [Uso delle variabili nell'attività Script](../extending-packages-scripting/task/using-variables-in-the-script-task.md)  
 Viene chiesta la conferma dell'utente per continuare o meno l'esecuzione del pacchetto, in base al valore di una variabile del pacchetto che potrebbe superare il limite specificato in un'altra variabile.  
  
 [Connessione a origini dati nell'attività Script](../extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md)  
 Vengono recuperate una connessione o le relative informazioni dalle gestioni connessioni definite nel pacchetto.  
  
 [Generazione di eventi nell'attività Script](../extending-packages-scripting/task/raising-events-in-the-script-task.md)  
 Viene generato un errore, un avviso o un messaggio informativo a seconda dello stato della connessione Internet nel server.  
  
 [Registrazione nell'attività Script](../extending-packages-scripting/task/logging-in-the-script-task.md)  
 Viene registrato il numero di elementi elaborati dall'attività nei provider di log abilitati.  
  
![Icona di Integration Services (piccola)](../media/dts-16.gif "icona di Integration Services (piccola)")**rimangono fino a Date con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visita la pagina di Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
  
