---
title: Registrazione nel componente script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], logging
ms.assetid: 17c19787-379e-43fe-9107-e36e17ecda53
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f44ec46f61e215fabe5c4ae2af78d898d7e35c64
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53356955"
---
# <a name="logging-in-the-script-component"></a>Registrazione del componente script
  La registrazione nei pacchetti di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] consente di salvare informazioni dettagliate su stato di esecuzione, risultati e problemi, tramite la registrazione di eventi predefiniti o di messaggi definiti dall'utente da analizzare in un secondo momento. Il componente script può utilizzare il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> della classe `ScriptMain` per registrare dati definiti dall'utente. Se la registrazione è abilitata e l'evento **ScriptComponentLogEntry** è selezionato per la registrazione nella scheda **Dettagli** della finestra di dialogo **Configura log SSIS**, una singola chiamata al metodo <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> archivia le informazioni dell'evento in tutti i provider di log configurati per l'attività Flusso di dati.  
  
 Di seguito è riportato un semplice esempio di registrazione:  
  
 `Dim bt(0) As Byte`  
  
 `Me.Log("Test Log Event", _`  
  
 `0, _`  
  
 `bt)`  
  
> [!NOTE]  
>  Anche se è possibile eseguire direttamente la registrazione dal componente script, è consigliabile implementare eventi anziché registrare. Quando si utilizzano gli eventi, oltre ad abilitare la registrazione dei messaggi di eventi, è anche possibile rispondere all'evento con gestori eventi predefiniti o definiti dall'utente.  
  
 Per altre informazioni sulla registrazione, vedere [Registrazione di Integration Services &#40;SSIS&#41;](../../performance/integration-services-ssis-logging.md).  
  
![Icona di Integration Services (piccola)](../../media/dts-16.gif "icona di Integration Services (piccola)")**rimangono fino a Date con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visita la pagina di Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [Registrazione di Integration Services &#40;SSIS&#41;](../../performance/integration-services-ssis-logging.md)  
  
  
