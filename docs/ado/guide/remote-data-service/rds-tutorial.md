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
author: rothja
ms.author: jroth
ms.openlocfilehash: f646bd95e3ae9cb809f04c2ef66c47386fbde6c6
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762982"
---
# <a name="rds-tutorial"></a>Esercitazione su RDS
In questa esercitazione viene illustrato l'utilizzo del modello di programmazione RDS per eseguire query e aggiornare un'origine dati. In primo luogo, vengono descritti i passaggi necessari per eseguire questa attività. L'esercitazione viene quindi ripetuta in Microsoft® Visual Basic Scripting Edition (con ADO for Windows Foundation Classes (ADO/WFC)).  
  
 Questa esercitazione è codificata in lingue diverse per due motivi:  
  
-   La documentazione per Servizi Desktop remoto presuppone i codici Reader in Visual Basic. In questo modo la documentazione risulta utile per i programmatori Visual Basic, ma meno utile per i programmatori che utilizzano altri linguaggi.  
  
-   Se non si è certi di una particolare funzionalità di Servizi Desktop remoto e si conosce un'altra lingua, si potrebbe essere in grado di risolvere la domanda cercando la stessa funzionalità espressa in un'altra lingua.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="how-the-tutorial-is-presented"></a>Presentazione dell'esercitazione  
 Questa esercitazione è basata sul modello di programmazione RDS. Viene illustrato ogni singolo passaggio del modello di programmazione. Viene inoltre illustrato ogni passaggio con un frammento di codice Visual Basic.  
  
 L'esempio di codice viene ripetuto in altri linguaggi con una discussione minima. Ogni passaggio di un'esercitazione specifica del linguaggio di programmazione è contrassegnato con il passaggio corrispondente nel modello di programmazione e nell'esercitazione descrittiva. Usare il numero del passaggio per fare riferimento alla discussione nell'esercitazione descrittiva.  
  
 Il modello di programmazione RDS è indicato nella sezione seguente. Usarlo come roadmap mentre si procede con l'esercitazione.  
  
## <a name="rds-programming-model-with-objects"></a>Modello di programmazione RDS con oggetti  
  
-   Specificare il programma da richiamare sul server e ottenere un metodo (proxy) per farvi riferimento dal client.  
  
-   Richiamare il programma server. Passare i parametri al programma server che identifica l'origine dati e il comando da emettere.  
  
-   Il programma server ottiene un oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) dall'origine dati, in genere tramite ADO. Facoltativamente, l'oggetto **Recordset** viene elaborato nel server.  
  
-   Il programma server restituisce l'oggetto **Recordset** finale all'applicazione client.  
  
-   Nel client, l'oggetto **Recordset** viene inserito facoltativamente in un modulo che può essere facilmente utilizzato dai controlli visivi.  
  
-   Le modifiche apportate all'oggetto **Recordset** vengono restituite al server e utilizzate per aggiornare l'origine dati.  
  
 Questa esercitazione contiene gli argomenti seguenti.  
  
-   [Passaggio 1: Specificare un programma del server (esercitazione su RDS)](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)  
  
-   [Passaggio 2: Richiamare il programma del server (esercitazione su RDS)](../../../ado/guide/remote-data-service/step-2-invoke-the-server-program-rds-tutorial.md)  
  
-   [Passaggio 3: Il server ottiene un recordset (esercitazione su RDS)](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)  
  
-   [Passaggio 4: Il server restituisce il recordset (esercitazione su RDS)](../../../ado/guide/remote-data-service/step-4-server-returns-the-recordset-rds-tutorial.md)  
  
-   [Passaggio 5: L'oggetto DataControl viene reso utilizzabile (esercitazione su RDS)](../../../ado/guide/remote-data-service/step-5-datacontrol-is-made-usable-rds-tutorial.md)  
  
-   [Passaggio 6: Le modifiche vengono inviate al server (esercitazione su RDS)](../../../ado/guide/remote-data-service/step-6-changes-are-sent-to-the-server-rds-tutorial.md)  
  
-   [Esercitazione su RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Passaggio 1: specificare un programma server (esercitazione su RDS)](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)   
 [Esercitazione su RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
