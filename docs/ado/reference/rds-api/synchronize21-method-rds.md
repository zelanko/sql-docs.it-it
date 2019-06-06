---
title: Metodo Synchronize21 (Servizi Desktop remoto) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Synchronize21 method [ADO]
ms.assetid: 6b35f136-9d9a-4bdd-8144-67decfd3c4e9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1d731738938eab5732dcbfa86c0d624ae7941ed5
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66697260"
---
# <a name="synchronize21-method-rds"></a>Metodo Synchronize21 (Servizi Desktop remoto)
Sincronizzare i set di record specificato con il database specificato dalla stringa di connessione per l'uso con ADO 2.1.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.Synchronize21(ConnectionString As String, HandlerString As String, lSynchronizeOptions As Long, ppRecordset As Object, pStatusArray)  
```  
  
#### <a name="parameters"></a>Parametri  
 *ConnectionString*  
 Stringa utilizzata per la connessione al provider OLE DB in cui verrà inviata la richiesta. Se viene utilizzato un gestore, il gestore può modificare o sostituire la stringa di connessione.  
  
 *HandlerString*  
 La stringa identifica il gestore da utilizzare con questa esecuzione. La stringa contiene due parti. La prima parte contiene il nome (ProgID) del gestore da utilizzare. La seconda parte della stringa contiene argomenti da passare al gestore. Come viene interpretata la stringa di argomenti è gestore specifico. Le due parti sono separate per la prima istanza di una virgola nella stringa. La stringa di argomenti può contenere virgole aggiuntive. Gli argomenti sono facoltativi.  
  
 *lSynchronizeOptions*  
 Maschera di bit delle opzioni di sincronizzazione.  
  
 1 =*UpdateTransact* aggiornamenti al database vengono eseguito il wrapping in una transazione. La transazione viene interrotta se uno o più aggiornamenti ha esito negativo.  
  
 2 =*RefreshWithUpdate* cause di righe da restituire quando nessuno dei due stati *aggiornare* né *RefreshConflicts* è impostata.  
  
 4 =*Aggiorna* il set di record viene aggiornato con i dati correnti dal database. Gli aggiornamenti in sospeso non vengono inseriti nel database. Se questo bit non è impostato, il set di record non viene aggiornato e vengono effettuato il push di eventuali aggiornamenti in sospeso al database.  
  
 8 =*RefreshConflicts* tutte le righe con modifiche in sospeso non è possibile aggiornare. Le righe che non è riuscita per l'aggiornamento vengono aggiornate con i dati correnti dal database.  
  
 *ppRecordset*  
 Un puntatore a un puntatore al set di record da sincronizzare.  
  
 *pStatusArray*  
 Una variante usata per restituire una matrice protetta di stati di riga per le righe interessate da sincronizzare. Non impostare se nessuna delle opzioni di sincronizzazione seguenti sono impostata: *RefreshWithUpdate*, *Refresh* e *RefreshConflicts*.  
  
## <a name="remarks"></a>Note  
 Il *HandlerString* parametro può essere null. Cosa accade in questo caso dipende dal modo in cui il server di servizi desktop remoto è configurato. Nome di un gestore di "MSDFMAP. Handler" indica che il gestore di Microsoft fornito (Msdfmap.dll) deve essere utilizzato. Nome di un gestore di "MASDFMAP.handler,sample.ini" indica che il gestore Msdfmap.dll deve essere utilizzato e che l'argomento "il file" deve essere passato al gestore. MSDFMAP.dll interpreterà quindi l'argomento come una direzione da utilizzare il file per controllare le stringhe di connessione e la query.  
  
> [!NOTE]
>  Il **Synchronize21** metodo è semplicemente una versione del [sincronizzare metodo (RDS)](../../../ado/reference/rds-api/synchronize-method-rds.md). In cui è necessario usare il **Synchronize** metodo per comunicare con ADO 2.1, il **Synchronize21** metodo può essere invece chiamato. Le funzionalità dei **Synchronize** metodo in ADO 2.5 e versioni successiva sono un soprainsieme delle funzionalità fornito per il metodo di stesso in ADO 2.1.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


