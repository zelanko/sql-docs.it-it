---
title: Errori del processo di gestione temporanea (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- staging process [Master Data Services], error messages
ms.assetid: 0d9be0dd-638f-4dd4-92b2-253fda655455
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 65de28bcf880fab6dc0546c5ed4c315978ad39f4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65478797"
---
# <a name="staging-process-errors-master-data-services"></a>Errori del processo di gestione temporanea (Master Data Services)
  Al termine del processo di staging, per tutti i record elaborati è presente un valore nella colonna ErrorCode delle tabelle di staging. Questi valori sono elencati nella seguente tabella.  
  
|Codice|Errore|Si verifica quando/Dettagli|Si applica alla tabella|  
|----------|-----------|--------------------------|----------------------|  
|210001|Lo stesso codice membro è presente più volte nella tabella di staging.|Nel batch di gestione temporanea lo stesso codice membro è presente più volte. Il membro non è stato né creato né aggiornato.|Foglia<br /><br /> Consolidata<br /><br /> Relazione|  
|210003|I valori degli attributi fanno riferimento a un membro inesistente o inattivo.|Quando si gestiscono temporaneamente gli attributi basati su dominio, è necessario utilizzare il codice, piuttosto che il nome. Si applica a **ImportType0**, **1**e **2**.|Foglia<br /><br /> Consolidata|  
|210006|Il codice membro è inattivo.|**ImportType** = **1** ed è stato specificato un codice membro che non esiste.|Foglia<br /><br /> Consolidata<br /><br /> Relazione|  
|210032|Il nome della gerarchia è mancante o non valido.|La gerarchia esplicita non è stata trovata o il valore **HierarchyName** è vuoto.|Consolidata<br /><br /> Relazione|  
|210035|Poiché non esiste una regola di business per la generazione di codice, **MemberCode** è obbligatorio.|In caso di creazione o aggiornamento dei membri, **MemberCode** è sempre obbligatorio, a meno che non si usi la generazione di codice automatica. Per altre informazioni, vedere [Creazione di codice automatica &#40;Master Data Services&#41;](automatic-code-creation-master-data-services.md).|Foglia<br /><br /> Consolidata|  
|210036|Poiché esiste una regola di business per la generazione di codice, **MemberCode** non è obbligatorio.|In caso di creazione o aggiornamento dei membri, **MemberCode** non è obbligatorio quando si usa la generazione di codice automatica. È tuttavia possibile specificare un codice. Per altre informazioni, vedere [Creazione di codice automatica &#40;Master Data Services&#41;](automatic-code-creation-master-data-services.md).|Foglia<br /><br /> Consolidata|  
|210041|"ROOT" non è un codice membro valido.|Il valore **MemberCode** contiene la parola "ROOT".|Foglia<br /><br /> Consolidata<br /><br /> Relazione|  
|210042|"MDMUNUSED" non è un codice membro valido.|Il valore **MemberCode** contiene la parola "MDMUNUSED".|Foglia<br /><br /> Consolidata<br /><br /> Relazione|  
|210052|MemberCode non può essere disattivato perché è utilizzato come valore di attributo basato su dominio.|Quando **ImportType** = **3** o **4**, la gestione temporanea ha esito negativo se il membro viene usato come valore di attributo per altri membri. Usare **ImportType5** o **6** per impostare il valore su NULL o modificare i valori prima di eseguire il processo di gestione temporanea.|Foglia<br /><br /> Consolidata|  
|300002|Il codice membro non è valido.|Relazioni: il codice membro padre o figlio non esiste.<br /><br /> Foglia o Consolidata: **ImportType** = **3** o **4** e il codice membro non esiste.|Foglia<br /><br /> Consolidata<br /><br /> Relazione|  
|300004|Il codice membro esiste già.|**ImportType** = **1** ed è stato usato un codice membro che già esiste nell'entità.|Foglia<br /><br /> Consolidata|  
|210011|Se **RelationshipType** è **1**, **ParentCode** non può essere un membro foglia.|Assicurarsi che il valore **ParentCode** sia un codice membro consolidato.|Relazione|  
|210015|Lo stesso codice membro è presente più volte nella tabella di staging per una gerarchia e un batch.|Per una gerarchia esplicita, si è specificata la posizione dello stesso membro più volte nello stesso batch.|Relazione|  
|210016|Impossibile creare la relazione poiché determinerebbe un riferimento circolare.|Ciò si verifica quando si tenta di assegnare un figlio come padre.|Relazione|  
|210046|Il membro non può essere di pari livello del nodo Radice.|Ciò si verifica quando **RelationshipType** = **2** (di pari livello) e **ParentCode** o **ChildCode** è **Radice**. I membri non possono essere allo stesso livello del nodo Radice; possono essere solo elementi figlio.|Relazione|  
|210047|Il membro non può essere di pari livello del nodo Inutilizzato.|Ciò si verifica quando **RelationshipType** = **2** (di pari livello) e **ParentCode** o **ChildCode** è **Inutilizzato**. I membri possono essere solo elementi figlio del nodo Inutilizzato.|Relazione|  
|210048|**ParentCode** e **ChildCode** non possono corrispondere.|Il valore **ParentCode** corrisponde al valore **ChildCode** . Questi valori devono essere differenti.|Relazione|  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare gli errori che si verificano durante il processo di gestione temporanea &#40;Master Data Services&#41;](view-errors-that-occur-during-staging-master-data-services.md)   
 [Importazione di dati &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)  
  
  
