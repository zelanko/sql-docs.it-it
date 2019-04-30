---
title: Oggetto DataSpace (Servizi Desktop remoto) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataSpace object [RDS]
ms.assetid: 9194bffa-5bdf-4dff-af86-f7158c23bfa7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d75a5dcd8a09388c031e4e01c8bb8b9c1d62bb80
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63134485"
---
# <a name="dataspace-object-rds"></a>Oggetto DataSpace (Servizi Desktop remoto)
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Crea proxy lato client di oggetti business personalizzata che si trova nel livello intermedio.  
  
 Servizio dati remoto deve proxy degli oggetti business in modo che i componenti lato client possono comunicare con oggetti business che si trova nel livello intermedio. I proxy semplificano la creazione di pacchetti, disassemblaggio e di trasporto (marshalling) dell'applicazione [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) dati attraverso i limiti di processo o al computer.  
  
 Il servizio dati remoto Usa il **Servizi Desktop remoto. DataSpace** dell'oggetto [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) metodo per creare i proxy di oggetti business. Il proxy di oggetti business in modo dinamico viene creato ogni volta che viene creata un'istanza della relativa controparte di oggetti business di livello intermedio. Servizio dati remoto supporta i protocolli seguenti: HTTP, HTTPS (HTTP Secure Socket), DCOM e in-process (componenti client e l'oggetto business si trovano nello stesso computer).  
  
> [!NOTE]
>  Servizi Desktop remoto si comporta in modo "senza stato" quando il **Servizi Desktop remoto. DataSpace** oggetto utilizza il protocollo HTTP o HTTPS. Eventuali informazioni interne su una richiesta client, ovvero vengono eliminati dopo che il server restituisce una risposta.  
  
> [!NOTE]
>  Anche se l'oggetto business sembra esistere per la durata del proxy dell'oggetto business, l'oggetto business è presente effettivamente solo fino a quando non viene inviata una risposta a una richiesta. Quando viene emessa una richiesta (vale a dire, viene richiamato un metodo sull'oggetto business), il proxy consente di aprire una nuova connessione al server e il server crea una nuova istanza dell'oggetto business. Dopo che l'oggetto business risponde alla richiesta, il server distrugge l'oggetto business e chiude la connessione.  
  
> [!NOTE]
>  Questo comportamento significa che è possibile passare i dati da una richiesta a un altro utilizzando una proprietà dell'oggetto business o una variabile. È necessario impiegare un altro meccanismo, ad esempio un file o un argomento del metodo, per rendere persistenti i dati.  
  
 L'ID della classe per il **Servizi Desktop remoto. DataSpace** oggetto è BD96C556-65A3 - 11d 0-983A-00C04FC29E36.  
  
 Il **DataSpace** oggetto è sicuro per lo scripting.  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Proprietà, metodi ed eventi dell'oggetto DataSpace (Servizi Desktop remoto)](../../../ado/reference/rds-api/dataspace-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di oggetto DataSpace e metodo CreateObject (VBScript)](../../../ado/reference/rds-api/dataspace-object-and-createobject-method-example-vbscript.md)


