---
title: Esercitazione su RDS | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO]
ms.assetid: 6e3305a0-7bc7-40d1-9122-235c15d23ab2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 3d1f328baf628e86c75abc9a452600e1f0e8cf88
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704260"
---
# <a name="rds-tutorial"></a>Esercitazione su RDS
Questa esercitazione viene illustrato l'utilizzo del modello di programmazione di servizi desktop remoto per eseguire query e aggiornare un'origine dati. In primo luogo, la descrive i passaggi necessari per completare questa attività. Quindi l'esercitazione viene ripetuta in Microsoft® Visual Basic Scripting Edition (con ADO per Windows Foundation Classes (ADO/WFC)).  
  
 Questa esercitazione viene codificata in linguaggi diversi per due motivi:  
  
-   La documentazione relativa a Servizi Desktop remoto si presuppone che i codici di lettura in Visual Basic. In questo modo la documentazione utile per i programmatori Visual Basic, ma meno utili per chi utilizza altri linguaggi.  
  
-   Se si è incerti su una determinata funzionalità di servizi desktop remoto e ha una conoscenza minima di un altro linguaggio, potrebbe essere in grado di risolvere la domanda cercando la stessa funzionalità in un altro linguaggio.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="how-the-tutorial-is-presented"></a>La modalità di presentazione dell'esercitazione  
 Questa esercitazione è basata sul modello di programmazione di servizi desktop remoto. Viene descritto ogni passaggio del modello di programmazione singolarmente. Inoltre, viene illustrato ogni passaggio con un frammento di codice Visual Basic.  
  
 L'esempio di codice viene ripetuto in altri linguaggi con discussione minimo. Ogni passaggio in un'esercitazione sul linguaggio di programmazione specificato è contrassegnato con il passaggio corrispondente nel modello di programmazione ed esercitazione descrittivo. Usare il numero del passaggio per fare riferimento alla trattazione nell'esercitazione descrittivo.  
  
 Il modello di programmazione RDS è indicato nella sezione seguente. Usarla come una Guida di orientamento mentre si esegue l'esercitazione.  
  
## <a name="rds-programming-model-with-objects"></a>Modello di programmazione RDS con oggetti  
  
-   Specificare il programma da richiamare sul server e ottenere un modo (proxy) per farvi riferimento dal client.  
  
-   Richiamare il programma del server. Passare parametri all'applicazione server che identifica l'origine dati e il comando da eseguire.  
  
-   L'applicazione server Ottiene un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto dall'origine dati, in genere utilizzando ADO. Facoltativamente, il **Recordset** oggetto viene elaborato nel server.  
  
-   Il programma del server restituisce l'elemento finale **Recordset** oggetto all'applicazione client.  
  
-   Sul client, il **Recordset** oggetto facoltativamente viene inserito in un form che può essere facilmente utilizzato dai controlli visual.  
  
-   Modifiche per il **Recordset** oggetto vengono inviati al server e consente di aggiornare l'origine dati.  
  
 Questa esercitazione contiene gli argomenti seguenti.  
  
-   [Passaggio 1: Specificare un'applicazione Server (esercitazione su RDS)](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)  
  
-   [Passaggio 2: Richiamare il programma di Server (esercitazione su RDS)](../../../ado/guide/remote-data-service/step-2-invoke-the-server-program-rds-tutorial.md)  
  
-   [Passaggio 3: Server otterrà un Recordset (esercitazione su RDS)](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)  
  
-   [Passaggio 4: Server restituisce il Recordset (esercitazione su RDS)](../../../ado/guide/remote-data-service/step-4-server-returns-the-recordset-rds-tutorial.md)  
  
-   [Passaggio 5: L'oggetto DataControl viene reso utilizzabile (esercitazione su RDS)](../../../ado/guide/remote-data-service/step-5-datacontrol-is-made-usable-rds-tutorial.md)  
  
-   [Passaggio 6: Le modifiche vengono inviate al Server (esercitazione su RDS)](../../../ado/guide/remote-data-service/step-6-changes-are-sent-to-the-server-rds-tutorial.md)  
  
-   [Esercitazione su RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Passaggio 1: Specificare un'applicazione Server (esercitazione su RDS)](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)   
 [Esercitazione su RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
