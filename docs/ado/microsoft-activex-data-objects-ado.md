---
title: Microsoft ActiveX Data Objects (ADO) | Microsoft Docs
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ADO, about
ms.assetid: 2fa6237b-44b8-4b6c-9952-5acd80a54e20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0994c4ee4c96e5ed9c373ec4bdc94b02ccddff7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63156265"
---
# <a name="microsoft-activex-data-objects-ado"></a>Microsoft ActiveX Data Objects (ADO)

ADO viene utilizzato nei programmi C++ per connettersi a SQL Server. Naturalmente, funziona anche per connettersi al Database SQL di Azure nel cloud.

In ogni sezione di questo articolo descrive un componente di ADO.

> [!NOTE]
> ADO.NET è diverso da quello di ADO. ADO.NET e molti altri driver di connessione SQL e delle lingue, vengono illustrate partire [driver di SQL Server](../connect/sql-connection-libraries.md).

  
## <a name="ado"></a>ADO  
 Microsoft ActiveX Data Objects (ADO) consentono alle applicazioni client accedere e modificare i dati da svariate origini tramite un provider OLE DB. Due vantaggi principali sono la facilità d'uso, ad alta velocità, il sovraccarico di memoria insufficiente e un footprint del disco di piccole dimensioni. ADO supporta le funzionalità principali per la compilazione di applicazioni basate su Web e client/server.  
  
## <a name="ado-md"></a>ADO MD  
 Microsoft ActiveX Data Objects (multidimensionale) (ADO MD) consente di accedere facilmente ai dati multidimensionali da linguaggi, ad esempio Microsoft Visual Basic e Microsoft Visual C++. ADO MD estende Microsoft ActiveX Data Objects (ADO) per includere gli oggetti specifici di dati multidimensionali, ad esempio gli oggetti di CubeDef e set di celle. Con ADO MD si può esplorare schema multidimensionale, un cubo di query e recuperare i risultati.  
  
 Ad esempio ADO, ADO MD Usa un provider OLE DB sottostante per ottenere l'accesso ai dati. Per lavorare con ADO MD, il provider deve essere un provider di dati multidimensionali (dati Multidimensionali) come definito dalla specifica OLE DB per OLAP. I provider di dati multidimensionali presentano i dati in visualizzazioni multidimensionali, anziché il provider di dati tabulare (TDP) che presentano i dati nelle visualizzazioni tabulari. Vedere la documentazione per il provider OLE DB OLAP per informazioni più dettagliate sulla sintassi specifica e i comportamenti supportati dal provider.  
  
## <a name="rds"></a>RDS  
 Servizio dati remoto (RDS) è una funzionalità di ADO, con cui è possibile spostare dati da un server a un'applicazione client o una pagina Web, modificare i dati nel client e restituire gli aggiornamenti al server in un unico round trip.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="adox"></a>ADOX  
 Microsoft ActiveX Data Objects Extensions per Data Definition Language and Security (ADOX) è un'estensione per gli oggetti ADO e di un modello di programmazione. ADOX include gli oggetti per la creazione di schemi e modifica, nonché protezione. Poiché si tratta di un approccio basato su oggetti per modificare lo schema, è possibile scrivere codice che funzionerà con i dati di varie origini indipendentemente dalle differenze nelle loro sintassi native.  
  
 ADOX è una libreria complementare agli oggetti principali ADO. Espone gli oggetti aggiuntivi per la creazione, modifica ed eliminazione di oggetti dello schema, ad esempio tabelle e procedure. Include anche gli oggetti di sicurezza per gestire utenti e gruppi e concedendo e revocando permessi di autorizzazioni per gli oggetti.  
  
## <a name="documentation"></a>Documentazione  
 [Problemi di progettazione della sicurezza ADO](../ado/guide/ado-security-design-issues.md)  
  
 [Manuale del programmatore di ADO](../ado/guide/ado-programmer-s-guide.md)  
  
 Introduzione all'uso di ADO, servizi desktop remoto, ADO MD e ADOX.  
  
 [Guida di riferimento per programmatori ADO](../ado/reference/ado-programmer-s-reference.md)  
  
 Questa sezione della documentazione ADO contiene argomenti per ogni ADO, servizi desktop remoto, ADO MD, ADOX oggetto, insieme, proprietà, proprietà dinamica, metodo, eventi e dell'enumerazione.  
  
 [Glossario ADO](../ado/ado-glossary.md)  
  
## <a name="support"></a>Supporto  
 Gratuitamente per risolvere problemi di ADO, ripetere la registrazione al newsgroup pubblico ADO. Questo newsgroup viene monitorato da professionisti del supporto tecnico Microsoft (tecnico) che coprono ADO e da altri esperti sviluppatori ADO.  
  
 Altre informazioni sulle opzioni di supporto sono reperibile sul sito Web supporto tecnico e Microsoft Help.


