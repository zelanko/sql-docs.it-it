---
title: Monitoraggio di tracce (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- XML for Analysis, traces
- XMLA, traces
- monitoring traces [XMLA]
- traces [Analysis Services]
ms.assetid: cdbfb984-18bd-4c4e-8fb7-d64ce298ed35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 678c6d2312261475f4b970b1535ce1faa1f00930
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62729072"
---
# <a name="monitoring-traces-xmla"></a>Monitoraggio di tracce (XMLA)
  È possibile utilizzare il comando [Subscribe](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/subscribe-element-xmla) in XML for Analysis (XMLA) per monitorare una traccia esistente definita in un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Il comando `Subscribe` restituisce i risultati di una traccia come set di righe.  
  
## <a name="specifying-a-trace"></a>Specifica di una traccia  
 La proprietà [Object](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) del `Subscribe` comando deve contenere un riferimento a un oggetto a un' [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] istanza di o a una traccia [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in un'istanza di. Se la proprietà `Object` non viene specificata o se un identificatore di traccia non viene specificato nella proprietà `Object`, il comando `Subscribe` consente di monitorare la traccia della sessione predefinita per la sessione esplicita specificata nell'intestazione SOAP per il comando.  
  
## <a name="returning-results"></a>Restituzione di risultati  
 Il comando `Subscribe` restituisce un set di righe che contiene gli eventi di traccia acquisiti dalla traccia specificata. Il `Subscribe` comando restituisce i risultati della traccia fino a quando il comando non viene annullato dal comando [Annulla](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla) .  
  
 Nel set di righe sono contenute le colonne elencate nella tabella seguente.  
  
|Colonna|Tipo di dati|Descrizione|  
|------------|---------------|-----------------|  
|EventClass|Integer|Classe di evento dell'evento ricevuto dalla traccia.|  
|EventSubclass|Long integer|Sottoclasse di evento dell'evento ricevuto dalla traccia.|  
|CurrentTime|Datetime|Ora di inizio dell'evento, se disponibile. I formati previsti per l'applicazione di filtri sono "YYYY-MM-DD" e "YYYY-MM-DD HH:MM:SS".|  
|StartTime|Datetime|Ora di inizio dell'evento, se disponibile. I formati previsti per l'applicazione di filtri sono "YYYY-MM-DD" e "YYYY-MM-DD HH:MM:SS".|  
|EndTime|Datetime|Ora di fine dell'evento, se disponibile. I formati previsti per l'applicazione di filtri sono "YYYY-MM-DD" e "YYYY-MM-DD HH:MM:SS".<br /><br /> Questa colonna non viene popolata per classi di evento che descrivono l'inizio di un processo o di un'azione.|  
|Duration|Long integer|Durata dell'evento (in millisecondi).|  
|CPUTime|Long integer|Tempo processore utilizzato per l'evento (in millisecondi).|  
|JobID|Long integer|Identificatore di processo.|  
|SessionID|string|Identificatore della sessione per cui si è verificato l'evento.|  
|SessionType|string|Tipo della sessione per cui si è verificato l'evento.|  
|ProgressTotal|Long integer|Numero o quantità complessiva dello stato di avanzamento segnalato dall'evento.|  
|IntegerData|Long integer|Dati di tipo integer associati all'evento. Il contenuto di questa colonna dipende dalla classe e dalla sottoclasse di evento.|  
|ObjectID|string|Identificatore dell'oggetto per cui si è verificato l'evento.|  
|ObjectType|string|Tipo dell'oggetto specificato in ObjectName.|  
|ObjectName|string|Nome dell'oggetto per cui si è verificato l'evento.|  
|ObjectPath|string|Percorso gerarchico dell'oggetto per cui si è verificato l'evento. Il percorso viene rappresentato come una stringa delimitata da virgole di identificatori di oggetto per i padri dell'oggetto specificato in ObjectName.|  
|ObjectReference|string|Rappresentazione XML del riferimento all'oggetto per l'oggetto specificato in ObjectName.|  
|NestLevel|Integer|Livello della transazione per cui si è verificato l'evento.|  
|NumSegments|Long integer|Numero di segmenti di dati interessati o utilizzati dal comando per cui si è verificato l'evento.|  
|Gravità|Integer|Livello di gravità di un'eccezione per l'evento. I possibili valori della colonna sono i seguenti:<br /><br /> Valore: 0 = esito positivo<br /><br /> Valore: 1 = informazioni<br /><br /> Valore: 2 = avviso<br /><br /> Valore: 3 = errore|  
|Operazione completata|Boolean|Indica se un comando ha avuto esito positivo o negativo.|  
|Errore|Long integer|Numero di errore di un evento, se applicabile.|  
|ConnectionID|string|Identificatore della connessione per cui si è verificato l'evento.|  
|DatabaseName|string|Nome del database per cui si è verificato l'evento.|  
|NTUserName|string|Nome utente di Windows dell'utente associato all'evento.|  
|NTDomainName|string|Dominio di Windows dell'utente associato all'evento.|  
|ClientHostName|string|Nome del computer in cui viene eseguita l'applicazione client. Questa colonna viene popolata con i valori passati dall'applicazione client.|  
|ClientProcessID|Long integer|Identificatore di processo dell'applicazione client.|  
|ApplicationName|string|Nome dell'applicazione client che ha creato la connessione all'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Questa colonna viene popolata con i valori passati dall'applicazione client anziché con il nome visualizzato del programma.|  
|NTCanonicalUserName|string|Nome utente di Windows in forma canonica dell'utente associato all'evento.|  
|SPID|string|ID del processo server (SPID) della sessione per cui si è verificato l'evento. Il valore di questa colonna corrisponde direttamente all'ID di sessione specificato nell'intestazione SOAP del messaggio XMLA per cui si è verificato l'evento.|  
|TextData|string|Dati di testo associati all'evento. Il contenuto di questa colonna dipende dalla classe e dalla sottoclasse di evento.|  
|ServerName|string|Nome dell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per cui si è verificato l'evento.|  
|RequestParameters|string|Parametri della query con parametri o del comando XMLA per cui si è verificato l'evento.|  
|RequestProperties|string|Proprietà del metodo XMLA per cui si è verificato l'evento.|  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo con XMLA in Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
