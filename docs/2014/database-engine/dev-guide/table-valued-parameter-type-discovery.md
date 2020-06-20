---
title: Individuazione dei tipi di parametri con valori di tabella
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, type discovery
ms.assetid: f55818c2-ebb5-4cf6-8c0c-0da41f592560
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: ab8d837e4ddf74256e4bae70f772557ec8ff67f7
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933252"
---
# <a name="table-valued-parameter-type-discovery"></a>Individuazione del tipo di parametro con valori di tabella
  Il consumer, ovvero l'applicazione client che utilizza il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native client, può individuare il tipo di ogni parametro del comando se il testo del comando è stato assegnato al provider di OLE DB. Una volta noto il tipo di un parametro con valori di tabella, il consumer può individuare le informazioni sui metadati per ogni singola colonna del parametro con valori di tabella.  
  
 Per la maggior parte dei tipi di parametri le informazioni sul tipo dei parametri di procedura sono supportate da ICommandWithParameters::GetParameterInfo. A partire da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , con l'introduzione di tipi definiti dall'utente e del `xml` tipo di dati, il metodo GetParameterInfo non è sufficiente a questo scopo perché non è stato possibile fornire informazioni sui tipi definiti dall'utente (nome, schema e catalogo) tramite ICommandWithParameters. Per fornire informazioni estese sul tipo è stata definita la nuova interfaccia ISSCommandWithParameters.  
  
 Per i parametri con valori di tabella, l'interfaccia ISSCommandWithParameters viene usata anche per individuare informazioni dettagliate. Il client chiama ISSCommandWithParameters::GetParameterInfo dopo aver preparato l'oggetto commando. Per i parametri con valori di tabella il membro *wType* della struttura DBPARAMINFO viene impostato su DBTYPE_TABLE dal provider. Il valore del campo *ulParamSize* della struttura DBPARAMINFO è ~0.  
  
 Il consumer può quindi richiedere proprietà aggiuntive (nome del catalogo del tipo di parametro con valori di tabella, nome dello schema del tipo di parametro con valori di tabella, nome del tipo di parametro con valori di tabella, ordinamento colonne e colonne predefinite) mediante ISSCommandWithParameters::GetParameterProperties.  
  
 Una volta noto il nome del tipo, per recuperare informazioni sulle singole colonne il consumer deve chiamare IOpenRowset::OpenRowset oppure ottenere il set di righe DBSCHEMA_TABLE_TYPE_COLUMNS specificando il nome del tipo di parametro con valori di tabella come nome della tabella.  
  
## <a name="see-also"></a>Vedere anche  
 [Parametri con valori di tabella &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usare parametri con valori di tabella &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
