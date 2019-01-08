---
title: Le associazioni e le conversioni (OLE DB) | Documenti di Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- conversions [OLE DB]
- bindings [OLE DB]
- OLE DB, bindings and conversions
ms.assetid: c187df58-a8c8-4c74-a76f-663abbc5f0c1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b35583f18cbe590773c6661091186f669e012555
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52763157"
---
# <a name="bindings-and-conversions-ole-db"></a>Associazioni e conversioni (OLE DB)
  In questa sezione viene descritto come eseguire conversioni tra valori `datetime` e `datetimeoffset`. Le conversioni descritte in questa sezione sono già disponibili in OLE DB o costituiscono un'estensione coerente di OLE DB.  
  
 Il formato di valori letterali e stringhe per date e ore in OLE DB segue in genere lo standard ISO e non dipende dalle impostazioni locali del client. Un'eccezione è rappresentata da DBTYPE_DATE, che utilizza come standard l'automazione OLE. Poiché, tuttavia, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client esegue conversioni tra tipi solo quando i dati vengono trasmessi al o dal client, un'applicazione non può forzare in alcun modo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client per eseguire conversioni tra DBTYPE_DATE e formati stringa. In caso contrario, le stringhe utilizzano i formati indicati di seguito. Il testo tra parentesi indica un elemento facoltativo.  
  
-   Formato delle stringhe `datetime` e `datetimeoffset`:  
  
     *aaaa*-*mm*-*gg*[ *hh*:*mm*:*ss*[. *9999999*] [?? *hh*:*mm*]]  
  
-   Formato delle stringhe `time`:  
  
     *hh*:*mm*:*ss*[.*9999999*]  
  
-   Formato delle stringhe `date`:  
  
     *aaaa*-*mm*-*gg*  
  
> [!NOTE]  
>  Le versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client e SQLOLEDB implementano conversioni OLE se le conversioni standard non vengono eseguite correttamente. Di conseguenza, alcune conversioni eseguite in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 10.0 e versioni successive differiscono dalla specifica OLE DB.  
  
 Le conversioni dalle stringhe consentono flessibilità nella larghezza degli spazi vuoti e dei campi. Per altre informazioni, vedere la "i formati di dati: Sezione stringhe e valori letterali"in [supporto dei tipi di dati per data OLE DB e miglioramenti per la fase](data-type-support-for-ole-db-date-and-time-improvements.md).  
  
 Di seguito vengono fornite le regole di conversione generali:  
  
-   Quando una stringa viene convertita in un tipo di data/ora, la stringa viene prima analizzata come valore letterale ISO. Se l'operazione ha esito negativo, la stringa viene analizzata come valore letterale di data OLE, che include componenti per l'ora.  
  
-   Se l'ora non è presente ma il ricevitore può archiviare l'ora, questa viene impostata su zero. Se la data non è presente ma il ricevitore può archiviare la data, questa viene impostata sulla data corrente quando si utilizzano conversioni ISO e su 1899-12-30 quando si utilizzano conversioni OLE.  
  
-   Se nel tipo di dati utilizzato dal client non è presente il fuso orario, ma il server può archiviare il fuso orario, la data nel client viene considerata nel fuso orario utilizzato dal client stesso.  
  
-   Se nel server non è presente il fuso orario ma il client dispone di informazioni sul fuso orario, viene presupposto il fuso orario UTC. Questo comportamento differisce da quello del server.  
  
-   Se l'ora è presente ma il ricevitore non può archiviare l'ora, il componente per l'ora viene ignorato.  
  
-   Se la data è presente ma il ricevitore non può archiviare la data, il componente per la data viene ignorato.  
  
-   Se si verifica un troncamento di secondi o di secondi frazionari durante la conversione dal client al server, viene restituito DB_E_ERRORSOCCURRED e viene impostato lo stato DBSTATUS_E_DATAOVERFLOW.  
  
-   Se si verifica un troncamento di secondi o di secondi frazionari durante la conversione dal server al client, viene impostato lo stato DBSTATUS_S_TRUNCATED.  
  
## <a name="in-this-section"></a>In questa sezione  
 [Conversioni eseguite da client a server](conversions-performed-from-client-to-server.md)  
 Vengono descritte le conversioni di data/ora eseguite tra un'applicazione client scritta con la specifica OLE DB di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client e [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (o versione successiva).  
  
 [Conversioni eseguite da server a client](conversions-performed-from-server-to-client.md)  
 Vengono descritte le conversioni di data/ora eseguite tra [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (o versione successiva) e un'applicazione client scritta con la specifica OLE DB di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="see-also"></a>Vedere anche  
 [Miglioramenti relativi a data e ora &#40;OLE DB&#41;](date-and-time-improvements-ole-db.md)  
  
  
